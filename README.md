# Home Assistant Dashboard Widget for Übersicht

A beautiful, feature-rich Home Assistant dashboard widget for [Übersicht](http://tracesof.net/uebersicht/).

## Features

- **Live temperature monitoring** - Thermostat, flue/fireplace temperature with color-coded status
- **Smart lock control** - Lock/unlock your front door with one click
- **Alarm panel** - Arm home, arm away, disarm your security system
- **Camera feeds** - Live camera thumbnails from your security cameras
- **Weather-aware theming** - Animated backgrounds change based on weather (rain, snow, sun, clouds, fog)
- **Holiday themes** - Automatic decorations for holidays (Christmas snow, Halloween bats, Thanksgiving leaves, etc.)
- **Day/night modes** - Automatic theme switching based on sun position
- **High temperature alerts** - macOS notification + alarm sound when flue exceeds threshold
- **Draggable position** - Move the widget anywhere on screen (position persists between refreshes)

## Installation

1. Install [Übersicht](http://tracesof.net/uebersicht/) if you haven't already

2. Download and unzip `home-assistant.widget.zip`

3. Copy `home-assistant.jsx` to your widgets folder:
   ```
   ~/Library/Application Support/Übersicht/widgets/
   ```

4. Edit the configuration section at the top of the file (see Configuration below)

## Configuration

Open `home-assistant.jsx` and edit these values at the top:

```javascript
// ============ CONFIGURATION ============
// Replace with your Home Assistant URL and long-lived access token
const HA_URL = "https://your-home-assistant.local:8123";
const HA_TOKEN = "your_long_lived_access_token_here";

// Entity IDs - customize these to match your Home Assistant setup
const ENTITIES = {
  flue: "sensor.fireplace_flue_temperature",       // Optional: fireplace/wood stove sensor
  thermostat: "climate.thermostat",                // Your thermostat entity
  currentTemp: "sensor.thermostat_temperature",    // Temperature sensor
  lock: "lock.front_door",                         // Smart lock entity
  alarm: "alarm_control_panel.home_alarm",         // Alarm panel entity
  cameraFront: "camera.front_camera",              // Front camera entity
  cameraBackyard: "camera.backyard_camera",        // Backyard camera entity
  weather: "weather.home",                         // Weather entity for conditions
  sun: "sun.sun",                                  // Sun entity for sunrise/sunset
};
```

### Getting a Long-Lived Access Token

1. In Home Assistant, click on your profile (bottom left corner)
2. Scroll down to "Long-Lived Access Tokens"
3. Click "Create Token"
4. Give it a name (e.g., "Übersicht Widget")
5. Copy the token and paste it into `HA_TOKEN`

### Finding Your Entity IDs

1. In Home Assistant, go to Developer Tools > States
2. Search for your devices (thermostat, lock, alarm, cameras, weather)
3. Copy the entity IDs (e.g., `climate.living_room_thermostat`)

## Customization

### Adding Custom Holidays

Add your own special dates to the `HOLIDAYS` object:

```javascript
const HOLIDAYS = {
  // ... existing holidays ...
  birthday: { month: 5, day: 15, name: "Birthday", icon: "🎂", particles: "confetti" },
  anniversary: { month: 6, day: 20, name: "Anniversary", icon: "💍", particles: "hearts" },
};
```

Note: Months are 0-indexed (January = 0, December = 11)

### Test Mode

To preview holiday or weather themes without waiting:

```javascript
const TEST_WEATHER = "snowy";      // Options: snowy, rainy, sunny, cloudy, fog, etc.
const TEST_HOLIDAY = "christmas";  // Options: christmas, halloween, thanksgiving, etc.
```

Set both to `null` for normal operation.

### Flue Temperature Alert

The widget sends a macOS notification and plays an alarm sound when the flue temperature exceeds the threshold:

```javascript
const FLUE_ALERT_THRESHOLD = 500;  // Degrees Fahrenheit
```

## Supported Weather Conditions

- Sunny / Clear
- Cloudy / Partly Cloudy
- Rainy / Pouring
- Snowy
- Foggy
- Windy
- Thunderstorm
- Night variations of all conditions

## Supported Holidays

- New Year's Day (Jan 1) - Confetti
- Valentine's Day (Feb 14) - Hearts
- St. Patrick's Day (Mar 17) - Clovers
- Easter (approx. Mar 20) - Eggs
- Independence Day (Jul 4) - Fireworks
- Halloween (Oct 31) - Bats
- Thanksgiving (4th Thu of Nov) - Falling leaves
- Christmas (Dec 25) - Snowflakes

## Requirements

- macOS with Übersicht installed
- Home Assistant instance accessible from your Mac
- Long-lived access token from Home Assistant

## Troubleshooting

**Widget shows "Cannot reach Home Assistant"**
- Verify your `HA_URL` is correct and accessible from your Mac
- Check that your access token is valid
- Ensure Home Assistant is running and accessible on your network

**Cameras not loading**
- Verify camera entity IDs are correct
- Check that cameras are online in Home Assistant

**Weather not showing**
- Ensure you have a weather integration configured in Home Assistant
- Verify the `weather` entity ID matches your setup

## License

MIT
