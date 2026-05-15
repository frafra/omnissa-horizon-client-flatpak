# Omnissa Horizon Client — Flatpak

Unofficial Flatpak packaging for the **Omnissa Horizon Client for Linux** (tarball edition).

## Prerequisites

```bash
# Install flatpak and flatpak-builder
sudo apt install flatpak flatpak-builder   # Debian/Ubuntu
sudo dnf install flatpak flatpak-builder   # Fedora/RHEL

# Add Flathub remote (needed for the runtime)
flatpak remote-add --if-not-exists flathub https://flathub.org/repo/flathub.flatpakrepo

# Install the runtime + SDK
flatpak install flathub org.freedesktop.Platform//25.08 org.freedesktop.Sdk//25.08
```

## Build

```bash
flatpak-builder --force-clean build-dir com.omnissa.HorizonClient.yaml
```

## Install locally

```bash
flatpak-builder --user --install --force-clean build-dir com.omnissa.HorizonClient.yaml
```

## Run

```bash
flatpak run com.omnissa.HorizonClient
```

Or launch **Omnissa Horizon Client** from your application menu.

## Maintenance

This manifest includes metadata for `flatpak-external-data-checker`. You can check for new versions of the Horizon Client by running:

```bash
uvx --from mitmproxy mitmdump -q --set modify_headers="/~q/User-Agent/" -m reverse:https://customerconnect.omnis
sa.com/
# Using the flatpak-external-data-checker tool
flatpak run org.flathub.flatpak-external-data-checker com.omnissa.HorizonClient.yaml
```

## Notes

- All shell wrappers that contain hard-coded `/usr/` paths are patched to `/app/` at build time.
- `~/.omnissa/` is used for client configuration (persisted across sessions).
- USB/smart card/scanner redirection requires `--device=all` (included in finish-args).
