# SPRINT 3

### Instal·lació i Configuració de LDAP a Linux

Començen configurant la màquina amb en xarxa NAT.

![imagen](img/Imatge enganxada (70).png)

Configurem la ip manualment `10.0.2.15`

![imagen](img/Imatge enganxada (71).png)

Un cop configurada la ip fem `ip a` i comprovem que esta bé.

![imagen](img/Imatge enganxada (72).png)

Fem un ping a google per verificar la connexió a internet.


![imagen](img/Imatge enganxada (73).png)

Posem el nostre hostname en `/etc/hostname `

![imagen](img/Imatge enganxada (85).png)


Entrem a `/etc/hosts` i cambiem el nostre nom domini

![imagen](img/Imatge enganxada (74).png)


- 1 Instal·lació dels paquets necessaris

Per instal·lar LDAP en un sistema basat en  Ubuntu, executem la següent comanda:

`apt install libnss-ldap libpam-ldap nscd`

![imagen](<img/Imatge enganxada (10).png>)

- 2 Configuració del servidor LDAP

Després d'acceptar la instal·lació, es mostrarà una pantalla de configuració del paquet ldap-auth-config. En aquest apartat haurem d'introduir diverses dades per configurar la connexió amb el servidor LDAP.

2.1 Introduir la URI del servidor LDAP

El sistema ens demanarà la URI Per exemple, si el servidor LDAP està a la IP 10.0.2.15:

![imagen](img/ldapip.png)

Continuem donat-li al sí ja que es el que es recomana.

![imagen](img/sisi.png)

2.2 Nom distingit de la base de cerca (Search Base DN)

Aquí hem d'introduir el "Distinguished Name" (DN) de la base de dades LDAP. Per exemple, si el domini LDAP és victor.com, escriurem:

`dc=victor,dc=com`


![imagen](img/ldaaap.png)

2.3 Seleccionar la versió de LDAP

El sistema ens preguntarà quina versió del protocol LDAP volem utilitzar. Se selecciona normalment la més alta disponible, en aquest cas:

`3`

![imagen](img/sass.png)

Ens demana si volem permetre que l'usuari root del sistema pugui gestionar contrasenyes locals com si estiguessin canviant-se a LDAP. Se selecciona:
Sí.

![imagen](img/saass.png)


Ens pregunta si és necessari iniciar sessió per accedir a la base de dades LDAP. Seleccionem:
Sí.

![imagen](img/asaroso.png)

Especificarem el compte que actuarà com a administrador en el directori LDAP. Normalment és:

`cn=admin,dc=victor,dc=com`

![imagen](img/toni.png)

Posem la nostra contrasenya:

![imagen](img/cinta.png)

Per evitar problemes de seguretat, es demana un compte d'usuari sense privilegis per accedir a LDAP:

`cn=admin,dc=victor,dc=com` el mateix.

![imagen](img/fufi.png)

També se sol·licita la contrasenya corresponent.

![imagen](img/Imatge enganxada (11).png)

El sistema permet seleccionar el tipus de xifratge per emmagatzemar contrasenyes. Es recomana triar:

`md5`

![alt text](<img/Imatge enganxada (12).png>)


3 Configuració dels fitxers del sistema per utilitzar LDAP

Després de la configuració inicial, hem d'editar alguns fitxers del sistema per assegurar-nos que LDAP es fa servir correctament.

3.1 Editar `/etc/nsswitch.conf`

Obrim el fitxer amb nano:


![alt text](<img/Imatge enganxada (13).png>)

Afegim ldap a les línies següents per permetre que el sistema utilitzi LDAP per gestionar usuaris, grups i altres serveis:


    passwd:   ldap compat files systemd sss
    group:    ldap compat files systemd sss
    shadow:   ldap compat files systemd sss


per a que pasi directament per al ldap.

3.2 Editar /etc/pam.d/common-session

Afegim la línia següent per assegurar-nos que es fa servir LDAP durant les sessions:

session optional pam_mkhomedir.so skel=/etc/skel umask=0022

