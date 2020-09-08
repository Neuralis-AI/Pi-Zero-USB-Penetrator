# Pi-Zero-USB-Penetrator
Project repository for creating a USB "tool" to perform automated penetrationtesting on default/insecure linux servers.
    
Short explanation:    
The way this works is by attaching a Pi Zero W as an "ethernet device" via USB, but with a DHCP server configured so the computer actually connects to us.
The pc/server conencts to us and we can remotely attack the server via the Pi.
    
Long explanation:    
By attaching the Pi Zero W directly to the server it's possible to directly attack the pc/server without having a presence on the internal network.
Paired with a 3g/4g card the results can be sent to the cloud or via internal wifi to a nearby preconfigured access point.
Since we're achting as a DHCP server we can decide which IP the server gets, which gets interesting as applications like fail2ban are usually configured to whitelist IP based instead of ethernet interface based.
    
Ideally the device will be remote operable after plugging it in, be it via services like ngrok or other similar services.

    
All parts and assembly video here:
    
    
TODO:    
Auto ip/pool switcher after each N tries    
Use same IP as main connection to circumvent fail2ban?    
    
Let me know any ideas or changes you want to see added to the project.
