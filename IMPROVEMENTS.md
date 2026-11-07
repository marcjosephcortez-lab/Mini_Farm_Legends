# Mini Farm Legends – Development Update

## Persistence and save reliability

- Added saved water-bucket contents so refilled water is not lost after restarting.
- Added the stored-crop total to saved game data.
- Added a save-data version marker for future migrations.
- Validated loaded values for levels, currency, seeds, tools, animals, basket contents, and plot states to reduce the risk of corrupted or malformed saves breaking the game.
- Kept compatibility with older saves; fields that older versions did not store use safe defaults.
- Save feedback now distinguishes a successful cloud sync, a local-device save, and a failed save.
- Loading now reports whether a valid save was actually found instead of always showing a success message.
- Saving is triggered after refilling the water bucket and selling the basket, so these important transactions are less likely to be lost before the next autosave.

## Verification performed

- JavaScript module syntax check: passed (`node --check`).
- Persistence round-trip test: passed for water, stored-crop total, basket items, animal counts, and crop growth state.
- Invalid-save handling test: passed for out-of-range values, unknown basket items, and invalid plot state/crop values.
- Tailwind CSS compilation: passed using the local Tailwind CLI.
- Capacitor Android sync: passed; updated web assets were copied into the Android project.

## Not yet verified

- A full Gradle APK build and testing on a physical Android device were not performed in this environment.
- Cloud save behavior still depends on the project being supplied with a valid Firebase configuration and authenticated user.


## World, character, camera, and tutorial update

- Rebuilt the farmer as a complete stylized character with a connected neck and head, visible eyes, pupils, nose, smile, ears, hair, straw hat, overalls, articulated arms, hands, legs, and boots.
- Kept the nine individual crop plots and arranged them in a clear 3-by-3 layout with enough separation from the well, storage shed, and seed stand.
- Removed the prominent cobblestone floor/path. The farm now uses continuous grass as its dominant ground surface, subtle worn-grass tracks, and sparse meadow details.
- Added a visible yellow selection ring to the nearest interactable crop plot.
- Moved gameplay prompts into a dedicated upper-screen lane so they no longer sit in the center of the character view. Added a separate tutorial card near the screen edge.
- Added three switchable camera framing presets: third-person, elevated farm view, and close third-person. The camera no longer automatically rotates to follow the farmer’s facing direction.
- Added a first-time interactive tutorial covering movement, plot selection, planting, refilling water, watering, crop growth, harvesting, and exploration. Tutorial completion is stored locally; players can replay it using the Guide button or skip it.
- Reduced the maximum renderer pixel ratio to 1.75 to help mobile performance.
- Updated the Capacitor Android bundled `public/index.html` to match the browser version.

## Verification for this update

- JavaScript module syntax check: passed (`node --check`).
- Static project checks: confirmed three camera presets, nine plot positions, nine tutorial steps, and matching browser/Android HTML files.
- Three.js compatibility review: avoided geometry classes newer than the bundled Three.js r128 library.
- Interactive browser and physical Android testing: not completed in this environment; verify camera switching, character appearance, touch controls, and the full tutorial on the target device.

## World & controls update — 2026-11-07
- Added a floating dynamic joystick that appears at the touch point in the selected movement zone and follows pointer movement.
- Added a control customization panel: joystick size and side, action-button size and side, and remappable Plant/Water/Harvest keyboard shortcuts. Settings persist in local storage.
- Added more expressive farmer idle, walk, planting, watering/refill, and harvesting animation states.
- Rebuilt the storage shed as a timber barn with a gabled roof, sliding double doors, loft window, foundation stones, hay bales, and lantern.
- Added a timber perimeter fence with an entrance gate, varied orchard trees, additional shrubs/rocks/flowers, and subtle wind sway.
- Improved individual crop beds with soil ridges, numbered plot markers, leaf details, and subtle crop sway.
- Synced the updated HTML to the Android Capacitor bundled public assets.
- Validation: module JavaScript syntax check passed; static feature checks and archive integrity checks completed. Interactive browser/device playtesting remains recommended.


## Manual touch-look camera update — 2026-11-07
- Replaced automatic behind-the-player camera rotation with a manual orbit camera. The camera follows the farmer’s position but preserves the player-selected viewing angle.
- Added a transparent right-side touch-look area: drag horizontally to orbit and vertically to adjust camera elevation, like mobile RPG/FPS controls.
- Camera movement stops immediately when the touch is released; it does not automatically recenter.
- Kept the left-side dynamic joystick independent so movement and camera-look can be used simultaneously. The configured joystick side remains respected because its touch layer sits above the look area.
- Preserved camera preset switching for framing/zoom and field-of-view changes without resetting the manual orbit direction.
- Added pitch limits to prevent the camera from flipping or moving below the ground.
- Validation: JavaScript module syntax and archive integrity checks passed. Physical Android touch testing is still required.

