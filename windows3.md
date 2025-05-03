### SPRINT 3: Implementació i Administració d'un Domini Windows

#### 1. 🚀 Què és un Domini Windows?

Un domini és una estructura centralitzada de xarxa gestionada per un servidor amb Active Directory. Permet administrar usuaris, equips, recursos i permisos de manera centralitzada, ideal per a entorns empresarials o escolars.

L'ordinador que gestiona el domini s'anomena controlador de domini (DC).

#### 2. 🔧 Implementar un domini amb Windows Server

Requisits previs:

    Windows Server instal·lat (recomanat: 2016, 2019 o 2022).

    Nom de la màquina configurat.

    IP estàtica assignada.

![imagen](img/Imatge enganxada (246).png)

##### Instal·lar el rol Active Directory Domain Services (AD DS)

    Obre el Server Manager.

    Fes clic a “Add roles and features”.

    Accepta les pantalles fins arribar a Server Roles.

![imagen](img/Imatge enganxada (247).png)

![imagen](img/Imatge enganxada (248).png)

![imagen](img/Imatge enganxada (249).png)


    Marca “Active Directory Domain Services”.

    Accepta les funcions addicionals que demani.

    Finalitza i clica “Install” (no cal reiniciar encara).

![imagen](img/Imatge enganxada (250).png)

![imagen](img/Imatge enganxada (251).png)

![imagen](img/Imatge enganxada (252).png)

![imagen](img/Imatge enganxada (253).png)

Passos bàsics:

Instal·lar el rol Active Directory Domain Services (AD DS).

Promoure el servidor com a controlador de domini.

Crear un nou domini (ex: empresa.local).

![imagen](img/Imatge enganxada (254).png)

![imagen](img/Imatge enganxada (255).png)

![imagen](img/Imatge enganxada (256).png)

![imagen](img/Imatge enganxada (257).png)


Reiniciar el sistema i verificar la funcionalitat.

![imagen](img/Imatge enganxada (258).png)

#### 3. 👥 Administració de comptes d'usuari i equips
##### 1. Crear comptes d’usuari al domini
🔧 Eina: Active Directory Users and Computers (dsa.msc)

    Obre Server Manager > Tools > Active Directory Users and Computers.

![imagen](img/Imatge enganxada (259).png)

    A la part esquerra, desplega el domini (ex: empresa.local).

    Fes clic dret sobre la carpeta Users (o una Unitat Organitzativa que hagis creat) > New > User.

![imagen](img/Imatge enganxada (260).png)


    Introdueix:

        Nom i cognoms

        Nom de login 

    Assigna una contrasenya i configura:

        Pots forçar canvi de contrasenya en el primer inici de sessió.

        Desactiva l’opció si vols una contrasenya fixa per fer proves.

![imagen](img/Imatge enganxada (261).png)

![imagen](img/Imatge enganxada (262).png)

##### 2. Crear grups per gestionar permisos de forma col·lectiva

    A Active Directory Users and Computers, clica dret sobre Users > New > Group.

    Escriu el nom del grup.

![imagen](img/Imatge enganxada (263).png)


    Tipus: Security | Àmbit: Global.

    Un cop creat, obre el grup > pestanya Members > Add per afegir usuaris

![imagen](img/Imatge enganxada (264).png)


#### 4. 🧲 Perfils mòbils i carpetes personals

Què són?

Perfil mòbil: L'entorn personal (escriptori, configuració...) es desa al servidor i es carrega a qualsevol equip del domini.

Carpeta personal (home folder): Espai al servidor on l'usuari desa els seus fitxers.

🗂️ Crear les carpetes al servidor

    A l’Explorador de fitxers del servidor:

        Crea una carpeta:

    C:\PerfilsMòbils  
    C:\CarpetesUsuaris  

Fes clic dret > Propietats > pestanya Compartir.

Fes clic a “Compartir avançat”:

![imagen](img/Imatge enganxada (266).png)

    Marca Compartir aquesta carpeta.

![imagen](img/Imatge enganxada (265).png)

Assigna un nom.

A Permisos, dóna control total.

Aplica i tanca.

**Solució: Permetre inici de sessió interactiva al client**

Inicia sessió amb l’administrador local del PC (no del domini).

Obre (Administració de directiva de grup).

Un cop dins de l’editor de polítiques:

Configuración del equipo >
Configuración de Windows >
Configuración de seguridad >
Directivas locales >
Asignación de derechos de usuario

Cerca “Permitir el inicio de sesión local” i fes-hi doble clic.

Fes clic a Agregar usuario o grupo.

Clica Comprobar nombres, després Aceptar.

