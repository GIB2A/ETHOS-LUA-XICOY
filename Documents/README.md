# GIB2A — Xicoy ProHub Turbine Telemetry Widget (ETHOS)

Repository: `https://github.com/GIB2A/ETHOS-LUA-XICOY`

An **ETHOS Lua widget** for **FrSky ETHOS radios** that displays **Xicoy ProHub** turbine telemetry with a pilot-focused dashboard and a full configuration menu.

---

## Highlights

- Core values (dashboard)
  - **RPM**
  - **EGT** (Temp1)
  - **Pump** (command/volt depending on mapping)
  - **Fuel** (remaining %)
- Red zones (defaults)
  - **EGT > 700°C**
  - **RPM > 100%** (up to **110%**)
- **ECU Status** decoding (Xicoy status codes)
- **Basic / Expert** setup mode
- Optional **Extended/Maximum** sensors (ProHub) in **Expert** mode
  - Ambient Temp, Pressure, Altitude, Fuel Flow, Serial Number, Battery Used, Engine Time, Pump Amperage
- **Fuel alarms**
  - Configurable thresholds (**Alert %**, **Critical %**)
  - Optional audio files per threshold (voice directory)
  - Haptic feedback on critical threshold crossing
- **Themes**
  - `0=Std`, `1=High contrast`, `2=Amber`

---

## Compatibility

- **ETHOS**: target **1.7.x** (widgets require ETHOS 1.1.0+ in general)
- **Radios**: FrSky radios running ETHOS with widget support (e.g., Tandem series)
- **Telemetry**: **Xicoy ProHub** configured in **FrSky** mode

---

## Hardware / Telemetry chain

Typical setup:

`Turbine ECU → Xicoy ProHub → Receiver S.Port (Smart Port) → ETHOS Radio`

**Important**: on some FrSky receivers you must explicitly assign a pin as **Smart Port (S.Port)** in the receiver options  
(RF System menu → receiver → Options → assign Smart Port).

---

## Simple Guide (no GitHub jargon)

### What you need
- ETHOS **1.7+**
- Xicoy **ProHub** connected to receiver **S.Port / Smart Port**
- Radio SD card access (USB or card reader)

### Step 1 — Download
1. Open the repository page
2. Click **Code → Download ZIP**
3. Extract/unzip the file

### Step 2 — Copy to SD card
Copy the folder so you end up with:

`SCRIPTS/GIB2A/main.lua`

**Do not** create extra nested folders (example: `SCRIPTS/GIB2A/GIB2A/main.lua` is wrong).

### Step 3 — Discover sensors (required)

#### A) Standard discovery (do this first)
1. Power the model (**ECU + ProHub + receiver**).
2. On the radio: **Telemetry → Discover sensors**  
   (depending on ETHOS version, it may be called **Discover new**).
3. Wait until sensors appear and values stabilize.

#### B) If some sensors do not appear (DIY Auto Detect)
Some setups expose certain values through “DIY” sensor discovery (e.g. `0A10`, `0A20`, `0A30`).
1. Go to **Telemetry → DIY Sensor → Auto Detect**.
2. If you have more than one (e.g. `0A10` and `0A20`), **detect one**, go back, then repeat Auto Detect for the next.

Tip (when scaling/precision looks wrong on some ECU types):
- Edit the relevant DIY sensor settings and adjust **Range** / **Precision** as needed.

### Step 4 — Add the widget
**Model → Display → Widgets → Add widget → GIB2A**  
Then open widget settings and **assign your discovered sensors**.

---

## ProHub setup (FrSky)

### 1) Select FrSky telemetry mode on the ProHub
On the ProHub:
1. Enter telemetry setup and select **FrSky**.
2. Choose **Basic**, **Extended**, or **Maximum**.
3. **Save** and power-cycle receiver/ProHub if required.

Notes:
- **Basic** uses standard FrSky addresses.
- **Extended/Maximum** exposes more measurements; higher data volume can reduce refresh rate.

### 2) Wiring
- Connect a **servo patch cable** from a ProHub telemetry port to the receiver **S.Port**.

### 3) Quick validation
- When connected correctly, the ProHub telemetry LED should indicate a successful link (typically green).
- On the radio, proceed with sensor discovery (section above).

---

## Widget installation (ETHOS)

1. Download the repository (Code → Download ZIP) or clone it.
2. Copy the folder **GIB2A** to your radio SD card so the final path is:

   `SCRIPTS/GIB2A/main.lua`

3. Reboot the radio.
4. Add the widget:
   - **Model → Display → Widgets**
   - Select **GIB2A**

