# Configurar Rede Interna

Instalar e configurar DNS


# EXEMPLOS
Instalar Bind9

```
sudo apt -y install bind9 bind9utils 
```
ADICIONAR include "/etc/bind/named.conf.internal-zones";
```
sudo nano /etc/bind/named.conf  
```
# add : set ACL entry for local network

```
sudo nano /etc/bind/named.conf.options 
```
```
acl internal-network {
        10.0.0.0/24;
};

options {
        directory "/var/cache/bind";

.....
.....

```
```
``` root@dlp:~# vi /etc/bind/named.conf

include "/etc/bind/named.conf.options";
include "/etc/bind/named.conf.local";
include "/etc/bind/named.conf.default-zones";
# add
include "/etc/bind/named.conf.internal-zones";

root@dlp:~# vi /etc/bind/named.conf.options

# add : set ACL entry for local network
acl internal-network {
        10.0.0.0/24;
};

options {
        directory "/var/cache/bind";

.....
.....

        # add local network set on [acl] section above
        # network range you allow to recieve queries from hosts
        allow-query { localhost; internal-network; };
        # network range you allow to transfer zone files to clients
        # add secondary DNS servers if it exist
        allow-transfer { localhost; };
        # add : allow recursion
        recursion yes;

        //=======================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //=======================================================================

        dnssec-validation auto;

        # if not listen IPV6, change [any] to [none]
        listen-on-v6 { any; };
};

root@dlp:~# vi /etc/bind/named.conf.internal-zones
# create new

# add zones for your network and domain name
zone "srv.world" IN {
        type master;
        file "/etc/bind/srv.world.lan";
        allow-update { none; };
};
zone "0.0.10.in-addr.arpa" IN {
        type master;
        file "/etc/bind/0.0.10.db";
        allow-update { none; };
};

# if you don't use IPv6 and also suppress logs for IPv6 related, possible to change

# set BIND to use only IPv4

root@dlp:~# vi /etc/default/named
# add

OPTIONS="-u bind -4
"

# For how to write the section [*.*.*.*.in-addr.arpa], write your network address reversely like follows
# case of 10.0.0.0/24
# network address     ⇒ 10.0.0.0
# network range       ⇒ 10.0.0.0 - 10.0.0.255
# how to write        ⇒ 0.0.10.in-addr.arpa

# case of 192.168.1.0/24
# network address     ⇒ 192.168.1.0
# network range       ⇒ 192.168.1.0 - 192.168.1.255
# how to write        ⇒ 1.168.192.in-addr.arpa




