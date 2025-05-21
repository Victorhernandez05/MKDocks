## Sprint 5 Windows

### Monitorització de Recursos

La gestió d’un sistema Windows Server implica monitoritzar el rendiment, garantir la seguretat i centralitzar la instal·lació i actualització de sistemes. Es fan servir eines natives com el Monitor de Rendiment, el Visualitzador de Recursos i el Gestor de Tasques per controlar la CPU, memòria, disc i xarxa, configurant alertes per detectar problemes i aplicar solucions eficaces.


A més, es configura una auditoria que registra accessos i modificacions, tant exitosos com fallits, per detectar anomalies i garantir la seguretat sense afectar massa el rendiment.


Per facilitar la instal·lació i manteniment, s’implanta un servidor FOG que permet capturar i desplegar imatges de Windows Server de manera automatitzada i desatesa, incloent scripts de postinstal·lació per aplicar configuracions i programari addicional. Això assegura una gestió eficient i ràpida, amb possibilitat de reinstal·lacions en cas d’error.


### 1. Monitoritzar el sistema per identificar problemes de rendiment

    Pas 1: Obre el Monitor de Rendiment (Performance Monitor) de Windows Server.

![imagen](img/Imatge enganxada (300).png)



    Pas 2: Selecciona els comptadors rellevants per a CPU (percentatge d’ús), memòria (ús de memòria física, paginació), disc (activitats de lectura/escriptura, temps d’espera) i xarxa (bytes enviats/rebuts, errors).

![imagen](img/Imatge enganxada (302).png)


![imagen](img/Imatge enganxada (301).png)


    Pas 3: Configura alertes perquè t’avisin quan es superin certs llindars, per exemple CPU > 80%, temps d’espera del disc elevat, etc.

![imagen](img/Imatge enganxada (303).png)

![imagen](img/Imatge enganxada (304).png)


    Pas 4: Executa el Visualitzador de Recursos per obtenir una vista en temps real de l’ús dels recursos i detectar processos que consumeixen massa.


![imagen](img/Imatge enganxada (305).png)

![imagen](img/Imatge enganxada (306).png)



    Pas 5: Utilitza el Gestor de Tasques per supervisar processos i serveis actius.

![imagen](img/Imatge enganxada (307).png)



### 2. Realitzar auditories per a l’ús i accés a recursos, assegurant la seguretat del sistema

    Pas 1: Configura la Política d’Auditoria de Windows per registrar esdeveniments rellevants:

        Dins de Directives locals, selecciona Política d'auditoria (Audit Policy).

        A la dreta apareixeran opcions com:

            Auditar accés a objectes (Audit object access)

            Auditar inici de sessió (Audit logon events)

            Auditar ús de privilegis (Audit privilege use)

![imagen](img/Imatge enganxada (308).png)

    Pas 2: Auditar carpetes/fitxers específics

        Obre l’Explorador de fitxers i ves a la carpeta que vols monitoritzar.

        Clic dret > Propietats.

        Pestanya Seguretat > Opcions avançades.

        Pestaña Auditoria > Afegir.

            Selecciona Un usuari o grup > escriu per exemple Everyone o un usuari concret.

            Defineix els permisos que vols auditar, com Lectura, Escriptura, Eliminar, etc.

            Aplica i tanca totes les finestres.


![imagen](img/Imatge enganxada (309).png)


    Pas 3: Visualitzar esdeveniments d'auditoria

        Prem Windows + R, escriu eventvwr.msc i prem Enter.

        Ves a:

        Registres de Windows > Seguretat.

        Aquí veuràs els esdeveniments generats per les accions que has configurat:

            Inicis de sessió correctes o fallits.

            Accés a fitxers.

            Canvis de permisos.

![imagen](img/Imatge enganxada (310).png)


