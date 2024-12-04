# Backup

## Prerequisites

* Create a directory called `Backup` in your OneDrive, e.g., through the web-interface

## Sync

### rclone

Use the [rclone sync](https://rclone.org/commands/rclone_sync/) command to sync 
a local directory to OneDrive (only the remote will be modified).

The following command will sync the `/home/USER/Documents` directory with
`Backup/Documents` in the OneDrive configuration named `uow-onedrive`: 

```bash
rclone sync --dry-run --verbose \
  /home/USER/Documents \
  uow-onedrive:Backup/Documents 
```

**NB:** It is recommended to perform a dry-run first (` --dry-run --verbose`).
If necessary, you can [exclude files and dirs](#exclude-filesdirectories).


### rclone-browser

* refresh the available configurations on the **Remotes** tab
* double-click the remote for which you want to create a sync task
* go to the newly added tab for the remote
* browse to the folder into which you want to sync your local files 
  (or create it, if not yet present)
* then click on the **Upload** button
* enter a **Task description** (bottom of dialog) and click on **Save task**
* switch to the **Tasks** tab
* select the just saved task and click on **Edit**
* change **mode** to **Sync**
* if required, go to the **Exclude** tab and adapt the patterns (see [Exclude files/directories](#exclude-filesdirectories))  

Once you have the task saved, you can either perform a **Dry-run** to check
the files that got synced or an actual **Run**. A job will be launched under
the **Jobs** tab and you can view the output. If there is more text generated
than the output text box can hold, check out the section 
[Limited output in rclone-browser](Troubleshooting.md#limited-output-in-rclone-browser)
on the [Troubleshooting](Troubleshooting.md) page.


## Exclude files/directories

You can easily exclude files and directories, see the 
[Filtering, includes and excludes](https://rclone.org/filtering/) page for 
full details.

For `rclone` tool, you can use the `--exclude PATTERN` option and for
`rclone-browser`, edit a task that you have defined and go to the *Exclude* tab.

Here are some examples:

```
file.jpg   - matches "file.jpg"
           - matches "directory/file.jpg"
           - doesn't match "afile.jpg"
           - doesn't match "directory/afile.jpg"
/file.jpg  - matches "file.jpg" in the root directory of the remote
           - doesn't match "afile.jpg"
           - doesn't match "directory/file.jpg"
```

For excluding directories, you can do the following:

```
dir1/**       - excludes the contents of dir1 anywhere
/dir1/**      - excludes the contents of dir1 in the root directory of the remote
/dir/subdir/  - excludes /dir/subdir/ 
```

## Links

* [rclone filtering](https://rclone.org/filtering/)
* [rclone sync](https://rclone.org/commands/rclone_sync/)
