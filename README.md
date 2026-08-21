# Grain Books — releases

Installers for the Grain Books desktop app, and the manifest the app reads to
find them.

**There is no source code here.** The app is developed in a private repository;
this one exists only so installed copies can check for and download updates
without carrying a credential. A token able to read the private repo has no
business sitting on a mill counter PC, where strings can be pulled out of any
shipped binary.

## latest.json

The app fetches this on launch and compares `build` against its own. Higher
means an update is offered.

```json
{
  "version": "1.0.1",
  "build": 2,
  "url": "https://github.com/.../releases/download/v1.0.1/GrainBooksSetup-1.0.1.exe",
  "notes": "What changed",
  "sha256": "…"
}
```

`sha256` is checked after download. The installer arrives over the public
internet and is then run with the user's privileges, so a file that does not
match is deleted rather than executed.

Published by `tool/release.ps1` in the app repository. The manifest is always
written **after** the installer is uploaded — it is what tells every installed
copy to update, so it must never point at an asset that is not there yet.
