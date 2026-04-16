# NFS-Server-Client-Setup-Linux-
Access remote storage like a local directory using NFS — fast, efficient, and centralized.

📌 Overview

This project demonstrates how to configure a Network File System (NFS) to enable centralized storage sharing between a Linux server and client.

Instead of transferring files manually, the client directly accesses the server’s directory in real-time.

🎯 Use Case

- Server has extra storage mounted on /var/Normal_apr16
- Client needs additional space without copying data
- Requirement for real-time file access

👉 Solution: NFS remote mounting

⚙️ Tech Stack

- OS: Linux (RHEL/CentOS)
- Service: NFS (nfs-utils)
- Core Services: nfs, rpcbind
- Configuration File: /etc/exports
- Port: 2049
  
🏗️ Architecture

- The setup includes two systems: NFS Server and NFS Client connected over a network
- The server (192.168.125.140) hosts storage mounted on /var/Normal_apr16
- This directory is shared using the /etc/exports configuration file
- The NFS service exposes this directory to other systems
- On the client side, a mount point /var/nfs_apr16 is created
- The client mounts the server’s shared directory using the NFS protocol
- After mounting, files can be accessed as if they are local
- Data is physically stored only on the server (centralized storage)
- Changes reflect instantly on both server and client (real-time sync)
  
🚀 Configuration Steps

🔹 1. Install NFS Package (Both Systems)

      - yum install nfs-utils -y
      
🔹 2. Configure NFS Share (Server)

Edit exports file:

      - vim /etc/exports

Add:

      - /var/Normal_apr16 *(rw,sync)

Apply configuration:

      - exportfs -rv
      
🔹 3. Start Required Services

      - service rpcbind start
      - service nfs restart
      
🔹 4. Verify Storage on Server

      - df -h

✔️ Confirms /dev/sdb1 mounted on /var/Normal_apr16

🔹 5. Configure Client

Create mount directory:

      - mkdir /var/nfs_apr16

Mount NFS share:

      - mount 192.168.125.140:/var/Normal_apr16 /var/nfs_apr16
      
🔹 6. Validate Mount

      - df -h

✔️ Remote storage appears as local directory

📸 Screenshots Explanation

🖼️ Image 1 – Environment & Service Check

- df -h shows disk partitions
- SELinux set to permissive (getenforce)
- FTP service running (environment validation)
  
🖼️ Image 2 – NFS Service Restart

- service nfs restart successful
- All required NFS services started
- Storage verified
  
🖼️ Image 3 – Export Configuration

- /etc/exports configured
- exportfs -rv applied
- Directory shared successfully
  
🖼️ Image 4 – Client Mounting

- NFS share mounted on /var/nfs_apr16
- df -h confirms remote storage
- Successful connection to server
- 
✨ Key Features

- ✔️ No manual file transfer required
- ✔️ Saves client storage space
- ✔️ Real-time file synchronization
- ✔️ Centralized data management

⚠️ Limitations

- Not secure (open access using *)
- Requires network connectivity
- Performance depends on network speed
  
📌 Conclusion

This project demonstrates how NFS enables efficient and centralized file sharing across Linux systems. It simplifies storage management and allows seamless access to remote directories as if they were local.
