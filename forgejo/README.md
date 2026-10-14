# Forgejo

LAN-only access via Traefik's internal `http`/`https` entrypoints (not the `-external` ones). TLS is Traefik's default self-signed cert, since a private local domain can't get a public cert.

## Deploy
1. Create the data and postgres directories referenced in `.env`, owned by the `apps` user (568).
2. `cp example.env .env` and set every value (`openssl rand -hex 32` for `POSTGRES_PASSWORD`).
3. DNS: add a rewrite on your local resolver pointing `FORGEJO_DOMAIN` at the Traefik host's IP, and whitelist it in the router's DNS rebind protection (see `traefik-v3/README.md`).
4. `docker compose up -d`
5. Create the admin (registration is disabled and the installer is locked):
   `docker exec -u 568 forgejo forgejo admin user create --admin --username <user> --email <email> --random-password`

## Usage
- HTTPS: `https://<FORGEJO_DOMAIN>/<user>/<repo>.git` (trust the cert or `git config http.sslVerify false` for that host).
- SSH: `ssh://git@<FORGEJO_DOMAIN>:<SSH_HOST_PORT>/<user>/<repo>.git` (host :22 is normally the TrueNAS sshd).

## Notes
- Access is restricted by the `forgejo-lan-only` ipAllowList (`ALLOWED_SOURCE_RANGE`). If Tailscale clients get 403, they are probably arriving from a NATed/docker address; widen the range.
- Traefik reaches Forgejo on port 3000 over the `proxy` network; no HTTP port is published on the host.
