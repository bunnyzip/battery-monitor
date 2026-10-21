# 🔋 Battery Monitor

Live LiFePO4 battery dashboard — ESP32-C3 + two JBD BMS batteries → Firebase → this page.

**No server, no PC needed.** The board pushes readings straight to Firebase;
this static page reads them in your browser.

👉 **Live page:** https://.github.io/battery-monitor/ *(enable GitHub Pages: Settings → Pages → main branch)*

## How it works

```
JBD BMS x2 ──BLE──> ESP32-C3 (ESPHome) ──HTTPS──> Firebase RTDB ──> GitHub Pages (this repo)
                    reads every 10s               batteries/1.json
                    pushes every 60s              batteries/2.json
                    history every 5min            history/N.json
```

## Files

| File | Purpose |
|---|---|
| `index.html` | Live report — reads Firebase directly, auto-refresh 30s |
| `firmware/bms-monitor.yaml` | ESPHome firmware (secrets redacted) |

## Firmware

Flash with [ESPHome](https://esphome.io):

```bash
esphome run firmware/bms-monitor.yaml
```

Put your own secrets in `firmware/secrets.yaml` (wifi, API PSK, Firebase URL).
