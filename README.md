# Mini Farm Legends 🌾

A low-poly 3D farming game for mobile (landscape) and desktop browsers, built with HTML, CSS, JavaScript and Three.js, and packaged for Android with Capacitor.

**Individual game project by Marc Joseph Cortez.**

## What's new in v1.2.0
- **Animations:** smoother character and world animations
- **Menu:** polished side pause menu and transitions
- **Color grading:** warmer, more natural farm lighting and colors
- **Character model:** updated player character
- **Camera:** improved camera follow and rotation
- **Joystick:** more responsive virtual joystick

See the [Changelog](#changelog) for earlier updates.

## Download (Android)
Get the latest APK from the [**Releases page**](../../releases/latest).

1. On your Android phone, open the Releases page and tap the `.apk` file under **Assets**.
2. When asked, allow your browser to **install unknown apps**.
3. Open the downloaded file and tap **Install**.
4. Play in landscape.

## Objective
Grow your farm from Level 1 to **Level 100**. Plant, water and harvest crops, sell your basket at the barn, earn XP and coins, and unlock better crops, tools, animals and achievements.

## Controls
| Action | Touch (landscape) | Keyboard |
|---|---|---|
| Move | Drag on the joystick side (the stick appears under your thumb) | W A S D / arrow keys |
| Look around | Drag on the other half of the screen | — |
| Plant / Water / Harvest | On-screen buttons | E / R / F (remappable) |
| Context action / station | Station button | Space / Enter |
| Change seed | Tap the seed counter | 1 – 6 |
| Pause menu | Menu button (top-left) | Esc |
| Chat | Chat bubble (bottom-left) | — |

## Features
- Plant → water → grow → harvest → sell loop across nine plots, using a four-stage plot state machine
- XP and level progression to 100, six unlockable crops, tools (watering-can tiers, fertilizer, sprinklers, tractor), animals and achievements
- Floating dynamic joystick, camera-relative movement and drag-to-look camera (both usable at the same time)
- Three camera views and a cinematic farm-gate entrance
- Pause menu with Save, Load, Controls, Settings, Camera Views, Inventory, Help / Tutorial and Return to Main Menu; pausing freezes movement, actions and crop timers
- Separate chat panel (local rooms between tabs via BroadcastChannel)
- Local save/load with validation, plus 30-second auto-save
- Interactive first-time tutorial

## Run in a browser
```bash
cd www
python -m http.server 8000
```
Then open http://localhost:8000 (use landscape on phones).

## Build the Android app
1. `npm install`
2. `npm run sync` — builds Tailwind CSS and copies `www/` into `android/`
3. `npm run open` (or Android Studio → Open → the `android` folder)
4. Build → Build APK(s). The APK is written to `android/app/build/outputs/apk/debug/app-debug.apk`

After editing `www/index.html`, run `npm run sync` again before rebuilding.

## Project structure
```
www/index.html          All game code (HTML, CSS and the JavaScript game module)
www/vendor/three.min.js Three.js r128
www/css/tailwind.css    Compiled Tailwind CSS
src/tailwind.css        Tailwind source
android/                Capacitor Android project
IMPROVEMENTS.md         Development change log
```

## Changelog
### v1.2.0 (latest)
Updated animations, menu, color grading, the character model, camera and joystick.

### v1.1.0: Pause menu update
- Replaced the scattered buttons with one side menu (top-left) that pauses the game
- Pausing stops movement, the joystick, camera look, farm actions and crop growth, and resumes exactly where you left off
- Added Settings and Inventory panels
- Moved Chat to its own button in the bottom-left corner

### v1.0.0: Initial release
Core farming loop, levels, crops, tools, animals, achievements, save/load and tutorial.

## Credits
- [Three.js](https://threejs.org/) r128: 3D rendering (MIT License)
- [Tailwind CSS](https://tailwindcss.com/): styling (MIT License)
- [Capacitor](https://capacitorjs.com/): Android packaging (MIT License)
- All 3D models are built from Three.js primitives in code. Sound effects are synthesized with the Web Audio API. No external model or audio files are used.
- Parts of the code were written with the help of AI coding assistants, including ChatGPT, Lovable, Gemini, and Claude. See `IMPROVEMENTS.md` for the development history.
