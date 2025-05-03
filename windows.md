
### SPRINT 1: Instal·lació i Configuració Inicial

#### Instal·lació SO

Crear una màquina virtual amb VirtualBox i muntar la ISO de Windows 10.


![imagen](img/Imatge enganxada (174).png)

Assignar 2-4 GB de RAM.

![imagen](img/Imatge enganxada (175).png)

1-2 CPUs.

![imagen](img/Imatge enganxada (176).png)

60 GB d'espai en disc (dinàmic o fix).

![imagen](img/Imatge enganxada (177).png)


Mode de xarxa: NAT o Bridge.

![imagen](img/Imatge enganxada (178).png)


Iniciar la instal·lació i seguir els passos:

![imagen](img/Imatge enganxada (179).png)

![imagen](img/Imatge enganxada (180).png)


Regió: Espanya.
![imagen](img/Imatge enganxada (181).png)

Un cop fet aquest punt, ja tenim la maquina operativa.


#### Punts de restauració

Un punt de restauració és una còpia de seguretat de l’estat del sistema operatiu que Windows crea automàticament (o manualment) en certs moments.

##### Què guarda un punt de restauració?

    Fitxers del sistema.

    Configuracions del registre.

    Controladors (drivers).

    Alguns programes instal·lats.

No inclou: documents personals, fotos, vídeos ni altres fitxers d’usuari.


##### Per a què serveix?

Serveix per tornar l’equip a un estat anterior si alguna cosa surt malament, per exemple:

    Un programa o driver causa errors o pantalla blava.

    Una actualització fa que el sistema deixi de funcionar bé.

Activar la protecció del sistema:

![imagen](img/Imatge enganxada (182).png)

![imagen](img/Imatge enganxada (183).png)

![imagen](img/Imatge enganxada (184).png)

Panell de control > Sistema > Protecció del sistema.

Crear un punt de restauració manual.

![imagen](img/Imatge enganxada (185).png)

![imagen](img/Imatge enganxada (186).png)

![imagen](img/Imatge enganxada (187).png)

![imagen](img/Imatge enganxada (188).png)

#### Llicències

Una llicència de programari és un permís legal que et permet instal·lar i utilitzar un sistema operatiu (com Windows) o una aplicació. Sense una llicència vàlida, el programari pot funcionar de manera limitada 


##### Funcions d’una llicència

    Autoritza l’ús del programari.

    Estableix quants dispositius poden utilitzar-lo.

    Defineix si es pot transferir a altres equips.

    Marca les condicions d’ús (entorn domèstic, empresarial, educatiu...).

##### Llicència OEM (Original Equipment Manufacturer)

Què és?

    És la llicència que ve preinstal·lada en ordinadors nous (ex: portàtils Dell, HP...).

    Està associada al maquinari (a la placa base) del dispositiu on es va instal·lar per primera vegada.

Característiques:

    No es pot transferir a un altre equip.

    Més barata que altres tipus de llicència.

##### Llicència Retail 

Què és?

    És la llicència que compres tu mateix, ja sigui en format físic (caixa amb clau de producte) o digital (Microsoft Store, Amazon...).

     Característiques:

    Transferible a altres ordinadors (només pot estar activa en un a la vegada).

    Permet reactivar en un nou dispositiu si l’anterior ja no s’usa.

##### Llicència de Volum (Volume Licensing)

Què és?

    És una llicència per a múltiples equips sota una mateixa empresa o organització.

    Gestionada mitjançant sistemes com KMS (Key Management Service) o MAK (Multiple Activation Key).

    Característiques:

    Permet activar diversos equips amb una sola clau.

    Ideal per a organitzacions grans.

##### Llicència Educacional

Què és?

    És una llicència especial per a estudiants, docents i centres educatius.

    S’obté mitjançant acords amb Microsoft, com Azure for Education o DreamSpark/Imagine (ara Microsoft Learn for Students).

     Característiques:

    Pot ser gratuïta o amb descompte.

    Legal per a ús en màquines virtuals i pràctiques acadèmiques.


#### Virtualització

La virtualització és una tecnologia que permet crear una versió simulada d’un entorn informàtic.

 Com funciona?

    S’utilitza un programa especial anomenat hipervisor (com VirtualBox o Hyper-V).

    Aquest programa crea màquines virtuals (VM), que són "ordinadors virtuals" dins del teu ordinador real.

![imagen](img/Imatge enganxada (189).png)

![imagen](img/Imatge enganxada (190).png)

![imagen](img/Imatge enganxada (191).png)

![imagen](img/Imatge enganxada (192).png)




#### Gestor arrencada


Els gestors d’arrencada (bootloaders) són programes que s’executen quan encens l’ordinador, abans que el sistema operatiu carregui. La seva funció principal és carregar el sistema operatiu a la memòria RAM 
 
Funcions principals d’un gestor d’arrencada:

    Detectar i carregar el sistema operatiu (Windows, Linux, etc.).

    Gestionar diferents particions i sistemes operatius (multi-boot).

Components relacionats:

    MBR (Master Boot Record): És l'àrea inicial del disc dur que conté el primer codi executat i la taula de particions.

    UEFI (substitut del BIOS): Porta integrat el seu propi gestor d’arrencada més avançat i segur.