## Camera-relative movement correction — 2026-11-07
- Corrected movement so joystick input is transformed from camera-local forward/right directions into world-space movement using the current manual camera yaw. Pushing up now moves the farmer toward the direction the camera is facing; left/right strafe relative to the current view.
- Character facing and walking animation now use the resulting camera-relative world movement vector.
- Kept the independent multi-touch joystick and look pointer behavior so the player can move and rotate the camera at the same time.
- Fixed touch-zone placement when the joystick is configured on the right: the camera-look zone moves to the left, avoiding overlap and preserving separate touch areas.
- Validation: JavaScript module syntax check passed; static checks confirm camera-relative movement and synchronized browser/Android HTML. Physical device verification remains necessary.


## Farm entrance and cinematic main-menu reveal (2026-11-07)
- Rebuilt the south entrance as a centered double-leaf wooden gate with heavier hinge posts, capped posts, multiple rails, vertical slats, and diagonal braces.
- Main menu camera now starts close to the gate, framing the entrance as the title-screen scene.
- Pressing ENTER FARM triggers a smooth camera pull-back toward the selected gameplay view while both gate leaves swing open.
- The normal manual touch-look camera and camera-relative movement remain active after the intro completes.
- Intro is rendered as part of the existing animation loop; gameplay and tutorial start only after the reveal finishes.


## Visual restoration update
- Rebuilt the storage barn with aligned roof planes, gable ends, symmetrical doors, trim, and consistent timber colors.
- Restored direct color output (no ACES tone mapping) and increased the mobile pixel-ratio cap to 2 while retaining antialiasing and soft shadows.
- Synchronized the Android bundled HTML with the browser version.


## Barn roof correction
- Replaced the incorrectly rotated/overlapping roof panels with a symmetrical pitched gable roof.
- Both roof planes slope upward toward the center ridge and downward toward the eaves.
- Added a narrow ridge cap and matching sloped fascia; synchronized Android public assets.


## Side menu, pause system & separate chat — 2026-11-07
- Replaced the row of scattered top-bar buttons (Shop, Gear, Badges, Online, Controls, View, Guide, Sound, Save) with a wooden menu button in the upper-left corner that opens a slide-in side menu.
- Side menu items: Resume, Save Game, Load Game, Controls, Settings, Camera Views, Inventory, Help / Tutorial, and Return to Main Menu, plus a small "Farm" row for Shop, Gear and Badges so no existing feature was lost.
- Sub-panels open in a second card beside the menu so most of the farm stays visible. They reuse the existing systems: `saveGameData` / `loadGameData`, the control customization (same element IDs and storage key), the three camera presets, the interactive tutorial, and the shop/tools/achievement modals.
- New Settings panel: sound on/off (same `muted` save field as before) and camera look sensitivity (stored with the control settings; older settings load with the 1.0 default).
- New Inventory panel: coins, gems, water, stored crops, seed selection, basket contents, tools and animals, all read from the existing game state.
- Centralized `PauseManager`. While paused: no movement, joystick and touch-look are released and blocked, Plant/Water/Harvest/station/keyboard actions are ignored, crop growth stops, action animations freeze mid-way (they now run on game time instead of `setTimeout`), sprinklers/tractor/animals stop, and the day/night cycle and tree/crop sway stop. Resume continues from the exact same values. Player position, crops, inventory and the save format are unchanged.
- The game also pauses automatically when the app goes to the background or the phone rotates to portrait. `Esc` opens/closes the menu on keyboards.
- Return to Main Menu saves first, then goes back to the gate title shot; ENTER FARM plays the entrance cinematic again and the farm continues as it was. The intro now blends the field of view into the selected camera view.
- The old Online lobby is now a separate Chat button in the bottom-left corner with its own panel (room code, messages, send), an unread badge, and touch isolation so chat touches and typing never move the farmer. Chat does not pause the game. The button moves up automatically when the action buttons are set to the left side.
- Rebuilt Tailwind CSS from `www/index.html` and synced `index.html` and `css/tailwind.css` into `android/app/src/main/assets/public`.

### Verification for this update
- JavaScript module syntax check passed (`node --check`); no duplicate element IDs; no references to removed elements.
- Automated headless-Chromium run at 844×390 and 667×375 landscape with touch: 52 checks passed, covering menu open/close, every menu item, crop timer and world clock frozen while paused and continuing after resume, a plant action frozen mid-animation, blocked keyboard/touch input while paused, two-finger joystick + camera-look at the same time, joystick released when pausing mid-drag, chat opening without pausing, chat typing not moving the farmer, chat touches not reaching the joystick, unread badge, Save/Load round-trip, and Return to Main Menu + re-entry keeping position and crops.
- Not verified here: a Gradle APK build and play on a physical Android device (real touch, soft keyboard, Android back button, performance).

### Test hook
- Open `index.html?debug` to get `window.__farm` in the browser console (pause state, plots, player position, camera yaw). It's inactive without `?debug`.
