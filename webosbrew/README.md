# Homebrew Channel repository

`apps.json` is a [Homebrew Channel](https://github.com/webosbrew/webos-homebrew-channel) repository with one app,
Chromium. Add it on the TV in Homebrew Channel under **Settings → Add repository**:

```
https://raw.githubusercontent.com/sarahahzub/WebOS-Chromium/main/webosbrew/apps.json
```

`org.nativechromium.browser.manifest.json` is the same manifest on its own. Attach it to each GitHub release so a
listing in the official repository can point at `releases/latest/download/org.nativechromium.browser.manifest.json`.

For every release, update `version`, `ipkUrl`, `ipkSize` and `ipkHash.sha256` in both files. Homebrew Channel checks
the hash, so they must describe the exact IPK attached to the release:

```
stat -c %s org.nativechromium.browser_<version>_arm.ipk
sha256sum org.nativechromium.browser_<version>_arm.ipk
```
