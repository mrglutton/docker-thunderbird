# This is unchanged eccept for the VNC password fix for Synology.



# Thunderbird in Docker optimized for Unraid
This container will download and install Thunderbird in the preferred version and language.

>**UPDATE:** The container will check on every restart if there is a newer version available.

>**ATTENTION:** If you want to change the language, you have to delete every file in the 'thunderbird' directory except the 'profile' folder.

RESOLUTION: You can also change the resolution from the WebGUI, to do that simply click on 'Show more settings...' (on a resolution change it can occour that the screen is not filled entirely with the Thunderbird window, simply restart the container and it will be fullscreen again).

## Env params
| Name | Value | Example |
| --- | --- | --- |
| DATA_DIR | Folder for Thunderbird | /thunderbird |
| THUNDERBIRD_V | Enter your preferred Thunderbird version or 'latest' to install the latest version | latest |
| THUNDERBIRD_LANG | Enter your preferred Thunderbird language you can get a full list here: https://archive.mozilla.org/pub/thunderbird/releases/latest/README.txt | en-US |
| CUSTOM_RES_W | Enter your preferred screen width | 1280 |
| CUSTOM_RES_H | Enter your preferred screen height | 768 |
| UID | User Identifier | 99 |
| GID | Group Identifier | 100 |
| UMASK | Umask value | 000 |
| DATA_PERM | Data permissions for /thunderbird folder | 770 |

## Run example
```
docker run --name Thunderbird -d \
	-p 8080:8080 \
	--env 'THUNDERBIRD_V=latest' \
	--env 'THUNDERBIRD_LANG=en-US' \
	--env 'TURBOVNC_PARAMS=-securitytypes none' \
	--env 'CUSTOM_RES_W=1280' \
	--env 'CUSTOM_RES_H=768' \
	--env 'UID=99' \
	--env 'GID=100' \
	--env 'UMASK=000' \
	--env 'DATA_PERM=770' \
	--volume /mnt/cache/appdata/thunderbird:/thunderbird \
	ich777/thunderbird
```
### Webgui address: http://[SERVERIP]:[PORT]/vnc.html?autoconnect=true

## Set VNC Password:
 Please be sure to create the password first inside the container, to do that open up a console from the container (Unraid: In the Docker tab click on the container icon and on 'Console' then type in the following):

1) **su $USER**
2) **vncpasswd**
3) **ENTER YOUR PASSWORD TWO TIMES AND PRESS ENTER AND SAY NO WHEN IT ASKS FOR VIEW ACCESS**

Unraid: close the console, edit the template and create a variable with the `Key`: `TURBOVNC_PARAMS` and leave the `Value` empty, click `Add` and `Apply`.

All other platforms running Docker: create a environment variable `TURBOVNC_PARAMS` that is empty or simply leave it empty:
```
    --env 'TURBOVNC_PARAMS='
```

This Docker was mainly edited for better use with Unraid, if you don't use Unraid you should definitely try it!

#### Support Thread: https://forums.unraid.net/topic/83786-support-ich777-application-dockers/

#### SYNOLOGY:

In Edit, Advanced Settings "TURBOVNC_PARAMS" due to resriction in new docker can not be left empty. Enter the value "-securitytypes VNC" and the password will work, but you have to set it in terminal before. Visual guide is here: https://www.youtube.com/watch?v=995uUSleHsg

More info is here: https://forums.unraid.net/topic/83786-support-ich777-application-dockers/page/87/

And when you are at it, go here and set the other stuff: https://www.reddit.com/r/synology/comments/uwnj97/using_your_synology_to_backup_your_imap_mail/

In the config editor set the setting mail.server.default.check_all_folders_for_new to true.

