# Backup CLI Example

Run the following commands to experiment with Backup CLI:

```bash
# Clone repository 
git clone https://github.com/vanegmondgroep/backup-cli.git

# Navigate to the example directory
cd backup-cli/example

# Install composer packages
composer install

# Start Docker containers
docker compose up -d

# Backup MySQL service
vendor/bin/bcli backup mysql

# List MySQL backups
vendor/bin/bcli snapshots mysql 

# Restore MySQL backup
vendor/bin/bcli restore mysql <snapshot-id>

# Backup Node-RED service
vendor/bin/bcli backup node-red

# List Node-RED backups 
vendor/bin/bcli snapshots node-red 

# Restore Node-RED backup
vendor/bin/bcli restore node-red <snapshot-id>
```
