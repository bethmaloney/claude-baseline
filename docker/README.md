# Docker Baseline

Claude Code permissions template for Docker and container tools.

## Allowed Commands

| Command | Purpose |
|---------|---------|
| `docker` | Docker CLI (build, run, compose, etc.) |
| `docker-compose` | Legacy standalone Docker Compose |
| `podman` | Docker-compatible container engine |
| `podman-compose` | Compose for Podman |
| `lazydocker` | Terminal UI for Docker |

### Common Operations Enabled

**Images**
- `docker build` / `docker pull` / `docker push` — Image management
- `docker images` / `docker rmi` — List and remove images

**Containers**
- `docker run` / `docker exec` — Run and execute in containers
- `docker ps` / `docker logs` — View container status and logs
- `docker stop` / `docker rm` — Manage container lifecycle

**Compose**
- `docker compose up` / `docker compose down` — Start/stop services
- `docker compose build` / `docker compose pull` — Build/pull images
- `docker compose logs` / `docker compose ps` — Monitor services

**Other**
- `docker network` / `docker volume` — Manage networks and volumes
- `docker system prune` — Cleanup unused resources

## Denied Patterns

| Pattern | Reason |
|---------|--------|
| `.env` / `.env.*` | Environment variables often passed to containers |
| `docker-compose.override.yml` | Local overrides often contain secrets/credentials |
| `docker-compose.override.yaml` | YAML extension variant |
| `**/docker-compose.override.*` | Nested override files |
| `secrets/**` / `**/secrets/**` | Docker secrets directories |
| `~/.docker/config.json` | Docker registry authentication |

## Usage

```bash
mkdir -p .claude
curl -o .claude/settings.json https://raw.githubusercontent.com/YOUR_USERNAME/claude-baseline/main/docker/settings.json
```

## Security Notes

- Docker commands can have significant system impact (mounting volumes, network access, privileged mode)
- `docker run` can mount host directories — be aware of what's being mounted
- Consider your threat model: this template is for development, not production CI/CD
- Registry credentials in `~/.docker/config.json` are protected

## Customization Ideas

- Add `dive` for exploring image layers
- Add `hadolint` for Dockerfile linting
- Add `trivy` or `grype` for image vulnerability scanning
- Add `skopeo` for image operations without Docker daemon
