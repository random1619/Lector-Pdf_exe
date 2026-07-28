# Lector PDF Reader — Desktop Edition

Lector PDF Reader is the Windows desktop build of the PDF reader and annotation app. It packages the React/Vite interface, the local Express API, and your PDF library into an Electron application that can be installed as a normal `.exe` app.

## What You Get

- Desktop window for the Lector PDF reader
- Local PDF library view from the bundled `pdfs/` folder
- PDF reading, page navigation, zoom, fullscreen reading, and thumbnails
- Local annotations, bookmarks, read status, settings, and reading position storage
- Windows installer generated with Electron Builder

## Project Layout

```text
pdf-reader/
├── electron/main.mjs      # Electron desktop entry point
├── server/index.js        # Local Express API used by web and desktop builds
├── src/                   # React PDF reader UI
├── pdfs/                  # PDFs bundled/copied into the desktop app
├── dist/                  # Vite production build output
├── release/               # Desktop build output
└── package.json           # Desktop scripts and electron-builder config
```

## Requirements

- Windows 10/11
- Node.js 20 or newer recommended
- npm

## Install Dependencies

From the project root:

```powershell
cd "C:\Users\gagan\Downloads\Current affairs PDF\pdf-reader"
npm install
```

## Run Desktop App in Development

```powershell
npm run desktop:dev
```

This starts Vite and opens the app in an Electron desktop window.

## Build Windows EXE Installer

```powershell
npm run desktop:dist
```

After a successful build, the installer is created at:

```text
release\Lector PDF Reader-Setup-0.0.0.exe
```

You can also run the unpacked desktop app directly from:

```text
release\win-unpacked\Lector PDF Reader.exe
```

## Build Output

The generated `release/` folder may include:

```text
release/
├── Lector PDF Reader-Setup-0.0.0.exe
├── Lector PDF Reader-Setup-0.0.0.exe.blockmap
├── builder-effective-config.yaml
└── win-unpacked/
    └── Lector PDF Reader.exe
```

## Runtime Data

In development mode, the app uses the project folder for data:

```text
pdfs/
.annotations/
.appdata/
```

In the installed desktop app, runtime data is stored in Electron's user data directory. Bundled PDFs from `pdfs/` are copied into the desktop app data folder on first launch.

## Common Build Warnings

### Vite chunk size warning

```text
Some chunks are larger than 500 kB after minification
```

This is only a warning. The app still builds successfully.

### Missing author warning

```text
author is missed in the package.json
```

This is optional metadata. Add an `author` field in `package.json` if you want to remove it.

### Default Electron icon warning

```text
default Electron icon is used
```

This means no custom app icon is configured yet. The app still works.

## Fix Windows File Lock Build Errors

If packaging fails with an error like:

```text
EPERM: operation not permitted, rename release\win-unpacked.tmp -> release\win-unpacked
```

Close any running Lector/Electron app and remove stale build folders:

```powershell
Get-Process electron,"Lector PDF Reader" -ErrorAction SilentlyContinue | Stop-Process -Force
Remove-Item -Recurse -Force ".\release\win-unpacked", ".\release\win-unpacked.tmp" -ErrorAction SilentlyContinue
npm run desktop:dist
```

If needed, delete the full release folder:

```powershell
Remove-Item -Recurse -Force ".\release" -ErrorAction SilentlyContinue
npm run desktop:dist
```

## Useful Scripts

| Script | Purpose |
| --- | --- |
| `npm run dev` | Run browser development mode |
| `npm run build` | Build the React/Vite app |
| `npm run desktop:dev` | Run desktop development mode |
| `npm run desktop:pack` | Create unpacked desktop app in `release/` |
| `npm run desktop:dist` | Create Windows installer `.exe` |
| `npm run dist:win` | Alias for `desktop:dist` |

## Distribution

To share the desktop app, distribute this file:

```text
release\Lector PDF Reader-Setup-0.0.0.exe
```

Users can install it like a normal Windows app.
