#Configurar NFS Cliente


```
root@node01:~# apt -y install nfs-common 
```

```
root@node01:~# vi /etc/idmapd.conf 
```

Alterar no ficheiro de Configuração:

```
 # line 6 : uncomment and change to your domain name

Domain = srv.world


```
```
root@node01:~# mount -t nfs dlp.srv.world:/home/nfsshare /mnt 
```


```
root@node01:~# df -hT 
```
Verificar se a pasta ja esta partilhada
```
root@node01:~# df -hT

Filesystem                        Type   Size  Used Avail Use% Mounted on
tmpfs                             tmpfs  393M  1.1M  392M   1% /run
/dev/mapper/ubuntu--vg-ubuntu--lv ext4    20G  6.3G   13G  34% /
tmpfs                             tmpfs  2.0G     0  2.0G   0% /dev/shm
tmpfs                             tmpfs  5.0M     0  5.0M   0% /run/lock
tmpfs                             tmpfs  4.0M     0  4.0M   0% /sys/fs/cgroup
/dev/vda2                         ext4   976M  128M  782M  14% /boot
tmpfs                             tmpfs  393M  4.0K  393M   1% /run/user/0
dlp.srv.world:/home/nfsshare      nfs4    20G  6.3G   13G  34% /mnt
```



```
root@node01:~# mount -t nfs -o vers=3 dlp.srv.world:/home/nfsshare /mnt 
```
