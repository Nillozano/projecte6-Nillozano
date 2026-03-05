# Introducció

La vostra implementació amb Apache ha estat un èxit i el client està satisfet. No obstant això, a la reunió d'estratègia tècnica d'ahir, la directiva va plantejar un nou repte: **l'escalabilitat**. Es preveu que Projecte *Nexus* rebi un pic de visites molt elevat durant la propera campanya de presentació.

Per aquest motiu, hem decidit obrir una línia de recerca i desenvolupament (R+D) per provar **Nginx**. Aquest servidor és conegut per la seva arquitectura orientada a esdeveniments, capaç de gestionar milers de connexions concurrents amb un consum de memòria molt inferior.

L'objectiu d'aquesta activitat és **replicar exactament la infraestructura creada amb Apache, però utilitzant Nginx**. Això ens permetrà comparar rendiment i disposar d'una alternativa d'altes prestacions al nostre catàleg de serveis.

> **Nota important:** Recordeu que dos serveis no poden escoltar pel mateix port (80/443) simultàniament a la mateixa IP. Caldrà aturar Apache abans de començar.

---

# Descripció de l'activitat

L'activitat consisteix en la **migració de la infraestructura web a un entorn Nginx sobre Ubuntu Server**. Heu de documentar tot el procés en l'informe tècnic.

## 1. Preparació de l'Entorn i Instal·lació

- Atureu i deshabiliteu el servei `apache2` per alliberar els ports 80 i 443.  
- Instal·leu el servidor web **Nginx**.  
- Verifiqueu que el servei està actiu i que la **pàgina de benvinguda de Nginx** es mostra correctament al navegador.

## 2. Configuració de *Server Blocks* (Multidomini)

- Aprofiteu l'estructura de carpetes ja creada:  
  - `/var/www/nexus`  
  - `/var/www/academia`
- Si cal, ajusteu els permisos (propietari `www-data`).
- Configureu **dos Server Blocks** (equivalent als VirtualHosts d’Apache) a:  
  - `/etc/nginx/sites-available/`
- Creeu els **enllaços simbòlics** a `sites-enabled/` per activar les configuracions.
- Verifiqueu la sintaxi amb:

```
nginx -t
```

- Reinicieu el servei Nginx.

## 3. Personalització d'Errors

- Configureu la directiva:

```
error_page 404 /ruta/de/la/pagina404.html;
```

- Assegureu-vos que, en demanar un fitxer inexistent, es mostri la **pàgina d’error personalitzada** creada anteriorment.

## 4. Seguretat i Certificats (HTTPS)

- Reutilitzeu els certificats SSL generats en l'activitat anterior (o genereu-ne de nous si cal).
- Configureu el *Server Block* perquè escolti al **port 443**, incloent-hi:

```
ssl_certificate /ruta/al/certificat.crt;
ssl_certificate_key /ruta/a/la/clau.key;
```

- **Redirecció forçada:**  
  Configureu un bloc de servidor al port 80 que respongui amb un **301 Permanent Redirect** cap a la versió HTTPS del domini `disseny.local`.

## 5. Optimització amb HTTP/2

- Habiliteu el protocol HTTP/2 afegint-lo a la directiva `listen` del bloc SSL:

```
listen 443 ssl http2;
```

- Comproveu amb les eines de desenvolupador del navegador que el contingut s’està servint amb aquest protocol.

---

# Què cal lliurar

Heu de redactar una **memòria tècnica** de la instal·lació i configuració, incloent també les **proves de funcionament**.  
És important que la memòria contingui **explicacions clares**, no només captures de pantalla: els clients no són experts i han d’entendre què heu fet.

---

# Material de suport

- **UD5.AA2. El servidor Nginx.**  
  Disponible al Moodle del mòdul de Serveis de Xarxa.
