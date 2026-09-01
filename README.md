# Simply Report — Releases

Download page and release hosting for **Simply Report** (`com.safehouse.simplyreport`), an Android app by Safe House Project.

- **Download page:** https://skyevasquez.github.io/simplyreport/
- **Releases:** https://github.com/skyevasquez/simplyreport/releases

## Publishing a new version

1. **Build & sign** the release APK.
2. **Checksum:**
   ```bash
   shasum -a 256 simplyreport-vX.Y.Z.apk > SHA256SUMS.txt
   ```
3. **Upload to GitHub Releases:**
   ```bash
   gh release create vX.Y.Z simplyreport-vX.Y.Z.apk SHA256SUMS.txt \
     --title "vX.Y.Z" --notes "…"
   ```
4. **Update the download page** (`index.html`): version chip, APK filename/URL, size, SHA-256 (truncated + full).
5. Commit and push — GitHub Pages redeploys automatically.

## Analytics (GitHub-native, no third-party tracking)

Download counts are counted server-side by GitHub on the release asset — every hit on the asset URL counts, even direct links shared elsewhere.

- **Download counts via API:**
  ```bash
  gh api repos/skyevasquez/simplyreport/releases --jq '.[] | .tag_name as $t | .assets[] | "\($t)  \(.name): \(.download_count) downloads"'
  ```
- **On the release page:** asset download counts show next to each file at
  https://github.com/skyevasquez/simplyreport/releases
- **On the download page:** a live "N downloads" chip is rendered from the public GitHub API.
- **Repo traffic** (visitors, views, clones, referrers): https://github.com/skyevasquez/simplyreport/graphs/traffic — note this covers repo traffic only; GitHub does not expose GitHub Pages pageviews via API.

## Verifying a download

```bash
shasum -a 256 -c SHA256SUMS.txt   # → simplyreport-vX.Y.Z.apk: OK
```
