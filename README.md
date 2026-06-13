# Card Scale Debug

Web Bluetooth debug page for the **Mnemonica Card Scale** — a precision scale hidden in a playing-card box that weighs a cut deck, works out how many cards were lifted, and reports the corresponding Mnemonica-stack card over BLE.

## Live page

**https://n3urs.github.io/card-scale-debug/**

Open it in the **[Bluefy](https://apps.apple.com/app/bluefy-web-ble-browser/id1492822055)** app on iOS (Safari does not support Web Bluetooth). On desktop, Chrome/Edge work directly.

## How to use

1. Flash `card_scale_ble.ino` to the Seeed XIAO nRF52840 Sense — it advertises as **`CardScale`**.
2. Open the live page in Bluefy (or Chrome).
3. Tap **Connect to Scale** and pick `CardScale`.
4. The page shows the live raw weight and the named card as the deck is cut.

## BLE contract

| Item | UUID | Format |
|------|------|--------|
| Service | `12345678-1234-1234-1234-123456789abc` | — |
| Card characteristic | `...abd` | UTF-8 string, e.g. `Q Hearts`, `Full deck`, `Ready` (read + notify) |
| Weight characteristic | `...abe` | float32 little-endian, grams (read + notify) |

Hardware: Seeed XIAO nRF52840 Sense + HX711 24-bit ADC + 1kg YZC-131 load cell. Firmware uses the Adafruit Bluefruit library (ArduinoBLE does not link on this board).
