# Pragon Mobile v18 (versionName 6.5): Tools hub

**Not compiled** here (no Android SDK). If the GitHub build prints `e:` lines, send them over.

## What changed
- Sidebar > Control > NAVIGATE > **🧰 Tools** opens the new Tools screen.
- `ToolsActivity.kt` + `assets/tools.html` (same black / cyan Newsreader style as the Optimiser).
- `Sidebar.kt`: `openTools()` and the button. `AndroidManifest.xml`: activity entry. Version 65 / 6.5.

## Tools
| Tool | What it does |
|---|---|
| Map | Opens an address, place name or lat,lng in Google Maps (any map app if Maps is missing) |
| Directions | Turn-by-turn to a destination. Driving, walking, two-wheeler, transit |
| Book a ride | Opens Rapido, Uber or Ola. Play Store page if not installed |
| Calendar | New event with title, start, end, location and notes filled in. You press save |
| Camera | System camera. The photo is written to Pictures/Pragon the moment it is taken |
| Calculator | Built in the page: + − × ÷, %, ±, ⌫, keyboard works |
| Google Lens | Opens the Lens app, or lens.google.com if the app is missing |
| Messages | New text to a number, pre-filled. Nothing is sent until you press send |
| Clock | Sets an alarm at a time, or a timer in minutes (uses the phone's clock app) |

## Not in this version (need your answers first)
- **Daily news (confirmed only)** and **news monitor on a topic**: which sources count as "confirmed", and do you want a background check with a notification?
- **Clock password**: what the password is (for example, the current time shown in a set format), and whether the phone should stay locked until it is typed.
- **Camera**: this uses the phone's own camera app. A built-in camera inside Pragon (CameraX) is a larger job; say if you want that.
- Ride app package names (com.rapido.passenger, com.ubercab, com.olacabs.customer) are the usual ones; check on the phone if one does not open.

## v18.1 audit fixes (static review, still not compiled)
- Camera: CAMERA is declared in the manifest, so Android refuses the capture intent until it is granted. The screen now asks for the permission first, then opens the camera (no orphan empty photo entries).
- Camera / Lens screens close themselves after the hand-off; the hand-off runs once (no repeat launch on page reload or rotation).
- Tools screens and Optimiser keep their state on rotation (configChanges); WebView is destroyed on exit; draft reply no longer touches a destroyed screen.
- Messages: number is passed with Uri.fromParts (keeps + and spaces intact).

## v18.2 second audit pass (static review, still not compiled)
- Video editor: exported file now really goes to Movies/Pragon (gallery and My Files see it); it was left in the app's private folder while the app said otherwise. Bad parts (end before start) are skipped instead of crashing; a failed start reports an error instead of crashing; WebView cleaned up on exit.
- Music: a malformed request from the page can no longer crash the app (JSON parsing guarded); play with an empty or out-of-range list is safe; Albums/Artists/Folders lists no longer merge "Rock" and "rock"; sharing a song is guarded.
- Notification monitors: missed-call monitor no longer replays the whole call log if call-log permission is granted after the service connected.
- Settings: opening a phone settings screen that does not exist on this device shows a message instead of crashing.
- My Files: a damaged bin entry is skipped instead of crashing the bin list.
- Manifest: added the LiteRT-LM GPU native-library entries so the chat model can use the GPU.
- settings.html: null-safe app picker toggle.

## v18.3 third audit pass (static review, still not compiled)
- Cache cleaner: any unexpected error in its background thread no longer crashes the app or leaves the page stuck on "Already running".
- Share to File Dock: the invisible share window always closes, even if a copy fails (it could crash or stay on screen blocking touches).
- Music: changing playback speed while paused no longer starts the music.
- Orb: orb page calls are now safe from any thread.

## v18.4 updated from your edited files
- app/src/main/assets/settings.html: replaced with your newer design (Music player, My Files and Optimiser groups removed from Settings, new icon heading on Float). Checked: script parses, every page-to-Kotlin call still exists, no broken buttons. The Kotlin side was left as is (extra methods are unused and harmless).
- preview/Pragon_Smart_Sidebar_v3_preview.html: replaced with your newer sidebar design (editor, reordering, section on/off, width, background gradient). Design preview only: the real sidebar is built in Sidebar.kt and does not have these editor features yet.
- preview/neural_chat.html: added (chat design mockup, standalone, not wired into the app).
- app/src/main/assets/orb/pragon_orb.html: your file is identical to the one in the project, nothing to change.

## v18.5
- preview/pragon_chat.html: HTML version of the native chat screen (StandaloneView.kt design), standalone, not wired into the app. Float button uses the Pragon logo.
