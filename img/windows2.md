
### SPRINT 2: Gestió de processos, Gestio d'usuaris, serveis i emmagatzematge a Windows


#### Què és la gestió de processos?

La gestió de processos en Windows és el conjunt de funcions i mecanismes que el sistema operatiu utilitza per controlar i administrar l’execució dels processos (programari o aplicacions en execució) en el sistema.

    Procés: És una instància d’un programa en execució. Cada aplicació o servei que s’està executant al Windows 10 és un procés.

    Gestió de processos: Inclou la creació, execució, pausa, reactivació, i finalització de processos. També controla la seva memòria assignada, els recursos que utilitzen i la prioritat d’execució.

**Funcions principals:**

    Creació i terminació: Quan s’inicia un programa, Windows crea un procés; quan es tanca, s’elimina.

    Assignació de recursos: CPU, memòria, I/O, etc.

    Planificació: Decideix quin procés s’executa i quan, segons prioritat i disponibilitat.

    Control i supervisió: Detecta processos que consumeixen molts recursos o que no responen.

    Gestió de processos amb interfície gràfica a Windows 10

    Windows 10 proporciona eines visuals per veure i gestionar processos, les principals són:

**1. Administrador de tasques (Task Manager)**

    Permet veure tots els processos actius, el seu consum de CPU, memòria, disc i xarxa.

    Es pot accedir prement Ctrl + Shift + Esc o clicant amb el botó dret a la barra de tasques i seleccionant "Administrador de tasques".

![imagen](img/Imatge enganxada (293).png)

    Des de l’Administrador de tasques pots:

        Finalitzar processos que no responen.

        Veure l’ús dels recursos en temps real.

        Gestionar aplicacions que s’executen a l’inici.

        Canviar la prioritat d’un procés (prioritat de CPU).

**2. Monitor de recursos (Resource Monitor)**

    Eina més detallada que mostra informació exhaustiva de l’ús de CPU, memòria, disc i xarxa per procés.

    S’hi accedeix des de l’Administrador de tasques a la pestanya “Rendiment” > “Obrir Monitor de recursos”.

![imagen](img/Imatge enganxada (294).png)

![imagen](img/Imatge enganxada (295).png)


#### Gestió de processos en CMD 

La comanda `tasklist` de Windows és una eina de línia de comandes que mostra una llista dels processos actius al sistema, amb informació útil sobre cadascun.


![imagen](img/Imatge enganxada (296).png)

#### Finalitzar procés amb taskkill i PID

Busca el proces que vols finalitzar i executa `taskkill /IM nombre.exe /F`

![imagen](img/Imatge enganxada (297).png)

També existeix la opció de matar el process amb PID `taskkill /PID numero /F`

![imagen](img/Imatge enganxada (298).png)


Iniciar un procés/programa

Executa `start programa.exe` per obrir-lo.

![imagen](img/Imatge enganxada (299).png)


#### Gestió d’usuaris, grups i permisos amb ACLs a Windows

En el sistema Windows, cada fitxer i carpeta compta amb una llista de control d’accés (ACL - Access Control List) que determina qui té permís per accedir i quins tipus d’accés pot realitzar sobre aquests recursos.

Una ACL està composta per diverses entrades de control d’accés (ACE - Access Control Entry), i cada ACE especifica:

    Quin usuari o grup de usuaris es veu afectat.

    Quins permisos específics s’atorguen o es neguen, com ara lectura, escriptura, execució o control total.


Els permisos gestionats per les ACLs són molt més detallats i flexibles que els permisos bàsics de compartir carpetes, perquè:

    Permeten assignar permisos diferents a nivell de fitxer o carpeta individual.

    Es poden establir permisos per a usuaris i grups de manera combinada i amb diferents nivells.

    Inclouen opcions avançades, com permisos exclusius per llegir, modificar o eliminar fitxers, o controlar qui pot canviar els propis permisos.

    Poden heretar-se automàticament des d’una carpeta superior o definir-se de manera manual segons la necessitat.



#### Cas pràctic: Control d’accés a la carpeta DadesVendes

Objectiu:

    Assignar Control Total al grup VH sobre la carpeta DadesVendes.

    Assignar només Permís de Lectura a l’usuari Víctor, tot i ser membre del grup VH.

