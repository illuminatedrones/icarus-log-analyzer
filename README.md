# ICARUS — Drone Log Analyzer

Browser-based analyzer for ArduPilot `.bin` logs from light-show drones. Parses the binary log entirely in the browser (nothing is uploaded), surfaces the most likely root cause of any flight issue, and lets you compare drones side-by-side.

## Live app

→ **https://illuminatedrones.github.io/icarus-log-analyzer/**

Drop one or more `.bin` files on the upload area to begin.

## What it surfaces

**Show-killer detection:**
- Sustained yaw spin (rolling 1s window — ignores single-sample noise)
- RTK / GPS quality measured as **% of flight at Fixed**, plus longest continuous degraded run and any hard fix-loss window
- EKF variance collapse (`NKF4` / `XKF4` innovation ratios)
- Vibration peaks + accelerometer clipping (`VIBE`)
- Sudden power loss / battery ejection inference
- Motor saturation (lift motors pinned at ≥1900 PWM)
- Autopilot crash-check, RC failsafe, throttle failsafe, parachute, force-land events
- Free-text autopilot diagnostics scanned from `MSG`

**"Likely cause" verdict** at the top of the findings list synthesizes the worst critical signal into a single plain-English root-cause statement.

**Message Explorer** — every logged message type comes with a multi-paragraph plain-English description: what it is, when it's logged, what each key field means, and what to look for when diagnosing.

## Local dev

It's one self-contained HTML file. To iterate:

```bash
open index.html        # opens in default browser
# or
python3 -m http.server # serve at http://localhost:8000
```

No build step, no dependencies.

## Privacy

All parsing happens client-side in the browser. Log files never leave your machine.
