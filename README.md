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
aws lightsail open-instance-public-ports --port-info fromPort=27015,toPort=27015:27015,protocol=UDP --instance-name cs-vm
```

