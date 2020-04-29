home-assistant-addons
=====================

Home Assistant addons by Max

Add to Home Assistant using the repository url: 

Add the following repository URL to Home Assistant via the "Add-On Store":  
https://github.com/maxkueng/home-assistant-addons

## http2mqtt

A bridge to connect HTTP-based IoT devices to MQTT.

### Installation

Add this repo to your add-on repositories and install "http2mqtt". Note that
there might be an error message after installation saying "[Object] [Object]"
or something. It's fine, just refresh the page.

### Example Configuration

```
mqtt:
  broker: 'mqtt://10.13.37.42:1883'
  username: mqtt
  password: secret
homeAssistant:
  discovery: 'yes'
options:
  mystrom-buttons:
    route: /mystrom/generic
    buttons:
      - mac: BADA55FA7A55
        name: Wifi Button Plus
        type: button-plus
        wheelMin: 0
        wheelMax: 255
        wheelSpeed: 2.5
      - mac: FA7A55BADA55
        name: Wifi Button
        type: button
  mystrom-switch:
    switches:
      - host: 10.13.37.43
        name: Wifi Switch 1
  edimax-plug:
    switches:
      - name: Edimax Plug 1
        host: 10.13.37.44
        username: admin
        password: s3cret
  shelly-switch:
    switches:
      - name: Shelly 1PM 1
        type: shelly-1pm
        host: 10.13.37.45
        username: admin
        password: s3cret
```

For details see https://github.com/maxkueng/http2mqtt
