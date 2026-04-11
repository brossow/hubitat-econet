# Rheem EcoNet Thermostat — Hubitat Driver

A Hubitat Elevation driver for Rheem EcoNet thermostats, ported from the [Home Assistant pyeconet integration](https://github.com/home-assistant/core/tree/dev/homeassistant/components/econet). Uses the ClearBlade cloud REST API for polling and MQTT command publishing.

## Features

- Reads current temperature, heating/cooling setpoints, HVAC mode, fan speed, and humidity
- Sends mode, setpoint, and fan commands via the ClearBlade HTTP→MQTT bridge
- Configurable poll interval (1 minute – 1 hour)
- Automatic token re-authentication on expiry
- Supports multiple thermostats on one account (select by index)
- Implements the Hubitat `Thermostat`, `RelativeHumidityMeasurement`, `Refresh`, and `Initialize` capabilities

## Supported Modes

| HVAC Mode | Fan Mode |
|---|---|
| Heat | Auto |
| Cool | Circulate (on continuous) |
| Auto (heat/cool) | |
| Fan Only | |
| Emergency Heat | |
| Off | |

## Installation

1. In Hubitat, go to **Drivers Code → New Driver**
2. Paste the contents of [`EcoNetThermostat.groovy`](EcoNetThermostat.groovy)
3. Click **Save**
4. Go to **Devices → Add Device → Virtual**
5. Give it a name and select **Rheem EcoNet Thermostat** as the driver type
6. Click **Save Device**
7. Enter your EcoNet email and password in the device preferences and click **Save Preferences**

The driver will authenticate, fetch your thermostat's state, and begin polling on the configured interval.

## Preferences

| Setting | Description |
|---|---|
| EcoNet Email | Your Rheem EcoNet account email |
| EcoNet Password | Your Rheem EcoNet account password |
| Thermostat Index | Which thermostat to control if you have multiple (0 = first) |
| Poll Interval | How often to refresh state from the cloud (default: 5 minutes) |
| Enable Debug Logging | Logs detailed info to the Hubitat log |

## Notes

- **Cloud-dependent**: All communication goes through Rheem's ClearBlade cloud API. Local control is not possible.
- **Commands**: Sent via the ClearBlade REST messaging endpoint, which proxies to MQTT — the same mechanism used by the Rheem mobile app.
- **Water heaters**: The Home Assistant integration also supports EcoNet water heaters; this driver covers thermostats only.

## Credits

Ported from the [Home Assistant EcoNet integration](https://github.com/home-assistant/core/tree/dev/homeassistant/components/econet) and the [pyeconet library](https://github.com/w1ll1am23/pyeconet) by [@w1ll1am23](https://github.com/w1ll1am23).
