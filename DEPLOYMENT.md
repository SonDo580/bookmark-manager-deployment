# Deployment

## Connect to VPS

```bash
ssh <user>@<ip>
# Enter password
```

- (Optional) Setup password-less login:

```bash
# Check for existing key (on local machine)
ls ~/.ssh/id_ed25519.pub

# Generate if not found
ssh-keygen -t ed25519 -C "example@example.com"`

# Copy to VPS
ssh-copy-id <user>@<ip>

# Try reconnecting
ssh <user>@<ip>
```

## First time

```bash
# Install docker
# Install git

# Clone repository
git clone https://github.com/SonDo580/bookmark-manager-deployment.git

cd <path-to-repo>

# Create .env
nano bookmark_service/.env

# Run
docker compose up -d
```

## Setup self-hosted runner for CD pipeline

- Follow GitHub guide to add self-hosted runner on VPS.
- Run `export RUNNER_ALLOW_RUNASROOT=1` before setup.
- Install and start runner as a background service.

## Subsequent times

- Update environment variables if needed:
  - `bookmark_service/.env`
- Push or merge to `main`. The CD pipeline do the rest.

## Domain & HTTPS

1. Buy a domain name

2. Onboard the domain to Cloudflare

- On registrar website, replace nameservers with ones of Cloudflare.
- On Cloudflare, go to DNS records settings:
  - Add an `A` record pointing `@` to the VPS's public IP with **Proxy status** turned on.
  - Optionally add a similar `A` record for `www` (or a `CNAME` record pointing `www` to `@`).

3. Enable SSL/TLS

- On Cloudflare, go to SSL/TLS settings:
  - Set encryption mode to **Flexible**.
- **TODO**:
  - On VPS:
    - Install certificate.
    - Update `nginx.conf` to listen on port 443.
    - Only allow Cloudflare's IP addresses on port 80 and 443.
  - On Cloudflare:
    - Switch to **Full (strict)** mode.
