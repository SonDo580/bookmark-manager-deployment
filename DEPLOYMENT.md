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

## Subsequent times

```bash
cd <path-to-repo>

# Pull latest code
git pull

# Update .env if needed
nano bookmark_service/.env

# Tear down to clear old state
docker compose down

# Run
docker compose up -d
```
