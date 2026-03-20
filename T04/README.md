# Introducció

Fins ara heu configurat dos servidors web diferents: el clàssic i robust **Apache** i el lleuger i ràpid **Nginx**. Aparentment, tots dos fan el mateix: mostrar les pàgines web del vostre client Nexus. Però, ¿es comporten igual sota pressió?

En aquesta pràctica deixareu de banda la configuració i us posareu el barret d'**Auditors de Sistemes**. Sotmetreu els vostres servidors a proves d'estrès (*Benchmarking*) des de la vostra màquina client (Zorin OS) per determinar quin dels dos gestiona millor les connexions. Això és clau a l’hora de presentar la vostra proposta als clients.

---

# Descripció de l'activitat

Cadascú de vosaltres haurà de disposar de la màquina virtual on teniu els servidors **Apache** i **Nginx**. El primer que caldrà fer és adaptar el contingut web perquè tingui un aspecte més professional i permeti fer unes proves més realistes.

Podeu usar la IA per generar una pàgina corporativa al site de Nexus. Hauria de tenir imatges, estils, etc.

- Un de vosaltres farà la prova sobre **Apache**  
- L’altre sobre **Nginx**

Assegureu-vos de tenir habilitat en cada màquina el servei que correspongui.

El client serà un Zorin, al qual caldrà que instal·leu les utilitats **apache2-utils** per terminal.

---

# Proves

## Prova de càrrega lleugera

Simulareu un trànsit normal. Imagineu que **10 usuaris** estan navegant per la web simultàniament, generant **1000 peticions**.

**Sintaxi de la comanda:**

**Valors a anotar per als dos servidors:**

- Time taken for tests (Temps total)  
- Transfer Rate  
- Requests per second (Peticions per segon — com més alt, millor)  
- Time per request (mean) (Temps mitjà de resposta — com més baix, millor)  
- Completed requests  
- Failed requests  

---

## Prova d'estrès

Ara posareu els servidors al límit. Simularem que la vostra web s'ha fet viral o que esteu rebent un petit atac.

Es llançaran **10.000 peticions** amb **100 usuaris simultanis** colpejant el servidor alhora.

**Nota:**  
Si algun servidor falla (errors o *Connection timed out*), anoteu-ho — **això també és un resultat important**.

Anoteu els mateixos valors que a la prova anterior.

---

# Què cal lliurar

Crear una **taula comparativa** amb les dades obtingudes:

| Mètrica                | Apache (prova lleugera) | Nginx (prova lleugera) | Apache (prova d’estrès) | Nginx (prova d’estrès) |
|------------------------|--------------------------|--------------------------|---------------------------|---------------------------|
| Time taken for test    |                          |                          |                           |                           |
| Transfer rate          |                          |                          |                           |                           |
| RPS                    |                          |                          |                           |                           |
| Time per request       |                          |                          |                           |                           |
| Completed requests     |                          |                          |                           |                           |
| Failed requests        |                          |                          |                           |                           |

---

# Material de suport

J.D. Muñoz. *El comando ab. Servicios de Red e Internet*. 2017.  
Disponible a: https://serviciosgs.readthedocs.io/es/latest/rendimiento/ab.html