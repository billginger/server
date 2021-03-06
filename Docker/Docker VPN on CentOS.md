# Docker VPN on CentOS

## Install Docker

Install required packages. yum-utils provides the yum-config-manager utility, and device-mapper-persistent-data and lvm2 are required by the devicemapper storage driver.

`yum install -y yum-utils device-mapper-persistent-data lvm2`

Use the following command to set up the stable repository. You always need the stable repository, even if you want to install builds from the edge or test repositories as well.

`yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo`

View installable version.

`yum list docker-ce --showduplicates | sort -r`

Install the latest version of docker.

`yum install docker-ce`

## Start Docker

`systemctl start docker`

Run `docker version` to check that you have the latest release installed.

## Pull Image

`docker pull hwdsl2/ipsec-vpn-server`

## Create env file

~/vpn.env

```r
# Define your own values for these variables
# - DO NOT put "" or '' around values, or add space around =
# - DO NOT use these special characters within values: \ " '
VPN_IPSEC_PSK=your_ipsec_pre_shared_key
VPN_USER=your_vpn_username
VPN_PASSWORD=your_vpn_password

# (Optional) Define additional VPN users
# - Usernames and passwords must be separated by spaces
# - All VPN users will share the same IPsec PSK
# - Uncomment and replace with your own values
# VPN_ADDL_USERS=additional_username_1 additional_username_2
# VPN_ADDL_PASSWORDS=additional_password_1 additional_password_2
```

For example:

```r
VPN_IPSEC_PSK=888888
VPN_USER=admin
VPN_PASSWORD=123456
VPN_ADDL_USERS=Jack Jones
VPN_ADDL_PASSWORDS=666666 777777
```

## Start VPN

**Important:** First, load the IPsec af_key kernel module on the Docker host:

`sudo modprobe af_key`

Create a new Docker container from this image (replace ./vpn.env with your own env file):

```r
docker run \
    --name vpn \
    --env-file ~/vpn.env \
    --restart=always \
    -p 500:500/udp \
    -p 4500:4500/udp \
    -v /lib/modules:/lib/modules:ro \
    -d --privileged \
    hwdsl2/ipsec-vpn-server
```

You can also save the above command as an alias:

```r
alias vpn='docker run --name vpn --env-file ~/vpn.env --restart=always -p 500:500/udp -p 4500:4500/udp -v /lib/modules:/lib/modules:ro -d --privileged hwdsl2/ipsec-vpn-server'
```

## Retrieve VPN login details

If you did not specify an env file in the docker run command above, VPN_USER will default to vpnuser and both VPN_IPSEC_PSK and VPN_PASSWORD will be randomly generated. To retrieve them, view the container logs:

`docker logs vpn`

Search for these lines in the output:

```r
Connect to your new VPN with these details:

Server IP: your_vpn_server_ip
IPsec PSK: your_ipsec_pre_shared_key
Username: your_vpn_username
Password: your_vpn_password
```

(Optional) Backup the generated VPN login details (if any) to the current directory:

`docker cp vpn:/opt/src/vpn-gen.env ./`

## Check server status

To check the status of your IPsec VPN server, you can pass ipsec status to your container like this:

`docker exec -it vpn ipsec status`

Or display current established VPN connections:

`docker exec -it vpn ipsec whack --trafficstatus`

## Exit VPN

`docker rm -f vpn`

## Next steps

Get your computer or device to use the VPN. Please refer to:

[Configure IPsec/L2TP VPN Clients](https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/clients.md)

[Configure IPsec/XAuth ("Cisco IPsec") VPN Clients](https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/clients-xauth.md)

If you get an error when trying to connect, see [Troubleshooting](https://github.com/hwdsl2/setup-ipsec-vpn/blob/master/docs/clients.md#troubleshooting).

Enjoy your very own VPN!
