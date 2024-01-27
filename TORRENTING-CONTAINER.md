# Guide to setup a container for torrenting

Follow the guide to create a container

## Setting up permissions
```
addgroup --gid 1000 container-data
usermod -aG container-data root
aduser --system --group qbittorrent-nox
usermod -aG container-data qbittorrent-nox
```
## Setup qbittorrent

- ```apt update & apt upgrade -y```
- ```addgroup --```
- ```apt install qbittorrent-nox```


## Setup flood
```
apt install nodejs
npm install --global flood
```


## Optional but recommanded: enable a systemctl service
- copy the content of 
    ```
    [Unit]
    Description=qBittorrent Command Line Client
    After=network.target
    
    [Service]
    #Do not change to "simple"
    Type=forking
    User=qbittorrent-nox
    Group=qbittorrent-nox
    UMask=007
    ExecStart=/usr/bin/qbittorrent-nox -d --webui-port=8080
    Restart=on-failure
    
    [Install]
    WantedBy=multi-user.target
    ```
  to `/etc/systemd/system/qbittorrent-nox.service`
- ```systemctl enable qbittorrent-nox.service```
- ```journalctl status qbittorrent-nox.service```
- copy 
    ```
    [Unit]
    Description=Flood service for user qbittorrent-nox
    After=network.target
    
    [Service]
    User=qbittorrent-nox
    Group=qbittorrent-nox
    Type=simple
    KillMode=process
    ExecStart=/usr/bin/env flood --host="0.0.0.0" --baseuri="/" --p>
    Restart=on-failure
    RestartSec=3
    
    [Install]
    WantedBy=multi-user.target
    ```

## Optional: Installing a vpn
- `apt install openvpn openresolv`

### 


### Verification
