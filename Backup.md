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
* on the **Transfer** tab, you can limit the **Bandwidth**; that way you can 
  avoid interfering with work too much when running this task during work hours

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

## Automation

### rclone

**rclone** commands can be easily added to shell scripts and then executed
via [cronjobs](https://linuxconfig.org/using-cron-scheduler-on-linux-systems) 
or [systemd services with timers](https://linuxconfig.org/how-to-schedule-tasks-with-systemd-timers-in-linux).


### rclone-browser

When using the newer **rclone-browser** from [Mercenar](https://github.com/Mercenar/RcloneBrowser),
then tasks can be easily scheduled in the GUI:

* select the **Tasks** tab
* right-click on the task that you want to schedule and select 
  **Add to the scheduler**
* on the daily schedule, select the days that you want backups to happen 
  (typically Mon to Fri) and select the time (e.g., 12:00 or 17:00)
* as **execution mode** select **add to the queue** if you have more than one
  task to schedule, executing them sequentially
* once in the scheduler, activate the task by clicking on the *run* button to show *Active* rather than *Paused*


## Logging

By default, rclone does not log anything, you need to specify that explictly. That can be done either via the `--log-file=FILE` or `--sys-log` option.
When using `--log-file=FILE`, create a directory where you want to store the log files.

### rclone

Simply add the relevant option to your `rclone` command.

### rclone-browser

* select the **Tasks** tab
* **edit** the task to which you want to add logging
* select the **Extra options** tab
* enter the relevant option
* save the task

**NB:** using the logging flags will redirect **all** output and the UI will look like nothing is happening.

## Links

* [rclone filtering](https://rclone.org/filtering/)
* [rclone sync](https://rclone.org/commands/rclone_sync/)
* [rclone logging](https://rclone.org/docs/#logging)
