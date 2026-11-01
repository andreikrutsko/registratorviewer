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
media tools; Ubuntu uses native `mpv`, `ffmpeg` and `ffprobe` system packages.
PowerShell and a development SDK are not needed to run the Ubuntu application.
Earlier releases may offer only the Windows asset.

Preferences are stored in `~/.registratorviewer-next.yml` in the current user's
home on both platforms. Online maps require a network connection. Google Maps
is optional and requires the user's own API key and billing; keys are not included.
