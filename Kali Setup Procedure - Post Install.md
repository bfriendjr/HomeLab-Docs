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


:: On a fresh install, note the password displayed at the end of the setup. You will need it to connect you to the Web UI GSA (greenbone-security-assistant)

```powershell
sudo gvm-setup
```



:: To update the data (CERT, SCAP, GVMD_DATA) from the feed server and to update the OpenVAS NVTs from Community Feed

```powershell
sudo gvm-feed-update
```


:: It will check the setup and start the all the required services if everything is OK. You can now open your browser on https://127.0.0.1:9392 and use GVM.

```powershell
sudo gvm-check-setup
```


:: To create a new gvm system user
```powershell
sudo runuser -u _gvm — gvmd —create-user=ironman —password=ICanFly2
```


:: Create a new user with Admin role permissions.
```powershell
sudo gvmd —create-user= ironman —password=ICanFly2 —role=Admin
sudo gvmd —inheritor= ironman
gvmd —delete-user=admin
```


:: To reset the admin password
```powershell
sudo -u _gvm gvmd —user=admin —new-password=<AdminPassword>
```

:: To reset the user password
```powershell
sudo runuser -u _gvm — gvmd —create-user=<UserName> —new-password=<UserPassword>
```


:: To start the GVM services, use:

```
sudo gvm-start
```


:: To stop the GVM services, use:

```powershell
sudo gvm-stop
```


:: GVM Versions Info

```powershell
gvmd —version
```

:: Access GVM Web Interface
URL: https://127.0.0.1:9392

:: Remove GVM
```powershell
sudo apt autoremove openvas*
```
```powershell
sudo apt-get purge openvas*
```
```powershell
sudo apt-get purge openvas9*
```
```powershell
sudo apt-get purge openvas*
```
```powershell
sudo apt-get purge libopenvas9
```
```powershell
sudo apt-get purge libopenvas9-dev
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