# Pi-Zero-USB-Penetrator
Project repository for creating a USB "tool" to perform automated penetrationtesting on default/insecure linux servers.  
  
## Short explanation:  
The way this works is by attaching a Pi Zero W as an "ethernet device" via USB, but with a DHCP server configured so the computer actually connects to us.  
The pc/server conencts to us and we can remotely attack the server via the Pi.  
  
## Long explanation:  
By attaching the Pi Zero W directly to the server it's possible to directly attack the pc/server without having a presence on the internal network.  
Paired with a 3g/4g card the results can be sent to the cloud or via internal wifi to a nearby preconfigured access point.  
Since we're achting as a DHCP server we can decide which IP the server gets, which gets interesting as applications like fail2ban are usually configured to whitelist IP based instead of ethernet interface based.  
  
Ideally the device will be remote operable after plugging it in, be it via services like ngrok or other similar services.  
  
  
## All parts and assembly video here:
  
  
  
## Instructions:  
First you need to do a base setup of a raspberry pi zero. I used Raspbian lite but this can be any OS (though Debian based makes it easier to follow along)  
I connected the Pi to my wifi via raspi-config and ssh'd to the Pi with the default credentials pi/raspberry  
apt-get install isc-dhcp-server //DHCP server  
sudo nano /etc/dhcpcd.conf //edit the DHCP server settings  
Put the following code under # Example static IP configuration  
```bash
interface usb0  
static ip_address=10.0.0.1/24  
```
sudo nano /etc/dhcp/dhcpd.conf  
Edit the bottom of the file to look like this:  
```bash
# Configuration file for DHCP server on Rasberry Pi  
#  
option domain-name "example";  
option domain-name-servers 8.8.8.8;  
default-lease-time 3600;  
max-lease-time 86400;  
  
# Configure service for local network 192.168.47.0 (the wireless AP)
subnet 10.0.0.0  netmask 255.255.255.0 {  
    range 10.0.0.50 10.0.0.250;  
    option routers 10.0.0.1;  
}  
##  
```
  
systemctl daemon-reload  
sudo systemctl restart dhcpcd.service  
  
You now have a usb ethernet adapter with working DHCP server.  
  
## TODO:  
Auto ip/pool switcher after each N tries  
Use same IP as main connection to circumvent fail2ban?  
Variable port and other cmd options.  
  
Let me know any ideas or changes you want to see added to the project.  
