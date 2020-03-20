# lightsail-cs16
HLDS Counter Strike 1.6 Server

## Create instance
Create AWS Lightsail instance via [AWS Lightsail CLI](https://docs.aws.amazon.com/cli/latest/reference/lightsail/index.html "AWS Lightsail CLI")
```
aws lightsail create-instances --instance-names "cs-vm" --availability-zone eu-west-2a --blueprint-id centos_7_1901_01 --bundle-id medium_2_0 --user-data file://user-data.txt
```
You can find the script in `/var/lib/cloud/instance/user-data.txt` on the instance

## Configure instance
### Open ports
```
aws lightsail open-instance-public-ports --port-info fromPort=27015,toPort=27015,protocol=TCP --instance-name cs-vm
aws lightsail open-instance-public-ports --port-info fromPort=27015,toPort=27015,protocol=UDP --instance-name cs-vm
```

### Assign static IP (optional)
Static IP addresses are free only while attached to an instance. You can manage five at no additional cost.
```
aws lightsail allocate-static-ip --static-ip-name cs-vm-static-ip
aws lightsail attach-static-ip --static-ip-name cs-vm-static-ip --instance-name cs-vm
```

### SSH
Download the key file [here](https://lightsail.aws.amazon.com/ls/webapp/account/keys "AWS Lightsail keys")
```
chmod 600 LightsailDefaultKey-eu-west-2.pem 
```
Obtain the public IP
```
aws lightsail get-static-ip --static-ip-name cs-vm-static-ip | grep ipAddress
```
Login to your instance
```
ssh -i LightsailDefaultKey-eu-central-1.pem  centos@PUBLIC_IP
```
View instances [here](https://lightsail.aws.amazon.com/ls/webapp/home/instances "View instances")

### Counter-Strik srever
Login with RCON privileges on your server:
1. Press the ~ key once your game loads up
2. In the dialog box that comes up type in ```rcon_password password```
3. You are now logged into your server with rcon privileges

Sample RCON Commands
*Changing the map : ```rcon changelevel de_dust```
*Kick a user : type ```rcon users``` to get IDs and then type ```rcon kick [userid]```