![alt text](<img/Imatge enganxada (14).png>)

4 Finalització i comprovació

Un cop finalitzada la configuració, podem reiniciar el servei nscd per aplicar els canvis:

5 Configuració de LightDM

Obrim el fitxer amb:

nano `/usr/share/lightdm/lightdm.conf.d/50-ubuntu.conf`

![alt text](<img/Imatge enganxada (15).png>)

Editem les línies següents:

    [Seat:*]
    user-session=ubuntu
    greeter-show-manual-login=true

**reeter-show-manual-login=true:** Activa l'opció per permetre l'inici de sessió manualment, útil per a autenticació amb LDAP

Després de configurar LightDM, es verifica que els usuaris LDAP poden iniciar sessió correctament.

Al iniciar sessió amb un usuari LDAP (alu1), executem la comanda:

`whoami`

![alt text](<img/Imatge enganxada (16).png>)

Sortida esperada:

alu1

### Gestió de domini

Passos per gestionar un domini amb LDAP, incloent la visualització de dades, l'afegiment d'entrades, la cerca, la modificació i l'eliminació d'usuaris.

**1 Llistat del contingut del directori LDAP**

Per obtenir informació sobre les entrades existents en el directori LDAP, es fa servir la comanda:

`slapcat`

Exemple de sortida:

![alt text](<img/Imatge enganxada (17).png>)

**2 Afegir usuaris i grups a LDAP**

Per afegir noves entrades al directori LDAP, es fa servir ldapadd juntament amb un fitxer .ldif que conté les dades dels usuaris o grups.

Comanda per afegir noves entrades:

![alt text](<img/Imatge enganxada (18).png>)

**3 Cerca d'usuaris en LDAP**

Per cercar informació sobre un usuari específic, es fa servir ldapsearch amb diversos filtres.


![alt text](<img/Imatge enganxada (19).png>)

3.2 Cercar diversos usuaris amb rang d'UID

Per cercar usuaris amb uidNumber superior a 1002:

`ldapsearch -xLLL -b "dc=victor,dc=com" "uidNumber>=1002"`

![alt text](<img/Imatge enganxada (20).png>)

**4 Afegir una nova unitat organitzativa**

Per afegir una nova unitat organitzativa (ou), creem un fitxer .ldif amb la següent informació:

![alt text](<img/Imatge enganxada (22).png>)

A continuació, executem:

![alt text](<img/Imatge enganxada (23).png>)

**5 Modificar un usuari en LDAP**

Per modificar un usuari existent, es pot utilitzar ldapmodify per afegir o canviar atributs, per exemple, el correu electrònic.

Fitxer .ldif per modificar un usuari:

![alt text](<img/Imatge enganxada (24).png>)

Modifiquem el gmail:

![alt text](<img/Imatge enganxada (25).png>)

I a continuació el eliminem:

![alt text](<img/Imatge enganxada (26).png>)

**6 Modificació del Cognom (sn) i Nom (cn)**

Entrem al fitxer editem guardem i executem amb ldapmodify.

![alt text](<img/Imatge enganxada (27).png>)

![alt text](<img/Imatge enganxada (28).png>)


### Entorns gràfics

Inici de la configuració 


Descarrega Apache desde la pagina web official.

![alt text](<img/Imatge enganxada (84).png>)

A continuació el executem:

![alt text](<img/Imatge enganxada (75).png>)

I selecionem LDAP new connection:

![alt text](<img/Imatge enganxada (76).png>)

Posem el nostre nom i la nostra ip:

![alt text](<img/Imatge enganxada (77).png>)

I posem la configuració del nostre servidor ldap:

![alt text](<img/Imatge enganxada (78).png>)

Un cop establerta la connexió ens surt la estructura LDAP.

![alt text](<img/Imatge enganxada (79).png>)

#### Afegir i configurar registres:

Escull l'opció de crear una entrada desde zero.

![alt text](<img/Imatge enganxada (80).png>)

Definim el objectClass seleccionant posixGroup:

![alt text](<img/Imatge enganxada (81).png>)

