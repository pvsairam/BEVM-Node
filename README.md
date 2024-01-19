# BEVM-Node
# Setting Up BEVM Node on Ubuntu 20.04

## Server Update

```
sudo apt update
sudo apt upgrade
sudo apt install --assume-yes git clang curl libssl-dev llvm libudev-dev make protobuf-compiler
sudo ufw allow ssh; sudo ufw allow 30333; sudo ufw allow 20222; sudo ufw allow 30334
```

## Fetching the Binary

```
mkdir -p $HOME/.bevm
wget -O bevm https://github.com/btclayer2/BEVM/releases/download/testnet-v0.1.1/bevm-v0.1.1-ubuntu20.04 && chmod +x bevm
sudo cp bevm /usr/bin/
```

## Creating and Starting the Service
### Make sure to replace the "node-name" with your Metamask (EVM) wallet address.

```
sudo tee /etc/systemd/system/bevm.service > /dev/null << EOF
[Unit]
Description=BEVM
After=network-online.target
StartLimitIntervalSec=0
[Service]
User=root
Restart=always
RestartSec=3
ExecStart=/usr/bin/bevm --chain=testnet --name="node-name" --pruning=archive --telemetry-url "wss://telemetry.bevm.io/submit 0"
[Install]
WantedBy=multi-user.target
EOF

sudo systemctl daemon-reload
sudo systemctl enable bevm
sudo systemctl start bevm
```

## Check the log

```
sudo journalctl -u bevm -f --no-hostname -o cat
```

## Additional Step: Verifying Node Status

Open [BEVM Telemetry](https://telemetry.bevm.io/#list/0x41cfeafc7177775a0e838b3725a0178b89ebf5dde1b5f766becbf975a24e297b)

Hit F on your keyboard to search for your EVM/MetaMask wallet address. You should see your node in the list.

![image](https://github.com/pvsairam/BEVM-Node/assets/9134015/91a5b80a-57dd-469e-baa1-78b7fd801acf)


# <p align="center"> THE END </p>
