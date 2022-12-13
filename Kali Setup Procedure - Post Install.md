# Kali Setup Procedure - Post Install


### Change Root Password:

`sudo -I passwd root`
<br>
<br>
<br>

### Create new SSH Keys:


:: Change to dir where ssh keys are located

```powershell
cd /etc/ssh
```

:: Make folder to backup original ssh keys.

```powershell
sudo mkdir old_keys
```

:: Move original ssh keys to the backup location.

```powershell
sudo mv ssh_host_* old_keys
```

:: Verify that the original ssh keys have been relocated.

```powershell
ls
```

:: Create new ssh keys.

```powershell
sudo dpkg-reconfigure openssh-server
```


:: Verify that the new ssh keys have been created.

```powershell
ls
```

:: Confirm that the new ssh keys have a different md5 hash from the originals

```powershell
sudo md5sum ssh_host_*
sudo md5sum /etc/ssh/old_keys/ssh_host_*
```

:: Remove old ssh keys.

```powershell
sudo rm -r old_keys
```

:: Confirm the “old_keys” directory is gone

```powershell
ls
```
<br>
<br>
<br>

### Install: OpenVas Scanner


:: Installation

```powershell
sudo apt-get install openvas
```
<br/><br/>

:: On a fresh install, note the password displayed at the end of the setup. You will need it to connect you to the Web UI GSA (greenbone-security-assistant)

```powershell
sudo gvm-setup
```
<br/><br/>

:: To update the data (CERT, SCAP, GVMD_DATA) from the feed server and to update the OpenVAS NVTs from Community Feed

```powershell
sudo gvm-feed-update
```
<br/><br/>

:: It will check the setup and start the all the required services if everything is OK. You can now open your browser on https://127.0.0.1:9392 and use GVM.

```powershell
sudo gvm-check-setup
```
<br/><br/>

:: Reset the admin password

```powershell
sudo -u _gvm gvmd —user=admin —new-password=<AdminPassword>
```
<br/><br/>

:: To create a new gvm system user

```powershell
sudo runuser -u _gvm — gvmd —create-user=<UserName> —password=<UserPassword>
```
<br/><br/>

:: Create a new user with Admin role permissions.

```powershell
sudo gvmd —create-user=<UserName> —password=<UserPassword> —role=Admin
```
```powershell
sudo gvmd —inheritor=<UserName>
```
<br/><br/>

:: Deleted admin Account

```powershell
sudo gvmd —delete-user=admin
```
<br/><br/>

:: Reset the user password

```powershell
sudo runuser -u _gvm — gvmd —create-user=<UserName> —new-password=<UserPassword>
```
<br/><br/>

:: To start the GVM services, use:

```powershell
sudo gvm-start
```
<br/><br/>

:: To stop the GVM services, use:

```powershell
sudo gvm-stop
```
<br/><br/>

:: GVM Versions Info

```powershell
gvmd —version
```
<br/><br/>

:: Access GVM Web Interface

URL: https://127.0.0.1:9392
<br/><br/><br/>
:: Remove GVM

```powershell
sudo apt autoremove openvas*
```
```powershell
sudo apt-get remove --purge openvas*
```
```powershell
sudo apt-get remove --purge openvas9*
```
```powershell
sudo apt-get remove --purge openvas*
```
```powershell
sudo apt-get remove --purge libopenvas9
```
```powershell
sudo apt-get remove --purge libopenvas9-dev
```
```powershell
sudo apt autoremove
```
```powershell
sudo rm -rf /var/lib/openvas/
```
```powershell
sudo rm -rf /var/log/gvm/
```
```powershell
sudo rm -rf /var/lib/gvm/
```









<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
#HomeLab/Kali