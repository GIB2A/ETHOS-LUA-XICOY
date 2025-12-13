# GIB2A — Xicoy ProHub Turbine Telemetry Widget (ETHOS)

This project is an **ETHOS widget** (a small dashboard) for **FrSky radios running ETHOS**, designed to display **Xicoy ProHub** turbine telemetry (RPM, EGT, pump, fuel, etc.).

## What you need
- A FrSky radio running **ETHOS 1.7** (or newer).
- A **Xicoy ProHub** connected to your receiver on **S.Port / Smart Port**.
- A **microSD card** in the radio.

---

## Step 1 — Download the widget
1. Open: `https://github.com/GIB2A/ETHOS-LUA-XICOY`
2. Click the green **Code** button
3. Click **Download ZIP**
4. Extract/unzip the file (right click → Extract)

---

## Step 2 — Copy to the radio SD card
1. Connect the radio by USB (or remove the SD card and use a card reader)
2. Open the SD card on your computer
3. Find the **SCRIPTS** folder  
   - If it does not exist, create a folder called **SCRIPTS** at the root of the SD card
4. Copy the **GIB2A** folder into **SCRIPTS**

When done, you must have exactly:

`SCRIPTS/GIB2A/main.lua`

Important:
- Do **not** create extra nested folders (example: `SCRIPTS/GIB2A/GIB2A/main.lua` is wrong).
- `main.lua` must be directly inside `SCRIPTS/GIB2A/`.

---

## Step 3 — Discover sensors (required)

### A) Standard discovery (do this first)
1. Power the model: **ECU + ProHub + receiver** (everything ON).
2. On the radio: **Telemetry → Discover sensors**  
   (depending on ETHOS version, it may be called **Discover new**).
3. Wait a few seconds until sensors appear and values stabilize.

### B) If some sensors do not appear (DIY Auto Detect)
In some setups, some values are exposed as “DIY” sensors (examples: `0A10`, `0A20`, `0A30`).
1. Go to: **Telemetry → DIY Sensor → Auto Detect**
2. If you have more than one DIY sensor (for example `0A10` **and** `0A20`):
   - Run **Auto Detect** for **one** sensor
   - Go back to the Telemetry menu
   - Run **Auto Detect** again for the other sensor

### Tip (if a value is wrong or looks “stuck”)
If a value has the wrong scale (too small/too large) or looks inaccurate, open the settings for that DIY sensor and adjust:
- **Range**
- **Precision / Unit**

---

## Step 4 — Add the widget to a screen
1. On the radio: **Model → Display → Widgets**
2. Add a widget and select **GIB2A**
3. Open the widget settings and **assign the sensors** (RPM, Temp1/EGT, Fuel, etc.)

---

## “Basic / Expert” setting (simple)
- **Basic (0)**: essentials (RPM, EGT, Fuel, Pump)
- **Expert (1)**: also enables **Extended/Maximum** fields (Ambient Temp, Pressure, Altitude, Fuel Flow, etc.) if your ProHub provides them

---

## Fuel alerts (optional)
In the widget menu, you can set:
- **Fuel Alert (%)**
- **Fuel Critical Alert (%)**
- (optional) a sound file for Fuel Alert and/or Fuel Critical  
The widget can also trigger haptic feedback when crossing the critical threshold.

---

## If it does not work (check these 3 items first)
1) SD path is correct: `SCRIPTS/GIB2A/main.lua`  
2) Sensors were discovered: run **Telemetry → Discover sensors** again  
3) Receiver S.Port is configured: on some FrSky receivers you must assign a pin as **Smart Port (S.Port)** in the receiver RF options

---

## Need help?
If you report an issue, please include:
- Radio model + ETHOS version
- ProHub mode (Basic / Extended / Maximum)
- List of discovered sensors (names + units)
- Screenshots of the Telemetry page and the widget settings
