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

