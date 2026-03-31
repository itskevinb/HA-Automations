# HA-Automations

Home Assistant configuration snippets for lighting, media, and bedroom presence
automations.

This repository is currently a focused automation/config export rather than a
full Home Assistant instance backup. The goal is to keep the logic versioned,
portable, and easier to review.

## Repository Layout

- `configuration.yaml`: Core Home Assistant configuration and MQTT sensor
  definitions.
- `automations.yaml`: Main automation rules.
- `scripts.yaml`: Placeholder include file so the config can load cleanly.
- `scenes.yaml`: Placeholder include file so the config can load cleanly.
- `themes/`: Placeholder themes directory required by `configuration.yaml`.
- `blueprints/`: Imported Home Assistant blueprints used for reusable
  automation/script patterns in the live instance.
- `custom_components/`: HACS and locally installed custom integrations in the
  live instance.
- `www/`: Frontend assets served by Home Assistant.
- `tts/`: Generated text-to-speech cache.
- `deps/`: Home Assistant dependency cache for the running container.

## What Is Automated

- Bedroom bedtime and wake-state lighting flows
- Bed occupancy and radar presence handling
- Spotify-driven dining-room amp control
- Outdoor lighting at sunset/sunrise
- Kitchen, sunroom, music-room, and garage-entry motion lighting

## Required Home Assistant Helpers And Entities

This repo references entities that are expected to exist in the Home Assistant
instance. The most important ones include:

- `input_boolean.input_boolean_bedroom_sleep_mode`
- `input_boolean.music_room_occupied`
- `media_player.spotify_itskevinbbitch`
- `media_player.spotify_babe`
- `media_player.apple_tv_mb`
- `media_player.music_room`
- `binary_sensor.bed_pressure_occupied`
- `binary_sensor.bed_radar_presence`
- `binary_sensor.motion_sensor`
- `binary_sensor.music_room_motion`
- `binary_sensor.contact_sensor_2`
- `light.bedside`
- `light.r_vanity`
- `light.l_vanity`
- `light.main_light`
- `light.kitchen_island`
- `light.kitchen_island_2`
- `light.sunroom_main`

Several automations also reference Home Assistant-generated `device_id` and
opaque entity registry IDs. Those values are instance-specific and may need to
be updated if the config is restored into a different HA environment.

## MQTT Topics Used

The config defines custom MQTT entities for:

- `cameraui/BackCam/motion`
- `bed/radar/presence`
- `bed/radar/distance`
- `bed/pressure/occupied`
- `bed/pressure/voltage`
- `bed/pressure/status`

## Live Instance Inventory

The production Home Assistant configuration root also includes:

- `blueprints/automation/homeassistant/motion_light.yaml`
- `blueprints/automation/homeassistant/notify_leaving_zone.yaml`
- `blueprints/automation/Raukze/contact-sensor-left-open-notification.yaml`
- `blueprints/script/homeassistant/confirmable_notification.yaml`

Installed custom integrations observed in the live instance:

- `hacs` (`2.0.5`)
- `qsys_qrc` (`v0.7.0`)
- `unraid_api` (`1.5.1`)

Other live-instance files present outside this repo snapshot:

- `secrets.yaml`
- `home-assistant.log`
- `home-assistant_v2.db`
- `.storage/`

These are intentionally not mirrored fully into this repository because they
contain environment-specific runtime state, credentials, registry data, or
generated artifacts.

## Operational Notes

- `scripts.yaml` and `scenes.yaml` are empty in the live instance as of
  March 31, 2026, so the placeholder files in this repo match production.
- The live instance currently has repeated localhost authentication failures
  from the Home Assistant iOS app user agent and an Xbox connectivity error in
  `home-assistant.log`.
- The mobile app registrations observed in `.storage/core.config_entries`
  include Kevin's Phone, Melbourne's iPad, and Melbourne's iPhone.

## Notes

- `scripts.yaml`, `scenes.yaml`, and `themes/` are intentionally included as
  placeholders so a fresh checkout matches the includes declared in
  `configuration.yaml`.
- This repository does not currently include dashboards, packages, secrets, or
  a full Home Assistant backup.
- Before deploying elsewhere, run a Home Assistant configuration check and
  verify helper/entity names match the destination instance.
