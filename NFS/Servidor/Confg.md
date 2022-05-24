#Confugure NFS Server

```
root@dlp:~# apt -y install nfs-kernel-server 
```

```
root@dlp:~# vi /etc/idmapd.conf 
```

Alterar no ficheiro de Configuração:
```
 # line 6 : uncomment and change to your domain name

Domain = srv.world
root@dlp:~# vi /etc/exports
# write settings for NFS exports

# for example, set [/home/nfsshare] as NFS share

/home/nfsshare 10.0.0.0/24(rw,no_root_squash)

```

```
root@dlp:~# mkdir /home/nfsshare 
```

```
root@dlp:~# systemctl restart nfs-server  
```
