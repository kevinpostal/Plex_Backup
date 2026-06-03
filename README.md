# Plex Server

Rootless Podman container running [LinuxServer Plex](https://docs.linuxserver.io/images/docker-plex/).

## Files

| File | Purpose |
|---|---|
| `plex.container` | systemd Quadlet definition (drop in `~/.config/containers/systemd/`) |
| `podman-compose.yml` | Podman Compose equivalent (optional) |

## Deploy / redeploy

### 1. Clone or copy this repo

```bash
cd /srv/podman/plex-server
```

### 2. Set your Plex claim token

Edit `plex.container` and replace `claim-XXXXXXXXXXXXXXXXXX` with a real claim token from https://www.plex.tv/claim/.

### 3. Install the Quadlet

```bash
cp plex.container ~/.config/containers/systemd/
systemctl --user daemon-reload
systemctl --user start plex.service
```

To start automatically on boot:

```bash
systemctl --user enable plex.service
```

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
