
### SPRINT 2: Gestio d'usuaris, serveis i emmagatzematge a Windows

#### 1. Gestio d'usuaris i grups


La gestió d'usuaris i grups a Windows és fonamental per controlar qui pot accedir al sistema i quines accions pot realitzar. Aquesta gestió permet crear comptes per a diferents usuaris, agrupar-los segons els rols o funcions, i aplicar permisos de manera centralitzada.

Els usuaris locals poden accedir al sistema amb el seu propi perfil, on tenen configuracions i fitxers personals. Els grups permeten aplicar permisos i configuracions a diversos usuaris alhora, facilitant l'administració en entorns amb múltiples comptes.

Les polítiques de seguretat associades als comptes (com ara la complexitat de les contrasenyes o la seva caducitat) ajuden a reforçar la protecció del sistema contra accessos no autoritzats.


#### Crear comptes d’usuari locals:

Obrir "Gestio d'equips" (compmgmt.msc).

![imagen](img/Imatge enganxada (214).png)


Anar a: Usuaris i grups locals > Usuaris.

Botó dret > Nou usuari...

![imagen](img/Imatge enganxada (215).png)


Assignar nom d’usuari, contrasenya.

Desmarcar "L'usuari ha de canviar la contrasenya..." si cal.

![imagen](img/Imatge enganxada (216).png)

#### Crear grups i assignar permisos:

A Grups, crear un grup nou o editar-ne un existent.

![imagen](img/Imatge enganxada (217).png)

Afegir usuaris segons rols: Administradors, Usuaris, Convidats, etc.

![imagen](img/Imatge enganxada (218).png)


🔐 Politiques de contrasenyes:

Obre secpol.msc (Directiva de seguretat local).

![imagen](img/Imatge enganxada (219).png)


Navega a: Directiva de comptes > Directiva de contrasenyes.

Longitud mínima: 8 caràcters.

![imagen](img/Imatge enganxada (220).png)


Complexitat: Activar.

![imagen](img/Imatge enganxada (221).png)


Caducitat: Opcional segons entorn.

#### 2. Administració de serveis i processos

⚙️ Gestio de serveis:

Obre services.msc.

![imagen](img/Imatge enganxada (222).png)

Revisa serveis com:

Windows Update, Superfetch, Windows Defender

Pots desactivar serveis innecessaris en entorns virtuals per optimitzar.




🏋️ Gestio de processos:

Obre el Gestor de tasques (Ctrl+Shift+Esc).

Revisa l'impacte en CPU, RAM.

Finalitza processos innecessaris (compte amb processos del sistema).

![imagen](img/Imatge enganxada (223).png)


#### 3. Gestio de discs, particions i sistemes de fitxers

🏛️ Crear particions amb Gestor de discos:

Crea un disc de minim 2 GB.

![imagen](img/Imatge enganxada (224).png)

Obre diskmgmt.msc.

![imagen](img/Imatge enganxada (225).png)


Clic dret sobre disc no assignat > Nou volum simple....

![imagen](img/Imatge enganxada (226).png)


Assignar lletra, format (NTFS, FAT32).

![imagen](img/Imatge enganxada (227).png)

![imagen](img/Imatge enganxada (228).png)

![imagen](img/Imatge enganxada (229).png)

![imagen](img/Imatge enganxada (230).png)

Comprova el volum.

Diskpart (CMD)

Escriu diskpart al cmd i executa.

![imagen](img/Imatge enganxada (231).png)

![imagen](img/Imatge enganxada (232).png)

`list disk`per mirar la llista de discos.

![imagen](img/Imatge enganxada (233).png)

`select disk N`s'utilitza per seleccionar el disc que vols.


#### 4. Estructura del sistema de fitxers

📁 Directoris principals:

C:\Windows\: Arxius del sistema operatiu.

![imagen](img/Imatge enganxada (234).png)


C:\Program Files: Aplicacions instal·lades (64 bits).

![imagen](img/Imatge enganxada (235).png)


⚙️ Fitxers de configuració importants:

C:\Windows\System32\config\: Base de dades del Registre.

![imagen](img/Imatge enganxada (236).png)


C:\Windows\System32\drivers\etc\hosts: Resolució de noms.

![imagen](img/Imatge enganxada (237).png)

C:\boot\BCD: Configuració d’arrencada.

![imagen](img/Imatge enganxada (238).png)


5. Quotes de disc i còpies de seguretat

♻️ Quotes de disc:

Obre Explorador de fitxers > clic dret sobre una unitat > Propietats > pestanya Quota.

Activa gestió de quotes.

![imagen](img/Imatge enganxada (239).png)


Defineix límits d’espai per usuari.

![imagen](img/Imatge enganxada (240).png)


📂 Sistema de còpies i restauració:

Activa la protecció del sistema: sysdm.cpl > pestanya Protecció del sistema.

Crea punts de restauració abans de canvis importants.

![imagen](img/Imatge enganxada (241).png)


Utilitza l’eina de Còpia de seguretat i restauració (Windows 7) o Historial de fitxers.

![imagen](img/Imatge enganxada (242).png)

![imagen](img/Imatge enganxada (243).png)

![imagen](img/Imatge enganxada (244).png)

Comprova que la copia de seguretat s'ha creat correctament en aquest cas cada diumenge a les 19:00.

![imagen](img/Imatge enganxada (245).png)


