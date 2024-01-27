# Syncing dropbox

## Use case

# temp code
```
sudo sed -i -re 's/([a-z]{2}\.)?archive.ubuntu.com|security.ubuntu.com/old-releases.ubuntu.com/g' /etc/apt/sources.list
sudo apt-get update && sudo apt-get dist-upgrade
sudo apt-get install ubuntu-release-upgrader-core
sudo do-release-upgrade
```