Tipus de gestors d’arrencada més comuns:

Windows Boot Manager (BOOTMGR)

Característiques: Gestor natiu de Windows, carrega winload.exe.

GRUB (GRand Unified Bootloader)

Característiques: Permet triar entre múltiples SO. Altament configurable.


#### Xarxa bàsica

Què és la xarxa bàsica?

Una xarxa bàsica és la infraestructura mínima necessària per connectar dos o més dispositius (ordinadors, impressores, servidors...)
Es basa en l'ús de protocols com TCP/IP i pot ser física (cables, switches) o (Wi-Fi).

PAN (Personal Area Network) Exemple: Bluetooth o USB.

LAN (Local Area Network) Exemple: Xarxa d’un institut o empresa petita.

WLAN (Wireless LAN) Exemple: Xarxa Wi-Fi de casa o d’un bar.

MAN (Metropolitan Area Network) Exemple: Xarxa d’una universitat amb diversos edificis.


###### Tres explicacions clares i adaptades sobre configuració de xarxa en la nostra màquina virtual.

Xarxa NAT (Network Address Translation)

![imagen](img/Imatge enganxada (193).png)

Característiques:

    Ideal per a connexió a Internet ràpida i sense configurar res.

    No permet connexió directa des d’altres dispositius de la xarxa física cap a la màquina virtual.

    IP assignada per un servidor DHCP intern de la màquina host.

Ús recomanat:
Per fer proves de navegació, actualitzacions, o treballar de manera aïllada del món exterior.
 
Adaptador Pont (Bridge Adapter)

![imagen](img/Imatge enganxada (194).png)

Característiques:

    Permet connexió completa entre VM, ordinadors físics, impressores, etc.

    Apte per fer proves de serveis de xarxa reals (servidors DHCP, web, fitxers...).

    Pot tenir conflictes si hi ha filtres de MAC a la xarxa física.

Ús recomanat:
Per entorns col·laboratius, simulació de servidors reals o proves en xarxes de producció.



Adaptador només amfitrió (Host-Only Adapter)

![imagen](img/Imatge enganxada (195).png)


Característiques:

    Utilitzat per simular comunicació local sense exposar la VM a la xarxa exterior.

    Molt útil per a pràctiques de serveis interns o seguretat.

    Cal configurar manualment IPs o utilitzar un DHCP del host-only.

Ús recomanat:
Proves de xarxa controlades, escenaris de formació o pràctiques sense risc de connexions externes.

Tipus de configuració de xarxa bàsica:

Configuració:

DHCP - Assigna automàticament IPs als dispositius connectats.

IP Estàtica - Assignació manual d’una IP fixa per a cada dispositiu.

DNS - Servei que tradueix noms (google.com) en adreces IP (8.8.8.8).


Configuració:

IP estàtica: Configurar manualment a "Canvia configuració de l'adaptador".

DHCP: Per defecte en mode NAT.

DNS: Manual o automàtic.

Grup de treball: Canviar nom del grup per treball col·laboratiu.

Verificació:

ipconfig

![imagen](img/Imatge enganxada (196).png)

Podem comprovar que la xarxa esta en mode NAT per la IP.

ping 8.8.8.8

![imagen](img/Imatge enganxada (197).png)

Tenim conexió a Internet fent ping a google.

ping nomPC

![imagen](img/Imatge enganxada (198).png)

Per últim comprovem que fa ping la nostra maquina.

#### Comandes generals

`ipconfig /all`:  Mostra informació avançada com MAC addresses i servidors DNS.


![imagen](img/Imatge enganxada (200).png)

`netstat`: Llista totes les connexions actuals.

![imagen](img/Imatge enganxada (201).png)

`tasklist`: Llista tots els processos amb el seu PID (ID del procés).

![imagen](img/Imatge enganxada (202).png)


`taskkill`: Permet tancar (terminar) un procés actiu.

![imagen](img/Imatge enganxada (203).png)


`systeminfo`: Ideal per recollir dades de informació del sistema.

![imagen](img/Imatge enganxada (204).png)


#### Instal·lació d'aplicacions

##### Google Chrome 

Passos:

Obre el navegador Microsoft Edge.

![imagen](img/Imatge enganxada (205).png)

Fes click en 'Baixa Chrome'.

![imagen](img/Imatge enganxada (206).png)

Li donem a Sí per a que s'executi.

![imagen](img/Imatge enganxada (207).png)

![imagen](img/Imatge enganxada (208).png)

Obre Google Chrome i comprova que funcioni correctament.

##### Instal·lació d'un Antivirus Gratuït (Exemple: Avast Free Antivirus)

Obre el navegador (pots usar Chrome ja instal·lat).

Accedeix a la web oficial d’Avast: `https://www.avast.com/free-antivirus-download`

Fes clic a Descargar Gratis.

![imagen](img/Imatge enganxada (209).png)

![imagen](img/Imatge enganxada (210).png)

Executa el fitxer descarregat (doble clic).

![imagen](img/Imatge enganxada (211).png)

Apreta Sí per al permís.

![imagen](img/Imatge enganxada (212).png)

Finalitza la instal·lació i reinicia si et demana.

![imagen](img/Imatge enganxada (213).png)

Per últim comprova que funciona corectament.