# Configurar Zonas

Configurar Zonas


# Configurar Zonas

crie arquivos de zona que os servidores resolvem o endereço IP do nome de domínio.
O exemplo abaixo usa rede interna [10.0.0.0/24], nome de domínio [srv.world].
Substitua para o seu próprio ambiente.

```
root@dlp:~# vi /etc/bind/srv.world.lan

$TTL 86400
@   IN  SOA     dlp.srv.world. root.srv.world. (
        # any numerical values are OK for serial number but
        # recommended : [YYYYMMDDnn] (update date + number)
        2021050501  ;Serial
        3600        ;Refresh
        1800        ;Retry
        604800      ;Expire
        86400       ;Minimum TTL
)
        # define Name Server
        IN  NS      dlp.srv.world.
        # define Name Server's IP address
        IN  A       10.0.0.30
        # define Mail Exchanger Server
        IN  MX 10   dlp.srv.world.

# define each IP address of a hostname
dlp     IN  A       10.0.0.30
www     IN  A       10.0.0.31


```
Crie arquivos de zona que os servidores resolvam nome de domínio do endereço IP.
O exemplo abaixo usa rede interna [10.0.0.0/24], nome de domínio [srv.world].
Substitua para o seu próprio ambiente.

```
 root@dlp:~# vi /etc/bind/0.0.10.db

$TTL 86400
@   IN  SOA     dlp.srv.world. root.srv.world. (
        2021050501  ;Serial
        3600        ;Refresh
        1800        ;Retry
        604800      ;Expire
        86400       ;Minimum TTL
)
        # define Name Server
        IN  NS      dlp.srv.world.

# define each hostname of an IP address
30      IN  PTR     dlp.srv.world.
31      IN  PTR     www.srv.world.



```
