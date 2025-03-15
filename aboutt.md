# SPRINT 4

### RAID’s

##### Què és un RAID?

Un RAID (Redundant Array of Independent Disks) és una tecnologia que permet combinar múltiples discos durs en una única unitat lògica per millorar el rendiment, la redundància o ambdues coses alhora. Aquesta tècnica s’utilitza principalment en servidors i sistemes d’emmagatzematge per garantir la seguretat i l’eficiència de les dades.

##### Tipus de RAID:

Hi ha diversos tipus de RAID, cadascun amb característiques diferents segons les necessitats de l'usuari:

    RAID 0 (Striping): Divideix les dades en múltiples discos per augmentar el rendiment, però no ofereix redundància. Si un disc falla, es perden totes les dades.
    RAID 1 (Mirroring): Duplica les dades en dos discos per garantir la seguretat. Si un disc falla, l’altre continua funcionant.
    RAID 5: Reparteix les dades i la informació de paritat entre almenys tres discos. Ofereix un bon equilibri entre rendiment i redundància.
    RAID 6: Similar al RAID 5, però amb el doble de paritat, la qual cosa permet suportar la fallada de fins a dos discos.


## RAID 1


Primerament fem un `apt update`

![imagen](<img/Imatge enganxada (91).png>)

I comencem a instalar el paquet per als RAID.

![imagen](<img/Imatge enganxada (89).png>)

Fem un `fdisk -l`per a veure el discos que hem afegit.

![imagen](<img/Imatge enganxada (92).png>)

Entrem als discos i cambiem el sistemes de fitxer

![imagen](<img/Imatge enganxada (93).png>)

Ara fem un altre cop `fdisk -l` per comprovar que s'han fet els canvis.

![imagen](<img/Imatge enganxada (94).png>)

Creem la carpeta raid y li donem tots els permisos.

![imagen](<img/Imatge enganxada (95).png>)

Creem el RAID:

![imagen](<img/Imatge enganxada (96).png>)

Caviem el format:

![imagen](<img/Imatge enganxada (97).png>)

Per rebre informació del raid utilitzarem “mdadm –detail /dev/md0”

![imagen](<img/Imatge enganxada (98).png>)

Ara farem que el raid es munti automàticament anant al fitxer “/etc/mdadm.conf” i afegim la següent línia.

![imagen](<img/Imatge enganxada (99).png>)

I afegirem també una línia al fitxer /etc/fstab

![imagen](<img/Imatge enganxada (100).png>)

Un cop aplicats els canvis reiniciem:

![imagen](<img/Imatge enganxada (101).png>)

Un cop s'hagi iniciat novament la màquina per comprovar que tot ha funcionat correctament farem un detail “mdadm –detail /dev/md0”

![imagen](<img/Imatge enganxada (102).png>)

Ara per fer les proves crearem una carpeta i un fitxer dins

![imagen](<img/Imatge enganxada (103).png>)


Ara farem fallar un dels discos per comprovar que passa “mdadm /dev/md0 -f /dev/sdb1”

![imagen](<img/Imatge enganxada (104).png>)

Hauria de sortir així en un detail

![imagen](<img/Imatge enganxada (105).png>)

Ara creem una carpeta comprovar que podem treballar amb un sol disc

![imagen](<img/Imatge enganxada (106).png>)

Ara traurem el disc que falla com es fa en màquines fisiques, es farà amb l'ordre “mdadm /dev/md0 -r /dev/sdb1”

![imagen](<img/Imatge enganxada (108).png>)

Reiniciem i comprovem que esta actiu:

![imagen](<img/Imatge enganxada (110).png>)

Ara eliminem el disc per comprovar com abans (amb la maquina apagada):

![imagen](<img/Imatge enganxada (107).png>)

I podem comprovar que a la carpeta raid 1 no hi ha res

![imagen](<img/Imatge enganxada (109).png>)

Creem novament un altre disc.

![imagen](<img/Imatge enganxada (111).png>)

I mirem que esta el disc afegit.

![imagen](<img/Imatge enganxada (112).png>)

Afegim el disc amb `mdadm /dev/md0 -a /dev/sdb1`

![imagen](<img/Imatge enganxada (113).png>)

