# Configurar Rede Externa

Instalar e configurar DNS


# Configurar Rede Externa

Instalar Bind9

```
 root@dlp:~# vi /etc/bind/named.conf
```
include "/etc/bind/named.conf.options";
include "/etc/bind/named.conf.local";
include "/etc/bind/named.conf.default-zones";
# add
include "/etc/bind/named.conf.external-zones";

root@dlp:~# vi /etc/bind/named.conf.options

options {
        directory "/var/cache/bind";

.....
.....

        # add : receive queries from all hosts
        allow-query { any; };
        # network range you allow to transfer zone files to clients
        # add secondary DNS servers if it exist
        allow-transfer { localhost; };
        # add : not allow recursion
        recursion no;

        //=======================================================================
        // If BIND logs error messages about the root key being expired,
        // you will need to update your keys.  See https://www.isc.org/bind-keys
        //=======================================================================

        dnssec-validation auto;

        # if not listen IPV6, change [any] to [none]
        listen-on-v6 { any; };
};

root@dlp:~# vi /etc/bind/named.conf.external-zones
# create new

# add zones for your network and domain name
zone "srv.world" IN {
        type master;
        file "/etc/bind/srv.world.wan";
        allow-update { none; };
};
zone "80.0.16.172.in-addr.arpa" IN {
        type master;
        file "/etc/bind/80.0.16.172.db";
        allow-update { none; };
};

# if you don't use IPv6 and also suppress logs for IPv6 related, possible to change

# set BIND to use only IPv4

root@dlp:~# vi /etc/default/named
# add

OPTIONS="-u bind -4
"

# For how to write the section [*.*.*.*.in-addr.arpa], write your network address reversely like follows
# case of 172.16.0.80/29
# network address     ⇒ 172.16.0.80
# network range       ⇒ 172.16.0.80 - 172.16.0.87
# how to write        ⇒ 80.0.16.172.in-addr.arpa


