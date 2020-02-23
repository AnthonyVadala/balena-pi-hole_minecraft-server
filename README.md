# balena Pi-hole & Minecraft Server

If you are looking for a way to quickly and easily get up and running with [Pi-hole]((https://github.com/klutchell/balena-pihole)) and a [Minecraft Server](https://github.com/AlexProgrammerDE/balena-minecraft-server) for your home network, this is the project for you.

This project is a [balenaCloud stack](https://www.balena.io/cloud/)

> balenaCloud is a free service to remotely manage and update your Raspberry Pi through an online dashboard interface.

## Getting Started

- A free balenaCloud account
- Raspberry Pi 4B (4GB Model **HIGHLY** recommended)
- 16GB or greater micro SD Card (SanDisk Extreme Pro SD cards recommended)

## Setting Up

### Setup the Raspberry Pi

- Login to the balenaCloud dashboard
- Create an application, selecting the correct device type for your Raspberry Pi
- Add a device to the application, enabling you to download the OS
- Flash the downloaded OS to your SD card with [balenaEtcher](https://www.balena.io/etcher/)
- Power up the Pi and check it's online in the dashboard
- Configure Application Environment Variables

#### Application Environment Variables

Application Environment Variables apply to all services within the application, and can be applied fleet-wide to apply to multiple devices.

##### Pi-Hole Variables
|Name|Example|Purpose|
|---|---|---|
|`TZ`|`America/New_York`|To inform services of the timezone in your location, in order to set times and dates within the applications correctly. Find a [list of all timezone values here](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones).|
|`DNSMASQ_LISTENING`|`eth0`|We set this to `eth0` to indicate we want DNSMASQ to listen on the ethernet interface of the Raspberry Pi. If you're connecting to your network with WiFi replace this with `wlan0`|
|`INTERFACE`|`eth0`|As above.|
|`WEBPASSWORD`|`mysecretpassword`|_(optional)_ password for accessing the web-based interface of Pi-hole - you won’t be able to access the admin panel without defining a password here.
|`DNS1`|`127.0.0.1#5053`|_(optional)_ Tell Pi-hole where to forward DNS requests that aren’t blocked. We’re using the [dnscrypt-proxy](https://github.com/DNSCrypt/dnscrypt-proxy) project here but you can specify your own.|
|`DNS2`|`127.0.0.1#5053`|_(optional)_ Secondary DNS server - see above.|
|`ServerIP`|`x.x.x.x`|_(recommended)_ Set to your server's LAN IP, used by web block modes and lighttpd bind address.|

##### Minecraft Server Variables
|Name|Example|Purpose|
|---|---|---|
|`SCP_PASSWORD`|`balenaserver`|_(optional)_ Set your own SCP password, defaults to `balenaminecraftserver` |
|`DEVICE_HOSTNAME`|`balenaminecraftserver`|_(optional)_ Set your own device hostname.|
|`DOUBLE_RAM`|`false`|_(recommended)_ The default value used by a Minecraft server is 1GB if value is set to `true` doubles it to 2GB.|

### Deploy This Application

- Install the [balena CLI tools](https://github.com/balena-io/balena-cli/blob/master/INSTALL.md)
- Login with `balena login`
- Download this project and from the project directory run `balena push <appName>` where <appName> is the name you gave your balenaCloud application in the first step.

### Connecting

#### Pi-hole
Open a web browser and enter the device IP address like this: `192.168.1.2/admin`. You can sign in and configure settings using the value set for `WEBPASSWORD`.

For more information on post install setup, check the offical Pi-hole documentation here: [https://docs.pi-hole.net/main/post-install/](https://docs.pi-hole.net/main/post-install/)

#### Minecraft
Open the Minecraft and enter your `DEVICE_HOSTNAME`, by default this will be `balenaminecraftserver`. You can also connect using the device IP address.

### Updating
- From the project direction run `git submodule foreach git pull origin master`
- Wait for project changes to be pulled
- Run `balena push <appName>` to push the changes

# Credit
All credit goes to:
- [https://github.com/klutchell](https://github.com/klutchell) for [balena-pihole](https://github.com/klutchell/balena-pihole)
- [https://github.com/AlexProgrammerDE](https://github.com/AlexProgrammerDE) for [balena-minecraft-server](https://github.com/AlexProgrammerDE/balena-minecraft-server)