# DigiBuddyVice

[English](README.md) · [Original Project (bortisoftware/DigiBuddy)](https://github.com/bortisoftware/DigiBuddy) · [Digimon World Vice Mod](https://github.com/Vicen04/Dw1DataAndPatches)

![DigiBuddy: Dual-screen Digimon World](docs/banner.png)

<p align="center">
  <a href="#whats-new-in-digibuddyvice">What's New in Vice</a> ·
  <a href="#installation">Installation</a> ·
  <a href="#features">Features</a> ·
  <a href="#compatible-games">Compatible Games</a> ·
  <a href="https://github.com/Wardoar/DigiBuddyVice/issues">Report an Issue</a>
</p>

**DigiBuddyVice** is a fork of [DigiBuddy](https://github.com/bortisoftware/DigiBuddy)—a **PlayStation Digimon World** emulator built for dual-screen Android handhelds—refactored to add full real-time companion panel support for the **[Digimon World Vice](https://github.com/Vicen04/Dw1DataAndPatches)** ROM hack alongside the original vanilla editions. Play on the top screen while tracking your partner, bag, live map radar, prosperity, and evolutions on the bottom touch panel in real time.

[![▶ Watch the DigiBuddy presentation video on YouTube](docs/video-preview.png)](https://www.youtube.com/watch?v=glKcUstdL5Q)

## What's New in DigiBuddyVice

Vanilla DigiBuddy validates static SHA-256 table hashes in `SLUS-01032` before unlocking the companion panel, which causes patched *Digimon World Vice* discs to stall on `"Waiting for a compatible game"`. **DigiBuddyVice** refactors the memory decoder, sprite renderer, and evolution engine to support **Digimon World Vice (v2.1 / v2.2)** and its optional installer sub-patches:

- **Digimon World Vice Structural RAM Verification:** Automatically detects Vice-patched `SLUS-01032` executables in Work RAM by validating invariant engine, skeleton, and evolution-gain structures when static data table hashes are modified by Vice or the Vice Randomizer.
- **Playable Partner & Evolution Slots 62–66 Unlocked:** Extends partner decoding, live evolution tree requirements, Direct Evolution, and Evolution Undo up to species ID `66`, unlocking **WereGarurumon**, **Panjyamon**, **Gigadramon**, **MetalEtemon**, **Myotismon**, and **Machinedramon**.
- **3D Model Portrait Fallback for Vice Ultimates:** Automatically renders front-facing 3D `.MMD`/`.TIM` portraits from the user's disc for partner and evolution slots `62–66` where 16×16 V-Pet icons are not populated.
- **Dynamic In-RAM Name Resolution (Sub-Patches & Custom Items):** Reads live ASCII species and item strings directly from `DIGIMON_DATA` and `ITEM_PARA` in PSX RAM. Automatically adapts to mutually exclusive Vice installer choices (*WereGarurumon* vs. *Panjyamon*, *Machinedramon* vs. *Myotismon*) and custom evolution items (*Machi Coder*, *King Crown*, *Weird Slime*, *Ugly Mirror*, *Moon Mirror*, *Noble Mane*, *Giga Hand*, *Metal Banana*).
- **Vice 2.2 Stat Cap Break & Hardmode Boss Support:** Expands HP/MP validation bounds up to `32,767` so Vice 2.2's boosted combat buff cap break and Hardmode/Bonus Area bosses render accurately on the companion panel and map radar.
- **Negative Happiness Fix:** Fixes a bounds check where negative partner happiness (`-100` to `-1`) previously disabled the live companion panel.

## Screenshots

Real captures on an Anbernic RG DS; the interface may vary slightly by version.

| Top screen · game | Bottom screen · companion |
| --- | --- |
| ![Digimon World on the top screen](docs/screenshots/game.png) | ![Agumon panel with live stats](docs/screenshots/companion.png) |

<details>
<summary>Startup and save selection</summary>

![DigiBuddy startup screen](docs/screenshots/startup.png)

</details>

## Devices

| Device | Status |
| --- | --- |
| AYN Thor | Tested (Vanilla & Digimon World Vice) |
| Anbernic RG DS | Tested, including save and load states |

Requires **Android 8.0 or later and ARM64**. Other dual-screen devices have not been tested.

## Installation

Download the latest APK from [Releases](https://github.com/Wardoar/DigiBuddyVice/releases/latest).

1. Install the APK on your handheld. If prompted by Android, allow installation from your browser or file manager.
2. Open DigiBuddy: choose **English** or **Español** (your system language is preselected on first launch). The setup wizard will ask you to select your PlayStation BIOS (`512 KiB`) and your *Digimon World* / *Digimon World Vice* disc image (`.bin`, `.iso`, `.img`, or `.chd`).
3. Start a new game, continue your latest emulator state, or load from the original in-game memory card menu.

*Note: If you already have the stock upstream DigiBuddy app installed, export your memory card first (`Settings → Saves → Export memory card`) and uninstall the stock app before installing DigiBuddyVice, as local/fork builds use a separate signing key.*

**No BIOS or game files are included. Each user must provide their own legally obtained files.**

## Languages

The interface, item catalog, recruitment hints, and status messages are available in **English and Spanish**. Change your language at any time under **Settings → App language**: English or Español. Changing the language rebuilds the companion panel immediately without restarting your game session.

The language inside the game itself depends on the ROM you load; the selector translates the DigiBuddy companion panel.

## Features

### The Companion · Bottom Screen

- **Partner:** Real-time stats (Offense, Defense, Speed, Brains), HP/MP meters, age, weight, happiness, discipline, fatigue, care mistakes, battle count, Bits, and active care need warnings.
- **Bag:** Live inventory slots and item icons; tap any item to view its quantity, effect description, and current usability before confirming use.
- **Map:** Your live tile position, direct and scripted zone exits, toilets (WC), loose ground items, unopened chests, and enemies with front-facing portraits. Tap an enemy to inspect its live stats and estimated difficulty (or choose from a list if multiple Digimon overlap). Colour-coded rings indicate battle difficulty. Recruitable Digimon detected in the area display a `!` badge and open their recruitment clue when tapped.
- **Prosperity:** File City prosperity score and up to four nearby pending recruitment hints prioritized by your current zone, adjacent exits, and region. Tap any hint to inspect its location, clue, and known prerequisites.
- **Evolution:** Live evolution routes read directly from game memory (including Vice and randomized trees); tap any target to check met and pending requirements (Stats, Weight, Care Mistakes, and Bonus criteria). Trigger valid evolutions directly with confirmation, or **Undo** your latest evolution to return to your previous form via the native in-game animation while preserving your current stats, care mistakes, age, remaining lifespan, and compatible techniques.
- **Cheats:** Eight built-in session helpers with confirmation and automatic pre-cheat state backups. Undoing a cheat restores the backup created immediately before it was applied.

### The Game · Top Screen

- Physical controller support and stereo audio.
- **Settings → Controls · Remap buttons:** Tap any PlayStation button on the diagram and press the physical button or axis you want to bind to it. Bindings are saved per controller device descriptor; you can cancel or reset to default controls at any time. The game pauses automatically while remapping.
- Original **4:3** aspect ratio or stretched widescreen fill.
- Internal resolution scaling up to **8×**, texture filtering, and PGXP geometry/perspective correction with **SwanStation OpenGL ES**.
- Software renderer and **PCSX ReARMed** compatibility core options.

Graphical enhancements primarily improve 3D models, while 2D pre-rendered backgrounds and FMVs retain their original resolution. Performance depends on your device and resolution settings.

Under **Settings → Appearance**, enable **Dark mode** to switch the bottom companion panel and dialogs to a dark slate palette while keeping the top game screen untouched.

Tap the **⏩** button next to Play (or hold your mapped physical Fast-Forward button) to toggle fast-forward (`×2`, `×3`, or `×4` configured under **Settings → Graphics and sound**). Audio mutes during fast-forward, and automated item/evolution sequences temporarily run at `×1` speed for reliability.

## Updates

Check the latest changes in the [changelog](CHANGELOG.md).

*Note: If you are using a self-compiled or DigiBuddyVice fork APK, you can disable automatic upstream update checks under **Settings → Updates → Check when the app opens**. Emulation and all companion features work 100% offline.*

Settings are organized into collapsible sections: Appearance, App language, Saves, Graphics and sound, Controls, Screens, Files, and Updates. Play, Fast-Forward, and Settings remain accessible across every tab, including the Map.

## Saves and States

- **Continue latest session:** Restores the most recent emulator save state for the current disc and core.
- **Load in-game save:** Boots the game normally so you can load your Memory Card save from the title screen.
- **New game:** Starts the game from the beginning without deleting your Memory Card or previous save states.

Manage manual save states, import/export states, and export your Memory Card (`.mcr`) under **Settings → Saves**. Save states display their timestamp and require confirmation before overwriting an active session. Imported states must match the same disc and emulation core.

## Compatible Games

The companion panel recognizes:
- **Digimon World Vice (v2.1 / v2.2 & sub-patches)** patched over **Digimon World USA (`SLUS-01032`)**
- **Digimon World USA (`SLUS-01032`)** (Vanilla reference edition)
- **Digimon World Japan (`SLPS-01797`)** with the reference Spanish translation patch

Memory fingerprints and structural table checks verify the loaded executable in RAM before reading data or enabling direct memory actions.

In USA (`SLUS-01032`) and Vice editions, automated item use confirms with `✕`; in the Japanese edition (`SLPS-01797`), it confirms with `○`. Save states and Memory Cards are isolated per disc SHA-256 hash, so switching between Vanilla and Vice discs keeps each playthrough's saves separate.

<details>
<summary>How to identify the reference disc</summary>

Reference disc image SHA-256:

```text
b5ff9ed251bced70c20eb911eab8ac3e5b77d7a140983d3b5dc31decac4837af
