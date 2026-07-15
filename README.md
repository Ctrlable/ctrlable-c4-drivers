# Ctrlable C4 Drivers

Compiled Control4 drivers that connect a Control4 system to a **Ctrlable** server (Home Assistant
compatible) over its WebSocket + REST APIs. A **Coordinator** driver holds the connection; each
device driver rides on top of it through a Control4 proxy binding.

This repository contains the **compiled `.c4z` packages** only. Source lives in the private
`ctrlable-c4-drivers-src` repository.

## Download

- **Individual drivers:** [`drivers/`](drivers) or the [latest release](../../releases/latest).
- **Everything in one package:** `C4-Ctrlable-Drivers-<version>.zip`.

| Driver | Connects | File |
| --- | --- | --- |
| Coordinator (install first) | connection to the Ctrlable server | `C4-Ctrlable-Coordinator.c4z` |
| Light | `light` (on/off, dim, color, CCT) | `C4-Ctrlable-Light.c4z` |
| Thermostat | `climate` | `C4-Ctrlable-Thermostat.c4z` |
| Media Player | `media_player` | `C4-Ctrlable-Media-Player.c4z` |
| Lock | `lock` | `C4-Ctrlable-Lock.c4z` |
| Fan | `fan` | `C4-Ctrlable-Fan.c4z` |
| Blinds | `cover` (position + tilt) | `C4-Ctrlable-Blinds.c4z` |
| Garage Door | `cover` (garage) | `C4-Ctrlable-Garage-Door.c4z` |
| Switch | `switch` | `C4-Ctrlable-Switch.c4z` |
| Binary Sensor | `binary_sensor` | `C4-Ctrlable-Binary-Sensor.c4z` |
| Generic Sensor | temperature / humidity / misc | `C4-Ctrlable-Generic-Sensor.c4z` |
| Alarm Panel | `alarm_control_panel` | `C4-Ctrlable-Alarm-Panel.c4z` |

## Installing

1. In Composer, add each `.c4z` to your driver library (or drop into the Control4 drivers folder).
2. Add **Ctrlable Coordinator** to the project and set:
   - **Ctrlable URL** — `host:port` of the Ctrlable server (e.g. `192.168.1.200:8123`).
   - **Long Lived Access Token** — a long-lived token from the Ctrlable server.
3. Add device drivers, bind each to the Coordinator, and set its **Entity ID**.

### TLS / SSL

Set **Use SSL = Yes** on the Coordinator to connect over `wss://` + `https://`.

- Leave the certificate path fields empty for the common server-only / self-signed case; with
  **Verify Certificate = No** (default) the driver connects without presenting a client certificate
  and without rejecting a self-signed server certificate.
- Set **Verify Certificate = Yes** with a **CA Certificate Path** to verify the server chain.
- Provide **Certificate Path** + **Private Key Path** only for mutual-TLS.

## Auto-update

The Coordinator can update connected Ctrlable drivers from this repository's
[Releases](../../releases/latest) (`C4-Ctrlable-*.c4z` assets). Keep this repository public so the
controller can download updates without authentication.

## Attribution

Derived from the open-source Control4 ↔ Home Assistant drivers by
[bphillips09](https://github.com/bphillips09), rebranded to Ctrlable with SSL and reliability fixes.
