# Allowing RegistratorViewer.Next to run on macOS

RegistratorViewer.Next for macOS has an **ad hoc (technical) code signature**.
It has no Apple Developer ID signature and is not notarized by Apple. The
technical signature allows macOS to validate the app's code, but does not identify
an Apple-verified developer or provide notarization. A downloaded copy requires
your manual permission at first launch.

The filename of this guide says "unsigned" for convenience; the released app
already has its technical signature. You do not need to sign it yourself.

## 1. Choose and verify your download

1. Check **Apple menu > About This Mac**. A **Chip** such as Apple M1/M2/M3/M4
   means Apple Silicon; an **Intel Processor** means Intel. Use macOS **26.0 or
   later**.
2. Open the project's [GitHub Releases page](https://github.com/andreikrutsko/registratorviewer/releases).
3. Download the matching application ZIP and `SHA256SUMS.txt` from the **same
   release**:

   | Mac | Application download |
   |---|---|
   | Apple Silicon | `RegistratorViewer.Next-macos-arm64.zip` |
   | Intel | `RegistratorViewer.Next-macos-x64.zip` |

4. Open **Terminal** from **Applications > Utilities**. If the files are in
   Downloads, use the command matching your ZIP:

   ```sh
   cd "$HOME/Downloads"
   shasum -a 256 "RegistratorViewer.Next-macos-arm64.zip"
   ```

   For Intel, replace the last command with:

   ```sh
   shasum -a 256 "RegistratorViewer.Next-macos-x64.zip"
   ```

5. Open `SHA256SUMS.txt` and compare the calculated value with the line naming
   that exact ZIP. Continue only if they match. If they differ, download the
   files again from the release page.

## 2. Install the complete application

1. Double-click the verified ZIP in Finder to extract it.
2. Move **RegistratorViewer.Next.app** to **Applications**. Finder may hide the
   `.app` suffix. Move the complete application, including its contents.
3. Keep the app as supplied. No separate .NET, Homebrew, mpv, FFmpeg or developer
   tools installation is required.

The commands below assume `/Applications/RegistratorViewer.Next.app`. If you
instead use your own `~/Applications` folder, substitute its actual full path.

## 3. Allow the first launch in System Settings

Use this procedure only for a download you trust and whose checksum you verified.

1. Double-click **RegistratorViewer.Next** in Applications.
2. macOS may say that the developer cannot be verified or Apple cannot check the
   app for malicious software. Dismiss that dialog with **Done**, **OK** or
   **Cancel**, depending on the wording.
3. Open **Apple menu > System Settings > Privacy & Security**.
4. Scroll down to **Security**. Find the message saying that
   RegistratorViewer.Next was blocked and click **Open Anyway**.
5. Authenticate with Touch ID or your Mac account password if requested.
6. In the confirmation dialog, click **Open**.

macOS saves an exception for this app, so subsequent launches normally work by
double-clicking it. A new version may need permission again. On macOS Sequoia
and later, Control-click is not a substitute for this approval procedure for
software that is not correctly signed or notarized.
[Apple's instructions](https://support.apple.com/en-us/102445) describe the
warning and the Privacy & Security exception; the
[Sequoia change](https://developer.apple.com/news/?id=saqachfa) explains the
Control-click behavior.

If **Open Anyway** does not appear, try opening the installed app again, then
return to Privacy & Security. On an organization-managed Mac, security policy
may require your administrator to authorize the application.

## 4. Optional Terminal procedure for a verified, trusted copy

If the usual approval procedure is unavailable, you can remove the quarantine
attribute from this application only. First check that its existing signature
is intact:

```sh
codesign --verify --deep --strict --verbose=2 "/Applications/RegistratorViewer.Next.app"
```

Continue only if verification succeeds. This checks signature integrity; it does
not turn the ad hoc signature into Developer ID signing or Apple notarization.
Then run:

```sh
xattr -dr com.apple.quarantine "/Applications/RegistratorViewer.Next.app"
open "/Applications/RegistratorViewer.Next.app"
```

The `xattr` command removes the quarantine attribute recursively from that exact
app bundle. It does not change the executable signature or disable Gatekeeper
for other applications. Administrator privileges are normally unnecessary for
an app you own. If access is denied, use your own Applications folder or ask
your administrator about installation permissions.

## If the app still will not open

- **Wrong architecture or macOS version:** check About This Mac and use the
  appropriate ZIP for macOS 26.0 or later.
- **No such file:** check where you moved the app and its actual name. You can
  drag the application from Finder into Terminal to insert its path.
- **Invalid signature or damaged bundle:** download and extract a fresh copy,
  verify its ZIP checksum, and keep the complete bundle. Removing quarantine
  cannot repair a changed or missing signature. Do not re-sign the release app
  as an installation step; this can change permissions it needs.
- **An explicit malware or “will damage your computer” alert:** do not treat it
  as the ordinary unidentified-developer warning. Stop and report the exact
  alert and release version through the project's support channel.

Do not disable Gatekeeper globally or System Integrity Protection to run this
application. See [installation](installation.md),
[system requirements](system-requirements.md#macos-versions-and-package-types)
and the [user guide](user-guide.md) for the remaining setup and controls.