Aplica els canvis i tanca l’editor.
![imagen](img/Imatge enganxada (267).png)

Prova iniciar sessió.

#### 5. 🛡️ Grups de seguretat i permisos

##### 1. 👥 Crear un grup de seguretat a Active Directory

    Obre (Active Directory Users and Computers).

    A la OU o carpeta Users, fes clic dret > New > Group.

    Dona-li un nom clar, per exemple:

    Departament_Local

    Tipus de grup: Security

    Àmbit del grup: Global

    Clica OK.

##### 2. ➕ Afegir usuaris al grup

    Obre el grup creat > Pestanya Members > Add.

    Escriu els noms d’usuari.

    Clica Comprobar nombres i després Aceptar.

![imagen](img/Imatge enganxada (268).png)

##### 3. 📁 Crear una carpeta compartida al servidor i aplicar permisos

    Al servidor, crea una carpeta:

C:\DadesVendes

Botó dret > Propietats > Compartir > Compartir avançat.

    Marca “Compartir aquesta carpeta”.

    Dona-li el nom: Vendes.

A Permisos de compartició:

    Elimina Tots.

    Afegeix el grup DepartamentVendes > Dona-li Control total.
![imagen](img/Imatge enganxada (269).png)

A la pestanya Seguretat (NTFS):

    Fes el mateix: afegeix el grup i assigna permisos.
    
![imagen](img/Imatge enganxada (270).png)


#### 6. 🔐 Directives de seguretat i drets d'usuari

##### 1. 🧭 Obrir el gestor de directives de grup

Al servidor:

    Obre gpmc.msc (Group Policy Management Console).

    Selecciona el domini (Victor.local) o una Unitat Organitzativa (OU).

    Crea una nova GPO o edita una ja vinculada:

        Botó dret > Crear GPO y vincularla aquí...

        Nom: Seguretat_Usuaris

##### 2. 🔐 Exemple de configuració de directives de seguretat

Complexitat i caducitat de contrasenyes

    Edita la GPO creada.

    Ves a:

    Configuración del equipo >
    Configuración de Windows >
    Configuración de seguridad >
    Directivas de cuenta >
    Directiva de contraseñas

    Configura:

        Longitud mínima: 8 caràcterers

![imagen](img/Imatge enganxada (271).png)


Permetre inici de sessió local

    Ves a:

Configuración del equipo >
Configuración de Windows >
Configuración de seguridad >
Directivas locales >
Asignación de derechos de usuario

Obre: Permitir el inicio de sesión local

Afegeix:

    Usuarios del dominio

    O grups concrets com DepartamentLocal

![imagen](img/Imatge enganxada (272).png)



#### 7. 📁 Accés a recursos locals i de xarxa

##### 1. 📂 Compartir una carpeta des del servidor

    Crea una carpeta al servidor:

    C:\DepartamentTecnologia

    Clic dret > Propietats > Compartir > Compartir avançat.

        Marca Compartir aquesta carpeta.

        Nom del recurs compartit: Tecnologia.

    Fes clic a Permisos:

        Elimina Tots.

        Afegeix el grup corresponent.

        Dona Control total.


![imagen](img/Imatge enganxada (273).png)

##### 2. 🛡️ Configurar permisos NTFS (seguretat)

    A la pestanya Seguretat, fes clic a Editar.

    Afegeix el mateix grup de seguretat.

    Assigna permisos.

    Aplica i tanca.

![imagen](img/Imatge enganxada (274).png)

##### 3. 🖨️ Compartir una impressora 

    A Configuració > Dispositius > Impressores i escàners, selecciona una impressora instal·lada.

    Fes clic a Gestionar > Propietats de la impressora > Compartir.

    Marca Compartir aquesta impressora i posa-li un nom clar.

    Dona permisos des de la pestanya Seguretat (igual que amb les carpetes).
Compartició (accés en xarxa)

![imagen](img/Imatge enganxada (275).png)

##### 4. 📜 Aplicar connexions de xarxa automàticament (GPO)

    A la GPO activa (gpmc.msc) ves a:

Configuración del usuario >
Preferencias >
Configuración de Windows >
Unidades

Clic dret > Nuevo > Unidad asignada.

Configura:

    Ruta: \\srv-victor\Tecnologia

    Unidad: Z:

![imagen](img/Imatge enganxada (276).png)


#### 8. 🧰 Servidors de fitxers, impressió i aplicacions
##### Crear una carpeta compartida amb permisos:

    Crea una carpeta, ex:

C:\Dades Compartides

Botó dret > Propietats > Compartir > Compartir avançat.

Marca Compartir aquesta carpeta, nom del recurs: Dades.

