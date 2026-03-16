## Descripció de l'activitat
Heu de documentar cada pas com si fos un informe tècnic d'implementació per al client. Abans de començar a realitzar les diferents accions, repenseu l’estructura d’unitats organitzatives (OU) que vau presentar inicialment al client, és possible que algun canvi us simplifiqui les accions que caldrà realitzar.

1. Polítiques de Seguretat i Contrasenyes (Seguretat Corporativa)

- El client exigeix endurir la política de contrasenyes per evitar accessos no autoritzats:
- Política Global: Modifiqueu la Default Domain Policy perquè tots els membres del grup personal (és a dir, tot el domini) hagin de tenir una contrasenya de, com a mínim, 8 caràcters.

Per fer-ho entrem a Group policy management

![](img/01.png)

Seguidament, despleguem fins trobar el default domain i el editem.

![](img/02.png)

Per anar a la configuració de la contrasenya anem fins a password policy del computer configuration.

![](img/03.png)

Dins anem a relax minimum password length limits i el definim posant-lo en enabled i apliquem el canvi.

![](img/04.png)

I seguidament posem que com a mínim la password sigui de 8 caràcters.

![](img/05.png)

- Política per a Gerència: La Unitat Organitzativa (OU) on ubiqueu la direcció conté els usuaris VIP (grup gerencia). Creeu una GPO específica per ells on la contrasenya sigui de 18 caràcters i caduqui cada 28 dies. No s'ha d'activar la complexitat.

Per fer aquest punt tornem a on abans i anem l'apartat de grups fem clic dret i posem la primera opció.

![](img/06.png)

Li posem el nom per crear-ho.

![](img/07.png)

Un cop creat l'editem, anem dins del password policy d'abans, però en des de l’edició del GPO creat anteriorment i editem el relax minmum password… com hem fet abans.

![](img/08.png)

Seguidament, canviem el nombre de caràcters de la password a 18. Tota queda així:

![](img/09.png)

Seguidament, editem el maximum password age i li posem 28 dies.

![](img/10.png)

I editem el mínim perquè sigui 1 dia. Queda així:

![](img/11.png)

- Millora Proactiva (Bonus): Com a consultors experts, heu de proposar i implementar una tercera GPO que considereu útil per a una empresa logística (ex: bloqueig de pantalla automàtic per als usuaris de magatzem per seguretat, fons d'escriptori corporatiu, etc.). Justifiqueu per què l'heu triat.

2. Desplegament Automatitzat de Programari

Per reduir els tiquets de suport tècnic, automatitzareu la instal·lació d'eines segons el departament:

Departament de Gestió: Els administratius (grup gestio) necessiten l'eina de compressió 7zip per gestionar factures. Creeu una GPO per desplegar-la de forma assignada (s'instal·la automàticament).

Creem una carpeta nova que es digui Software en el disc que havíem creat.

![](img/12.png)

Ara dins de les propietats de la carpeta en l’apartat de sharing, la compartim.

![](img/13.png)

Després dins en el desplegable posem everyone i l'afegim i enviem.

![](img/14.png)

Seguidament, descarregarem el 7-zip, el que es .msi de 64 bits. Un cop descarregat el traslladem a la carpeta que hem creat i compartit.

![](img/15.png)

Ara anirem dins de Group Polici Management, Domains, translogic17.test, fem clic dret i creem un altre GPO, li posem de nom 7-zip.

![](img/16.png)

Ara dins del GPO creat dins de l’apartat de security filtering posem add.

![](img/17.png)

I posem el grup de gestio.

![](img/18.png)

Podem treure el Authenticated Users, ja que no fa falta. Seguidament editem la GPO.

![](img/19.png)

I dins, a la configuració d'usuari creem un nou package.

![](img/20.png)

El nou package sera el 7-zip que hem instal·lat i el escollim, un cop escollit en el deploy software escollim l'opció de advanced.

![](img/21.png)

Un cop fet dins de deployment posem les següents configuracions perquè un cop l’usuari inicia la sessió se l’hi descarregui el 7-zip.

![](img/22.png)

