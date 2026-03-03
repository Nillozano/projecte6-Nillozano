# Encàrrec d’Infraestructura Web per a Nexus

Les prediccions dels assessors de la incubadora s’han confirmat: ja teniu un primer client amb un encàrrec relacionat amb la infraestructura web.

**Nexus** és una nova empresa de formació a Mataró que ha contactat amb vosaltres per al desplegament i gestió de la seva infraestructura web. En aquesta fase inicial, l’objectiu és establir una base sòlida i segura per als serveis corporatius abans de migrar definitivament al núvol.

## Requisits del client

El client necessita:

- Allotjar **dos portals web diferenciats** (agència de disseny i acadèmia de formació) en un únic servidor.
- Garantir **seguretat màxima** en les comunicacions mitjançant xifratge SSL/TLS.
- Assegurar **rendiment òptim** utilitzant protocols moderns.
- Configurar un **servidor web Apache** sobre Ubuntu Server amb criteris professionals.

---

## Descripció de l’encàrrec

Abans del desplegament en un VPS, es realitzarà el projecte en una màquina virtual local. Un cop superades les proves i amb el vistiplau del client, es desplegarà a Internet.

Les accions inclouen la instal·lació, configuració de dominis virtuals i securització avançada d’un servidor Apache. Tot el procés s’ha de documentar en un informe tècnic.

---

## Tasques específiques

### 1. Instal·lació i configuració base

- Instal·lar el servidor web Apache a Ubuntu Server.
- Verificar el funcionament del servei amb `apachectl`.
- Comprovar que l’usuari `www-data` s’ha creat correctament i revisar permisos de `/var/www`.

### 2. Desplegament de VirtualHosts (Multidomini)

- Els dominis del client són:
  - **projectenexus.test** (Site 1)
  - **academia.test** (Site 2)
- Crear l’estructura de directoris corresponent dins de `/var/www/`.
- Configurar dos VirtualHosts a `/etc/apache2/sites-available/` basant-se en el fitxer per defecte.
- Activar els llocs amb `a2ensite` i modificar `/etc/hosts` per simular DNS.

### 3. Personalització d’errors

- Configurar una pàgina **404 personalitzada** per a un dels VirtualHosts amb un missatge corporatiu.

### 4. Seguretat i certificats (HTTPS)

- Habilitar el mòdul SSL d’Apache.
- Generar un **certificat autosignat** per als dos dominis amb:
  - Validesa: 365 dies
  - Clau RSA: 2048 bits
- Configurar els VirtualHosts segurs (port 443) amb les claus generades.
- Configurar redirecció forçada de HTTP (80) a HTTPS (443).

### 5. Optimització amb HTTP/2

- Habilitar el protocol HTTP/2.
- Afegir la directiva `Protocols` als VirtualHosts corresponents.
- Demostrar el seu funcionament amb `curl` o eines del navegador.

---

## Què cal lliurar

Un **informe tècnic complet** amb explicacions detallades i proves de funcionament. Les captures de pantalla han d’acompanyar, però no substituir, les explicacions.

---

## Material de suport

UD5.AA2. *El servidor Apache*. Disponible al Moodle del mòdul de Serveis de Xarxa.