A Permisos, afegeix:

    Grup de seguretat del domini (ex: Departament_Local)

    Dona permisos de lectura/escriptura segons el cas.

![imagen](img/Imatge enganxada (277).png)

A la pestanya Seguretat (NTFS), fes el mateix.

![imagen](img/Imatge enganxada (278).png)

##### Servidor d’impressió

✅ Com compartir una impressora:

    Connecta una impressora al servidor o instal·la’n una virtual.

    Ves a Configuració > Dispositius > Impressores i escàners.

    Selecciona la impressora > Gestionar > Propietats de la impressora > Compartir.

    Marca Compartir aquesta impressora, i dóna-li un nom (ex: Impresora).

    A la pestanya Seguretat, afegeix grups d’usuaris amb permís per imprimir.

![imagen](img/Imatge enganxada (279).png)

🧪 Des d’un client:

    A Dispositius i impressió > Afegir impressora > Buscar en xarxa o escriure:

\\VICTOR\Impresora

![imagen](img/Imatge enganxada (280).png)


##### 3. Servidor d’aplicacions

Exemple senzill: compartir instal·lador d’Office.

    Crea una carpeta al servidor:

C:\Aplicacions

Copia-hi els instal·ladors.

Dona permisos només de lectura als grups autoritzats.

![imagen](img/Imatge enganxada (281).png)



#### 9. 🚄 Connexió remota i administració

##### 1. Activar l’Escriptori remot al servidor

    A la màquina Windows Server:

        Inici > Sistema > Configuración avanzada del sistema

        Pestanya “Acceso remoto”

    Marca:

    Permitir las conexiones remotas a este equipo

    Pots deixar desmarcada l’opció de “Solo con NLA” si és per proves.

    Aplica els canvis.

![imagen](img/Imatge enganxada (282).png)

##### 2. Autoritzar usuaris a connectar-se

    A la mateixa finestra (Acceso remoto), fes clic a:

Seleccionar usuarios...

Afegeix usuaris del domini que vulguis que tinguin accés remot al servidor.

Exemple:

VICTOR\Administrador
VICTOR\Alberto

Aplica i tanca.

![imagen](img/Imatge enganxada (283).png)

 3. Verificar la IP del servidor

Obre una consola al servidor i escriu:

`ipconfig`

![imagen](img/Imatge enganxada (284).png)


 4. Connectar des d’un client

Des del client Windows:

    Premeu Win + R > escriu mstsc.

    A l’eina Escritorio remoto, escriu la IP del servidor.

Quan et demani credencials, escriu:

VICTOR\Alberto

Accepta l’avís de certificat si apareix.

![imagen](img/Imatge enganxada (285).png)


#### 10. ⛔️ Seguretat i protecció d'accés


##### 1. Polítiques de contrasenya i bloqueig
✅ Configura-ho des d’una GPO:

    Obre gpmc.msc al servidor.

    Edita o crea una GPO i ves a:

Configuración del equipo >
Configuración de Windows >
Configuración de seguridad >
Directivas de cuenta >
Directiva de contraseñas

Longitud mínima de contraseña	8 caràcters

![imagen](img/Imatge enganxada (286).png)

##### 2. Aplicar tallafocs i antivirus
✅ Tallafocs:

    Assegura’t que el Firewall de Windows està actiu:

        Panel de control > Sistema y seguridad > Firewall de Windows Defender

    Si tens antivirus de tercers, comprova que no el desactivi.

![imagen](img/Imatge enganxada (287).png)


✅ Antivirus:

    Si no tens un de pagament, pots usar Microsoft Defender (actiu per defecte).

    Comprova que les actualitzacions estan actives:

        Configuración > Actualización y seguridad > Seguridad de Windows > Protección contra virus y amenazas

![imagen](img/Imatge enganxada (288).png)


##### 3. Limitar accessos a recursos
✅ Carpeta o impressora compartida:

    A les propietats > seguretat, assegura’t que només hi accedeixen els grups de seguretat necessaris.

    Elimina Tots si hi és per defecte.

![imagen](img/Imatge enganxada (289).png)


##### 4. Documentar i registrar accions

Activa l’auditoria d’esdeveniments per detectar accés no autoritzat:

    A la GPO, ves a:

    Configuración del equipo >
    Configuración de Windows >
    Configuración de seguridad >
    Directiva local >
    Directiva de auditoría

    Activa:

        Auditoría de inicios de sesión

        Auditoría de acceso a objetos

![imagen](img/Imatge enganxada (290).png)

![imagen](img/Imatge enganxada (291).png)

Els resultats es registraran al Visor d’esdeveniments (eventvwr.msc).

![imagen](img/Imatge enganxada (292).png)