Ara dins de delegation clicquem en add i afegim el authenticated users li posem permisos de read.

![](img/23.png)

I mirem que en la màquina client ens surti.

![](img/24.png)

- Departament de Gerència: Els directius (grup gerencia) necessiten un navegador segur. Creeu una GPO per desplegar Firefox de forma publicada (l'usuari decideix si l'instal·la des del Tauler de Control).

Per això descarreguem el firefox .msi de 64 bits i el posem a la carpeta de Software.

![](img/25.png)

Ara el que farem serà crear una nova GPO com hem fet amb el 7-zip. L'únic que canvia és que en les configuracions de deployment posem aquestes configuracions.

![](img/26.png)

Surt.

![](img/27.png)

Nota tècnica: Els fitxers .msi els podeu trobar a la carpeta de recursos compartits o descarregar-los. 
Pregunta de consultoria: El client us pregunta: "Com podem crear els nostres propis fitxers .msi si una aplicació només ve amb un .exe?". Responeu a l'informe.

3. Mobilitat d'Usuaris (Perfils Mòbils)

Els usuaris del departament de gestio canvien sovint entre un portàtil o amb un equip d’escriptori.

- Habiliteu una carpeta compartida al servidor anomenada perfils.

Creem la carpeta.

![](img/28.png)

La compartim.

![](img/29.png)

I afegim gestio en el compartir.

![](img/30.png)

- Configureu la plantilla d'usuari del grup gestio perquè utilitzi un perfil mòbil que es guardi en aquesta carpeta.

Ara editarem el usuari de gestio, anem dins de propietats i editem el profile de la següent forma:

![](img/31.png)

- Creeu un usuari nou de prova a gestio, inicieu sessió i demostreu que s'ha creat la carpeta del seu perfil al servidor.

4. Seguretat de Dades (Redirecció de Carpetes)

Per evitar pèrdues de dades si un ordinador s'espatlla:

- Configureu una directiva per a tot el domini perquè la carpeta local Documents es redirigeixi a una ubicació de xarxa segura (la carpeta home folder que tot usuari té a la xarxa).

Ara dins de translogic17.test creem un altre GPO que es digui Redirecció.

![](img/32.png)

El editem en el folder redirectio.

![](img/33.png)

Anem a Documents Properties,  posem: Basic, posem en Root Path (Camí d'arrel) la ruta
corresponent a la carpeta homes (també podríem posar T05 al davant, per agafar
tota la ruta).

![](img/34.png)

I mirem en la màquina client que tingui la ruta correcte.

![](img/35.png)

- Verifiqueu que, en desar un fitxer a "Documents" des del client, aquest apareix realment al servidor.

![](img/36.png)
![](img/37.png)

5. Delegació de Funcions (Helpdesk)

TransLògic S.A. ha contractat un auxiliar de suport. No volen donar-li les claus de tot el sistema:

- Creeu un usuari anomenat adminOU dins la OU d'usuaris.

![](img/38.png)

Li posem contrasenya.

![](img/39.png)

Resultat.

![](img/40.png)

- Delegueu el control de la Unitat Organitzativa principal (ex: OU TransLogic) a aquest usuari adminOU. Només ha de poder:

Per això en translogic fem clic dret i la primera opció.

![](img/41.png)

I posem el adminOU.

![](img/42.png)

- Reiniciar contrasenyes dels treballadors.
- Modificar la pertinença als grups (gestio, magatzem, etc.).

![](img/43.png)

Demostreu (amb captures) que l'adminOU pot canviar un password però NO té permisos per crear un usuari nou.

Iniciem la sessió en la màquina client amb l’admin i afegim les característiques.

![](img/44.png)

Les escollim i les agreguem.

![](img/45.png)

Un cop agregats iniciem sessió amb el adminOU i entrem a l’administrador del servidor i entrem a usuaris i equips del directori.

![](img/46.png)

Ara comprovem que podem posar un usuari a un grup.

![](img/47.png)

Que pot canviar la contrasenya.

![](img/48.png)

I que no pot eliminar usuaris.

![](img/49.png)