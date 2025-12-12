# GIB2A — Xicoy ProHub graphical widget (ETHOS 1.7)

GIB2A is an **ETHOS Lua widget** that displays **Xicoy ProHub** turbine telemetry with a configuration menu and a pilot-focused layout.

## Highlights
- Core values: **RPM**, **EGT**, **Pump**, **Fuel**
- Red zones (defaults):
  - **EGT > 700°C**
  - **RPM > 100%** (up to **110%**)
- White text with title + subtitle + signature
- **Basic / Expert** mode (depending on configuration)

## Installation (ETHOS)
1. Download the latest release (recommended) or clone this repository.
2. Copy the **`GIB2A`** folder to your radio SD card so you end up with:

   `SCRIPTS/WIDGETS/GIB2A/main.lua`

3. Reboot the radio.
4. Add the widget on a screen (Model → Display → Widgets) and select **GIB2A**.

## Configuration
Open the widget settings and select the telemetry **sources discovered by ETHOS** (via ProHub).

If a value is missing:
- confirm telemetry is active and sensors are discovered/updated;
- verify the selected source is correct (and has the expected unit);
- try a reboot after copying/updating the widget.

## Compatibility
- Firmware: ETHOS **1.7.x** (target)
- Radios: FrSky ETHOS radios that support widgets (e.g., Tandem X20/X20S, etc.)
- Telemetry: Xicoy **ProHub** (sensors discovered by ETHOS)

## Development
- Source code: `GIB2A/main.lua`
- Contributions are welcome (see `CONTRIBUTING.md`)

## Support / Feedback
Use **GitHub Issues** (Bug / Feature request). Please include:
- radio model + ETHOS version
- ProHub version
- detected sensors (names + units)
- screenshot(s) / short video
- steps to reproduce

## License
MIT — see `LICENSE`.

See DISCLAIMER.md for warranty and liability limitations.
