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

Users can install it like a normal Windows app.
