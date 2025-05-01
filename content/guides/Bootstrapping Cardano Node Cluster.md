---
tags:
  - guides
  - mochi
  - sop
date: 2025-04-30
draft: 'false'
title: 'Bootstrapping Cardano Node Cluster'
toc: 'true'
---

# Cloning/Provisioning of VM
1. Clone template
	1. Set unique vm id and name
	2. Change mode from linked to full clone
2. Hardware
	1. Edit memory to `3720 MiB` (30 GiB)
	2. Change processors to 4 cores
	3. Resize harddisk to 398 GiB
	4. Include vlan on the network device (for dango vlan tag 90)
3. Cloud-Init
	1. User: mochi
	2. Set password
	3. Set ip config to static ipv4 value
	4. Set gateway correctly
4. Options
	1. Set shutdown order
	2. Set qemu agent to enabled
	3. Enable protection (make this the last last step after configuring everything)
# VM Configuration

## Preconfiguration 
1. Log in
2. Install `qemu-guest-agent`
3. Install `chrony`
4. Edit the cloud init host file in `/etc/cloud/templates/hosts.debian.tmpl`
	1. add `192.167.8.100 ca-teleport.mochipool.com`
5. Do a system reboot
6. Enroll the resource into teleport
7. Log back in

## Guild Operators Download and Configuration
1. Download cnode from intersect
2. Download cardano-cli seperately since the one packaged with cnode may be outdated.
3. Download Guild Operators SPO Scripts
	- Provision guild scripts with parameters: `pdlcowm`
4. Configure Guild Operators ENV file
	- In the Relay, set `CNODE_PORT=4001`
	- `MITHRIL_DOWNLOAD=Y` (only if provisioning from scratch)

## Provisioning Guild Scripts

### Producer Setup
1. Go into script directory and edit env file
	1. Change cnode port to 4001
	2. Set pool name: `mochi`
	3. Mithril download: Y
	4. mithril signer enable: Y
	5. For cncli to work, we must also include the BECH32 pool ID as a manual entry in the `cncli.sh` script. For Mochi, this is `POOL_ID_BECH32="pool1ferfwtmcjm9rxc00ugtdwrm9m042jf4xjvse6a8u5smxqt0pwnx"`
2. Edit the submitapi.sh file (in the relay only)
	1. Change `HOST_ADDR=0.0.0.0`
3. Edit cncli.sh file
	2. Get pool tool API key from pool tool
	3. Change pool tool: `PT_API` key:
	4. Change pool ticker to `MOCHI`
4. Issue the deploy at systemd shell scripts
	1. Cardano node: Y
	2. Cardano submit api: Y
	3. Mithril signer: Y
	4. Set mithril signer relay ip to cardano node ip
	5. Ogmios: Y
	6. Topology updater: N
	7. Cncli: Y
	8. Pool tool send slots: Y
	9. Pool tool send tip: Y
	10. Log monitor: Y
	11. Block perf: N
5. Rename Pool files
	1. mochi.vrf.skey -> vrf.skey
	2. mochi.vrf.vkey -> vrf.vkey
	3. mochi.kes-xxxxx.skey -> hot.skey
	4. mochi-kes-xxxx.vkey -> hot.vkey
	5. mochi.pool.id -> pool.id
	6. mochi.node-xxx.opt.cert -> opt.cert
	
	*Note: Remove group and other permissions from signing keys*
6. Copy the files
	1. Create directory priv/mochi
	2. Decrypt the keys
	3. Use teleport to copy the files securely into the priv/mochi onthe producer
7. Remove the priv files from the local computer
8. Edit topology file
	1. Edit local roots
	2. Keep P2P enabled
	3. For the producer: delete local roots which are not trusted (mochi) relays
	

### Relay Setup
1. Do the same thing as the producer **except** for the following:
	1. cncli
	2. producer keys
	3. mithril
2. Issue the mithril-relay command with squid

# Backing Up
Once everything is configured correctly, go back to proxmox `Backup` and configure VM backups, with the following properties:
- Retention: keep last 5 backups
# Verification

Check that all systemd services are running:

## General
- `cnode`
- `cnode-submit-api.service`
- `cnode-ogmios.service`

## Producer
- `cnode-cncli-sync.service`
- `cnode-cncli-validate.service`
- `cnode-mithril-signer.service`
- `cnode-cncli-ptsendtip.service`
- `cnode-cncli-ptsendslots.service`

