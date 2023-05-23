# Backup CLI

An extendable command-line interface for backing up and restoring data using [Restic](https://restic.net).

## Install

Before installing Backup CLI, please make sure your environment meets the minimum requirements:

* [Ubuntu 20.04 / 22.04](https://ubuntu.com/)
* [Restic](https://restic.net)

Once you’ve verified the requirements, download and install Backup CLI using the following commands:

```bash
# Download Backup CLI
curl -O https://raw.githubusercontent.com/vanegmondgroep/backup-cli/main/bcli 

# Make the file executable
chmod +x ./bcli 

# Move it to somewhere in your PATH
sudo mv ./bcli /usr/local/bin/bcli
```

Run the above commands again to update Backup CLI.

## Commands

```bash
# Backup a service
bcli backup <service>

# Display service snapshots
bcli snapshots <service>

# Restore a service
bcli restore <service> <snapshot-id>

# Display backup logs
bcli logs <service>
```

## Configuration

Backup CLI loads environment variables from a `.env` file within the current working directory. The following variables
are available:

| Variable                   | Default                 |
|----------------------------|-------------------------|
| `BACKUP_PASSWORD`          | `supersecret`           |
| `BACKUP_LOGS_PATH`         | `./backup/logs`         | 
| `BACKUP_HOOKS_PATH`        | `./backup/hooks`        |
| `BACKUP_REPOSITORIES_PATH` | `./backup/repositories` |
| `<service>_BACKUP_PATH`**  | -                       | 
| `BACKUP_KEEP_LAST`         | 5                       | 
| `BACKUP_KEEP_DAILY`        | 31                      | 
| `BACKUP_KEEP_MONTHLY`      | 12                      | 
| `BACKUP_KEEP_YEARLY`       | 1                       | 

** This defines a service path you would like to back up (e.g. `MYSQL_BACKUP_PATH`).

## Hooks

Backup CLI calls scripts (hooks) before and after a backup or restore. This allows you to perform an action, such as
exporting a database before a backup is made. The following hooks are available:

| Hook                                             | Description              |
|--------------------------------------------------|--------------------------|
| `$BACKUP_HOOKS_PATH/<service>_pre_backup_hook`   | Invoked before a backup  |
| `$BACKUP_HOOKS_PATH/<service>_post_backup_hook`  | Invoked after a backup   | 
| `$BACKUP_HOOKS_PATH/<service>_pre_restore_hook`  | Invoked before a restore |
| `$BACKUP_HOOKS_PATH/<service>_post_restore_hook` | Invoked after a restore  | 

## Logs

Logs are written to `$BACKUP_LOGS_PATH/<service>.log`.

## Example

The [example configuration](./example) shows how you can back up / restore a MySQL and Node-RED container.

## Cronjobs

To schedule a backup, add the following line to your crontab:

```crontab
# Run MySQL backup every day at 01:00
0 1 * * * cd <project-dir> && /usr/local/bin/bcli backup mysql

# Run Node-RED backup every day at 02:00
0 2 * * * cd <project-dir> && /usr/local/bin/bcli backup node-red
```
