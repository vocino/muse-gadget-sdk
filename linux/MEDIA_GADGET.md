# Media gadget

A Meta Muse gadget that runs your *arr stack and Jellyfin. Built on the
[Muse Gadgets Linux SDK](https://github.com/facebookincubator/muse-gadget-sdk)
(fork), so Muse can manage your media server from your phone instead of you
SSHing into it.

## Install

On a Raspberry Pi on the same LAN as your media server:

```sh
sudo useradd -m muse && sudo usermod -aG docker muse
bash install.sh --from . --run-as muse --sdk-token mgst_…
```

Copy `media.env.example` to `/var/lib/musegadget/media.env` (root, `chmod 600`)
and fill in your *arr and Jellyfin URLs and API keys. Then pair in the Muse
app: Settings > Devices > Developer mode > +.

## Use

Ask Muse things like:

- "Find the show Severance" (searches Sonarr)
- "Add it and start downloading" (adds, monitors, triggers a search)
- "What's downloading right now?"
- "What's new on Jellyfin?"

## Commands

| Command | What it does |
|---|---|
| `media.search` | Search Sonarr/Radarr by title |
| `media.add` | Add a series/movie by id, monitor, start search |
| `media.queue` | Merged Sonarr/Radarr download queue |
| `media.recent` | Recently added on Jellyfin |
| `homelab.docker` | `ps` lists containers, `restart` bounces one |

## What's inside

- `src/musegadget/media.py`: the media commands (stdlib only, no new deps)
- `src/musegadget/executor.py`: command specs and dispatch
- `tests/test_media.py`: mocked HTTP tests
- `media.env.example`: config template (real keys stay on the Pi)

## Develop

```sh
PYTHONPATH=src python3 -m pytest tests -q
```
