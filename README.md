# ❄️ LG Refrigerator Card

A custom [Home Assistant](https://www.home-assistant.io/) Lovelace card for LG ThinQ refrigerators (French Door, Side-by-Side, Bottom Freezer, Top Freezer). It displays fridge and freezer temperature setpoints, door status, Express Freeze mode, air/water filter status, water usage, and dismissible notifications, all in a compact, mobile-friendly layout.

| Light Theme | Dark Theme |
|---|---|
| <img width="503" height="330" alt="image" src="https://github.com/user-attachments/assets/beb4c852-0d78-4c27-93b1-9771a97fd7ee" /> | <img width="504" height="334" alt="image" src="https://github.com/user-attachments/assets/8784d0f2-d640-4285-b6e9-2d45065fecdf" /> |

## ✨ Features

- **Two independent temperature zones** (fridge and freezer) with +/- stepper controls that respect each entity's own min/max/step attributes.
- **Door status indicator** with a live pulsing badge when the door is open.
- **Express Freeze toggle** with visual on/off state.
- **Air and water filter status**, with automatic warning highlight when a filter needs replacement.
- **Water usage tracking** (in m³).
- **Dismissible notification banner** for appliance alerts. Once dismissed, the same notification won't reappear, it stays hidden until a *new* notification arrives (persisted per browser via `localStorage`).
- **Multi-language support**: English, French, Spanish, Italian, Portuguese, German, and Dutch. Automatically detects your Home Assistant profile language, or can be forced via configuration.
- **Refrigerator Layouts**: Choose your model (French Door, Side-by-Side, Bottom Freezer, or Top Freezer) directly from the visual editor, and the illustration adapts automatically, including door positions, handles, and control panel placement.
- **Configurable illustration**: show/hide the refrigerator illustration, and choose whether it appears on the left or right of the temperature zones.
- **Visual editor**: fully configurable through the Lovelace UI editor, no YAML required.

## ℹ️ Prerequisite

This card is designed to work with entities exposed by the [LG Thinq](https://www.home-assistant.io/integrations/lg_thinq) integration.

## 📦 Installation

### HACS (recommended)

1. Open **HACS** in Home Assistant.
2. Click on the three dots in the top right corner
3. Select "Custom repositories"
4. Add this repository URL `https://github.com/KroFR/ha-lg-refrigerator-card`
5. Select "Dashboard"
6. Click "Add"
7. Search for **LG Refrigerator Card** and install it

### Manual installation

1. Download `lg-refrigerator-card.js` from the `dist` folder of this repository.
2. Copy it into your Home Assistant `www/community/ha-lg-refrigerator-card/lg-refrigerator-card.js` folder.
3. Go to **Settings** > **Dashboards** > three-dot menu > **Resources**.
4. Select **Add resource**, set the URL to `/hacsfiles/ha-lg-refrigerator-card/lg-refrigerator-card.js?v=1`, and set resource type to **JavaScript module**.
5. Refresh your browser.

## Adding the card

1. Edit any dashboard and select **Add Card**.
2. Search for **LG Refrigerator Card**, or select **Manual** and use the YAML shown below.
3. Configure the entities either through the visual editor or directly in YAML.

## ⚙️ Configuration options

| Name | Type | Required | Default | Description |
|---|---|---|---|---|
| `type` | string | Yes | — | Must be `custom:lg-refrigerator-card`. |
| `name` | string | No | — | Card title shown in the header. |
| `language` | string | No | — | Force a specific language. One of `en`, `fr`, `es`, `it`, `pt`, `de`, `nl`. Leave unset to auto-detect from your Home Assistant profile. |
| `door_entity` | string (`binary_sensor`) | No | — | Entity reporting the refrigerator door state (`on` = open). |
| `express_mode_entity` | string (`switch`) | No | — | Entity controlling Express Freeze mode. |
| `notification_entity` | string (`event`) | No | — | Event entity used to surface appliance alerts/notifications. |
| `air_filter_entity` | string (`sensor`) | No | — | Air filter status sensor. |
| `water_filter_entity` | string (`sensor`) | No | — | Water filter status sensor. |
| `water_filter_used_entity` | string (`sensor`) | No | — | Sensor reporting total filtered water usage, in m³. |
| `zone1_label` | string | No | — | Label for the first temperature zone. |
| `zone1_temp_entity` | string (`number`) | No | — | Number entity controlling the fridge temperature setpoint. |
| `zone2_label` | string | No | — | Label for the second temperature zone. |
| `zone2_temp_entity` | string (`number`) | No | — | Number entity controlling the freezer temperature setpoint. |
| `fridge_layout` | string | No | `french_door` | Choose your model from `french_door`, `side_by_side`, `bottom_freezer`, or `top_freezer`. |
| `fridge_visual_position` | string | No | `left` | Position of the refrigerator illustration relative to the temperature zones. One of `left`, `right`. |
| `hide_fridge_visual` | boolean | No | `false` | Hides the refrigerator illustration entirely. |

## 📝 Usage example

### Full sensor setup
The complete configuration, with both zone temperatures, the Bottom Freezer layout to the right, air and water filter information.

| Light Theme | Dark Theme |
|---|---|
| <img width="502" height="329" alt="image" src="https://github.com/user-attachments/assets/cfc67d1e-62c4-476e-9125-c8a9d0a0d809" /> | <img width="503" height="332" alt="image" src="https://github.com/user-attachments/assets/456efb94-ffa0-4b70-8fdf-7b8579636e29" /> |

```yaml
type: custom:lg-refrigerator-card
door_entity: binary_sensor.refrigerateur_door
express_mode_entity: switch.refrigerateur_express_mode
notification_entity: event.refrigerateur_notification
air_filter_entity: sensor.refrigerateur_fresh_air_filter
water_filter_entity: sensor.refrigerateur_water_filter
water_filter_used_entity: sensor.refrigerateur_water_filter_used
zone1_temp_entity: number.refrigerateur_fridge_temperature
zone2_temp_entity: number.refrigerateur_freezer_temperature
fridge_visual_position: right
hide_fridge_visual: false
fridge_layout: bottom_freezer
```

### Compact layout without illustration
Minimal example (temperature zones only, illustration hidden) with forced language.

| Light Theme | Dark Theme |
|---|---|
| <img width="501" height="244" alt="image" src="https://github.com/user-attachments/assets/3f75a980-df76-4d5b-b5f2-656e1eeebc93" /> | <img width="506" height="249" alt="image" src="https://github.com/user-attachments/assets/56dc27f1-db1b-41a0-a370-c253ed2e20ed" />
 |

```yaml
type: custom:lg-refrigerator-card
zone1_temp_entity: number.refrigerateur_fridge_temperature
zone2_temp_entity: number.refrigerateur_freezer_temperature
hide_fridge_visual: true
language: fr

```

## 📄 License

[<img width="78" height="20" alt="image" src="https://github.com/user-attachments/assets/c14c93d7-50c2-4726-9a47-77f6c466e5b5" />](https://github.com/KroFR/ha-lg-refrigerator-card/blob/main/LICENSE)
