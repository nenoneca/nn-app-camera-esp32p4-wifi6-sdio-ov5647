# nn-app-camera-esp32p4-wifi6-sdio-ov5647

nn camera firmware for the **ESP32-P4-WIFI6** board (production v3.1 silicon)
with an **OmniVision OV5647** (5 MP, Raspberry Pi Camera v1.3 class module).

This repo is configuration + glue only:

- `sdkconfig.board` — sensor selection (OV5647 native 1080p30 RAW10 — no crop,
  no PPA scale, unlike the IMX708 variants) and neutral colour defaults
  awaiting on-hardware tuning.
- `main/` — registers nn-app-media's `app_main.c` verbatim; no app-code copy.
- All shared code arrives via the `nn-app-media` submodule (which recursively
  brings `nn-modules`: libraries + the esp_video/esp_cam_sensor/esp_ipa/
  esp_sccb_intf forks).

## Build

    git submodule update --init --recursive
    idf.py set-target esp32p4 build

## Status

Builds green; NOT yet validated on hardware — the OV5647 CCM is identity and
WB is unity until a module is connected and tuned (`isp wb`, `isp ccm`).
