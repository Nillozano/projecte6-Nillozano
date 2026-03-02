# Breu descripció

## Introducció

Aprofitant que ja hi esteu treballant amb la seva infraestructura web, des de **Projecte Nexus** us sol·licita una nova petició d’ajuda.  
A causa del gran volum de dades sensibles que gestionen (dades personals d'estudiants, exàmens oficials no publicats i certificats de notes), estan molt preocupats per la integritat i privacitat de la seva gestió acadèmica.

La direcció de Projecte Nexus us ha demanat una demostració pràctica de com la vostra empresa pot garantir els tres pilars de la seguretat en la seva informació: **Confidencialitat**, **Integritat** i **Autenticitat**.

---

# Descripció de l'activitat

## Tasca 1: Protecció de dades en repòs (Xifratge Simètric)

Els caps de departament necessiten transportar els exàmens finals en memòries USB per imprimir-los a secretaria, però tenen por de perdre el dispositiu i que les preguntes es filtrin abans de la data de la prova.

Heu de crear un contenidor xifrat (unitat virtual) dins d'un pendrive (simulat al disc dur) utilitzant el programari **VeraCrypt** (o similar).

### Requisits:
- Crear un volum de **100 MB**.  
- Utilitzar l'algorisme de xifratge **AES-256**.  
- Establir una contrasenya robusta.  
- Dins la unitat xifrada, copiar un fitxer:  
  **EXAMEN_FINAL_SEGURETAT.txt** amb preguntes de prova.
- Demostrar que, sense muntar la unitat amb la contrasenya, el fitxer és inaccessible.

---

## Tasca 2: Verificació d'Integritat (Hashing)

Nexus distribueix material didàctic i software als alumnes a través del seu servidor web.  
Volen estar segurs que els fitxers no han estat alterats per un atacant per incloure malware.

Utilitzant una eina com **CertUtil (Windows)**, **md5sum/sha256sum (Linux)** o **7-Zip**:

1. Crear un document de text anomenat **nota_final_curs.txt** amb el text:  
   *"L'alumne ha aprovat amb un 5".*
2. Calcular el **Hash SHA-256** del fitxer original.
3. Modificar el fitxer canviant una sola xifra (ex.: *"L'alumne ha aprovat amb un 9"*).
4. Tornar a calcular el Hash i comparar resultats per demostrar com l'empremta digital canvia totalment i revela la manipulació.

---

# Què cal lliurar

Heu de redactar un informe tècnic per al client (format Markdown) que inclogui:

### Justificació Teòrica
Una breu explicació (màxim 10 línies) per al client de la diferència entre **xifratge** (Tasca 1) i **funció hash** (Tasca 2), explicant que:
- el xifratge *amaga* la informació  
- el hash *en garanteix la integritat*.

### Evidències de la Tasca 1
- Captura de pantalla de la configuració del volum (algorisme escollit).  
- Captura de la unitat muntada amb l'examen secret a dins.  
- Captures que permetin veure el procés per accedir al fitxer.

### Evidències de la Tasca 2 (Hashing)
- Captura de pantalla del terminal o programa mostrant els dos hashos (l'original i el modificat) per demostrar que són diferents.

### Conclusió
Una breu recomanació final a Nexus sobre:
- la importància de protegir les dades, especialment les portables, amb xifrat i gestió segura de contrasenyes  
- la necessitat d’usar hash per assegurar la integritat de documentació important com actes de notes, contractes, etc.

---

# Material de suport
- Material de l’assignatura *Seguretat Informàtica. RA3. Introducció a la criptografia* [Moodle de l’assignatura].  
- Tutorial VeraCrypt: https://veracrypt.io/en/Beginner's%20Tutorial.html
