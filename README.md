# T1000-E SOS Test Firmware

Prebuilt **test firmware** for **SenseCAP / Seeed T1000-E** screenless trackers with an improved SOS user experience.  
**No compilation required.** This repository is intended for testers who just want to flash and evaluate behavior.

---

## What this is

This repo provides **ready-to-flash binaries** for T1000-E that include a finalized SOS flow:

- Reliable SOS trigger via long-press
- Clear receiver-side SOS alarm with repeats
- **Delayed, single “ta-daa” confirmation sound** on the sender when an SOS is acknowledged
- Defensive handling when multiple receivers respond

This is a **test distribution**. Source code lives elsewhere; this repo is only for binaries, docs, and feedback.

---

## Supported devices

- **SenseCAP / Seeed T1000-E**
- Screenless trackers only  
⚠️ Do **not** flash on other models.

---

## Download

Go to **Releases** and download the **latest test build**:

➡️ **Latest Release**  
(Assets include ready-to-flash firmware files and checksums.)

Each release name clearly indicates:
- device: `TRACKER_T1000_E`
- version
- test/stable status

---

## Flashing instructions (overview)

> Use the same tool you normally use to flash T1000-E firmware.

General steps:
1. Download the firmware file from the latest Release.
2. Put the device into DFU / flashing mode (per Seeed/SenseCAP instructions).
3. Flash the firmware using your preferred tool (nRF Connect, nrfutil, etc.).
4. Power-cycle the device.

Detailed, step-by-step guides (with screenshots if needed) are in **`docs/`**.

---

## Expected behavior (what to test)

### Sender (the device that sends SOS)
- Long-press **≥ 2 s and < 5 s**, then release.
- SOS is sent immediately.
- If another device receives the SOS and sends ACK:
  - After ~2–3 seconds, you hear **one short “ta-daa”** confirmation sound.
- No immediate chirp on release.
- If no ACK arrives → **no sound**.

### Receiver (device that receives SOS)
- Plays a **distinct SOS alarm** (different from normal messages).
- Alarm **repeats** on a bounded schedule (initially more frequent, then every ~15 minutes).
- Alarm stops immediately when the local button is pressed.

### Multiple devices
- If multiple receivers send SOS-ACK:
  - Sender still plays **only one** confirmation sound per SOS gesture.

---

## Known limitations

- Behavior with **3–4+ devices** in the same channel requires field testing.
- SOS-ACK arriving **after ~10 s timeout** is ignored for audio playback.
- Sender-side ACK state is not persistent across power cycles.

---

## Rollback

To return to a stable firmware:
1. Download a known stable release.
2. Flash it using the same steps as above.

---

## How to report feedback

Please open an **Issue** and include:
- Firmware version (from Release name)
- Device: T1000-E
- Number of devices involved
- Steps to reproduce
- Expected vs actual behavior
- Logs (if available)

Clear reports = faster fixes.

---

## Status

- SOS flow: **complete**
- ACK UX: **finalized**
- This repo is for **testing and validation**, not development.

Thank you for testing 🙏