# CLOAK (Discord Updater)
1. Install python v3.11, python3.pip, and python3-venv
2. Clone [cloak](https://github.com/mochipool/cloak) to the local machine **not** the remote
3. Copy the source files from src folder on the local machine to the /opt/cloak folder on the remote machine
4. Activate the python virtual environment `/opt/cloak/env/bin/activate`
5. Install the python requirements using the pythonrequirements.txt file on the remote machine
6. Edit the config file config.ini
7. Edit the mariaDB 
8. Get a discord webhook
9. Edit the sqlite block db location


## Creating the systemd services
1. Copy the services folder from the local machine to the home folder on the remote machine
2. On the remote machine, use sudo to copy the services in the home folder to the path /etc/systemd/system
3. enable the systemctl services for the timers:
	1. cloak-sync.timer
	2. cloak-push.timer
4. Copy systemd files to `/etc/systemd/system`
5. Reload systemd with `sudo systemctl daemon-reload`

--- 

# Grafana
*Note: we use the grafana cloud free tier to visualize metrics and create alerts as it serves our purposes and separates the tooling from monitoring.*

## Configure InfluxDB Using the NAS
- Create InfluxDB volume on the NAS. this is usually the path `/volume1/docker/mochi/influxdb`
- Create container deployment on the NAS using InfluxDB. NOTE *This creates self-signed certificates; make sure that this configuration is correct*

```yaml
version: '3'
services:
  influxdb:
    container_name: influxdb
    image: influxdb:2.7.3
    ports:
      - "8086:8086"
    volumes:
      - /volume1/docker/mochi/influxdb/db:/var/lib/influxdb2
      - /volume1/docker/mochi/influxdb/certs:/etc/ssl
    command: ["influxd", "--tls-cert=/etc/ssl/influxdb-selfsigned.crt", "--tls-key=/etc/ssl/influxdb-selfsigned.key"]
```


- Navigate to the influxdb web portal at `https://<NAS_ip>:8086` 
- Create an organization named `proxmox` 
-  Create a bucket called `proxmox`
- Create an API token and save securely on the local machine; this will be used by proxmox to export metrics to the database.
- Create an API token for Grafana and save it securely on the local machine; this will be used by grafana to connect to the influxdb.

## Exporting metrics from proxmox to InfluxDB
- Create InfluxDB exporter on proxmox. To do this, go the datacenter view > matrix server > add InfluxDB matrix exporter.
	- Input the NAS IP address with the port specified in the yaml configuration. In this case, it may differ from the default port.
	- Paste in the API token from the previous step.
	- Expose the database the influxdb server to the internet

## Importing metrics to Grafana
- Create a grafana account and organization
- Once the organization is created, add the influxdb data source to the grafana dashboard. This can be done using the data sources tab under the Connections tab
	- Create a data source
	- Point it to the influxdb server
	- add (tick off) the self-signed certificates. (For convenience, you can skip this)
	- Paste in the API token created from influxdb
	- save and test
- Create a dashboard using influxdb source with the template linked [here](https://grafana.com/grafana/dashboards/18621-proxmox-7-influxdb2/). Select the proxmox bucket to see the data.

### Setting Alerts
- Setup the alerts under the Alerting & IRS > Alerting > Alerting Rules
	- Low Storage Available
	- High CPU Usage
	- CPU Temperature?
- Create alerting target to Discord under Alerting & IRS > Alerting > Contact points
	- Create a webhook in Discord and paste it in the contact point

#### Queries
Storage Pool
```flux
from(bucket: "proxmox")
  |> range(start: v.timeRangeStart, stop: v.timeRangeStop)
  |> filter(fn: (r) => r["_measurement"] == "system")
  |> filter(fn: (r) => r["_field"] == "avail")
  |> filter(fn: (r) => r["host"] == "local-lvm")
  |> filter(fn: (r) => r["nodename"] == "pve")
  |> filter(fn: (r) => r["object"] == "storages")
  |> filter(fn: (r) => r["type"] == "lvmthin")
  |> aggregateWindow(every: v.windowPeriod, fn: mean, createEmpty: false)
  |> yield(name: "mean")
```

VM Count
```flux
from(bucket: "proxmox")
  |> range(start: v.timeRangeStart, stop: v.timeRangeStop)
  |> filter(fn: (r) => r["_measurement"] == "system")
  |> filter(fn: (r) => r["_field"] == "running-machine")
  |> distinct(column: "host")
  |> group(columns: [])
  |> count()
  |> toInt()
  |> yield(name: "_value")
```
