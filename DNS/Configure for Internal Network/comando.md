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
acl internal-network {
        10.0.0.0/24;
};

```
sudo nano /etc/bind/named.conf.options 
```

Bulk git push operation (some repositries folders)
 
```
bulk-git --status repFolder01 repFolder02 respFolder03 branch 
```

Git status of the myrepA and myrepB prj
```
bulk-git --status myrepA myrepB main 
```
