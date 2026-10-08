# N_m3u8DL-CLI GUI Edition

> **⚠️ Important Notice**
> This repository is an **unofficial GUI modification** of the open-source project **N_m3u8DL-CLI**,
> and is **not** a release published by the original author.
> The download engine and all core source code come from **nilaoda**'s open-source project,
> licensed under the **MIT License**. Copyright belongs to the original author.
> See [Credits & Origin](#credits--origin) below.

A Windows desktop m3u8 downloader with a graphical interface:
**paste a link → click a button → it downloads and merges automatically**.
It shows live download speed and progress, and all videos are saved into the `Videos` folder.

![Screenshot](界面预览.png)

---

## Interface & Usage

### Step 1 — Run the program
Double-click `N_m3u8DL-CLI.exe` to open the window.

### Step 2 — Download in three steps
1. Paste an `m3u8` / `mpd` / direct video URL into **Download URL**;
2. Click **Start Download**;
3. When it finishes, the video is saved in the `Videos` folder next to the program
   (click **Open** in the window to open that folder directly).

### Interface reference

| Area | Control | Description |
| --- | --- | --- |
| Top | Download URL | `m3u8` / `mpd` / direct link. Required |
| Top | Save name | Optional; leave empty to auto-name with a timestamp |
| Top | Threads | Number of parallel segment threads, default 32 |
| Top | Speed limit (KB/s) | `0` = unlimited; e.g. `500` caps it at 500 KB/s |
| Top | Proxy | Optional, supports `http://` and `socks5://` |
| Top | Save folder | Defaults to `Videos`; can be changed |
| Top | Headers | Optional, one per line, e.g. `Referer: https://example.com` |
| Top | Start Download | Adds a new task; several tasks can run at the same time and the app stays open |
| Top | Stop / Remove / Clear finished | Manage the task list |
| Top | Delete temp segments when done | If checked, only the final video is kept |
| Middle | Task list | Name / Progress / Speed / Status / URL. Select a row to see the details below; double-click a row to open its folder |
| Bottom | Progress bar & speed | Live progress, download speed and ETA of the selected task |
| Bottom | Status swatch | Color follows the state: grey = idle, blue = downloading, green = done, orange = stopped, red = failed |
| Bottom | Log area | Every line starts with a colored block: grey = info, green = success, orange = warning, red = error |
| Footer | Status bar | `开发者:NIL` on the left, `version:1.0.0` on the right |

---

## Folder Structure

The folder is the complete, runnable program. Only four items are kept at the top level;
all dependencies live inside `bin`:

```
N_m3u8DL-CLI\
├── N_m3u8DL-CLI.exe      ← the program (double-click to open the GUI)
├── Videos\               ← downloaded videos are saved here
├── 使用说明.txt           ← user manual (Chinese)
├── 界面预览.png           ← screenshot
└── bin\                  ← required dependencies, do NOT delete
    ├── ffmpeg.exe                     (required for merging)
    ├── Newtonsoft.Json.dll
    ├── CommandLine.dll
    ├── NiL.JS.dll
    ├── BrotliSharpLib.dll
    ├── MihaZupan.HttpToSocks5Proxy.dll
    ├── UACHelper.dll
    ├── System.Runtime.CompilerServices.Unsafe.dll
    ├── logo_3Iv_icon.ico              (window icon)
    └── NO_UPDATE
```

> The whole folder can be copied anywhere (Desktop, another drive, USB stick, ...) and runs standalone;

---

## Requirements

* Windows 7 SP1 / 8.1 / 10 / 11
* .NET Framework 4.6 or later (usually preinstalled on Windows 10 / 11)
* No separate ffmpeg installation needed — it is bundled at `bin\ffmpeg.exe`

---

## Building from Source

No build artifacts are committed to this repository. To build it yourself:

1. Run `fetch-deps.ps1` (**requires internet access, first time only**).
   It downloads the Roslyn compiler (`csc.exe`) and the required NuGet packages into `tools\` and `libs\`.
2. Run `build.ps1`.
   It compiles everything into the `dist\` folder (`N_m3u8DL-CLI.exe` plus the `bin\` dependencies).
   If `ffmpeg.exe` is available on your `PATH`, the script copies it into `dist\bin\` automatically.

You may also open `N_m3u8DL-CLI.sln` in Visual Studio and build it there (restore the NuGet packages first).

---

## Command-line Compatibility

Started **without arguments** it opens the GUI; started **with arguments** it still behaves as the
original command-line tool:

```bat
N_m3u8DL-CLI.exe "https://example.com/playlist.m3u8" --workDir "E:\video" --saveName "abc"
```

For the full list of command-line options, please refer to the original project documentation
(see below).

---

## Credits & Origin

**The original project and all core code belong to:**

| Item | Detail |
| --- | --- |
| Original project | **N_m3u8DL-CLI** |
| Original author | **nilaoda** |
| Original repository | <https://github.com/nilaoda/N_m3u8DL-CLI> |
| Original documentation | <https://nilaoda.github.io/N_m3u8DL-CLI/> |
| License | **MIT License** (see `LICENSE` in the repository root) |

The changes made in this repository are limited to UI-related work: adding a **WinForms GUI**
on top of the original command-line program, reorganizing the output folder structure,
hiding the console window and adding colored log output.
**Downloading, parsing, decryption and merging all come from the original author.**

When using or redistributing this software you **must keep the original copyright notice and the
MIT License**, and comply with the original project's license terms.

### Third-party components

* **ffmpeg** — used for video merging, distributed under its own LGPL / GPL terms. Copyright belongs to the FFmpeg project.
* **Newtonsoft.Json**, **CommandLineParser**, **NiL.JS**, **BrotliSharpLib**, **HttpToSocks5Proxy**, **UACHelper**, etc. — each under its own original open-source license.

---

## Disclaimer

* This project is intended for **personal study, technical research and backing up content you are entitled to access** only.
* Do not use it to download or distribute copyrighted material you do not have the rights to. You are solely responsible for your own actions.
* Do not use this project for any commercial or illegal purpose.
* Because of the nature of such tools, some antivirus products may raise **false positives** — please judge carefully and only add exclusions if you understand the risk.

---

## License

This project continues to use the original **MIT License**; see [LICENSE](LICENSE).
Copyright of the original code belongs to **nilaoda**.