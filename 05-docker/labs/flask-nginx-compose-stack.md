# Lab: Dockerized Flask app behind nginx in a Compose stack

## Goal
Stand up a shipped-shaped multi-container app where traffic, state, image, and secrets are each handled the way production handles them — and prove the visit counter's state survives container recreation but not volume removal.

## Setup
- Started from a copied in `app.py`: a small Flask app that increments a visit counter, persists it to `/data/counter.txt`, and listens on `0.0.0.0` so traffic can reach it from outside the container.
- Files authored over the session: `Dockerfile`, `docker-compose.yml`, `nginx.conf`, `.env`, `.dockerignore`, `.gitignore`.

## Steps

1. Wrote the `Dockerfile` multi-stage, non-root, `data`owned by `appuser` before the volume mounts.
   - **Multi-stage build.** Dependencies install in the `builder` stage under `--prefix=/install`. The runtime stage copies only `/install` via `--from=builder`. The toolchain stays behind, so the final image is lighter and has a smaller attack surface.
   - **Run as `appuser`.** A non-root user via `useradd`, then `USER appuser` to implement least privilege, so a compromised app has the least access possible.
   - **`mkdir -p /data && chown appuser:appuser /data`, before the `USER` line.** A fresh named volume defaults to root ownership, which would give permission-denied on `appuser`'s first write. Pre-owning `/data` in the image means the empty volume inherits `appuser` ownership at first mount. The chown has to come before `USER appuser` since chown is a privileged operation, and every build step after the `USER` instruction runs as `appuser`, who can't chown.

2. Wrote `docker-compose.yml` with two services, one named volume.
   - `web` builds from the Dockerfile, mounts `counter_data:/data`, reads its env from `.env`. No `ports:` it's reached through the proxy.
   - `nginx` maps host port 5002 to container port 80 and bind mounts `nginx.conf` as read only.
   - `counter_data` declared at the top level and mounted at `/data`, so data written there survives a container being removed and recreated.

3. Wrote `nginx.conf`: `upstream web_backend { server web:5000; }`, `proxy_pass http://web_backend`. Targets `web:5000` by service name because Compose's embedded DNS resolves service names, so no IP is needed.

4. Wrote `.env`, `.dockerignore`, `.gitignore`. `.env` sits in both ignore files, kept out of git history and image layers.

5. `docker compose config`, validate both services are configured correctly and that `web` has `counter_data` at `/data`.
   Output (trimmed):
   ```
   web:
     volumes:
       - type: volume
         source: counter_data
         target: /data
     environment:
       APP_SECRET: ...
       DATA_DIR: /data
   nginx:
     ports:
       - target: 80
         published: "5002"
   ```

6. `docker compose up --build -d` — build the image and bring the stack up.
   Output:
   ```
   Image day43-web Built
   Container day43-web-1 Started
   Container day43-nginx-1 Started
   ```

7. `docker compose ps` — confirm both services are up.
   Output:
   ```
   day43-nginx-1  nginx:latest  ...  Up 35 seconds  0.0.0.0:5002->80/tcp
   day43-web-1    day43-web     ...  Up 36 seconds
   ```

8. `curl localhost:5002` ×7 — confirm the counter climbs (traffic reaching Flask through nginx).
   Output: `This page has been visited 1 times.` … through `... 7 times.`

## Verification

Persistence, tested as a two-phase control:

- **Recreate without touching the volume.** `docker compose down` then `docker compose up --build -d`. Containers destroyed and recreated, volume untouched.
  `curl localhost:5002` gave `This page has been visited 8 times.` The count carried across the recreation.
- **Recreate and remove the volume.** Tore the stack down together with the volume this time (`down -v`), then back up.
  `curl localhost:5002` gave `This page has been visited 1 times.` The reset confirms it was the volume, not the container, holding the state.

## What this teaches

- How to practically attach volumes to containers.
- Containers can be removed and recreated without losing data using volumes. Only down -v destroys the data.
- Publishing a port is for exposure, not for connecting services. Containers on the same Compose network already reach each other's ports directly using service names. Only nginx maps to the host with 5002:80 while everything behind it stays unreachable from outside.
- When hardening a runtime image perform all privileged setups before the `USER`instruction. 
