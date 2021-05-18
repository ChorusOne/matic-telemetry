# Matic-stats-exporter

- ## Bor:-
Telemetry data for Bor nodes on Mainnet and Mumbai-testnet can be found here https://bor-mainnet.vitwit.com and https://bor-mumbai.vitwit.com.
![](https://github.com/vitwit/matic-telemetry/blob/main/docs/screen.png)

To export your nodes telemetry data to these dashboards do the following steps - 
#### Restart your bor node with the ethstats flag

  
   - Add `--ethstats` flag to your bor bash script which will be present at `~/node/bor/start.sh`. After adding the flag to the bash file it should look like this:
   ```#!/usr/bin/env sh

set -x #echo on

BOR_DIR=${BOR_DIR:-~/.bor}
DATA_DIR=$BOR_DIR/data

bor --datadir $DATA_DIR \
  --ethstats <node-name>:<key>@<server-ip>:<port> \
  --port 30303 \
  --http --http.addr '0.0.0.0' \
  --http.vhosts '*' \
  --http.corsdomain '*' \
  ......
  ......
```
**Note**:- For connecting to the mainnet dashboard use  `--ethstats <node-name>:mainnet@bor-mainnet.vitwit.com:3000`. For connecting to the testnet dashboard use `--ethstats <node-name>:testnet@bor-mumbai.vitwit.com:3000`. `<node-name>` is just an identifier to display it on the dashboard.
   - Restart your bor service `sudo systemctl restart bor`
   
To set up your own dashboard follow these [instructions](./docs/bor-setup.md).

- ## Heimdall:-
Telemetry data for Heimdall nodes on Mainnet and Mumbai-testnet can be found here [https://heimdall-mainnet.vitwit.com](https://heimdall-mainnet.vitwit.com) and [https://heimdall-mumbai.vitwit.com](https://heimdall-mumbai.vitwit.com)

To export your nodes telemetry data to these dashboards do the following:-

```
git clone https://github.com/vitwit/matic-telemetry.git
cd matic-telemetry
cp example.config.toml config.toml
```
Replace default value of `node` with your <node-name> in `config.toml`.

Use the following secret_key and IP to connect to mainnet dashboard

```
[stats_details]
secret_key = "heimdall_mainnet"  
node = "<node-name>" 
net_stats_ip = "heimdall-mainnet.vitwit.com:3000"
```

Use the following secret_key and IP to connect to testnet dashboard

```
[stats_details]
secret_key = "heimdall_testnet"  
node = "<node-name>" 
net_stats_ip = "heimdall-testnet.vitwit.com:3000"
```
Run the exporter using
```
go run main.go
```


