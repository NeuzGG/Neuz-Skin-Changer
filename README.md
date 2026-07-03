# NeuzSkinChanger 🎮

> **Dota 2 Skin Changer — Patch 7.02 (July 2026)**
> A premium Electron desktop app for managing Dota 2 cosmetic skins via the VPK search path override method.

[![Platform](https://img.shields.io/badge/platform-Windows-blue)]()
[![Node](https://img.shields.io/badge/node-18%2B-green)]()
[![License](https://img.shields.io/badge/license-MIT-lightgrey)]()

---

## Screenshots

| Default | Custom |
|---|---|
| ![Invoker Default](screenshots/invoker_default.png) | ![Invoker Custom](screenshots/invoker_custom.png) |
| ![Shadow Fiend Default](screenshots/sf_default.png) | ![Shadow Fiend Custom](screenshots/sf_custom.png) |
| ![Slark Default](screenshots/slark_default.png) | ![Slark Custom](screenshots/slark_custom.png) |

---

## How It Works

Dota 2's Source 2 engine loads files using a **VPK search path priority** system defined in `gameinfo_branchspecific.gi`. By adding a custom folder `Dota2SkinChanger` at a higher priority than the default `dota` folder, any files placed there override the game's defaults.

```
Dota 2 loads files in this order:
1. Dota2SkinChanger/   ← Your custom skins (HIGHEST PRIORITY)
2. dota/               ← Default game content
3. core/
```

This approach:
- ✅ **No DLL injection** — does not touch game executables
- ✅ **Self-contained** — no external website dependencies for skin rendering
- ✅ **Easily reversible** — a backup of the original `gameinfo_branchspecific.gi` is kept
- ⚠️ **Client-side only** — other players see your actual equipped items

---

## Quick Start

### First Time Setup
1. Run **`Install.bat`** as Administrator
   - Auto-detects your Dota 2 installation
   - Patches `gameinfo_branchspecific.gi`
   - Creates the `Dota2SkinChanger` folder
   - Repairs the matchmaking file signature so the client still passes launch checks

2. Launch **`NeuzSkinChanger.exe`**

3. Browse heroes → select a skin → click **Apply**

4. If you have a `.vpk` file for the skin, click **VPK** to import it

5. Launch Dota 2 from the app

### License Activation
NeuzSkinChanger uses a license key (`NEUZ-XXXX-XXXX-XXXX`) for access. Keys are issued and can be verified through our Discord — see the **Key Checker** in the app or on the landing page.

---

## Development Setup

### Prerequisites
- Node.js 18+
- npm 9+

### Install & Run
```bash
npm install
npm run dev
```

### Build for Production
```bash
npm run build
```

Output will be in the `out/` directory.

---

## Project Structure

```
NeuzSkinChanger/
├── src/
│   ├── main/               ← Electron main process (Node.js)
│   │   ├── index.ts        ← App entry & IPC handlers
│   │   ├── steam.ts        ← Steam/Dota path detection
│   │   ├── patcher.ts      ← gameinfo.gi patching
│   │   ├── vpk-manager.ts  ← VPK file & loadout management
│   │   └── skin-catalog.ts ← Hero & item data
│   ├── preload/
│   │   └── index.ts        ← Secure IPC bridge
│   └── renderer/
│       ├── index.html
│       └── src/
│           ├── main.ts     ← UI logic
│           └── styles/
│               └── main.css ← Premium dark theme
├── dota/
│   └── gameinfo_branchspecific.gi  ← Pre-patched gameinfo
├── Install.bat             ← First-time setup
├── Uninstall.bat           ← Restore originals
└── loadout.json            ← Active skin preferences (auto-created)
```

---

## VPK Skin Files

The app manages which skins are "active" in `loadout.json`. To actually have skins render in-game, you need `.vpk` files containing the model overrides.

To import a VPK:
1. Open the app
2. Click a hero → select a skin
3. Click the **VPK** button
4. Browse to your `.vpk` file
5. The app copies it to your `Dota 2 beta\game\Dota2SkinChanger\` folder

---

## Restore Original Files

Run **`Uninstall.bat`** — it will:
1. Restore `gameinfo_branchspecific.gi` from backup
2. Leave VPK files in place (you can delete them manually)

---

## FAQ

**Will this get me VAC banned?**
The tool only swaps local cosmetic files and doesn't touch the game executable or memory, but any modification of game files is outside Valve's Subscriber Agreement. Use at your own risk.

**Can other players see my custom skins?**
No — changes are rendered locally only. Everyone else still sees your actual equipped items.

**Does it work after a Dota 2 update?**
Client updates can reset `gameinfo_branchspecific.gi`. Re-run `Install.bat` if skins stop applying after a patch.

---

## Disclaimer

> This software modifies local game files. Cosmetic changes are **client-side only** and not visible to other players. This is not an official Valve product and is not endorsed by Valve. Use at your own risk and preferably on an alternate account. The authors are not responsible for any consequences, including account actions taken by Valve.

---

*Made with ❤️ by Neuz*
