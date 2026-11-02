# ZS Localizer — releases

The built installers of [ZS Localizer](https://github.com/blkpanfa/zs-localizer) (private) and the `latest.json` the installed app's
updater reads. Nothing here is source.

- Each release is a tag `vX.Y.Z` made by `app/scripts/release.mjs` in the zs-localizer repo, run on the computer that builds
  that platform (Windows: the NSIS `-setup.exe`; macOS: the `.app.tar.gz`), each with its `.sig` from the update key kept in
  `~/.tauri/zs-localizer.key`, never in a repo. Publishing (gh release create / upload) needs the signed-in blkpanfa account,
  which both computers have.
- `latest.json` on a release lists every platform published to it; the installed app fetches
  `https://github.com/blkpanfa/zs-localizer-releases/releases/latest/download/latest.json` (tauri.conf.json › plugins.updater),
  checks the signature against the public key built in, and offers Install and restart.
- 🔴 That fetch is unauthenticated, so the updater only works while this repo is PUBLIC (it is, since 2026-11-02): a private
  repo's release assets cannot be downloaded without a token, and the installed app carries none. Keep it public; the
  installers are what a user would get anyway, and nothing else lands here.
- Until the first release is published, an installed copy's update check reports an error (there is no `latest.json` to read).
