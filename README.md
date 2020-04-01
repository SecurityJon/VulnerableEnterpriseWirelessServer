# Vulnerable Enterprise Wireless Server
These are instructions for setting up a radius server on Kali Linux for serving wireless clients. This will appear on the surface to be configured fairly well (all clients will be using TLS mutual authentication for authentication) but the server will be left with a vulnerable radius version enabled (MD5) which permits phished credentials to be used against the Wifi as well, unknowingly.

# Installing software
We will install freeradius for this.

`sudo apt-get install freeradius freeradius-utils`




nano /etc/freeradius/3.0/radiusd.conf 


nano /etc/freeradius/3.0/mods-enabled/eap
