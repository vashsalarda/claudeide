# Building the macOS releases

ClaudeIDE ships the native `node-pty` module, so build on macOS. The release
build creates DMG installers and ZIP archives for both Apple Silicon and Intel:

- `dist/ClaudeIDE-<version>-mac-arm64.dmg` and `.zip`
- `dist/ClaudeIDE-<version>-mac-x64.dmg` and `.zip`

Install Xcode Command Line Tools and Node.js LTS, then run from the project
directory:

```bash
xcode-select --install
npm ci
npm run dist:mac
```

The files are written to `dist/` and can be uploaded to the GitHub Release.
For an unpacked app directory instead, run `npm run pack:mac`.

The app is currently unsigned and not notarized. macOS may require users to
control-click the app and choose **Open** the first time they launch it.
Claude Code CLI is not bundled; install it separately and ensure `claude` is
available in the shell's PATH.