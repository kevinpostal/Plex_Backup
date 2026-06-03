# Plex Server

Rootless Podman container running [LinuxServer Plex](https://docs.linuxserver.io/images/docker-plex/).

## Files

| File | Purpose |
|---|---|
| `podman-compose.yml` | Podman Compose definition |

## Volumes (host → container)

| Host | Container | Note |
|---|---|---|
| `/srv/podman/plex-server/config` | `/config` | Plex metadata, settings, library state |
| `/mnt/storage/Movies` | `/data/movies` | Movie library (read-only) |
| `/mnt/storage/TV_Shows` | `/data/tv_shows` | TV library (read-only) |

## What is NOT in this repo

Runtime state is ignored by `.gitignore`:

- `config/` — contains Plex database, metadata, settings, and cached artwork

If you want to back up your Plex library state, archive the whole `config/` directory separately (e.g., `tar czf plex-config-backup.tar.gz config/`).
