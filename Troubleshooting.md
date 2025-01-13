# Troubleshooting

## Limited output in rclone-browser

The text box with the output of the rclone command has only a very small
number of lines that are kept, which is impractical for dry-run tests 
of large directories. To get the full output, do the following:

* on the **Tasks** tab execute a **Dry-run**
* go to the **Jobs** tab and click on the icon next to the X icon for copying
  the command to the clipboard
* open a terminal and paste the command in there
* append ` &> log.txt`
* execute the command and wait for it to finish
* open `log.txt` in a text editor and use it to adjust your exclude patterns


## Web interface fails to delete folders recursively

The OneDrive web interface is a terrible piece of software (neither automatic 
refreshes nor an explicit refresh button available) and deleting
folders is something that is not only extremely slow, it also seldom succeeds.

Instead, use the [rclone delete](https://rclone.org/commands/rclone_delete/) 
command in the terminal to delete a whole directory tree. The following 
command-line removes the directory `Backup/Documents/shouldntbethere` recursively 
for the remote configuration called `uow-onedrive`:

```bash
rclone delete --rmdirs uow-onedrive:Backup/Documents/shouldntbethere
```

Once finished, manually delete the empty `Backup/Documents/shouldntbethere`
through OneDrive web interface (for some reason, rclone does not delete that
directory).

**NB:** It is recommended to perform a dry-run (`--dry-run`) first or 
perform it interactively (`--interactive`), there is absolutely 
**no** going back!


## Slow transfers

Apart from having bandwidth limitations (have you set limits on your transfer rates?)
having a lot of little files, can result in transfers taking a long time, 
unfortunately. Especially build environments with lots of temporary files
that change a lot, can lead to long sync times. Since this files can be 
regenerated at any time, they should not be synced to avoid wasting space. 

In such a case, to speed things up, try optimizing the [exclude patterns](Backup.md#exclude-filesdirectories). 
See section [Limited output in rclone-browser](#limited-output-in-rclone-browser)
for how to redirect output of commands in `-n/--dry-run` mode for further
investigation.

Also, you can increase the number of parallel transfers to speed up the 
transfer. At the time of writing the default was 4, so you could increase that
to 8 or 16. Please note that this may gobble up more bandwidth when transferring
large files, so a bandwidth limit is recommended.

## Symlinks

Add the `--links` option on the `Extra options` tab in the rclone-browser. This will
sync them with the `.rclonelink` extension and resolve back again when going the other
direction. See discussion [here](https://forum.rclone.org/t/cant-follow-symlink-without-l-copy-links/20650).

## error: pathIsTooLong: Path is too long

If you get this error, then you have run into an incompatibility between your local file system and OneDrive.
In other words, you can have longer file names locally than in OneDrive. Unfortunately, there is no solution
or workaround. There are only the following options:

* ignore the error and accept that some dirs/files don't get transferred
* identify the dirs/files and shorten any long (you may need to [enable logging](./Backup.md#logging))

See also the article on OneDrive/SharePoint regarding [file name and path lengths](https://support.microsoft.com/en-us/office/restrictions-and-limitations-in-onedrive-and-sharepoint-64883a5d-228e-48f5-b3d2-eb39e07630fa#filenamepathlengths).
