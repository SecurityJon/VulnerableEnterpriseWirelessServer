# Vulnerable Enterprise Wireless Server PoC
These are instructions for setting up a radius server on Kali Linux for serving wireless clients. This will appear on the surface to be configured fairly well (all clients will be using TLS mutual authentication for authentication) but the server will be left with a vulnerable radius version enabled (MD5) which permits phished credentials to be used against the Wifi as well, unknowingly.

You will need a Wireless Access Point that is capable of serving wireless that can back off to a radius server, and a Virtual Machine (I've  used Kali 2020.1) which has network connectivity to the rest of your network (to get DNS/DHCP/Routing).

# Installing software
We will install freeradius for this.

`sudo apt-get install freeradius freeradius-utils`

Move the eap file into the {install location}/mods-enabled directory, replacing the one already here

Move the radiusd.conf file into the {install location} directory

Move the clients.conf into the {install location} directory

Edit the {install location}/clients.conf file and change the "ipaddr = 172.16.10.8" at the top of the file to that of the IP address of your Access Point

# Creating Certificates

We'll need client and server certificates for TLS. 

Move the client.cnf into {install location}/certs directory
Move the ca.cnf into {install location}/certs directory
Move the server.cnf into {install location}/certs directory

Now make all of the certificates and keys
```
make ca
make server
make client
```

# Setting up the Clients

Copy {install location}/certs/ca.pem from the server onto the client (this contains public keys)
Copy {install location}/certs/client@testcorp.com.pem from the server onto the client (this contains private and public keys)

Move the two files from the {git location}/client_configs/ from git down to the client

Update the 'wpa_supplicant_tls.conf' on the client to point to the certificates moved there earlier

# Configuring the Access Point

Set up the Access Point to back off to a radius server. Set up as follows:

SSID = VulnerableWireless
SharedSecret = thisisasharedsecret
IPAddress = <IP address of radius server>

