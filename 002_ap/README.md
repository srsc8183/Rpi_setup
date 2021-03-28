### Install the access point software



software package installed

```shell
sudo apt-get install hostapd
sudo apt-get install dnsmasq

sudo systemctl stop hostapd
sudo systemctl stop dnsmasq

```



### Configure a static IP for the wlan0 interface

```shell
sudo nano /etc/dhcpcd.conf
```



add the following lines at the end

```
interface wlan0
static ip_address=192.168.1.10/24
#denyinterfaces eth0
denyinterfaces wlan0
```

### Configure the DHCP server 

```shell
sudo mv /etc/dnsmasq.conf /etc/dnsmasq.conf.orig
sudo nano /etc/dnsmasq.conf
```

```shell
interface=wlan0
  dhcp-range=192.168.0.11,192.168.0.30,255.255.255.0,24h
```



### Configure the access point host software

```shell
sudo nano /etc/hostapd/hostapd.conf
```

```shell
interface=wlan0
bridge=br0
hw_mode=g
channel=7
wmm_enabled=0
macaddr_acl=0
auth_algs=1
ignore_broadcast_ssid=0
wpa=2
wpa_key_mgmt=WPA-PSK
wpa_pairwise=TKIP
rsn_pairwise=CCMP
ssid=NETWORK
wpa_passphrase=PASSWORD
```

```shell
sudo nano /etc/default/hostapd
```


```shell
DAEMON_CONF="/etc/hostapd/hostapd.conf"
```


```shell
sudo reboot
```

[wireless access point](https://thepi.io/how-to-use-your-raspberry-pi-as-a-wireless-access-point/)

[bridged wireless access point](https://www.raspberrypi.org/documentation/configuration/wireless/access-point-bridged.md)

[routed wireless access point]( https://www.raspberrypi.org/documentation/configuration/wireless/access-point-routed.md)





