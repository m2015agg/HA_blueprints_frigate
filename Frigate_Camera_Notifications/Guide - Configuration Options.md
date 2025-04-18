# Configuration Options Guide

This guide will give more detail about each of the configuration options and provide some troubleshooting tips where appropriate.

## Required Configuration

### Frigate Cameras
Select the cameras that will trigger notifications. If you do not see cameras listed in the drop-down, check you have the Frigate integration installed.

### Mobile Device
Select a device that runs the official Home Assistant app to receive notifications. If you wish to notify a group of devices and/or Android/Fire TV use the field below to override this selection. This will be ignored in that case but is still required.

### Base URL
The external URL for your Home Assistant instance. Recommended for iOS and required for Android/Fire TV. Must include the scheme i.e http:// or https://

### MQTT Topic
The MQTT topic Frigate sends review messages in.

## Notification Customisations

### Title

A bold Heading for yuor notification. Typically left blank. 

### Message

A message attached to the notification. Several prebuild formats are available in the drop down, but you can also write your own. 

#### Message Variables

| Name | Variable | Description | Events/Reviews |
| -----------| ---------- | -------- | -------- |
| Camera Name | {{camera_name}} | The formatted (friendly) name of the camera | Both |
| Confidence | {{ event['after']['top_score'] \|float(0) }} | The value indicating the frigate confidence value | Events |
| Object | {{label}} | The Object type - replaced by persons name if double take face match is correctly configured  | Both |
| Time | {{event['before']['start_time']\|timestamp_custom('%H:%M')}} | The event start time | Both |
| Zones (Entered) | {{enteredzones}} or formatted like: <br>{% if enteredzones %} in the {{ enteredzones \| join(', ') \| replace('_',' ') }}{% endif %}| The dictionary containing all entered zones. | Both |

### Subtitle

Another message field available for use. 

### Update Sub Labels

Friagte can integrate with face matching software DoubleTake to identify who the person detected is. If configured properly within Frigate, enabling this option will result in the Name replacing the generic Person label provided the `{{label`}} variable is contained in the text fields above. 

### Critical
default: false

On most devices, this will bypass dnd or silent modes. This field can be templated so that it only is critical at certain times of day or when other conditions are met. Some examples exist in the drop down. Must result in the text `true` or `false` to function. 

### TTS Override

Uses Text to Speach to announce the message. 

Some phones (the Samsung galaxy line, in particular,) disable the ability to use alarm_stream as a means to bypass the current sound settings. This option allows TTS to announce the alert instead, which does bypass the sound settings.

### TTS Entity

This entity is used to store which announcements have already been made and prevent double ups. You need to creat an input text helper and select it here. 

### Alert Once

On most Android and iOS devices, this will prevent the notification from making sounds except for the notification triggered at the very start of the event. 

### Initial Attachment

The attachment to include at the beginning of the event. Typically videos and gifs don't show much at the very beginning, so you may wish to send a snapshot of the object initially.

### Subsequent Attachment

After the initial trigger notification, subsequent notifications can have a different attachment if selected here. 
Gif is probably the best option here vs video below. 

### Video

Similar to attchment, except for videos. It will override attachments.

### Final Update

Force a notification at the end of the event. Used to ensure the full video of GIF is sent. Configure the delay if necessary in the timers section (default - 5 seconds).

### Color

Set the color of the notification on your Android mobile device or TV.
TV supports grey, black, indigo, green, red, cyan, teal, amber or pink only.

### Icon

Change the icon that displays on the notification. You can enter a single icon or create a template like the example given in the dropdown. You must include 'mdi:' in the icon name.

### Group

The group name that will determine if notifications are grouped on your mobile device. If you want notifications grouped by camera, ensure it contains {{camera}}

### Sound (IOS)

You can specify a sound file on your device that will play for the notifications. You will need to import the sound file into Home Assistant.

### Volume (IOS)

Set the default notification volume. Overridden by Critical. 

### Live View (IOS)

Attach a live view from the selected entity to the notification for iOS devices.

### Android Auto (Android)

Show the notification on Android Auto if the receiving device is connected.

### Sticky (Android)

By default, tapping on the notification on android (except for when using the action buttons) clears the notification. This sticky option stops the notification from clearing when tapped and notifications must be manually swiped away.

### Channel (Android)

Notification channels on android allow you to customise things like the notification sound. This is configured on your device and not within the blueprint. To edit a channel the phone must first recieve a notification in that channel, so trigger th eautomation once after setting the channel and then find it in your device notification settings.

## Filters

### Event Type

Set the severity that you wish to be notified about. You can select one or both. 

### Master Condition

An overarching condition builder that can be used to stop the notifications from being sent when false. 

### Zone Filter

### Zone Filter On/Off Toggle

Enable or disable the Zone Filter. 

#### Required Zones

Only notifiy if the selected zones are entered (one or more depending on below toggles)

Enter the name of one zone at a time. It must be lowercase and include underscores as per your Frigate config.

#### Multi Zone Toggle

Require all zones specified above to be entered, instead of any listed zone. Zone Filter must be enabled also

#### Zone Order Enforced

Combined with Multi-Zone, requires zones to be entered in the same order as specified above.

### Object Filter
Select only objects that you wish to be notified for.  Enter or select one object at a time.

### Presence Filter

Only notify if ALL of the selected presence entities are not "home".

### State Filter

### State Filter States

### Time Filter

### Cooldown

### Silence timer

### Loitering

## Action Buttons

### Tap Action

### Action Button 1

### Action Button 2

### Action Button 3

## TV Options

### Position

### Size

### Duration

### Transparency

### Interrupt

## Troubleshooting

## Debug

### Debug enabled

Helps with troubleshooting by sending debug information about the variables to the home assistant log, and more usefully, displayed them within the automation trace in an easy to read format. 

### Redact Base URL

Default: true

Hide your base URL from the debug ouput to make sharing it easier and safer. 



