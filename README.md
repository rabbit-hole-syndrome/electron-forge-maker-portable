# Electron Forge Maker Portable

> Electron Forge Maker for portable Windows apps

Electron Forge Maker Portable is a [Maker plugin](https://www.electronforge.io/config/makers) for Electron Forge that allows you to bundle your Electron files into a single standalone & portable `.exe` file on Windows.

## Usage

Add `@rabbitholesyndrome/electron-forge-maker-portable` to your `electron-forge` Maker config:

```json
{
  "config": {
    "forge": {
      "makers": [
        {
          "name": "@rabbitholesyndrome/electron-forge-maker-portable"
        }
      ]
    }
  }
}
```

## Background

In `electron-forge`, the only built-in way to package Windows binaries is using the `Windows.Squirrel` Maker. Why do we need to package Electron apps? Electron requires a bunch of extra files and dependencies (eg. `.dll` files) in order for the `.exe` file to run, so we need a way to distribute all of these files together.

`Windows.Squirrel` works great if you are okay with an "installer" `.exe` that unpacks all the files to a location on the user's PC. If you wish to have a single portable `.exe` instead, this will not work.

Other Electron tools like `electron-builder` support additional targets on top of `Windows.Squirrel`, specifically NSIS (Nullsoft Scriptable Install System). NSIS is capable of bundling all of the Electron files into a single portable `.exe` file.

This plugin injects `electron-builder`'s NSIS portable builder logic into `electron-forge` as a Maker plugin so that you can build portable `.exe` files while staying within the Electron Forge ecosystem.

## Config

This Maker accepts a `config` property. Anything passed to `config` will get merged into `electron-builder`'s [configuration](https://www.electron.build/configuration/configuration) before it is executed by `electron-builder`:

```json
{
  "config": {
    "forge": {
      "makers": [
        {
          "name": "@rabbitholesyndrome/electron-forge-maker-portable",
          "config": {
            "appId": "com.example.app"
          }
        }
      ]
    }
  }
}
```

Specifically you might be interested in the [`nsis`/`portable`](https://www.electron.build/configuration/nsis) config options:

```json
{
  "config": {
    "forge": {
      "makers": [
        {
          "name": "@rabbitholesyndrome/electron-forge-maker-portable",
          "config": {
            "portable": {
              "artifactName": "${productName}-app-${version}.${ext}"
            }
          }
        }
      ]
    }
  }
}
```

Please see the `electron-builder` [documentation](https://www.electron.build/configuration/configuration) for all the configuration options available.

## License

MIT
