# Lab: Flask behind nginx, talking over a Compose network

## Goal
Stand up a Flask app reachable only through an nginx reverse proxy, both in a Docker Compose stack, where nginx finds Flask by service name over a shared network and only nginx is published to the host.

## Setup
- Ubuntu VM, Docker Engine + Compose plugin installed.
- Working directory `~/app/` containing four files written from an empty editor (no copying):
  - `app.py` — minimal Flask app
  - `Dockerfile` — single-stage, multi-stage-ready
  - `nginx.conf` — reverse-proxy config
  - `docker-compose.yml` — wires both services
- No prior containers or images for this project.

## Steps

1. Wrote `app.py` — minimal Flask app, one route, bound to `0.0.0.0` so it's reachable from another container (not loopback, which would only answer from inside its own container):
   ```python
   from flask import Flask
   app = Flask(__name__)
   @app.route('/')
   def home():
       return "Hey app worked!"
   if __name__ == '__main__':
       app.run(host='0.0.0.0', port=5000)
   ```

2. Wrote `Dockerfile` — slim Python base, install Flask, run the app:
   ```dockerfile
   FROM python:3.10-slim
   WORKDIR /app
   COPY . .
   RUN pip install flask
   CMD ["python", "app.py"]
   ```

3. Wrote `nginx.conf` — reverse-proxy to Flask by service name, not IP:
   ```nginx
   server {
       listen 80;
       location / {
           proxy_pass http://flask_backend:5000;
       }
   }
   ```

4. Wrote `docker-compose.yml` — both services on the default shared network; only nginx publishes a host port, Flask has no `ports:` entry:
   ```yaml
   services:
     flask_backend:
       build: .
     nginx_proxy:
       image: nginx:latest
       ports:
         - "8080:80"
       volumes:
         - ./nginx.conf:/etc/nginx/conf.d/default.conf
   ```

5. `docker compose up --build` — build the Flask image and bring the stack up.
   Output (relevant lines):
   ```
   ✔ Network app_default            Created
   ✔ Container app-nginx_proxy-1    Created
   ✔ Container app-flask_backend-1  Created
   flask_backend-1  | * Running on all addresses (0.0.0.0)
   flask_backend-1  | * Running on http://172.18.0.3:5000
   nginx_proxy-1    | ... start worker processes
   ```
   Both containers up; Flask bound to `0.0.0.0`, reachable internally at `172.18.0.3:5000`; nginx serving.

6. `curl http://localhost:8080` — positive path: host → nginx → Flask-by-name → back.
   Output:
   ```
   Hey app worked!
   ```

7. `curl http://localhost:5000` — negative check: confirm Flask is genuinely unpublished to the host.
   Output:
   ```
   curl: (7) Failed to connect to localhost port 5000 after 0 ms: Couldn't connect to server
   ```

8. `grep "172" nginx.conf` — negative check: confirm no hard-coded IP literal; nginx reaches Flask by service name only.
   Output: *(empty — no matches)*

## Verification
- **Positive:** `curl localhost:8080` returns `Hey app worked!` — the full chain resolved: host hit nginx on the published port, nginx resolved `flask_backend` by name over the shared `app_default` network, proxied to Flask on 5000, and the response came back.
- **Negative (Flask unpublished):** `curl localhost:5000` from the host returns connection refused. Flask has no `ports:` entry, so the host has no route to it — it's reachable only by nginx over the internal network. Proves the closed path is actually closed, not incidentally working.
- **Negative (name-based, not IP):** `grep "172" nginx.conf` returns nothing. The proxy target is the service name `flask_backend`, not a `172.x` literal, so resolution depends on Compose's shared-network DNS, not a brittle hard-coded address.

## What broke (if anything)
- **Symptom:** `docker compose up --build` failed validation with `services.flask_backend additional properties 'nginx_proxy' not allowed`.
- **Cause:** `nginx_proxy` was indented one level too deep, so YAML read it as a key *inside* `flask_backend` instead of as a sibling service under `services:`.
- **Fix:** De-indented `nginx_proxy` to line up with `flask_backend`, making both direct children of `services:`. Stack came up clean after that.

## What this teaches
Service-name resolution between containers isn't magic — it works because Compose puts both services on a shared network and runs DNS so a name like `flask_backend` resolves to the right container; hard-coding a `172.x` IP would break the moment that address changes. Not publishing a port is itself a security boundary: a service with no `ports:` entry is reachable only by its network peers, and the way you *prove* that is by failing to connect to it from the host, not by assuming.
