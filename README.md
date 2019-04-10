# docker-home

So today we will need this commands:

### Portainer
``` make dirs```

```docker run -d -p 9000:9000 --name portainer --restart always -v /var/run/docker.sock:/var/run/docker.sock -v ~/smart-home/portainer/data:/data portainer/portainer:arm```

### Home-Assistant
```docker run -d --restart always --name="home-assistant" -v ~/smart-home/home-assistant/config:/config -v /etc/localtime:/etc/localtime:ro -p 8123:8123 homeassistant/raspberrypi3-homeassistant```

### Mosquito
```docker run -itd --name="mosquitto" --restart on-failure -p 1883:1883 -p 9001:9001 -v ~/smart-home/mosquitto/log:/mosquitto/data -v /home/ency/smart-home/mosquitto/log:/mosquitto/log eclipse-mosquitto```

#### Integrating Switch
```
mqtt:
  broker: IP_ADDRESS_BROKER
```

```
switch:
    platform: mqtt
    name: "Whatever you want"
    command_topic: "cmnd/<topic>/power"
    state_topic: "stat/<topic>/POWER"
    qos: 1
    payload_on: "ON"
    payload_off: "OFF"
    retain: true
 ```

### Node Red (Optional)

```docker run -d --name=node-red --restart=always -p 1880:1880 -u 1000:1000 -v ~/smart-home/node-red:/data nodered/node-red-docker:rpi-v8```
