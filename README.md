# RegistratorViewer.Next

A Windows and Ubuntu x64 dashcam player with continuous grouped playback, GPS routes, G-sensor charts, online maps, video zoom and screenshots, and lossless cutting and merging.

The application offers English, German, Polish, Lithuanian and Ukrainian interfaces. Language changes apply immediately.

Indexed 16 KiB GPS MP4 recordings are detected automatically. Native GPS blocks and recovery indexes are retained through stream-copy cutting and joining; invalid fixes remain gaps, recorded speed/course are preserved, and unavailable G-force is not fabricated. Cuts align to complete GOP boundaries.

## System requirements

- **Windows x64:** use a serviced Windows 11 edition, with **Microsoft Edge
  WebView2 Evergreen Runtime**. The Windows package includes .NET 10 and its media
  tools; a separate SDK, .NET runtime, mpv or FFmpeg installation is unnecessary.
- **Ubuntu x64:** Ubuntu **24.04 LTS** with a graphical X11/XWayland session is the
  validated family. Install `mpv`, `ffmpeg`, GTK 3, WebKitGTK 4.1 and libsoup 3 from
  Ubuntu packages. The Linux executable includes .NET 10; no SDK or PowerShell is
  required. Wayland-native, other distributions, ARM and macOS are not certified.
- **Graphics:** Windows uses Vulkan or Direct3D 11; Ubuntu uses the installed
  mpv renderer and graphics driver. The Windows bundled player also
  requires the **64-bit Vulkan loader** (`vulkan-1.dll`), including in D3D11 mode;
  it is normally supplied with the graphics driver.
- **Network:** required for online maps and update checks; local playback and
  editing work offline.

See [system requirements](docs/system-requirements.md) for Windows builds, Ubuntu
installation commands, included/system runtimes, hardware and validation limits.

## Supported Models

Full support for the data channels present in the tested MOV/MP4 recording variants:

- **70mai:** A810-2, T800 4K.
- **BlackVue:** ELITE 9.
- **CARCAM:** R2s.
- **Garmin:** Dash Cam 57.
- **Lexand:** LR300.
- **Mini:** 0806.
- **Mio:** MiVue 812, MiVue C530, MiVue C530 Pro, MiVue i95, MiVue J60, MiVue ViVa V51.
- **Navitel:** MR155 NV, MR450 GPS, R250 Dual, RS2 Duo.
- **Neoline:** WIDE S21.
- **Rexing:** Model unidentified (tested source recording).
- **ROAV:** Model unidentified (tested trimmed recording).
- **Street Guardian:** SGGCX2Pro+.
- **Tesla:** TeslaCam (tested 2021 and 2026 recordings; vehicle model unidentified).
- **Thinkware:** F770.
- **TrendVision:** Bullet, Proof Pro, X2.
- **Type S:** S403.
- **Vantrue:** N5, model-unidentified source recording.
- **VIOFO:** A119 Mini, A119 V3, A119M Pro, A119S, A129 Plus Duo, A129 Pro, A139, A229, A329, A329S.
- **Vueroid:** S1-4K Infinite.
- **WonVon:** W4K.
- **Yi:** Dash Cam.

Vueroid and WonVon acceleration is explicitly estimated (`~g`), with the
original raw data retained; it is not manufacturer-calibrated G-force. The Yi
entry covers the acquired processed video/audio sample, without a recorded
GPS/G-force channel or certification of an unidentified hardware variant.

Rexing, ROAV and the additional model-unidentified Vantrue entry cover only
the acquired video/audio recordings; their investigated carriers contain no
identified digital GPS/G-force. TeslaCam covers four camera views from each
of two recording generations: the 2026 sources include recorded GPS and linear
acceleration, while those channels were not found in the 2021 sources. These
source-scoped results do not certify unidentified hardware models or every
firmware. Mini 0806 is the original supported MOV/LOG baseline with GPS and
recorded XYZ acceleration; additional Mini Series catalog links have not yielded
new samples and do not extend support to other models or firmware.
The listed sample variants have passed focused acceptance, final regression and
local release packaging checks. Published binaries are available from Releases;
sample-scoped validation does not certify every firmware or recording mode.

### Partial support

- **iZEEKER:** Model unidentified; video/audio, GPS and native cut/join/reopen
  are supported. Recorded acceleration is displayed and preserved in raw device
  units; its physical g scale and vehicle-axis orientation remain unconfirmed.

## Downloads

Use the [Releases page](https://github.com/andreikrutsko/registratorviewer/releases).
Paired releases contain **`RegistratorViewer.Next.exe`** for Windows x64 and
**`RegistratorViewer.Next-linux-x64`** for Ubuntu x64, with one `SHA256SUMS.txt`
covering both. Each application is a self-contained single executable. On Ubuntu,
run `chmod u+x RegistratorViewer.Next-linux-x64` before launching it. Ubuntu's
media/browser system packages are prerequisites, rather than embedded Windows
tools. Earlier releases may contain only the Windows asset. This repository's
automatic “Source code” archives contain user documentation only.

Application source is private and is not distributed in this repository. The owner approved the current distribution model and exact dependency inventory on 2026-10-25, including the documented source-material risk exception. Offline full license texts are accessible through **? → Third-party Licenses** and About.

See the [exact media manifest](media-tool-manifest.json), [desktop runtime catalog](desktop-runtime-manifest.json), [third-party notices](THIRD_PARTY_NOTICES.md) and [full license texts](THIRD_PARTY_LICENSES/). Binary releases include notices, full licenses, the exact manifest and any explicitly declared source assets. On 2026-10-25 the owner accepted the risk of release without complete corresponding sources and build materials for the exact GPL media binaries; source completeness remains UNKNOWN and no complete source package is claimed. This decision changes project policy, not third-party licenses. These compliance assets are separate from the single platform executable required to run the application; automatic GitHub documentation archives do not replace them. The owner approved all distribution review categories; final artifact, public-document and publication checks remain required.

Telegram updates: https://t.me/RegistratorViewer

Discussion: https://t.me/RegistratorViewerChat

See [installation](docs/installation.md) and [user guide](docs/user-guide.md).
