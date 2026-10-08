# Codex Usage installation model

Codex Usage remains a single native Windows executable. Installation only places the executable and an uninstall helper in a stable per-user directory; it does not add a runtime, service, driver, telemetry component, or machine-wide dependency.

## Direct installation

- Install directory: `%LOCALAPPDATA%\Programs\CodexUsage`
- Executable: `%LOCALAPPDATA%\Programs\CodexUsage\codex-usage.exe`
- Uninstall helper: `%LOCALAPPDATA%\Programs\CodexUsage\uninstall.ps1`
- Start menu shortcut: `%APPDATA%\Microsoft\Windows\Start Menu\Programs\Codex Usage.lnk`
- Add/Remove Programs key: `HKCU\Software\Microsoft\Windows\CurrentVersion\Uninstall\CodexUsage`

The installer is per-user and does not request elevation. It verifies the release SHA256 before replacing an existing executable. Replacement uses a temporary file and keeps the previous executable until the new file has been placed successfully.

## Portable mode

`codex-usage.exe` can be run from any user-writable directory without installation. Portable mode uses the same `%APPDATA%\CodexUsage\settings.json` settings as a direct or WinGet installation.

## Settings and startup behavior

- Upgrades preserve `%APPDATA%\CodexUsage\settings.json`.
- Normal uninstall preserves settings so a later reinstall restores preferences.
- `uninstall.ps1 -RemoveSettings` explicitly deletes the settings directory.
- The installer does not enable startup automatically. If startup was already enabled, installation preserves that choice and updates the registry value to the stable installed executable. Users otherwise control startup from the application's settings menu.
- Uninstall removes the `CodexUsage` startup entry because its executable no longer exists.

## WinGet

The upstream project's WinGet package has the identifier `Ray.CodexUsage`. This fork is distributed through its own GitHub Releases and is not published to WinGet. Use this fork's portable executable or PowerShell installer to retain its display and multi-monitor changes.

Existing WinGet-managed installations belong to the upstream project. WinGet owns their installation directory and upgrade/uninstall lifecycle, and the in-app updater delegates those upgrades back to WinGet.

The PowerShell installer is not used as a WinGet installer because the public WinGet community repository does not accept script-based installers.
