# Setting-up-a-WiFi-Hotspot-for-VR-Streaming-on-Arch-Linux

`sudo pacman -S dnsmasq wireless-regdb`

`sudo nano /etc/conf.d/wireless-regdom`

uncomment US

`echo 1 | sudo tee /proc/sys/net/ipv4/ip_forward`

`nmcli connection add type wifi ifname wlp4s0 con-name MyHotspot \
  802-11-wireless.ssid "APNAME" \
  802-11-wireless.mode ap \
  802-11-wireless.band a \
  802-11-wireless.channel 149 \
  802-11-wireless.channel-width 80 \
  802-11-wireless.powersave 2 \
  wifi-sec.key-mgmt wpa-psk \
  wifi-sec.psk "PASSWORD" \
  ipv4.method shared \
  ipv4.addresses 192.168.200.1/24`
  
