# Setting up NFS
Assume that a large hardware RAID array (e.g., 4TB) has been created and partitioned and that an EXT4 filesystem has been enumerated as `/dev/sdb1`.  To set up basic NFS on the server, perform the following:

## Step 1: Install NFS Server

Install the NFS server package (package name may vary based on the distribution):

```bash
apt-get update
apt-get install nfs-kernel-server
```

## Step 2: Configure NFS Exports

Add this line to `/etc/exports`

```plaintext
/srv/nfs4/tools		192.168.0.0/24(ro,fsid=0,no_subtree_check)
```

The subnet `192.168.0.0/24` with the allowed IP range or specific client IP addresses.
The subnet may need to be altered 

## Step 3: Apply NFS Export Changes

Reexport all directories specified in `/etc/exports`

```bash
exportfs -ra
```

## Step 4: Restart the NFS Service

Restart the NFS service and check the status afterwards (if you're paranoid)

```bash
systemctl restart nfs-kernel-server
systemctl status nfs-kernel-server
```

## Step 5: Configure Firewall

Adjust firewall rules to allow NFS traffic.

## Step 6: Accessing NFS Share from Clients

Clients can mount the share with:

```bash
sudo mount -t nfs <NFS_server_IP>:/srv/tools /mnt/mount_point
```

