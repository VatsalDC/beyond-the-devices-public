# Security policy

## Supported versions

| Platform | Version | Status |
| --- | --- | --- |
| macOS | 1.3.0 | Supported |
| Android | latest Play release | Supported |

Older versions receive no fixes. The macOS app's built-in updater (Sparkle)
prompts to install the latest release automatically.

## Reporting a vulnerability

If you believe you have found a security issue in Beyond the Devices, please
report it privately instead of opening a public issue:

**Email: <support@beyondthedevices.com>** — start the subject with
`[SECURITY]`.

Please include:

1. Which app and version is affected (macOS, Android, or both).
2. A description of the issue and its potential impact.
3. Steps to reproduce, and any proof-of-concept you can share.
4. Whether you plan to disclose publicly, and when.

What to expect:

- We acknowledge reports within **5 business days** and aim to confirm or
  decline within **30 days**.
- We will keep you informed of progress and credit you when the fix ships
  (unless you prefer to stay anonymous).
- We follow a 90-day coordinated-disclosure window where the reporter agrees
  to it. Reports about the website's static hosting are in scope too.
- There is no bug bounty program and no reward for reports, but reports made
  in good faith are treated as contributions, not violations.

### Safe harbor

We will not pursue claims against you for security research conducted in good
faith if you: test only your own devices or environments you are authorized to
test, avoid accessing other users' data, and give us a reasonable window
before disclosing.

## Architecture summary

Beyond the Devices is **local-only by design**. There is no account system, no
cloud relay, no telemetry service, and no server component for the product to
host user data on. The attack surface is the two devices and the link between
them:

- **Discovery** — while paired, the Mac advertises an mDNS/Bonjour service
  (`_beyondthedevices._tcp`). The TXT record carries only
  `SHA-256(a 6-digit token)`, never the token itself, and the phone accepts an
  advertisement only if the hash matches what it stored at pairing. The QR
  code / manual entry carries the literal `ip:port` as a fallback.
- **Pairing** — a short-lived (5-minute), single-use invitation is encoded in
  the QR code together with the Mac's certificate fingerprint. The phone
  connects over TLS, verifies the pinned fingerprint, and the Mac must approve
  the device explicitly.
- **Transport** — TLS 1.2 minimum, with the Mac serving a per-install
  EC P-256 self-signed certificate from the Keychain, and the phone pinning
  the exact SHA-256 of that certificate. There is no plaintext fallback. On
  top of TLS, every session authenticates with a 32-byte credential whose
  SHA-256 (only) is stored on the Mac and compared in constant time.
- **Storage** — the Mac's TLS private key and certificate live in the macOS
  Keychain; the pairing record is a 0600 file holding only a device id, a
  display name and a hash verifier. On Android, pairing secrets live in
  EncryptedSharedPreferences (Android KeyStore-backed). Clipboard text is
  memory-only on both sides.

The only traffic that leaves the local network is the Mac's Sparkle update
check (a static feed on beyondthedevices.com; EdDSA-signed updates) and
Android's normal Google Play traffic. The QR scanner uses Google ML Kit's
bundled, on-device scanner, which sends limited diagnostics to Google (see the
[privacy policy](https://beyondthedevices.com/privacy)).

The full technical deep-dive is at
<https://beyondthedevices.com/security>.

## Known limitations (current release)

These are disclosed, not hidden:

- **Not notarized.** The macOS build is signed with an Apple Development
  certificate and is not notarized; macOS blocks the first launch and the user
  must choose *Open Anyway*. Once notarization is in place this entry will be
  removed.
- **Keychain re-prompts after updates.** The Keychain binds access to the
  signing identity of each build, so macOS may ask once for the app's own TLS
  key after an update. The app shows an explanatory "One-Time Security Setup"
  screen first. Choosing *Always Allow* binds the grant to that build.
- **No signed PGP releases.** Release integrity is provided by SHA-256
  checksums on the download page, GitHub releases and this changelog, plus
  EdDSA signatures for in-app Sparkle updates.
