#DHCP no Cliente

```
root@dlp:~# vi /etc/netplan/01-netcfg.yaml 
```

enable dhcp4 and comment out static IP related settings

```
network:
  version: 2
  renderer: networkd
  ethernets:
    ens3:
      dhcp4: yes
      #addresses: [10.0.0.31/24]
      #gateway4: 10.0.0.1
      #nameservers:
      #  addresses: [10.0.0.10]
```
```
root@dlp:~# netplan apply 
```
