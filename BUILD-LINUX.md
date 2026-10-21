# Building the Linux packages

ClaudeIDE ships a native module (`node-pty`), so build on Linux to produce a
Linux package. The configured artifacts target x86_64 Ubuntu systems:

- `dist/ClaudeIDE-<version>-linux-x64.deb` — installable Debian package
- `dist/ClaudeIDE-<version>.AppImage` — portable application image

## Build on Ubuntu

Install the build tools and Electron's Linux development dependencies:

```bash
sudo apt update
sudo apt install -y build-essential python3 make g++ libgtk-3-dev libnotify-dev \
  libnss3 libxss1 libxtst6 libatspi2.0-dev
```

Install the Node.js LTS release, then from the project directory run:

```bash
npm ci
npm run dist:linux
```

`npm ci` runs the project's postinstall hook, which rebuilds `node-pty` against
the Electron version in this project. The `.deb` and AppImage are written to
`dist/`. To create an unpacked app directory for local inspection instead:

```bash
npm run pack:linux
```

The `.deb` declares the Electron runtime libraries as package dependencies, so
APT installs any missing libraries when installing the package. The AppImage
bundles the application; the host still needs a working graphical desktop and
FUSE 2 support (or the AppImage can be extracted with `--appimage-extract`).

Install the Debian package with:

```bash
sudo apt install ./dist/ClaudeIDE-*-linux-x64.deb
```

Claude Code CLI is not bundled. Install it separately and ensure `claude` is on
the PATH of the user launching ClaudeIDE.
