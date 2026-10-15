# UFW lab command reference

Commands below reflect the workflow demonstrated in the lab. Run them on the indicated VM and adapt IP addresses to your own network.

## Ubuntu Server — inspect and configure

```bash
sudo ufw status verbose
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw allow OpenSSH
sudo ufw enable
sudo ufw status numbered
```

## Kali Linux — connectivity and service checks

```bash
ping -c 4 192.168.243.131
nmap -Pn -sV 192.168.243.131
curl http://192.168.243.131:8000/test.html
```

## Ubuntu Server — temporary HTTP test

```bash
mkdir -p ~/webtest
cd ~/webtest
echo "UFW lab test page" > test.html
python3 -m http.server 8000
```

Stop the HTTP server with `Ctrl+C` after testing.

## Ubuntu Server — allow and remove port 8000

```bash
sudo ufw allow 8000/tcp
sudo ufw status numbered
sudo ufw delete allow 8000/tcp
sudo ufw status numbered
```

## Ubuntu Server — restrict SSH to Kali

```bash
sudo ufw allow from 192.168.243.129 to any port 22 proto tcp
sudo ufw status numbered
```

If a broad SSH rule already exists, verify the restricted rule first, then remove the broad rule by its current number. Rule numbers may change after each deletion, so check `status numbered` before every numbered deletion.
