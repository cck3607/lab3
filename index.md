## Cloud VPN Docker Project

## Step 1. Open terminal with docker already installed and enter the code below. 
```markdown
mkdir -p ~/wireguard/
mkdir -p ~/wireguard/config/
nano ~/wireguard/docker-compose.yml
```
### Step 2. Now you should be in the nano edit for docker-compose.yml copy and past the contents below into the file. Once done press control x to save and exit.

```markdown
version: '3.3'
services:
  wireguard:
    container_name: wireguard
    image: linuxserver/wireguard
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Asia/Hong_Kong
      - SERVERURL=1.2.3.4
      - SERVERPORT=51820
      - PEERS=pc1,pc2,phone1
      - PEERDNS=auto
      - INTERNAL_SUBNET=10.0.0.0
    ports:
      - 51820:51820/udp
    volumes:
      - type: bind
        source: ./config/
        target: /config/
      - type: bind
        source: /lib/modules
        target: /lib/modules
    restart: always
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    sysctls:
      - net.ipv4.conf.all.src_valid_mark=1
```
## Step 3. Start wireguard by running the commands below. 
```markdown
sudo cd ~/wireguard/
sudo docker-compose up -d
```
## Step 4. Connect wireguard to your phone by running the command below and scanning the qr code when it appears.
```markdown
sudo docker-compose logs -f wireguard
```
## Step 5. Open wireguard on your phone and turn on the VPN.
## Step 6. Open files on your VM, and click the wireguard folder. Inside copy the config file to your laptop.
## Step 7. Search the link below without your VPN turned on.
```markdown
https://ipleak.net/
```
## Step 8. In a new tab search the same link above with the VPN now turned on in wireguard.
## Step 9. Screen shot both IPs running, should have different locations for both.
