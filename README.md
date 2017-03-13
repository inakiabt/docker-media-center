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
An environment variables file is required on: `$HOME/.config/ubot/env` like
```bash
UBOT_TOKEN=YOUR_TOKEN
UTORRENT_PASSWORD=YOUR_UTORRENT_PASSWORD
UTORRENT_USERNAME=YOUR_UTORRENT_USERNAME
UTORRENT_PORT=YOUR_UTORRENT_PORT
UTORRENT_HOST=YOUR_UTORRENT_HOST
```

## Local configuration (macOS)
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
**Configure and restart**
```bash
echo "nameserver 127.0.0.1" > /etc/resolver/htpc
echo "address=/.htpc/192.168.1.10\n" >> /path/to/dnsmasq.conf
sudo brew services restart dnsmasq
```

## Thanks to

- [linuxserver.io](https://www.linuxserver.io/) for those awesome [dockerfiles](http://tools.linuxserver.io/dockers)
- [jwilder](https://github.com/jwilder) for [nginx-proxy](https://github.com/jwilder/nginx-proxy)
- [ekho](https://github.com/ekho) for the [dockerized version of utorrent](https://github.com/ekho/dockerized-tools)
- [gfjardim](https://github.com/gfjardim) for the [dockerized version of hamachi](https://github.com/gfjardim/docker-containers)
