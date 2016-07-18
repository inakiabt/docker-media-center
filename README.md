# docker-media-center
Docker compose to start my local media center

## Includes

### Couchpotato
Running on: http://couchpotato.htpc/

### Plex Media Center
Running on: http://plex.htpc/web/

### uTorrent
Running on: http://utorrent.htpc/gui/web/

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
