# Backup CLI Example

Run the following commands to experiment with Backup CLI:

```bash
# Clone repository 
git clone https://github.com/vanegmondgroep/backup-cli.git

# Navigate to the example directory
cd backup-cli/example

# Start Docker containers
docker compose up -d

# Backup MySQL service
../bcli backup mysql

# List MySQL backups
../bcli snapshots mysql 

# Restore MySQL backup
../bcli restore mysql <snapshot-id>

# Backup Node-RED service
../bcli backup node-red

# List Node-RED backups 
../bcli snapshots node-red 

# Restore Node-RED backup
../bcli restore node-red <snapshot-id>
```