Estableix el RDN en aquest cas cn = Public.


![alt text](<img/Imatge enganxada (82).png>)

Assigna un valor en gibNumber per exemple 5000.

![alt text](<img/Imatge enganxada (83).png>)

Comprovació:

Desde un client integrat al domini LDAP verifiquem el whaomi i id.


![alt text](<img/imagenVirtual.png>)

###  Instal·lació del servidor NFS

1 Servidor NFS

El sistema de fitxers NFS (Network File System) permet compartir directoris a través de la xarxa. Per instal·lar-lo en un servidor Ubuntu, executem:

`apt install nfs-kernel-server`

![alt text](<img/Imatge enganxada (29).png>)

Fem un `systemctl status nfs-server` per comprovar que esta actiu el servidor.

![alt text](<img/Imatge enganxada (30).png>)

2 Configuració del client NFS (Ubuntu)

2.1 Actualització del sistema

Fem un ` apt update` per actualizar la màquina client.

![alt text](<img/Imatge enganxada (31).png>)

2.2 Instal·lació del client NFS

Instalem  el servidor amb `apt install nfs-common rpcbind`

![alt text](<img/Imatge enganxada (32).png>)

3 Configuració del client NFS a Windows

Per connectar un client Windows a un servidor NFS, cal activar la funció "Client per a NFS":

    Obrir "Activar o desactivar les característiques de Windows".
    Marcar l'opció "Client per a NFS" dins de "Serveis per a NFS".
    Aplicar els canvis i esperar que Windows completi la instal·lació.


![alt text](<img/Imatge enganxada (33).png>)

![alt text](<img/Imatge enganxada (34).png>)

4 Compartició de carpetes al servidor NFS

4.1 Creació de la carpeta compartida

Executem les següents comandes per crear un directori compartit:

`cd /`
`mkdir compartida`

![alt text](<img/Imatge enganxada (35).png>)

A continuació, verifiquem els permisos:

` ls -l | grep compartida`

![alt text](<img/Imatge enganxada (36).png>)

Per garantir que qualsevol usuari pugui accedir-hi, modifiquem els permisos:

`chown nobody:nogroup compartida`
`chmod -R 777 compartida`

4.2 Afegir la carpeta a /etc/exports

Afegim la línia següent per compartir la carpeta amb qualsevol client:

**/compartida *(rw,sync,no_subtree_check)**


![alt text](<img/Imatge enganxada (37).png>)

**4.3 Reiniciar el servei NFS**

`systemctl restart nfs-kernel-server`

![alt text](<img/Imatge enganxada (38).png>)

5 Connexió del client Ubuntu a la carpeta compartida

5.1 Crear el punt de muntatge

A la màquina client, creem un directori per muntar la carpeta compartida i també muntarem la carpeta compartida del servidor NFS al client Ubuntu:

Podem comprovar que s'ha muntat correctament amb:

`df -h`

![alt text](<img/Imatge enganxada (42).png>)

6 Connexió del client Windows a la carpeta compartida

    Obrir "Explorador de fitxers".
    A la barra d’adreces, introduir \\10.0.2.15\compartida (substituint 10.0.2.15 per la IP del servidor).
    Ara la carpeta compartida hauria d'aparèixer com una unitat de xarxa.


![alt text](<img/Imatge enganxada (39).png>)

**7 Verificació de la connexió i proves d'escriptura**

Per provar la connexió, es pot crear un fitxer tant des del servidor com des del client i comprovar que apareix a l'altra màquina.


![alt text](<img/Imatge enganxada (40).png>)

![alt text](<img/Imatge enganxada (41).png>)

![alt text](<img/Imatge enganxada (43).png>)

![alt text](<img/Imatge enganxada (44).png>)

**8 Afegir més carpetes compartides**

Si volem compartir més carpetes, "perfils", repetim els passos:

![alt text](<img/Imatge enganxada (45).png>)

Afegim la nova línia a `/etc/exports`:

/perfils *(rw,sync,no_subtree_check)

/perfils *(rw,sync,no_subtree_check)

