# Edge removal link fix

[中文](README.md) | English

Tested on **Windows 11 25H2**.

After Microsoft Edge has been force-removed, clicking a web link brings up *"You'll need a new app to open this https link"* and the link never opens. The removal also deletes Windows' built-in `http` / `https` protocol definitions. Importing the registry file in this repo restores them.

> Getting an ms-gamebar popup when you press the Xbox button on a controller? That is a separate problem — see [xbox-popup-fix](https://github.com/AINLZE/xbox-popup-fix).

## Fix with the file

1. Download `fix-https-popup.reg`.
2. Double-click it and approve the UAC prompt. **Administrator rights are required** because it writes to `HKEY_LOCAL_MACHINE`.

If links still won't open afterwards, pick your browser again under *Settings › Apps › Default apps*.

## What it changes

- Recreates the `http` and `https` protocol definitions under `HKEY_LOCAL_MACHINE\SOFTWARE\Classes`.
- Per-user `http` / `https` keys override the system ones, so if they exist they are marked as `URL Protocol` too.

## Fix it by hand

Run `regedit` as administrator:

1. Create `HKEY_LOCAL_MACHINE\SOFTWARE\Classes\https` and add an empty string value named `URL Protocol`.
2. Do the same for `http`.
3. If `HKEY_CURRENT_USER\Software\Classes\https` (or `http`) already exists, add `URL Protocol` to it as well.

> This edits the registry. Use at your own risk.
