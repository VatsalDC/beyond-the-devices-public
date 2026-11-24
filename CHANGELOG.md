# Changelog

All notable changes to Beyond the Devices are documented in this file. Versions
follow the **macOS app** release train; the Android companion is released
alongside it and keeps its own Play Store version codes.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.3.0] - 2026-11-22

macOS artifact: `BeyondTheDevices-1.3.0.dmg`
SHA-256: `f93213ddbc778c7a809498f51009b5276ee143b6796a373b22fdc3b67eedd7d1`

### Added

- **Home-screen widgets** — battery rings for your phone and Mac, a Mac
  battery bar, a Command Center for sync and playback, and Now Playing, on the
  phone's home screen.
- **Per-widget appearance** — long-press a widget to set its opacity, from
  fully solid to fully clear, independently of the others.
- **One-time Security Setup screen** — the Mac app now explains the Keychain
  prompt before macOS shows it on first launch (and once per updated build).

### Changed

- **Charging detection** — charging is now reported whenever the Mac is on
  power, not only while the battery is actively filling, so a Mac holding at
  80% on the charger reads as charging.
- **Widget colour** — widgets follow the battery level: green when charging or
  healthy, yellow in the middle, orange when low, red when critical.

[1.3.0]: https://github.com/VatsalDC/beyond-the-devices-public/releases/tag/v1.3.0
