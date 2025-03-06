*N*etwork *F*ile *S*ystem is a [[network]] protocol for distributing file sharing. This allows multiple computers to share some critical files while maintaining a single source of truth. NFS uses [[RPC]] to route request between the clients. It is important to note that NFS needs of specific libraries both on the server and clients to work

# Practice
## Server
These are the commands used to create an NFS server
(using a Debian based [[OS]]. But they are the same on any other [[linux]] OS)
{} will be used as placeholders 
```sh
sudo apt update
sudo apt install -y nfs-kernel-server
sudo chmod 777 {folderToShare}
echo "{folderToShare} {clientIP1}(rw,sync,no_subtree_check) {clientIP2}(rw,sync,no_subtree_check)" >> /etc/exports
sudo exportfs -r
sudo systemctl restart nfs-kernel-server
sudo systemctl restart rpcbind
sudo systemctl start rpcbind
sudo systemctl enable rpcbind
sudo systemctl start nfs-common
sudo systemctl enable nfs-common
#if it fails
	rm /lib/systemd/system/nfs-common.service
	sudo passwd
	systemctl daemon-reload
```
## Client
These are the commands used on the client after having the server ready
{} will be used as placeholders
```sh
sudo apt update
sudo apt install -y nfs-common
sudo mount -t nfs {serverIP}:{folderToShare} {clientfolder}
```
remember that `{folderToShare}` must be the same as the folder created on the server

Also as a common practice you use the path `/mnt` for any mounts that you create