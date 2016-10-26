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