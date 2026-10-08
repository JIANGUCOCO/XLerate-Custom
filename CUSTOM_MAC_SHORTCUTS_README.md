# XLerate — Macabacus-inspired keyboard edition

This is a source-code modification of XLerate, **not** Macabacus and not a preinstalled executable. It reuses existing XLerate functionality. Check the original project's MIT license.

## Keyboard shortcuts (Mac: Control is the `⌃` key, not Command)

| Shortcut | Operation |
|---|---|
| Ctrl+Shift+1 | Cycle number formats |
| Ctrl+Shift+2 | Cycle cell formats |
| Ctrl+Shift+3 | Cycle date formats |
| Ctrl+Shift+4 | Cycle text styles |
| Ctrl+Shift+R | Smart Fill Right |
| Ctrl+Shift+0 | Reset workbook format settings |
| Ctrl+Option+Shift+Q | Trace precedents |
| Ctrl+Option+Shift+W | Trace dependents |
| Ctrl+Option+Shift+S | Switch sign |
| Ctrl+Option+Shift+H | Horizontal check |
| Ctrl+Option+Shift+A | Auto-color |
| Ctrl+Option+Shift+G | Insert CAGR |

The last six are new and are **not** Macabacus's original key combinations. Macabacus-inspired refers to one-key access to financial modeling actions, not an exact clone. Keys could conflict with system or Excel shortcuts and are not yet verified on a live Mac.

## Critical: deploying modified files

The original `manifest.xml` points at `https://omegarhovega.github.io/XLerate/` and **will load the original application**, even if you simply replace a local `manifest.xml` in Excel's `wef` folder. This project cannot change the upstream website.

To run your changed version:

1. Install Node.js (LTS), then in the `XLerate/` directory execute `npm ci` and `npm run build`.
2. Host the generated `dist/` web assets over HTTPS on **a domain you control** (for example your own GitHub Pages site). Include `taskpane.html`, `shortcuts.json`, generated JS/CSS, icons and any referenced assets.
3. Copy `manifest.xml` to `manifest.custom.xml` and replace **all** instances of `https://omegarhovega.github.io/XLerate/` with your own hosted HTTPS base URL. The `ExtendedOverrides` URL must point to your hosted `shortcuts.json`.
4. Change the `<Id>` GUID to a new GUID for this personalized add-in, so it does not collide with the original installation. Optionally update `<DisplayName>` to `XLerate Custom`.
5. Place the personalized manifest XML in `~/Library/Containers/com.microsoft.Excel/Data/Documents/wef/`. Restart Excel and open the new add-in. Use Excel's shortcut-conflict prompt to assign the key to XLerate Custom.
6. Before testing, save a copy of the workbook. Validate that *both* ribbon buttons and shortcuts operate. The Mac LTSC 2024 client has not been tested by this build environment.

**If you lack an HTTPS host, stop before step 3:** modifying a local manifest alone won't work. An HTTPS development server and a manifest targeting that server are an alternative, but you need it running every time you use the add-in.

## Source modifications

- `XLerate/shortcuts.json`: six new keyboard action definitions and platform mappings.
- `XLerate/src/taskpane/ribbonActions.ts`: six keyboard handlers mapped to existing services.

No proprietary Macabacus code has been copied. No claim of equivalence with Macabacus functionality.
