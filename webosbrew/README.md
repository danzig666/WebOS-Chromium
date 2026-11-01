# Homebrew Channel repository

`apps.json` is a [Homebrew Channel](https://github.com/webosbrew/webos-homebrew-channel) repository with one app,
Chromium. Add it on the TV in Homebrew Channel under **Settings → Add repository**:

```
https://raw.githubusercontent.com/sarahahzub/WebOS-Chromium/main/webosbrew/apps.json
```

`org.nativechromium.browser.manifest.json` is the same manifest on its own. Attach it to each GitHub release so a
listing in the official repository can point at `releases/latest/download/org.nativechromium.browser.manifest.json`.

## Releasing

The **Release** workflow (`.github/workflows/release.yml`) keeps both files up to date:

1. Create a GitHub release with the tag `v<version>` and attach `org.nativechromium.browser_<version>_arm.ipk`.
2. Publish it (not as a pre-release). The workflow checks that the IPK's package id and version match the tag,
   writes `version`, `ipkUrl`, `ipkSize` and `ipkHash.sha256` into both files, commits them to the default branch,
   and attaches the manifest and a `SHA256SUMS` file to the release.

To re-run it for an existing release, use **Actions → Release → Run workflow** and enter the tag.

Homebrew Channel checks the hash, so the files must describe the exact IPK attached to the release. To update them
by hand instead:

```
stat -c %s org.nativechromium.browser_<version>_arm.ipk
sha256sum org.nativechromium.browser_<version>_arm.ipk
```
