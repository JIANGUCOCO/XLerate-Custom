# XLerate Custom – JIANGUCOCO edition

This repository contains a modification of the open-source XLerate project (MIT license). It is not Macabacus. Mac Excel shortcut support is subject to Excel/OS conflicts.

## GitHub Upload (browser method)

1. On your empty GitHub repository, select **uploading an existing file** (or Add file > Upload files).
2. **Extract the ZIP**, open its `XLerate-Custom-Upload` folder and drag **all files and folders from within it**, including `.github`, into the repository root. Do not upload the ZIP itself or a parent folder.
   - On macOS Finder, `.github` is hidden by default. Press `Command + Shift + .` to show hidden files, or upload via GitHub Desktop/git instead. **The `.github/workflows/deploy-pages.yml` file is necessary for automatic deployment.**
3. Commit changes on `main`. In repository **Settings > Pages > Build and deployment**, choose **GitHub Actions**.
4. Open **Actions > Deploy Pages**. If necessary select **Run workflow**, then wait until the deploy job is green.
5. Open https://jiangucoco.github.io/XLerate-Custom/taskpane.html to ensure it loads.
6. Download `manifest-install-on-mac.xml` from the repository (or this ZIP). Rename the downloaded file to `manifest-custom.xml` and put it in `~/Library/Containers/com.microsoft.Excel/Data/Documents/wef/`. Keep the original manifest too. Quit Excel fully (Cmd+Q) and restart.
7. Open **XLerate Custom** and test ribbon buttons and keyboard commands. If Excel asks about shortcut conflicts, choose XLerate Custom.

**Important:** Before GitHub Pages deployment the personalized manifest will not work. If GitHub Pages workflow fails, do not attempt installation yet. A GitHub Actions workflow may require enabling Actions in repository settings.

## Keyboard shortcuts

Ctrl+Shift+1 number formats; Ctrl+Shift+2 cell formats; Ctrl+Shift+3 date formats; Ctrl+Shift+4 text styles; Ctrl+Shift+R smart fill right.

New: Ctrl+Option+Shift+Q/W/S/H/A/G for Trace Precedents / Trace Dependents / Switch Sign / Horizontal Check / Auto-color / Insert CAGR respectively. Test on a disposable workbook.

The custom source retains the MIT license and does not copy proprietary Macabacus code.
