
Movement Tracker 
A tiny, privacy-first Android app that tracks how far you move each day — pure GPS, no ads, no internet, no tracking-you-back. The whole app is a single 58 KB APK.

UI language is Banglish (Bengali written in English letters) — because that's how the author talks. 

Features
Button
What it does
Start Today's Journey 🚀	Starts GPS tracking. Live km counter updates right on the big screen.
Onek Hoise ⏸	Temporarily pauses tracking (tap again to resume — "Abar Chalu ▶").
Obosheshe 😮‍💨	Ends today's journey, stops tracking and saves the km to history.
Past is Past 📜	Shows the last 30 days: a 7-day bar chart, day-by-day list, total and best day.

Background tracking — runs as a foreground service with a persistent notification, so km keeps counting even with the screen off (requires "Allow all the time" location permission).
Manual day reset — nothing auto-clears at midnight; a day ends only when you tap Obosheshe.
Kill-proof — distance is persisted continuously, so if the system kills the service, your km are not lost.
GPS noise filtering — fixes with accuracy worse than 25 m are ignored; movements under 3 m don't count, so shivering GPS doesn't inflate your km.
🖥 Screens
Main screen — dark navy + neon-green fitness theme, a big live km card and the four buttons above.
History screen — 30-day list plus a hand-drawn (no chart library!) 7-day bar chart.
📱 Install
Grab MovementTracker.apk (58 KB), copy it to your phone, and install it ("allow unknown apps"). Then:

Tap Start Today's Journey
Grant location permission — pick "Allow all the time" for background tracking
On Android 13+, allow notifications
Minimum: Android 6.0 (API 23)
Target: Android 14 (API 34)
🛠 Build it yourself
No Gradle, no AndroidX, no dependencies — plain Java compiled straight against android.jar:

bash
bash scripts/build_apk.sh
The script runs the whole pipeline: aapt2 → javac → d8 → zipalign → apksigner (you only need JDK 11+ and Android SDK with platform 34 + build-tools 35).

📁 Project structure
text
AndroidManifest.xml
res/                              icons (PIL-generated) + dark theme
scripts/build_apk.sh              one-shot build script
scripts/make_icons.py             launcher/notification icon generator
src/com/movementtracker/app/
  MainActivity.java               main screen, permissions, buttons
  TrackingService.java            foreground service + GPS distance accumulator
  HistoryActivity.java            30-day history screen
  BarChartView.java               custom 7-day bar chart View
  Prefs.java                      SharedPreferences data layer
Privacy
The app only reads your GPS location to sum up distances. Nothing leaves your phone — no network permission is even requested. All data lives in SharedPreferences on your device.

License
Do whatever you want with it (public domain / CC0). Attribution appreciated but not required.
