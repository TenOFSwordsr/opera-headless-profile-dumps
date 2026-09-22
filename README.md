# da-debug - Opera headless browser profile dumps

Debugging scratch for a headless Opera launch: two throwaway Chromium user-data
directories and the console log from one run. There is no source code here.

**Suggested repo name:** - (do not publish)
**Stack:** Chromium/Opera profile state only
**Status:** data only
**Last modified:** 2026-09-03

## What it is

- `profile/` and `profile2/` - two `--user-data-dir` trees captured while driving headless
  Opera (~126 MB and ~123 MB). Each holds the standard Chromium layout: `Default/`,
  `Local State`, component bundles (`WidevineCdm`, `PKIMetadata`,
  `CertificateRevocation`, `AmountExtractionHeuristicRegexes`, `MEIPreload`),
  `GPUPersistentCache`, `GrShaderCache`, `Crash Reports`.
- `opera_headless.log` - 8 lines of stderr from a single run: registry-key warnings for
  `UrlAssociations\https\UserChoiceLatest\ProgId`, a missing partner-speeddials file, and
  an absl log-initialisation notice. No request traces, no errors from the driving script.

## Layout

```
opera_headless.log     1.4 KB stderr capture
profile/               126 MB Chromium user-data-dir
profile2/              123 MB Chromium user-data-dir (second attempt)
```

## Notes

- The `browser.js` files inside each profile are Opera/Chromium component files, not
  authored code.
- **Nothing publishable here.** A `user-data-dir` is exactly the artifact that accumulates
  cookies, session tokens and history; the two `Default/` trees must be treated as
  containing live credentials for whatever was logged in during the debug session.
- The parent work this belongs to is the Opera-driven automation in
  `Documents/Projects/linkedin-search` and `~/opera-job-auto-apply`, not this folder.
- Safe to delete once the scraping/debug work it came from is finished - it is ~250 MB of
  regenerable browser state.
