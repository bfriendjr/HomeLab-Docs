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

`sudo dpkg-reconfigure openssh-server
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
<br>
<br>
<br>
<br>
<br>
#HomeLab/Kali