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

Primerament fem un `apt update`

![imagen](<img/Imatge enganxada (91).png>)

I comencem a instalar el paquet per als RAID.

![imagen](<img/Imatge enganxada (89).png>)

Fem un `fdisk -l`per a veure el discos que hem afegit.

![imagen](img/Imatge enganxada (92).png)

Entrem als discos i cambiem el sistemes de fitxer

![imagen](img/Imatge enganxada (93).png)

Ara fem un altre cop `fdisk -l` per comprovar que s'han fet els canvis.

![imagen](img/Imatge enganxada (94).png)

Creem la carpeta raid y li donem tots els permisos.

![imagen](img/Imatge enganxada (95).png)

Creem el RAID:

![imagen](img/Imatge enganxada (96).png)

Caviem el format:

![imagen](img/Imatge enganxada (97).png)

Per rebre informació del raid utilitzarem “mdadm –detail /dev/md0”

![imagen](img/Imatge enganxada (98).png)

Ara farem que el raid es munti automàticament anant al fitxer “/etc/mdadm.conf” i afegim la següent línia.

![imagen](img/Imatge enganxada (99).png)

I afegirem també una línia al fitxer /etc/fstab

![imagen](img/Imatge enganxada (100).png)

Un cop aplicats els canvis reiniciem:

![imagen](img/Imatge enganxada (101).png)

Un cop s'hagi iniciat novament la màquina per comprovar que tot ha funcionat correctament farem un detail “mdadm –detail /dev/md0”

![imagen](img/Imatge enganxada (102).png)

Ara per fer les proves crearem una carpeta i un fitxer dins

![imagen](img/Imatge enganxada (103).png)


Ara farem fallar un dels discos per comprovar que passa “mdadm /dev/md0 -f /dev/sdb1”

![imagen](img/Imatge enganxada (104).png)

Hauria de sortir així en un detail

![imagen](img/Imatge enganxada (105).png)

Ara creem una carpeta comprovar que podem treballar amb un sol disc

![imagen](img/Imatge enganxada (106).png)

Ara traurem el disc que falla com es fa en màquines fisiques, es farà amb l'ordre “mdadm /dev/md0 -r /dev/sdb1”

![imagen](img/Imatge enganxada (108).png)

Reiniciem i comprovem que esta actiu:

![imagen](img/Imatge enganxada (110).png)

Ara eliminem el disc per comprovar com abans (amb la maquina apagada):

![imagen](img/Imatge enganxada (107).png)

I podem comprovar que a la carpeta raid 1 no hi ha res

![imagen](img/Imatge enganxada (109).png)

Creem novament un altre disc.

![imagen](img/Imatge enganxada (111).png)

I mirem que esta el disc afegit.

![imagen](img/Imatge enganxada (112).png)

Afegim el disc amb `mdadm /dev/md0 -a /dev/sdb1`

![imagen](img/Imatge enganxada (113).png)

Ara veurem si funciona correctament després de fer un reboot.

![imagen](img/Imatge enganxada (114).png)

Ara desmuntem el raid i fem un stop també eliminem la carpeta de `/mnt/raid1` (no vaig fer captura)

Comentem la linia que vam afegir.

![imagen](img/Imatge enganxada (115).png)

I borrem el interior de  `etc/mdadm.conf`

![imagen](img/Imatge enganxada (116).png)
