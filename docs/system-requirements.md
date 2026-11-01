# System requirements

Paired releases provide two self-contained x64 executables under one version:
`RegistratorViewer.Next.exe` for Windows and `RegistratorViewer.Next-linux-x64`
for Ubuntu. Each includes .NET 10; no SDK or separate .NET runtime is required.
Browser, graphics and Linux media prerequisites remain system packages. Earlier
releases may contain only the Windows executable.

## Windows versions

Use an updated, currently serviced **Windows 11 x64** installation. Windows 11
24H2 (build **26100**) and newer are the recommended deployment family. Version
numbers below identify release branches; install their applicable cumulative
updates rather than looking for one exact revision.

| Windows release | Base OS build | Compatibility scope |
|---|---|---|
| Windows 11 24H2 | 26100 | Recommended family; Microsoft servicing depends on edition. |
| Windows 11 25H2 | 26200 | Newer deployment target; keep Windows and graphics drivers updated. |
| Windows 11 26H2 | 26300 | Current local validation host: Pro, build 26300.9711. This does not certify every GPU or Windows build. |
| Windows 10 Enterprise / IoT Enterprise LTSC 2021, 21H2 | 19044 | Upstream .NET 10 and WebView2 compatibility target; a complete application regression on this OS has not been performed. |
| Windows 10 22H2 | 19045 | Legacy compatibility only, not a certified application baseline. It is not listed in the current .NET 10 supported-OS matrix; WebView2 availability alone does not establish full support. |

The older Windows 10 LTSC versions appearing in Microsoft's component support
lists are not certified for this complete application package. Windows 7, 8 and
8.1 are outside the supported scope. There is no 32-bit, native ARM64 or
macOS release; Windows ARM64 emulation, Windows Server and headless/remote GPU
environments have not been certified.

