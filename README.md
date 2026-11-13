# RegistratorViewer.Next

Cross-platform dashcam player for Windows x64, Ubuntu x64 and macOS on Apple Silicon or Intel, with continuous grouped playback, GPS routes, G-sensor charts, online maps, video zoom and screenshots, and lossless cutting and merging.

The application offers English, German, Polish, Lithuanian and Ukrainian interfaces. Language changes apply immediately.

## System requirements

- **Windows x64:** Windows 11 with **Microsoft Edge WebView2 Evergreen Runtime**.
  The required .NET runtime and media tools are included.
- **Ubuntu x64:** Ubuntu **24.04 LTS** with X11 or XWayland. Install `mpv`,
  `ffmpeg`, GTK 3, WebKitGTK 4.1 and libsoup 3 from Ubuntu packages.
  A separate .NET installation is unnecessary.
- **macOS:** **26.0 or later**, on Apple Silicon (`arm64`) or Intel (`x86_64`).
  Download the ZIP for your processor. Runtime and media components are included;
  Homebrew and a separate .NET installation are unnecessary.
- **Graphics:** keep your graphics drivers up to date. Windows requires the
  64-bit Vulkan loader (`vulkan-1.dll`), normally supplied with the graphics driver.
- **Network:** required for online maps and update checks. Local playback and
  editing work offline.

See [system requirements](docs/system-requirements.md) for hardware and OS
dependencies, and [installation](docs/installation.md) for setup instructions.

## Supported formats

GPS track import supports GPX, TCX, FIT, NMEA, timed KML/KMZ, GeoJSON,
CSV/TSV, OziExplorer PLT and General LOG files. The application identifies
formats by their contents rather than the filename extension. Tracks need
timestamps for synchronization with video. See the [GPS track guide](docs/user-guide.md#gps-tracks-and-corrections)
for attachment, source selection and conversion.

## Supported Models

Support for MOV/MP4 recordings depends on the camera firmware, recording mode
and available GPS or sensor data:

- **70mai:** 4K Omni (X800), A510, A810-2, A810S, A900, A900 Ultra, M300, M310 Plus, Rearview Dash Cam Wide (MIDRIVE D07), T800 4K.
- **BlackVue:** ELITE 9, ELITE 10.
- **CARCAM:** R2s.
- **DDPAI:** mini, Mini5, Mola N3, N5 Dual.
- **Garmin:** Dash Cam 57.
- **Lexand:** LR300.
- **Mini:** 0806.
- **Mio:** MiVue 812, MiVue C530, MiVue C530 Pro, MiVue i95, MiVue J60, MiVue ViVa V51.
- **Navitel:** MR155 NV, MR450 GPS, R250 Dual, RS2 Duo.
- **Neoline:** WIDE S21.
- **Nexar:** Model unidentified (tested 1080p source recording).
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
- **Xiaomi:** MiJia Car DVR 1S Camera.
- **Yi:** Dash Cam.

### Partial support

- **iZEEKER:** Model unidentified; video/audio, GPS and native cut/join/reopen
  are supported. Recorded acceleration is displayed and preserved in raw device
  units; its physical g scale and vehicle-axis orientation remain unconfirmed.

## Downloads

Download available packages from the
[Releases page](https://github.com/andreikrutsko/registratorviewer/releases).
Check the **Assets** list for the packages available in each release.

| Platform | Package |
|---|---|
| Windows x64 | `RegistratorViewer.Next.exe` |
| Ubuntu x64 | `RegistratorViewer.Next-linux-x64` |
| macOS Apple Silicon | `RegistratorViewer.Next-macos-arm64.zip` |
| macOS Intel | `RegistratorViewer.Next-macos-x64.zip` |

On Windows, launch the EXE. On Ubuntu, run
`chmod u+x RegistratorViewer.Next-linux-x64` before launching the application.
On macOS, extract the ZIP and keep the complete `RegistratorViewer.Next.app`.
See [installation](docs/installation.md) for detailed instructions.

Use `SHA256SUMS.txt` to verify your download. GitHub's automatic **Source code**
archives contain this repository's documentation; install the application using
the packages listed above.

## Licenses

See the [application license](LICENSE.txt), [third-party notices](THIRD_PARTY_NOTICES.md)
and [full third-party license texts](THIRD_PARTY_LICENSES/). License texts are also
available offline through **? → Third-party Licenses** and About. Third-party
source archives, when supplied, are listed among the release assets; see
[source-material instructions](docs/installation.md#third-party-source-materials).

Telegram updates: https://t.me/RegistratorViewer

Discussion: https://t.me/RegistratorViewerChat

See [installation](docs/installation.md) and [user guide](docs/user-guide.md).