Ara veurem si funciona correctament després de fer un reboot.

![imagen](<img/Imatge enganxada (114).png>)

Ara desmuntem el raid i fem un stop també eliminem la carpeta de `/mnt/raid1` (no vaig fer captura)

Comentem la linia que vam afegir.

![imagen](<img/Imatge enganxada (115).png>)

I borrem el interior de  `etc/mdadm.conf`

![imagen](<img/Imatge enganxada (116).png>)


## RAID 5

Per a raid 5 haurem d'afegir 4 discos durs.

![imagen](<img/Imatge enganxada (117).png>)


![imagen](<img/Imatge enganxada (118).png>)

Hem d'entrar dins de cada disc per canviar el sistema de fitxers de cadascun.


![imagen](<img/Imatge enganxada (119).png>)


![imagen](<img/Imatge enganxada (120).png>)


![imagen](<img/Imatge enganxada (121).png>)


![imagen](<img/Imatge enganxada (122).png>)

fem un `fdisk -l` per comprovar que surten els discos que hem canviat i verificar que esta tot bé.

![imagen](<img/Imatge enganxada (123).png>)

![imagen](<img/Imatge enganxada (124).png>)

Creem la carpeta on es formarà el raid i apliquem els permisos per fer-la servir.

![imagen](<img/Imatge enganxada (125).png>)


![imagen](<img/Imatge enganxada (127).png>)

Creem el RAID amb aquesta comanda:

`mdadm –create /dev/md0 –level=5 –raid-devices=4 /dev/sdb1 /dev/sdc1 /dev/sdd1 /dev/sde1`

I cambiem el format per utilitzar-lo.

![imagen](<img/Imatge enganxada (128).png>)

Per rebre informació de raid utilitzarem `mdadm –detail /dev/md0`

![imagen](<img/Imatge enganxada (129).png>)


Ara farem que el –detail –scan se'n vagi a una carpeta en un .txt que nosaltres li indicarem

![imagen](<img/Imatge enganxada (130).png>)

Farem que el raid es munti automàticament anant al fitxer /etc/mdadm/mdadm.conf i afegim la següent línia

![imagen](<img/Imatge enganxada (131).png>)

A `/etc/fstab` afegim l'ultima linea.

![imagen](<img/Imatge enganxada (132).png>)

#### Abans de fer el reboot apliquem aquestes comandes:

![imagen](<img/Imatge enganxada (133).png>)

Un cop s'hagi iniciat novament la màquina comprovem que tot ha funcionat correctament farem un `mdadm --detail /dev/md0`

![imagen](<img/Imatge enganxada (134).png>)

Ara per fer les proves crearem una carpeta i un fitxer dins.

![imagen](<img/Imatge enganxada (135).png>)

Ara farem fallar un dels discs per comprovar què passa mdadm /dev/md0 -f /dev/sdb1.

![imagen](<img/Imatge enganxada (136).png>)

Comprovem amb `mdadm --detail /dev/md0` que realment esta fallant.

![imagen](<img/Imatge enganxada (137).png>)


`mdadm /dev/md0 -r /dev/sdb1` amb aquesta comanda treurem el disc que falla.

![imagen](<img/Imatge enganxada (138).png>)

Comprovem amb un detail i surt "removed" esta bé.

![imagen](<img/Imatge enganxada (139).png>)

Ara per comprovar que podem treballar amb un disc menys crearem novament un altra carpeta.

![imagen](<img/Imatge enganxada (140).png>)

Ara quitem un altre disc.

![imagen](<img/Imatge enganxada (141).png>)

![imagen](<img/Imatge enganxada (142).png>)

![imagen](<img/Imatge enganxada (143).png>)

![imagen](<img/Imatge enganxada (144).png>)

fem un ls i comprovem que funciona.

![imagen](<img/Imatge enganxada (145).png>)

Continua funcionant, per la qual cosa sortirem de la màquina i traurem els discos de la mateixa per comprovar què passa.

![imagen](<img/Imatge enganxada (146).png>)


Comprovem i fem novament un detail.

![imagen](<img/Imatge enganxada (147).png>)

I podem confirmar que ja no funciona

![imagen](<img/Imatge enganxada (148).png>)

