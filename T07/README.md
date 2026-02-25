# Introducció

Malgrat que l’encàrrec de Projecte Nexus consumeix bona part de la vostra energia i temps, no podeu deixar de banda els clients existents. TransLògic S.A. va confiar amb vosaltres per fer el salt a una infraestructura amb Directori Actiu, i ara cal rematar el projecte.

Cal realitzar una sèrie de millores crítiques en la seva infraestructura de xarxa. La direcció de l'empresa està preocupada per la seguretat de les contrasenyes, la mobilitat dels seus treballadors i la gestió eficient del programari. A més, volen començar a delegar certes tasques bàsiques a un assistent tècnic sense donar-li privilegis totals d'administrador.

# Descripció de l'activitat

Heu de documentar cada pas com si fos un informe tècnic d'implementació per al client. Abans de començar a realitzar les diferents accions, repenseu l’estructura d’unitats organitzatives (OU) que vau presentar inicialment al client; és possible que algun canvi us simplifiqui les accions que caldrà realitzar.

## 1. Polítiques de Seguretat i Contrasenyes (Seguretat Corporativa)

El client exigeix endurir la política de contrasenyes per evitar accessos no autoritzats:

### Política Global
Modifiqueu la *Default Domain Policy* perquè tots els membres del grup **personal** (és a dir, tot el domini) hagin de tenir una contrasenya de, com a mínim, **8 caràcters**.

### Política per a Gerència
La Unitat Organitzativa (OU) on ubiqueu la direcció conté els usuaris VIP (grup *gerencia*). Creeu una GPO específica per ells on:

- La contrasenya sigui de **18 caràcters**
- Caduci cada **28 dies**
- **No** s'activi la complexitat

### Millora Proactiva (Bonus)
Com a consultors experts, heu de proposar i implementar una tercera GPO útil per a una empresa logística (ex: bloqueig automàtic de pantalla, fons d'escriptori corporatiu...).  
Justifiqueu per què l'heu triat.

## 2. Desplegament Automatitzat de Programari

Per reduir els tiquets de suport tècnic, automatitzareu la instal·lació d'eines segons el departament:

### Departament de Gestió
Els administratius (grup *gestio*) necessiten l'eina de compressió **7zip**.  
Creeu una GPO per desplegar-la **assignada** (instal·lació automàtica).

### Departament de Gerència
Els directius (grup *gerencia*) necessiten un navegador segur.  
Creeu una GPO per desplegar **Firefox** de forma **publicada** (instal·lació opcional des del Tauler de Control).

**Nota tècnica:** Els fitxers `.msi` els podeu trobar a la carpeta de recursos compartits o descarregar-los.

### Pregunta de consultoria
El client pregunta:  
**"Com podem crear els nostres propis fitxers .msi si una aplicació només ve amb un .exe?"**  
Responeu a l'informe.

## 3. Mobilitat d'Usuaris (Perfils Mòbils)

Els usuaris del departament *gestio* canvien sovint entre portàtil i equip d’escriptori.

1. Habiliteu una carpeta compartida al servidor anomenada **perfils**.
2. Configureu la plantilla d'usuari del grup *gestio* perquè utilitzi un **perfil mòbil** desat en aquesta carpeta.
3. Creeu un usuari nou de prova, inicieu sessió i comproveu que s'ha creat la carpeta del seu perfil al servidor.

## 4. Seguretat de Dades (Redirecció de Carpetes)

Per evitar pèrdues de dades si un ordinador falla:

- Configureu una directiva per a tot el domini perquè la carpeta **Documents** es redirigeixi a la ubicació de xarxa segura (la *home folder* que tot usuari té a la xarxa).
- Verifiqueu que en desar un fitxer a *Documents* apareix realment al servidor.

## 5. Delegació de Funcions (Helpdesk)

TransLògic S.A. vol donar autonomia al seu auxiliar de suport sense donar-li privilegis complets.

1. Creeu un usuari anomenat **adminOU** dins la OU d'usuaris.
2. Delegueu el control de la Unitat Organitzativa principal (ex: *OU TransLogic*) a aquest usuari. Només ha de poder:
   - Reiniciar contrasenyes
   - Modificar la pertinença a grups (gestio, magatzem, etc.)
3. Demostreu amb captures que **adminOU pot canviar un password però NO pot crear usuaris nous**.

# Què cal lliurar

## Informe tècnic
- Canvis en l’estructura d’OU i justificació
- Captures de pantalla comentades de cada pas realitzat
- Justificació de la 3a GPO
- Explicació breu sobre com crear/convertir fitxers MSI
- Proves de funcionament (gpresult, redirecció de carpetes, error en crear usuaris amb adminOU...)