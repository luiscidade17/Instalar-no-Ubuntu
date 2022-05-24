# Instalar e configurar DHCP 

Configurar Zonas


```
root@dlp:~# apt -y install isc-dhcp-server 
```

```
root@dlp:~# vi /etc/dhcp/dhcpd.conf 
```

```
 # line 10 : specify domain name

option domain-name "srv.world"
;
# line 11 : specify nameserver's hostname or IP address

option domain-name-servers dlp.srv.world
;
# line 24 : uncomment

authoritative;
# add to the end

# specify network address and subnet-mask

subnet 10.0.0.0 netmask 255.255.255.0 {
    # specify default gateway
    option routers 10.0.0.1;
    # specify subnet-mask
    option subnet-mask 255.255.255.0;
    # specify the range of leased IP address
    range dynamic-bootp 10.0.0.200 10.0.0.254;
}



```

```
root@dlp:~# systemctl restart isc-dhcp-server 
```
