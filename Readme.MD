<div align="center">

# XLerate Custom

**Macabacus-inspired keyboard workflows for Excel financial modeling**

An experimental, Mac-focused customization of the open-source [XLerate](https://github.com/omegarhovega/XLerate) Office.js add-in.
Spend less time navigating the ribbon—and more time building, checking, and understanding models.

[![CI](https://github.com/JIANGUCOCO/XLerate-Custom/actions/workflows/ci.yml/badge.svg)](https://github.com/JIANGUCOCO/XLerate-Custom/actions/workflows/ci.yml)
[![Deploy Pages](https://github.com/JIANGUCOCO/XLerate-Custom/actions/workflows/deploy-pages.yml/badge.svg)](https://github.com/JIANGUCOCO/XLerate-Custom/actions/workflows/deploy-pages.yml)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
![Status: experimental](https://img.shields.io/badge/Status-experimental-orange.svg)

[What's new](#whats-new) · [Shortcuts](#keyboard-shortcuts) · [Install on Mac](#installation-mac-excel) · [Demo](#demo) · [Troubleshooting](#troubleshooting)

</div>

> [!IMPORTANT]
> **Project status: experimental.** The added keyboard mappings are implemented in the source and shortcut configuration; they have **not** all been confirmed to work in Excel for Mac (Office LTSC 2024). The customized ribbon has also displayed as blank in some local tests. Check both ribbon commands and shortcuts in a disposable workbook before using this add-in on live financial models. A green CI/Pages badge means the code pipeline ran—not that Excel client behavior has been verified.

## Why this project?

Building three-statement models, operating forecasts, or valuation workbooks involves constant formatting, formula tracing, and checking. XLerate already implements useful modeling actions; this customization experiments with making more of those **existing features keyboard-accessible on Mac**.

It is inspired by the **keyboard-first productivity approach** of Macabacus, but it is **not Macabacus**, is not affiliated with Macabacus, and does not copy Macabacus proprietary code.

## What's new?

| Area | Original XLerate | XLerate Custom |
|:--|:--|:--|
| Core financial-modeling operations | Formula tracing, sign switching, formatting cycles, checks, auto-color, CAGR | **Preserved** existing XLerate implementations |
| Keyboard access | Shortcuts for selected formatting and fill actions | **Six additional shortcut bindings** for existing analysis / formatting actions |
| Mac shortcuts | Primarily shared key combinations | **Mac-specific Command + Option + Shift** combinations for the six new bindings |
| Deployment | Upstream hosted resources | Custom GitHub Pages deployment with GitHub Actions |
| Development focus | General add-in workflow | Experimental keyboard-first Mac Excel workflow |

**Scope:** 12 shortcut mappings are currently configured. This is an extension of the input workflow, **not** six newly invented calculation engines or a complete Macabacus replacement.

## Keyboard shortcuts

### Standard XLerate actions (retained)

| Mac keys | Action | What it does |
|:--|:--|:--|
| `⌃ ⇧ 1` | Cycle number formats | Rotate through configured number formats |
| `⌃ ⇧ 2` | Cycle cell formats | Rotate through preset cell formatting |
| `⌃ ⇧ 3` | Cycle date formats | Rotate through preset date formats |
| `⌃ ⇧ 4` | Cycle text styles | Rotate through text style presets |
| `⌃ ⇧ R` | Smart Fill Right | Extend the active formula to a detected right boundary |
| `⌃ ⇧ 0` | Reset format settings | Reset workbook-specific format settings |

### Additional bindings in XLerate Custom

| Mac keys | Action | Modeling use |
|:--|:--|:--|
| `⌘ ⌥ ⇧ Q` | Trace Precedents | Investigate the inputs behind a calculation |
| `⌘ ⌥ ⇧ W` | Trace Dependents | See where an assumption flows through a model |
| `⌘ ⌥ ⇧ S` | Switch Sign | Flip signs on selected amounts / formulas |
| `⌘ ⌥ ⇧ H` | Horizontal Check | Spot inconsistent copy-across formulas |
| `⌘ ⌥ ⇧ A` | Auto-color | Apply input / formula / link color conventions |
| `⌘ ⌥ ⇧ G` | Insert CAGR | Build a CAGR formula from the adjacent data series |

**Key legend:** `⌃` Control · `⌥` Option · `⇧` Shift · `⌘` Command. The new Mac mappings reflect the latest `XLerate/shortcuts.json` configuration. **Configured ≠ independently verified**; Excel and macOS may intercept a combination or require resolution of a shortcut conflict. Windows/default shortcuts for the six additions are `Ctrl + Alt + Shift + Q/W/S/H/A/G`.

## Core features

| Feature | How to use it in a worksheet |
|:--|:--|
| **Trace Precedents / Dependents** | Select a formula or assumption, then run the matching command to inspect source or downstream references. |
| **Switch Sign** | Select numeric constants or formulas to reverse their sign; text remains unchanged. |
| **Smart Fill Right** | Start from a **formula cell**. XLerate looks up to three rows above for a continuous reference area that defines the fill boundary. |
| **Horizontal Check** | Select a row of formulas and inspect possible breaks in copy-across patterns. |
| **Cycle formats** | Apply consecutive number, date, cell, or text presets, configurable in the task pane. |
| **Auto-color** | Color selected populated cells by model semantics (inputs, formulas, sheet references and other categories). |
| **Insert CAGR** | Select an empty result cell immediately to the right of a suitable consecutive numeric series. |

## Demo

**Real Excel demo footage is being prepared.** The existing screenshots from early development showed a blank Custom ribbon, so they are intentionally **not presented as a working-feature demonstration**.

A short before/after screen recording will demonstrate:

1. **Switch Sign** — select `100`, run the key combination, verify `-100`.
2. **Trace Precedents** — select `=B2*C2`, open the formula trace dialog.
3. **Auto-color / Horizontal Check** — show coloring and a deliberately inconsistent projection formula.

See [the demo capture guide](assets/demo/README.md) for a one-minute storyboard and the exact screenshot filenames. When verified captures are available, add these images to `assets/demo/` and uncomment the image lines below.

<!-- Verified assets only; do not publish mockups as Excel screenshots.
![XLerate Custom ribbon in Excel for Mac](assets/demo/ribbon.png)
![Switch Sign before and after](assets/demo/switch-sign.png)
![Formula tracing example](assets/demo/trace-precedents.png)
-->

## Installation: Mac Excel

This is a **sideloaded Office.js add-in**, not a classic `.xlam` file. These steps are for testing your own build; the initial source deployment has been configured for this repository.

1. Confirm the [Deploy Pages workflow](https://github.com/JIANGUCOCO/XLerate-Custom/actions/workflows/deploy-pages.yml) completed successfully. Confirm the [hosted task pane](https://jiangucoco.github.io/XLerate-Custom/taskpane.html) opens in your browser.
2. Download [**`manifest-install-on-mac.xml`**](manifest-install-on-mac.xml) using GitHub's **Raw / Download raw file** control (save it as `.xml`, not `.txt`).
3. In Finder use `Shift + Command + G` and open:

   ```text
   ~/Library/Containers/com.microsoft.Excel/Data/Documents/wef/
   ```

   Create the `wef` folder if needed. Place the downloaded XML file there.
4. Quit Excel completely (`Command + Q`), then restart Excel and open a workbook. Find the sideloaded add-in / its ribbon entry.
5. Test a harmless command on a **copy of a workbook**. Where an Office shortcut-conflict dialog appears, choose the XLerate Custom action you intend to use.

**Important:** If you have both original XLerate and XLerate Custom installed, they may display similarly named ribbon tabs. Temporarily remove the old **original** manifest from `wef` to isolate conflicts, but keep a backup. The add-in name and ribbon tab label can differ. Do not use Excel's classic **Tools → Excel Add-ins → Browse** dialog for this Office.js XML manifest.

### Build from source

```bash
cd XLerate
npm ci
npm run build
```

GitHub Actions builds and hosts the `XLerate/dist` output over HTTPS. To deploy changes, commit to `main` and review **Actions → Deploy Pages**. See [deployment notes](DEPLOY_README.md) for repository-specific details.

## Troubleshooting

| Symptom | Check |
|:--|:--|
| **Custom ribbon tab is blank** | This is a known unresolved Mac test issue. Do not assume a successful GitHub Pages build proves ribbon commands are registered correctly. Inspect the manifest, icon/resource URLs, Office client cache, and task pane command registration. |
| **Task pane opens, shortcuts do nothing** | Test the corresponding ribbon action first, check shortcut conflicts, verify the deployed `shortcuts.json` is the new build, and distinguish Command from Control. |
| **Two XLerate tabs** | The original and customized manifests may both be registered; isolate them while testing. |
| **Shortcut invokes Excel instead** | Resolve Excel's shortcut conflict dialog for that specific combination; if available, use Office's **Reset Office Add-in Shortcut Preferences** command to choose again. |
| **Changes not appearing** | Confirm Pages deployment succeeded, then fully quit and restart Excel; cached manifest or assets may persist. |

Found a bug? Please [open an issue](https://github.com/JIANGUCOCO/XLerate-Custom/issues) with Excel edition/version, macOS version, exact key combination, and screenshots or steps to reproduce. **Never post credentials or personal workbook data.**

## Credits & licensing

Built on the original **[XLerate](https://github.com/omegarhovega/XLerate)** by **omegarhovega**, licensed under the [MIT License](LICENSE). Credit and copyright notices are retained. The original implementation supplies the modeling functions; this repository customizes shortcut registration and deployment for an experimental Mac workflow.

**Macabacus** is referenced only as inspiration for efficient, keyboard-led modeling workflows. This project is not affiliated with or endorsed by Macabacus, Microsoft, or the original XLerate author.
