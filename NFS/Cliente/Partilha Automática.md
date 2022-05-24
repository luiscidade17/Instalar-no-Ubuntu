#Configurar Partilha Automática, depois do start


```
root@node01:~# vi /etc/fstab 
```

# add to the end : set NFS share
```
dlp.srv.world:/home/nfsshare /mnt               nfs     defaults        0 0

```
