# System requirements

These requirements describe the published, self-contained **Windows x64** EXE.
They do not require a development environment or a separate media player.

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
8.1 are outside the supported scope. There is no 32-bit, native ARM64, Linux or
macOS release; Windows ARM64 emulation, Windows Server and headless/remote GPU
environments have not been certified.

Check your edition, version and OS build with **Win+R > winver**. Build numbers
are documented by Microsoft in [Windows 11 release information](https://learn.microsoft.com/en-us/windows/release-health/windows11-release-information)
and [Windows 10 release information](https://learn.microsoft.com/en-us/windows/release-health/release-information).
Component compatibility follows the [.NET 10 supported-OS matrix](https://github.com/dotnet/core/blob/main/release-notes/10.0/supported-os.md)
and [WebView2 supported platforms](https://learn.microsoft.com/en-us/microsoft-edge/webview2/#supported-platforms).
These upstream lists are broader than the application's tested OS coverage.

## Runtimes and included components

| Component | What to install |
|---|---|
| .NET 10 / Windows Desktop Runtime | Nothing separately: the single-file release includes its runtime. Updating an unrelated system .NET installation does not update the bundled runtime; use a newer application release. |
| Microsoft Edge WebView2 Evergreen Runtime | Install or update the [Evergreen Runtime from Microsoft](https://developer.microsoft.com/en-us/microsoft-edge/webview2/#download). The WebView2 Runtime is separate from the Edge browser and is not bundled. Use the x64 installer for offline installation. |
| mpv, FFmpeg and ffprobe | Included and extracted automatically. No PATH setup, codec pack or separate installation is required for the built-in tools. |
| Windows graphics and system runtime components | Keep Windows and the GPU manufacturer's drivers updated. Development SDKs and Vulkan SDK are not required. |

Exact bundled versions are listed in the release's
[media manifest](../media-tool-manifest.json) and **? > Third-party Licenses**.
If you explicitly select external media tools, those executables must be
compatible x64 builds and may have additional requirements of their own.

## Graphics, video decoding and maps

Video needs a functioning **Vulkan or Direct3D 11** graphics driver.
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

Online vector maps also need WebView2 with usable browser graphics/WebGL support.
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

1. Confirm the Windows version/architecture and install WebView2 Evergreen Runtime.
2. Update the GPU manufacturer's driver. If Windows reports a missing
   `vulkan-1.dll`, repair the x64 loader/driver installation before changing renderers.
3. If the player starts but Vulkan rendering fails, select **Settings > Renderer >
   Direct3D 11 (D3D11VA)** and inspect **Renderer diagnostics**.
4. Check free space, writable user caches and execution policy. Built-in tools
   should remain selected unless you intentionally configured compatible external tools.

See [installation](installation.md) for download verification and the
[user guide](user-guide.md) for application controls.
