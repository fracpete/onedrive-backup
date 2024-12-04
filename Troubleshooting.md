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
