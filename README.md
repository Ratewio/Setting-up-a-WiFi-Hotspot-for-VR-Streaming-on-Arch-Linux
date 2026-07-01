# Setting-up-a-WiFi-Hotspot-for-VR-Streaming-on-Arch-Linux

`sudo pacman -S dnsmasq wireless-regdb`

`sudo nano /etc/conf.d/wireless-regdom`

uncomment US

Firewalld:
`sudo firewall-cmd --zone=nm-shared --add-interface=wlp4s0 --permanent
sudo firewall-cmd --zone=nm-shared --add-service=dhcp --permanent
sudo firewall-cmd --zone=nm-shared --add-service=dns --permanent`

UFW:
`sudo ufw allow in on wlp4s0 to any port 67 proto udp1
sudo ufw allow in on wlp4s0 to any port 53 proto udp`

`sudo sysctl net.ipv4.ip_forward=1`


`sudo iptables -t nat -A POSTROUTING -o Ваш_Интернет_Интерфейс -j MASQUERADE
sudo iptables -A FORWARD -m conntrack --ctstate RELATED,ESTABLISHED -j ACCEPT
sudo iptables -A FORWARD -i wlp4s0 -o Ваш_Интернет_Интерфейс -j ACCEPT`

`nmcli connection add type wifi ifname wlp4s0 con-name hotspot-5g ssid "archlinux" \
  802-11-wireless.mode ap \
  802-11-wireless.band a \
  802-11-wireless.channel 149 \
  802-11-wireless.channel-width 80 \
  802-11-wireless.powersave 2 \
  ipv4.method shared \
  ipv4.addresses 10.42.0.1/24 \
  wifi-sec.key-mgmt wpa-psk \
  wifi-sec.psk "meowmeow"`
  