![alt text](<img/Imatge enganxada (46).png>)
**9 Creació de l'usuari en un altre home**

Es defineix un nou usuari alu2 dins del directori LDAP mitjançant un fitxer .ldif (usu.ldif).

![alt text](<img/Imatge enganxada (47).png>)

homeDirectory: /perfils/alu2 → Aquest usuari tindrà el seu directori personal a /perfils/alu2 dins del servidor NFS.

Executem la següent comanda per afegir l'usuari a LDAP:

![alt text](<img/Imatge enganxada (48).png>)

Muntatge del directori NFS per als perfils d'usuaris

L'objectiu és assegurar que /perfils sigui accessible automàticament des dels clients a través de NFS.

9.1 Configurar /etc/fstab al client

S'afegeix la següent línia a /etc/fstab per muntar automàticament /perfils des del servidor:

`10.0.2.15:/perfils /perfils nfs auto,noatime,nolock,bg,nfsvers=3,intr,id,tcp,actimeo=1800 0 0`

![alt text](<img/Imatge enganxada (49).png>)


![alt text](<img/Imatge enganxada (50).png>)

Posem les credencials i entrem.

### Instal·lació Samba

Per instal·lar Samba executem `apt install samba`

![alt text](<img/Imatge enganxada (51).png>)

Un cop tenim samba instalat començem creant una carpeta proves, i cambiem els permisos de proves amb `chmod -R 777 proves ` també li cambiem el propietari amb `chown nobody:nogroup proves` i afegim l'arxiu "hola" a dins la carpeta.

![alt text](<img/Imatge enganxada (53).png>)

Dins de ` etc/samba/smb.conf ` podem veure o modificar el recurs compartit en samba.

![alt text](<img/Imatge enganxada (52).png>)

Fem un restart per a que es guardin les modificacions aplicades.

![alt text](<img/Imatge enganxada (54).png>)

Ara afegim els usuaris Blau, Groc i Roig, per a fer unes proves.

![alt text](<img/Imatge enganxada (55).png>)

Afegim al grup "colors" Roig i Groc.

![alt text](<img/Imatge enganxada (56).png>)

I fem un `tail` per comprovar que esta creat.

![alt text](<img/Imatge enganxada (57).png>)

Afegim una contrasenya als usuaris en samba per a utilitzar-los.

![alt text](<img/Imatge enganxada (58).png>)

#### Samba en Client

Instalem el samba amb `apt install smbclient`

![alt text](<img/Imatge enganxada (59).png>)

Per a conectarse al servidor entrem al arxius i en altres ubicacions afegim `smb://IP/Repositori/`

![alt text](<img/Imatge enganxada (86).png>)

I en conectem

![alt text](<img/Imatge enganxada (87).png>)

Pero al conectarnos amb anomin ens surt un misatge d'error que es normal.

![alt text](<img/Imatge enganxada (60).png>)

Llavors anem a la carpeta per a cambiar el parametres.

![alt text](<img/Imatge enganxada (61).png>)


Reiniciem el servidor.

![alt text](<img/Imatge enganxada (62).png>)

I ara si ens deixa obrir les carpetes de samba desde el client.

![alt text](<img/Imatge enganxada (63).png>)

I fem la comprovació de que es veu la carpeta actualizada desde el servidor.

![alt text](<img/Imatge enganxada (64).png>)

Ara fem una prova pero en un altre usuari.

![alt text](<img/Imatge enganxada (65).png>)

Comprovem que es pot veure la carpeta perque hem afegit els parametres en smb.conf.

![alt text](<img/Imatge enganxada (66).png>)

I comprovem el usuari.

![alt text](<img/Imatge enganxada (67).png>)

Ara desde el usuari groc fem la mateixa prova.

![alt text](<img/Imatge enganxada (68).png>)

I ens salta l'error, ja que, no te permisos.

![alt text](<img/Imatge enganxada (69).png>)

Finalment provem el usuari Roig que directament no ens deixa ni entrar.

![alt text](<img/Imatge enganxada (88).png>)
