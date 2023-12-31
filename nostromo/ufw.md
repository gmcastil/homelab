# Basic Firewall Configuration

Need to install and configure the firewall to allow SSH connections as well as NFS.

1. First install the `ufw`

```bash
apt-get install ufw
```

2. Before enabling it, since this is almost certainly being done via SSH, make sure that SSH traffic is allowed

```bash
ufw allow ssh
ufw enable
```

3. Now allow NFS as well

```bash
ufw allow from 192.168.0.0/24 to any port 2049
ufw allow 111          # for rpcbind/portmap service
```

4. Optionally, for NFSv4 lock management, these may need to be allowed as well

```bash
ufw allow 32765:32768
```

5. Finally, reload the firewall

```bash
ufw reload
```

