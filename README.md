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
4. **Update the download page** (`index.html`): version chip, APK filename/URL, size, SHA-256 (truncated + full), and the `RELEASE_PROPS` analytics object.
5. Commit and push — GitHub Pages redeploys automatically.

## Analytics

The page tracks via [PostHog](https://posthog.com): page views, `download_clicked`, `checksum_copied`, `checksum_expanded`, and `github_release_clicked`.

To activate, paste your PostHog **project API key** (starts with `phc_`) into `POSTHOG_KEY` at the bottom of `index.html`. Until then, the page works normally with tracking disabled.

Release download counts are also available from GitHub:
```bash
gh api repos/skyevasquez/simplyreport/releases --jq '.[].assets[] | {name, download_count}'
```

## Verifying a download

```bash
shasum -a 256 -c SHA256SUMS.txt   # → simplyreport-vX.Y.Z.apk: OK
```
