# Bosch Island — Spatial Audio (Linux Build)

Linux-compiled fork of the Bosch Island Spatial Audio plugin for Mumble. See the main plugin's README for configuration and usage.

## Requirements

- **Mumble 1.5.0 or newer**
- **Linux x86_64** with glibc 2.17+ (covers every current desktop distro, including Steam Deck)

No other dependencies — libstdc++ is statically linked into the `.so`.

## Installation

### Option 1: Install via Mumble UI (recommended)

1. Open Mumble.
2. Go to **Configure → Settings → Plugins**.
3. Click **Install plugin…** and select the `.so` file.
4. Tick the checkbox next to **Bosch Island — Spatial Audio** to enable it.
5. Click **Apply**, then **OK**.

### Option 2: Manual install

Drop the `.so` into Mumble's user plugin directory:

| Install type | Path                                                          |
|--------------|---------------------------------------------------------------|
| Standard     | `~/.local/share/Mumble/Mumble/Plugins/`                       |
| Flatpak      | `~/.var/app/info.mumble.Mumble/data/Mumble/Mumble/Plugins/`   |
| Steam Deck   | `~/.local/share/Mumble/Mumble/Plugins/` (Desktop Mode)        |

Create the directory if it doesn't exist. Restart Mumble, then enable the plugin under **Settings → Plugins**.

## Building from source

Portable build that works on any glibc 2.17+ system:

```bash
docker run --rm -v "$PWD":/src -w /src \
  quay.io/pypa/manylinux2014_x86_64 \
  bash -c 'g++ -std=c++17 -O2 -fPIC -shared -fvisibility=hidden \
    -o theisle_spatial.so plugin.cpp connection.cpp \
    -static-libgcc -static-libstdc++ \
    -Wl,--exclude-libs,ALL -Wl,--no-undefined \
    -lpthread -ldl'
```
