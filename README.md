# Proxmox-Virtualization-Cluster
Server rack dedicated to hosting various services 
The goal is to host several high-availability services with a robust backup system capable of enabling agile development. 

Components:
- Several servers running Proxmox to host virtual machines
- Server running TrueNAS baremetal with an HBA connected to 2 drive bay chassis, 30 hard drives total split into RAID-Z2 arrays as large storage/backup storage
- 10G Intel Network Cards connected to a 10G switch on all servers
- Raspberry Pi with an External HDD to run less critical services that benefit from a lower power solution and to act as a second backup location

Services:
- Proxmox - VMs and Containers are stored on ZFS Mirrored SSDs installed in the individual Proxmox nodes
	- VMs
		- OPNsense router, with an additional low power device planned on being added as a second bare metal router for high-availability 
		- Game servers split into their own VMs
		- Windows VMs to use for testing
	- Containers
		- Frigate - AI powered Network video recorder for local IP cameras
		- Proxmox Backup Server - Maintains and de-duplicates data for backups for all virtualized VMs/containers and linux hosts such as proxmox hosts and the raspberry pi. Backups stored on NFS shares on the Rasberry pi and TrueNAS
- Raspberry Pi
	- Home Assistant - Home automation and MQTT for smart devices
	- Wireguard - VPN
	- Syncthing - Sync files between my PC, laptop, mobile devices, and TrueNAS with versioning on the files
	- NFS
- TrueNAS
	- SMB and NFS shares - Data access for several services that need it and my PC, also allows for true high availability barring the TrueNAS device going offline 
	- Syncthing
