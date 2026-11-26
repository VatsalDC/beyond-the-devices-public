# Beyond the Devices

**A little more connected.** Clipboard sync, media controls, Android
notifications, link handoff, and file transfers between your Android phone and
your Mac — over your own local network. No account, no cloud relay, no
telemetry.

> This repository is the **public home** of Beyond the Devices: bug and feature
> tracking, release downloads with checksums, and security documentation. The
> application source code is proprietary and is not published here.

## System requirements

| Platform | Minimum | Notes |
| --- | --- | --- |
| macOS | macOS 14 Sonoma | Apple Silicon (arm64) only |
| Android | Android 8.0 (API 26) | Google Play |
| Network | — | Both devices on the same local network |

## Download

- **macOS app (v1.3.1):** <https://beyondthedevices.com/download> or the
  [latest GitHub release](https://github.com/VatsalDC/beyond-the-devices-public/releases/latest).
- **Android app:** Google Play (`com.beyondthedevices.app`). The app is in
  closed testing until production access is granted; the download page shows
  the current status.

### Verify your download (SHA-256)

Every disk image is published with its SHA-256 checksum so you can confirm the
file you received is the file we published.

macOS (built-in):

```sh
shasum -a 256 ~/Downloads/BeyondTheDevices-1.3.1.dmg
```

Linux:

```sh
sha256sum ~/Downloads/BeyondTheDevices-1.3.1.dmg
```

Windows (PowerShell):

```powershell
Get-FileHash .\Downloads\BeyondTheDevices-1.3.1.dmg -Algorithm SHA256
```

The expected value for v1.3.1 is:

```
ab941bca3538bdf23035b040222adf759a686a099356a309218671a6a4f4cd8f
```

The same value is listed on the [download page](https://beyondthedevices.com/download)
and in [`checksums/SHA256SUMS.txt`](checksums/SHA256SUMS.txt).

> **First-launch note (macOS).** The current build is signed with an Apple
> Development certificate and is not notarized, so macOS blocks the first
> launch. Open **System Settings → Privacy & Security** and click
> **Open Anyway** once — the download page walks through it. Updates delivered
> through the app's built-in Sparkle updater are EdDSA-signed and verified
> before they are installed.

## Security

- Traffic stays on your local network. There is no relay server, no account
  system, and no telemetry to trust — the two devices talk to each other
  directly.
- The connection is TLS 1.2+ with certificate pinning on both sides, plus a
  per-device credential checked on every session.
- Pairing uses a short-lived, single-use QR code and requires explicit approval
  on the Mac.

Read [`SECURITY.md`](SECURITY.md) to report a vulnerability, and
<https://beyondthedevices.com/security> for the full technical deep-dive.

## Feedback

- **Bug report:** [Open an issue](https://github.com/VatsalDC/beyond-the-devices-public/issues/new/choose)
  using the bug template. Include your macOS version, Android version and app
  versions — that makes every report reproducible.
- **Feature request:** [Open an issue](https://github.com/VatsalDC/beyond-the-devices-public/issues/new/choose)
  using the feature template.
- **Questions:** [Discussions](https://github.com/VatsalDC/beyond-the-devices-public/discussions).
- **Anything else:** <support@beyondthedevices.com>

## Privacy

No account, no sign-up, and no profile to build. Clipboard text, notifications,
media state and files move only between your paired devices. See
<https://beyondthedevices.com/privacy>.

## Release history

Every macOS release is published here as a GitHub release with the disk image
and checksums attached. See [`CHANGELOG.md`](CHANGELOG.md).

## License

The Beyond the Devices applications are proprietary software, © Vatsal Chevli.
The content of this repository — documentation, issue templates, release notes
and checksums — is provided to support your use of the applications. Do not
redistribute the application binaries.
