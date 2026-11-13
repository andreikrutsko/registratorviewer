# Installation

Download `RegistratorViewer.Next.exe` from a published release and run it on Windows x64. Install Microsoft WebView2 Evergreen if it is not already present. A separate .NET runtime installation is not required.

Check [system requirements](system-requirements.md) for Windows versions/builds,
graphics drivers, the Vulkan loader and runtime download links.

Verify a download in PowerShell:

```powershell
Get-FileHash ./RegistratorViewer.Next.exe -Algorithm SHA256
```

Compare the resulting value with that release's `SHA256SUMS.txt`. Do not use an EXE whose checksum differs.

## Ubuntu x64

For paired releases, choose `RegistratorViewer.Next-linux-x64` from the same
[release](https://github.com/andreikrutsko/registratorviewer/releases) as its
`SHA256SUMS.txt`. Install the Ubuntu media/browser prerequisites in
[system requirements](system-requirements.md#ubuntu-versions), then run:

```sh
sha256sum --ignore-missing --check SHA256SUMS.txt
chmod u+x RegistratorViewer.Next-linux-x64
./RegistratorViewer.Next-linux-x64
```

The .NET runtime is included in each platform's executable. Windows includes its
media tools; Ubuntu uses native `mpv`, `ffmpeg` and `ffprobe` executables.
PowerShell and a development SDK are not needed to run the Ubuntu application.
Earlier releases may offer only the Windows asset.

### Optional dependency installation on minimal Ubuntu

The commands below target **Ubuntu 24.04 LTS amd64**. Use them if a minimal
installation lacks the media tools, browser engine or desktop libraries. Skip
this step when the prerequisites are already installed. Installing them does
not require installing a separate .NET runtime or SDK.

If `mpv` or `ffmpeg` has no installation candidate, enable Ubuntu's Universe
repository first:

```sh
sudo apt-get update
sudo apt-get install -y software-properties-common
sudo add-apt-repository -y universe
sudo apt-get update
```

Explicitly install the media tools and native UI/browser/runtime dependencies:

```sh
sudo apt-get update
sudo apt-get install -y \
  mpv ffmpeg \
  libgtk-3-0t64 libwebkit2gtk-4.1-0 libsoup-3.0-0 \
  libfontconfig1 fonts-dejavu-core \
  libx11-6 libice6 libsm6 libxrandr2 libxi6 libxcursor1 libxkbcommon-x11-0 \
  libgl1 libegl1 libvulkan1 libasound2t64 libpulse0 \
  ca-certificates tzdata libc6 libgcc-s1 libstdc++6 \
  libgssapi-krb5-2 libicu74 libssl3t64 zlib1g
```

The Ubuntu **`ffmpeg` package includes `ffprobe`**; there is no separate
`apt install ffprobe` step. APT also installs each package's required libraries.
The native system libraries above are still needed by a self-contained .NET
application. See the [Ubuntu FFmpeg package](https://packages.ubuntu.com/noble/ffmpeg)
and [Microsoft's Ubuntu dependency list](https://learn.microsoft.com/en-us/dotnet/core/install/linux-ubuntu-install#dependencies-3).

To force reinstallation of already installed media tools, for example after a
missing or damaged executable, run:

```sh
sudo apt-get update
sudo apt-get install --reinstall mpv ffmpeg
```

For a damaged GTK/WebKit installation, use the same `--reinstall` option with
`libgtk-3-0t64 libwebkit2gtk-4.1-0 libsoup-3.0-0`. It reinstalls the named packages
without changing the application executable.

### A graphical session and graphics drivers

The application needs a running **X11 or XWayland graphical session**. Installing
libraries alone does not turn a headless Ubuntu Server shell into a desktop.
On a machine without any desktop, optionally install Ubuntu's minimal desktop,
then sign in to its graphical session:

```sh
sudo apt-get install ubuntu-desktop-minimal xwayland
```

For WSL2, use a working **WSLg** display/audio session instead; installing a full
Ubuntu desktop inside WSL is unnecessary. On bare metal, install the appropriate
GPU driver through Ubuntu's Additional Drivers settings. Missing Mesa rendering
components on an Intel/AMD or software-rendered setup can be installed with:

```sh
sudo apt-get install libgl1-mesa-dri mesa-vulkan-drivers
```

### Check the installed tools

Run these checks in the same Ubuntu session used to start the application:

```sh
command -v mpv ffmpeg ffprobe
mpv --version
ffmpeg -version
ffprobe -version
```

All three commands must resolve to native Linux tools on `PATH`. Restart the
application after installing or repairing dependencies. For display, audio and
graphics limitations, see [system requirements](system-requirements.md#ubuntu-versions).

## macOS Apple Silicon and Intel

Mac packages currently come from local/private CI builds; public availability is
listed in [Downloads](../README.md#downloads). Use macOS **26.0 or later** and select
`RegistratorViewer.Next-macos-arm64.zip` for Apple Silicon or
`RegistratorViewer.Next-macos-x64.zip` for Intel. These are separate builds.
Verify the ZIP's SHA-256 against the supplied checksum, extract it and keep the
complete `RegistratorViewer.Next.app`, including its frameworks and media tools.
No separate .NET, Homebrew, mpv or FFmpeg installation is required.

Current packages use ad-hoc technical signing. Developer ID/notarization and
downloaded-app clean-user acceptance remain pending; local startup success does
not establish Gatekeeper acceptance for a downloaded archive.

### Third-party source materials

The shared `RegistratorViewer.Next-macos-third-party-sources.zip` accompanies Mac
distributions for both architectures. Check its outer ZIP checksum, extract it,
then run `shasum -a 256 -c SHA256SUMS.txt` inside its source directory. Start with
its `README.md`, `BUILD-PLAYBACK.md`, `BUILD-EXPORT.md` and
`REPLACE-LIBRARIES.md`. `BUILD-PLAYBACK-HOMEBREW.md` provides a Homebrew-tool
alternative for rebuilding compatible libmpv. `SOURCE-MANIFEST.json` maps the source versions and build
paths to the exact Mac application ZIPs and signed media binaries. Source
packaging alone does not establish a successful native rebuild or replacement.

## Preferences and online maps

Preferences are stored in `~/.registratorviewer-next.yml` in the current user's
home on every platform. Online maps require a network connection. Google Maps
is optional and requires the user's own API key and billing; keys are not included.
