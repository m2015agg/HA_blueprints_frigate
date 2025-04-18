# HA_blueprints_frigate
A collection of Home Assistant automation blueprints for Frigate camera notifications

## Frigate Camera Notifications

This blueprint will send a notification to your device when a Frigate event for the selected camera is fired. The notification will initially include the thumbnail of the detection, but include an actionable notification allowing you to view the clip and snapshot.

With this blueprint, you may send the notification to multiple devices by leaving "Device" blank and instead use a notification group.

### Import Options

STABLE: [![Import blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/m2015agg/HA_blueprints_frigate/main/Frigate_Camera_Notifications/Stable.yaml)

BETA: [![Import blueprint](https://my.home-assistant.io/badges/blueprint_import.svg)](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https://raw.githubusercontent.com/m2015agg/HA_blueprints_frigate/main/Frigate_Camera_Notifications/Beta.yaml)

### Software Version Requirements

- Minimum Home Assistant Version: 2024.11
- Minimum Frigate Version: 0.14
- Minimum Frigate Integration Version: 5.7.0
  - "Enable the unauthenticated notification event proxy" must be ticked during setup
- An MQTT broker connected to home assistant and frigate.
- Minimum iOS Version: 15.0

### Required Entities

- Frigate Camera Name
- Mobile App Device or the name of a Notification Group

### Features

- Easily select one or more camera entities or mobile device using a drop down menu
- Send notifications to iOS mobile devices
- Configure the title and message of the notification
- Include a thumbnail, snapshot, GIF or video of the event with bounding box and crop options for images
- Dynamically handle things like object type, zones and face detection from doubletake
- Automatically handle some common errors like case matching and bad urls etc
- Optionally send the notification as a critical alert
- Optionally limit the playing of audio for secondary notification updates, and on iOS, customise the sound (Alert Once)
- Customise the notification colour and icon

#### Filters
- Specify which zones to be notified about (Zone Filter)
  - Choose between enforcing all required zones simultaneously or any one zone (Multi Zone)
  - Choose to enforce zones in a specific order (e.g arriving but not leaving)
- Specify what type of objects to be notified about (Object Filter)
- Disable notifications if a presence entity or group is "home" (Presence Filter)
- Limit notifications based on the state of another entity (State Filter)
- Limit notifications to certain hours of the day (Time Filter)
- Configure a cooldown for the camera to reduce the number of notifications when back-to-back events occur
- Silence new notifications for a defined amount of time
- Set a loitering timer to notify you of stationary objects that remain for a set period of time
- Custom Template Filters

#### Actions
- Configure what happens when you tap the notification (Tap Action)
- Configure 3 action buttons to open almost anything (defaults are: View Clip, View Snapshot and Silence New Notifications)

#### More
- Debug option to help troubleshooting and the ability to redact your Base URL from the debug output
- Support for multiple Frigate instances by specifying the ClientID and MQTT topic
- Custom sounds on iOS
- Optionally send a live view to iOS

### Documentation

For detailed configuration options and guides, please refer to:
- [Configuration Options Guide](Frigate_Camera_Notifications/Guide%20-%20Configuration%20Options.md)
- [Debug Options Guide](Frigate_Camera_Notifications/Guide%20-%20Debug%20Option.md)