⚠️ Folder structure matters: if you accidentally create extra subfolders, the widget will not load.

---

## Widget configuration

Open the widget settings and assign the **telemetry sources** discovered by ETHOS.

### Setup Mode
- `0 = Basic`  
  Use this when ProHub is configured for **Basic** telemetry and you only want the core dashboard.
- `1 = Expert`  
  Enables the **Extended/Maximum** optional source fields (Ambient Temp, Pressure, etc.).

### Core sources (typical mapping)
- **RPM Source**: turbine RPM
- **Temp1 Source**: EGT
- **Temp2 Source**: ECU status code
- **ADC3 Source**: ECU voltage (if provided by your telemetry mapping)
- **ADC4 Source**: pump command/volt (if provided by your telemetry mapping)
- **Fuel Source**: fuel remaining (%)
- **RSSI Sensor 1 / 2**: receiver link quality
- **RxBatt**: receiver battery voltage
- **Chrono Source**: timer or time source (optional)
- **DIY1/DIY2/DIY3**: optional extra sources (user-defined)

### Fuel alarms
- **Fuel Alert (%)**
- **Fuel Critical Alert (%)**
- **Fuel Alert Sound** (optional audio file)
- **Fuel Critical Sound** (optional audio file)

### Themes
- Theme: `0=Std 1=High 2=Amber`

---

## ProHub FrSky measurement reference (useful for debugging)

ProHub FrSky telemetry modes and corresponding measurements:

### Basic
- EGT: `0x400`
- RPM: `0x500`
- Throttle %: `0xA20`
- Battery voltage: `0x900`
- Pump RPM: `0x910`
- Fuel remaining (%): `0xA10`
- Status: `0x410`

### Extended / Maximum (examples)
- EGT: `0x4400`
- RPM: `0x4401`
- Ambient Temp: `0x4407`
- Pressure: `0x4408`
- Altitude: `0x4409`
- Fuel Flow: `0x440A`
- Serial Number: `0x440B` (Maximum only)
- Battery Used: `0x440C` (Maximum only)
- Engine Time: `0x440D` (Maximum only)
- Pump Amperage: `0x440E` (Maximum only)

---

## Troubleshooting

### Widget does not appear in the widget list
- Confirm the SD path is exactly: `SCRIPTS/GIB2A/main.lua`
- Remove any accidental nested folders and reboot.

### No telemetry values / “No data”
- Confirm ProHub is set to **FrSky** telemetry and the mode is saved.
- Confirm ProHub → receiver **S.Port** wiring.
- Confirm sensors are discovered (**Telemetry → Discover sensors**).
- Check ProHub telemetry LED status.

### Only some values are present
- Try **DIY Auto Detect** for `0A10 / 0A20 / 0A30` style sensors.
- Verify each widget source selection matches the expected unit (°C, rpm, %, mBar, etc.).
- If using Extended/Maximum data, set **Setup Mode = Expert** in the widget.

---

## Safety (Xicoy turbine reminder)

This widget is software-only; safe turbine operation remains your responsibility.

Key safety points:
- The engine is **NOT a toy**; misuse can cause damage and injury.
- Keep a **CO₂ (or gaseous) fire extinguisher (≥2kg)** nearby; avoid powder extinguishers unless last resort.
- Operate in **open air**; exhaust gases can cause asphyxiation.
- Keep spectators/children/animals away (safety radius).
- Protect eyes/ears during start.

---

## Design principles (project direction)

- ETHOS-friendly architecture: keep `wakeup()` for logic/telemetry, `paint()` for drawing, `configure()` for UX.
- Prefer stable, predictable behavior and minimal setup burden.

---

## Debug checklist (developer)

When a user reports “no data”:
1) Confirm SD path: `SCRIPTS/GIB2A/main.lua`  
2) Confirm ProHub is in FrSky mode and receiver S.Port is configured  
3) Confirm ETHOS telemetry discovery was run  
4) Confirm widget sources are bound (RPM, Temp1, Fuel at minimum)  
5) Ask for: discovered sensor list (names + units) + screenshots  

---

## Support / Feedback

Please open a GitHub Issue and include:
- Radio model + ETHOS version
- ProHub firmware/version (if known)
- Selected telemetry mode (Basic / Extended / Maximum)
- List of discovered sensors (names + units)
- Screenshots (Telemetry page + widget settings)

---

## License / Disclaimer

MIT — see `LICENSE`.  
See `DISCLAIMER.md` for warranty/liability limitations.
