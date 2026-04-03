# Sticky sessions and Connection draining

### Keywords & Connections:

- Sticky sessions (session affinity): binds users to a specific instance by giving them a cookie that the LB can recognize them and redirect them to their instance with. 
    - You can control how long the "stickiness" lasts by setting **cookie expiration**.
    - **Used when** session data is stored locally in instances.
    - **Trade of** is that it can cause uneven traffic distribution in case too many users get assigned the same instance.
    - **Not needed** when app is stateless where session data is stored in a shared store (like a database)
    - **Works on** CLB, ALB and NLB
- Connection draining: setting a grace period before scaling in an instance for the purpose of giving the users a smooth experience.
    - 2 actions of connection draining:
        - 1. No new requests are sent to the instance
        - 2. Any in-flight requests are given a grace period to finish (between 0-3600 seconds)

### What problem does this solve?
- Sticky sessions: in case where sessions are stored locally, a user could be redirected to another instance where their session data isn't stored (like their shopping cart) and giving them a frustrating experience. Sticky sessions solves this and redirects them to the same instance where their data is stored.
- Connection draining: gives users a smoother experience by preventing them from being abruptly cut off from a request when an instance is shutting down (like during a scaling event).

### How does this connect to what I already know?
- Connection draining relates to ASGs and what happens during scale-in events.