Pas 1: Crear el grup i afegir usuaris

    Obre Gestió d’Equips (clic dret a Aquest Equip → Gestionar → Usuaris i Grups Locals → Grups).
    

    Crea un grup nou anomenat 'VH'.

![imagen](img/Imatge enganxada (217).png)

![imagen](img/Imatge enganxada (218).png)

    Afegeix els usuaris que vulguis al grup Limitats, inclòs Víctor.

Pas 2: Assignar permisos a la carpeta DadesVendes

    Navega fins a la carpeta Dades\Vendes.

    Clic dret a la carpeta → Propietats → pestanya Seguretat.

    Clic a Editar per canviar permisos.

    Afegeix el grup VH.

    Per al grup VH, marca Control Total a "Permetre".

    Afegeix l'usuari alumne2 (si no està).

    Per a alumne2, marca només Lectura i Llistar contingut a "Permetre".

    Confirma i aplica els canvis.

Pas 3: Validar permisos

    Com a usuari limitat (dins el grup Limitats però diferent d’alumne2), comprova que pots crear, modificar i esborrar fitxers dins Projectes.

    Com a alumne2, comprova que només pots obrir i llegir fitxers, sense poder modificar-los ni esborrar-los.

Explicació tècnica:

    Els permisos heretats del grup Limitats donen control total.

    El permís explícit de alumne2 (només lectura) preval sobre el grup, per això només pot llegir.

    Això garanteix que encara que alumne2 sigui membre del grup amb permisos amplis, es limita el seu accés específicament.

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


Politiques de contrasenyes:

Obre secpol.msc (Directiva de seguretat local).

![imagen](img/Imatge enganxada (219).png)


Navega a: Directiva de comptes > Directiva de contrasenyes.

Longitud mínima: 8 caràcters.

![imagen](img/Imatge enganxada (220).png)


Complexitat: Activar.

![imagen](img/Imatge enganxada (221).png)


Caducitat: Opcional segons entorn.

#### 2. Administració de serveis i processos

Gestio de serveis:

Obre services.msc.

![imagen](img/Imatge enganxada (222).png)

Revisa serveis com:

Windows Update, Superfetch, Windows Defender

Pots desactivar serveis innecessaris en entorns virtuals per optimitzar.




Gestio de processos:

Obre el Gestor de tasques (Ctrl+Shift+Esc).

Revisa l'impacte en CPU, RAM.

Finalitza processos innecessaris (compte amb processos del sistema).

![imagen](img/Imatge enganxada (223).png)


#### 3. Gestio de discs, particions i sistemes de fitxers

Crear particions amb Gestor de discos:

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

Directoris principals:

C:\Windows\: Arxius del sistema operatiu.

![imagen](img/Imatge enganxada (234).png)


C:\Program Files: Aplicacions instal·lades (64 bits).

![imagen](img/Imatge enganxada (235).png)


Fitxers de configuració importants:

C:\Windows\System32\config\: Base de dades del Registre.

![imagen](img/Imatge enganxada (236).png)


C:\Windows\System32\drivers\etc\hosts: Resolució de noms.

![imagen](img/Imatge enganxada (237).png)

C:\boot\BCD: Configuració d’arrencada.

![imagen](img/Imatge enganxada (238).png)


5. Quotes de disc i còpies de seguretat

Quotes de disc:

Obre Explorador de fitxers > clic dret sobre una unitat > Propietats > pestanya Quota.

Activa gestió de quotes.

![imagen](img/Imatge enganxada (239).png)


Defineix límits d’espai per usuari.

![imagen](img/Imatge enganxada (240).png)


Sistema de còpies i restauració:

Activa la protecció del sistema: sysdm.cpl > pestanya Protecció del sistema.

Crea punts de restauració abans de canvis importants.

![imagen](img/Imatge enganxada (241).png)


Utilitza l’eina de Còpia de seguretat i restauració (Windows 7) o Historial de fitxers.

![imagen](img/Imatge enganxada (242).png)

![imagen](img/Imatge enganxada (243).png)

![imagen](img/Imatge enganxada (244).png)

Comprova que la copia de seguretat s'ha creat correctament en aquest cas cada diumenge a les 19:00.

![imagen](img/Imatge enganxada (245).png)


