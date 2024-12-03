# Configuration

The instructions below are based on [this tutorial](https://research.reading.ac.uk/act/knowledgebase/rclone-sync/)
from the University of Reading.

This is a one-time process for each cloud service that you want to sync with.


## Prerequisites

Make Chromium/Chrome the default browser (I couldn't get it to work with Firefox/Floorp), used for OAuth further down.


## Configuration

Run the following command in the terminal to start the configuration process:

```bash
rclone config
```

```
No remotes found, make a new one?
n) New remote
s) Set configuration password
q) Quit config
n/s/q> 
```

No remote environments exist, so we select `n` and then enter our name for the cloud service.
Since we are setting up a connection with a University of Waikato OneDrive account, we will call it `uow-onedrive`: 

```
n/s/q> n
Enter name for new remote.
name> uow-onedrive
```

From the available list of **storage** options, choose **Microsoft OneDrive/onedrive**. In the
output below, this is **30** (this may change as the tool evolves):

```
Option Storage.
Type of storage to configure.
Choose a number from below, or type in your own value.
 1 / 1Fichier
   \ (fichier)
...
30 / Microsoft OneDrive
   \ (onedrive)
...
46 / seafile
   \ (seafile)
Storage> 30
```

Proceed, leaving **client_id** and **client_secret** empty:  

```
Option client_id.
OAuth Client Id.
Leave blank normally.
Enter a value. Press Enter to leave empty.
client_id>

Option client_secret.
OAuth Client Secret.
Leave blank normally.
Enter a value. Press Enter to leave empty.
client_secret>
```

Then, choose **Microsoft Cloud Global** as the **region** (at the time of writing):

```
Option region.
Choose national cloud region for OneDrive.
Choose a number from below, or type in your own string value.
Press Enter for the default (global).
 1 / Microsoft Cloud Global
   \ (global)
 2 / Microsoft Cloud for US Government
   \ (us)
 3 / Microsoft Cloud Germany
   \ (de)
 4 / Azure and Office 365 operated by Vnet Group in China
   \ (cn)
region> 1
```

Decline editing the **advanced configuration**:

```
Edit advanced config?
y) Yes
n) No (default)
y/n> n
```

Continue with using **auto config** and check your browser whether it succeeded 
(the `rclone` application has been approved by the UoW M365 admins already):

```
Use auto config?
 * Say Y if not sure
 * Say N if you are working on a remote or headless machine

y) Yes (default)
n) No
y/n> y

2024/12/03 16:40:04 NOTICE: If your browser doesn't open automatically go to the following link: http://127.0.0.1:53682/auth?state=SOMERANDOMSTUFF
2024/12/03 16:40:04 NOTICE: Log in and authorize rclone for access
2024/12/03 16:40:04 NOTICE: Waiting for code...
2024/12/03 16:40:07 NOTICE: Got code
```

When prompted for **config type**, select **OneDrive Personal or Business/onedrive**:  

```
Option config_type.
Type of connection
Choose a number from below, or type in an existing string value.
Press Enter for the default (onedrive).
 1 / OneDrive Personal or Business
   \ (onedrive)
 2 / Root Sharepoint site
   \ (sharepoint)
   / Sharepoint site name or URL
 3 | E.g. mysite or https://contoso.sharepoint.com/sites/mysite
   \ (url)
 4 / Search for a Sharepoint site
   \ (search)
 5 / Type in driveID (advanced)
   \ (driveid)
 6 / Type in SiteID (advanced)
   \ (siteid)
   / Sharepoint server-relative path (advanced)
 7 | E.g. /teams/hr
   \ (path)
config_type> 1
```

As for the **drive ID**, select **OneDrive (business)**:  

```
Option config_driveid.
Select drive you want to use
Choose a number from below, or type in your own string value.
Press Enter for the default (...).
 1 / OneDrive (business)
   \ (...)
 2 / Preservation Hold Library (business)
   \ (...)
 3 / PersonalCacheLibrary (business)
   \ (...)
config_driveid> 1
```

You will be asked to confirm that the drive that `rclone` found is the correct one. It should contain
`waikatouniversitynz-my` and your name in the URL:

```
Drive OK?

Found drive "root" of type "business"
URL: https://waikatouniversitynz-my.sharepoint.com/personal/...

y) Yes (default)
n) No
y/n> y
```

With that in place, you will get a lot of output including the type, token and drive information. 
Answer `y` to the question to keep the `uow-onedrive` remote to make it persistent: 

```
Configuration complete.
Options:
- type: onedrive
- token: {...}
- drive_id: ...
- drive_type: business
Keep this "uow-onedrive" remote?
y) Yes this is OK (default)
e) Edit this remote
d) Delete this remote
y/e/d> y
```

`rclone` will then list all your configured cloud connections.

```
Current remotes:

Name                 Type
====                 ====
uow-onedrive         onedrive
```

Now you can select `q` to exit the setup process:

```
e) Edit existing remote
n) New remote
d) Delete remote
r) Rename remote
c) Copy remote
s) Set configuration password
q) Quit config
e/n/d/r/c/s/q> q
```
