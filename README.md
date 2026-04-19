# Pump Control — Web Bluetooth

Control the ESP32 pump from a web page over BLE. No app install required.

## Requirements

- **Chrome or Edge on Android** (Web Bluetooth is not supported in Safari/iOS or Firefox).
- The page must be served over **HTTPS** (GitHub Pages, Netlify, etc.). `file://` and plain `http://` will not work.
- ESP32 running the `Pump-Control` BLE firmware and powered on.

## First-time setup on your phone

If you see **"Error: Web Bluetooth API globally disabled"** when you tap Connect, enable the Chrome flag:

1. In Chrome, open a new tab and go to `chrome://flags`.
2. Search for `web bluetooth`.
3. Set **Web Bluetooth** to **Enabled**.
4. Tap **Relaunch** at the bottom of the screen to restart Chrome.

If `chrome://flags` doesn't show a Web Bluetooth entry, try Microsoft Edge for Android (same flag path), or reinstall Chrome from the Play Store.

## Do NOT pair the device in Android Bluetooth settings

Web Bluetooth connects directly from the browser — it does **not** use Android's system pairing. If you add Pump-Control under **Settings → Connected devices**, Android holds the connection and Chrome cannot access it.

If you've already paired it:

1. Go to **Settings → Connected devices**.
2. Find **Pump-Control**, tap the gear icon, and choose **Forget** (or **Unpair**).
3. Toggle Bluetooth off and back on to clear the cached connection.

## Connecting

1. Power on the ESP32 and confirm it is advertising (serial monitor shows `BLE advertising as "Pump-Control"`).
2. Open the hosted page in Chrome on your phone (e.g. `https://<your-username>.github.io/pump-control/`).
3. Tap **Connect**. Chrome shows a device picker — select **Pump-Control**.
4. Use the on-screen **Turn ON** / **Turn OFF** button to control the pump.
5. Pressing the physical BOOT button on the ESP32 updates the page in real time via BLE notifications.

Tip: add the page to your home screen (Chrome menu → **Add to Home screen**) so it opens like an app. You still tap Connect once per session — that's a browser security requirement.

## Troubleshooting

- **"Web Bluetooth API globally disabled"** — enable the Chrome flag (see above).
- **Device doesn't appear in the picker** — make sure it isn't paired in system Bluetooth settings, and that nothing else (e.g. nRF Connect on another phone) is currently connected. BLE allows only one central at a time.
- **Connects then drops immediately** — usually an ESP32 power issue; try a better USB cable or a powered port.
- **Page shows old data after reflashing firmware** — in Android Bluetooth settings toggle Bluetooth off/on to clear the GATT cache, then reconnect.
