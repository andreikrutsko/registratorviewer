# Installation

Download `RegistratorViewer.Next.exe` from a published release and run it on Windows x64. Install Microsoft WebView2 Evergreen if it is not already present. A separate .NET runtime installation is not required.

Check [system requirements](system-requirements.md) for Windows versions/builds,
graphics drivers, the Vulkan loader and runtime download links.

Verify a download in PowerShell:

```powershell
Get-FileHash ./RegistratorViewer.Next.exe -Algorithm SHA256
```

Compare the resulting value with that release's `SHA256SUMS.txt`. Do not use an EXE whose checksum differs.

Application preferences are stored per Windows user. Online maps require a network connection. Google Maps is optional and requires the user's own API key and billing; keys are not included in releases.
