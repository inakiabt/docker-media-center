# docker-media-center
Docker compose to start my local media center

## Includes

### Couchpotato
Running on: http://couchpotato.htpc/

### Plex Media Center
Running on: http://plex.htpc/web/

### uTorrent
Running on: http://utorrent.htpc/gui/web/

### Dashboard
[manage-this-node](https://github.com/onedr0p/manage-this-node) running on: http://dashboard.htpc/

### NGINX Proxy
This container act as a reverse proxy of the above containers

### LogmeIn Hamachi
*Notes: start container, enter with `docker exec -it hamachi bash` and join your network manually with `hamachi join <network id> <password>`*

### Emby
Running on: http://emby.htpc/

### Mr. Potato Slack bot
https://github.com/RolfKoenders/potato

An environment variables file is required on: `$HOME/.config/mrpotato/env` like
```bash
CB_SLACK_KEY=YOUR_SLACK_KEY
CB_SLACK_NAME=mrpotato
CB_HOST=http://couchpotato
CB_PORT=5050
# CB_BASE_URL=/
CB_COUCH_KEY=YOUR_COUCHPOTATO_KEY
```

### uTorrent Slack bot
https://github.com/inakiabt/utorrent-bot

An environment variables file is required on: `$HOME/.config/ubot/env` like
```bash
UBOT_TOKEN=YOUR_TOKEN
UTORRENT_PASSWORD=YOUR_UTORRENT_PASSWORD
UTORRENT_USERNAME=YOUR_UTORRENT_USERNAME
UTORRENT_PORT=YOUR_UTORRENT_PORT
UTORRENT_HOST=YOUR_UTORRENT_HOST
```

## DNS (macOS)
Taken from: https://medium.com/@williamhayes/local-dev-on-docker-fun-with-dns-85ca7d701f0a
### dsnmasq
**Install [brew services](https://github.com/Homebrew/homebrew-services)**
```bash
brew tap homebrew/services
```
**Install and start the service**
```bash
brew install dnsmasq
sudo brew services start dnsmasq
```
**Setup 127.0.0.1 alias**
```bash
sudo ifconfig lo0 alias 10.254.254.254
cat << EOF | sudo tee -a /Library/LaunchDaemons/com.docker-media-center.loopback1.plist
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
  <dict>
    <key>Label</key>
    <string>com.docker-media-center.loopback1</string>
    <key>ProgramArguments</key>
    <array>
        <string>/sbin/ifconfig</string>
        <string>lo0</string>
        <string>alias</string>
        <string>10.254.254.254</string>
    </array>
    <key>RunAtLoad</key>
    <true/>
  </dict>
</plist>
EOF
sudo launchctl load /Library/LaunchDaemons/com.docker-media-center.loopback1.plist
```

**Configure and restart**
```bash
echo "nameserver 10.254.254.254" > /etc/resolver/htpc
echo "domain htpc" >> /etc/resolver/htpc
echo "search_order 1" >> /etc/resolver/htpc

echo "address=/.htpc/10.254.254.254\n" >> /path/to/dnsmasq.conf
sudo brew services restart dnsmasq
```

## Thanks to

- [linuxserver.io](https://www.linuxserver.io/) for those awesome [dockerfiles](http://tools.linuxserver.io/dockers)
- [jwilder](https://github.com/jwilder) for [nginx-proxy](https://github.com/jwilder/nginx-proxy)
- [ekho](https://github.com/ekho) for the [dockerized version of utorrent](https://github.com/ekho/dockerized-tools)
- [gfjardim](https://github.com/gfjardim) for the [dockerized version of hamachi](https://github.com/gfjardim/docker-containers)