Check your edition, version and OS build with **Win+R > winver**. Build numbers
are documented by Microsoft in [Windows 11 release information](https://learn.microsoft.com/en-us/windows/release-health/windows11-release-information)
and [Windows 10 release information](https://learn.microsoft.com/en-us/windows/release-health/release-information).
Component compatibility follows the [.NET 10 supported-OS matrix](https://github.com/dotnet/core/blob/main/release-notes/10.0/supported-os.md)
and [WebView2 supported platforms](https://learn.microsoft.com/en-us/microsoft-edge/webview2/#supported-platforms).
These upstream lists are broader than the application's tested OS coverage.

## Ubuntu versions

The validated Linux family is **Ubuntu 24.04 LTS x86-64**, including local Ubuntu
24.04.3 under WSL2/WSLg. Use an X11 graphical session or working XWayland: the
embedded video adapter uses X11. Native Wayland without XWayland, other Ubuntu
releases/distributions, ARM, musl/Alpine and macOS are not certified application
targets, even where the upstream [.NET support matrix](https://github.com/dotnet/core/blob/main/release-notes/10.0/supported-os.md)
lists additional systems. Bare-metal GPU combinations need separate validation.

Install runtime prerequisites from Ubuntu repositories:

```sh
sudo apt update
sudo apt install mpv ffmpeg libgtk-3-0t64 libwebkit2gtk-4.1-0 libsoup-3.0-0 \
  libfontconfig1 libx11-6 libice6 libsm6 libicu74 libssl3t64 zlib1g
```

The `ffmpeg` package supplies `ffprobe`. The application uses these native ELF
tools, rather than Windows executables through WSL interoperability. GTK 3,
WebKitGTK 4.1 and libsoup 3 provide the system browser engine; see the
[Avalonia browser prerequisites](https://docs.avaloniaui.net/docs/app-development/embedding-web-content).
These browser and media packages are installed/updated by the operating system,
not bundled in the Linux executable. A normal Ubuntu desktop includes several
listed libraries already. No PowerShell or development SDK is needed to run it.

Download the executable and the shared checksum file from the same release:

```sh
sha256sum --ignore-missing --check SHA256SUMS.txt
chmod u+x RegistratorViewer.Next-linux-x64
./RegistratorViewer.Next-linux-x64
```

Keep recordings with their companion LOG/sidecar files. In WSL, telemetry parsing
through `/mnt/c` can be substantially slower than native Linux storage because
of small random reads. The application does not relocate recordings. WSLg needs
a working display and PulseAudio session; a headless shell alone is insufficient.

## Runtimes and included components

The following table describes Windows. Ubuntu includes the same desktop UI,
local map assets, translations, icon and full notices, but obtains its browser,
graphics/audio libraries and three media tools from system packages as above.

| Component | What to install |
|---|---|
| .NET 10 runtime | Nothing separately: the single-file release includes its runtime. Updating an unrelated system .NET installation does not update the bundled runtime; use a newer application release. |
| Microsoft Edge WebView2 Evergreen Runtime | Install or update the [Evergreen Runtime from Microsoft](https://developer.microsoft.com/en-us/microsoft-edge/webview2/#download). The WebView2 Runtime is separate from the Edge browser and is not bundled. Use the x64 installer for offline installation. |
| mpv, FFmpeg and ffprobe | Included and extracted automatically. No PATH setup, codec pack or separate installation is required for the built-in tools. |
| Windows graphics and system runtime components | Keep Windows and the GPU manufacturer's drivers updated. Development SDKs and Vulkan SDK are not required. |

Exact bundled versions are listed in the release's
[media manifest](../media-tool-manifest.json) and **? > Third-party Licenses**.
If you explicitly select external media tools, those executables must be
compatible x64 builds and may have additional requirements of their own.

Both platforms use `~/.registratorviewer-next.yml` in the current user's home
(`%USERPROFILE%` on Windows). Units, timezones and pane proportions are portable
preferences. Settings need a writable private location; Linux settings-file
overrides require a filesystem that enforces private Unix permissions. An ordinary
Windows mount without that enforcement is unsuitable for the settings override.
Single-file runtime contents extract to the user's cache, so allow free space
and execution permissions there. System .NET updates do not update the runtime
inside a downloaded application executable; obtain a newer application release.

## Graphics, video decoding and maps

Windows video needs a functioning **Vulkan or Direct3D 11** graphics driver.
Ubuntu uses the native mpv renderer and graphics driver; D3D11 is unavailable.
**Settings > Renderer > Auto** prefers Vulkan and can use D3D11 when the player
starts successfully but Vulkan initialization is unavailable. The explicit
**Direct3D 11 (D3D11VA)** option selects D3D11 rendering.

The bundled mpv executable imports **`vulkan-1.dll`**. Consequently, a working
**64-bit Vulkan loader is required even when D3D11 is selected**. Backend fallback
cannot repair a missing DLL that prevents Windows from starting the player.
The loader is normally installed with the graphics driver; see the
[Khronos loader documentation](https://github.com/KhronosGroup/Vulkan-Loader/blob/main/docs/LoaderApplicationInterface.md).
This requirement does not mean every video must be rendered with Vulkan.

Hardware decoding is optional and depends on the GPU, driver, codec, resolution
and bit depth. Unsupported decoding can use the CPU while keeping the selected
GPU renderer. A 4K HEVC recording may need substantially more CPU capacity than
1080p AVC. Check **Settings > Renderer > Renderer diagnostics** for the actual
renderer and decoder. Software decoding does not remove the graphics requirement.

Online vector maps need usable browser graphics/WebGL support: WebView2 on
Windows, the installed WebKitGTK engine on Ubuntu.
Remote Desktop, virtual machines and restricted graphics drivers may behave
differently from a local desktop session.

## CPU, memory and storage

An **Intel/AMD-compatible x64 processor** is required. A universal minimum CPU
model, clock speed or RAM figure has not been benchmarked across all recording
formats. As practical sizing guidance, plan for **at least 4 GB RAM**, preferably
**8 GB or more** for 4K footage, long routes or large file groups. These figures
are recommendations, not guaranteed playback-performance thresholds.

Allow roughly **2 GB of free system-drive space** for the EXE, extracted runtime/
media tools and browser data, with additional headroom for retained application
versions and growing caches. Export destinations also need space for the final
output and temporary working media; available space must scale with the selected
recordings. An SSD is useful for large groups and high-bitrate video.

The current user must be able to write to their temporary and local application
data directories, save per-user settings and launch the bundled media processes.
Normal application use does not require administrator privileges; installing
machine-wide prerequisites may require them. Enterprise execution policies must
allow the EXE and its extracted child processes.

## Internet access and offline use

Local playback, GPS/G-force reading, screenshots and editing work offline once
prerequisites are installed. Online maps need HTTPS access to the selected map
provider; version checking and release downloads need GitHub access. Google Maps
is optional and requires your own API key and billing configuration. A cached map
is not a guaranteed offline map service.

## If startup or playback fails

On Ubuntu, verify the native packages listed above, use an X11/XWayland graphical
session, and check the downloaded executable's execute permission and checksum.
Keep preferences on a filesystem that supports private user-only permissions.
Install or repair mpv/ffmpeg and browser libraries through the Ubuntu package
manager; do not copy Windows media tools into the Linux application directory.
The following driver/renderer steps apply to Windows:

1. Confirm the Windows version/architecture and install WebView2 Evergreen Runtime.
2. Update the GPU manufacturer's driver. If Windows reports a missing
   `vulkan-1.dll`, repair the x64 loader/driver installation before changing renderers.
3. If the player starts but Vulkan rendering fails, select **Settings > Renderer >
   Direct3D 11 (D3D11VA)** and inspect **Renderer diagnostics**.
4. Check free space, writable user caches and execution policy. Built-in tools
   should remain selected unless you intentionally configured compatible external tools.

See [installation](installation.md) for download verification and the
[user guide](user-guide.md) for application controls.
