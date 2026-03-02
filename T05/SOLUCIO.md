# Introducció
Aprofitant que ja hi esteu treballant amb la seva infraestructura web, des de Projecte Nexus us sol·licita una nova petició d’ajuda.
A causa del gran volum de dades sensibles que gestionen (dades personals d'estudiants,
exàmens oficials no publicats i certificats de notes), estan molt preocupats per la integritat i privacitat de la seva gestió acadèmica.
La direcció de Projecte Nexus us ha demanat una demostració pràctica de com la vostra empresa pot garantir els tres pilars de la seguretat en la seva informació: Confidencialitat, Integritat i Autenticitat.

## Descripció de l'activitat

### Tasca 1: Protecció de dades en repòs (Xifratge Simètric)
Els caps de departament necessiten transportar els exàmens finals en memòries USB per imprimir-los a secretaria, però tenen por de perdre el dispositiu i que les preguntes es filtrin abans de la data de la prova.

Heu de crear un contenidor xifrat (unitat virtual) dins d'un pendrive (simulat al disc dur)
utilitzant el programari VeraCrypt (o similar).

![](img/01.png)

#### Requisits:
- Crear un volum de 100MB.

![](img/02.png)
![](img/03.png)

L’apliquem a la màquina perquè ens surti com un volum.

![](img/04.png)
![](img/05.png)

- Utilitzar l'algorisme de xifratge AES-256.

Dins de VeraCrypt creem un nou volum. Dins de alla li posem cifrar partició/unitat secundaria.

![](img/06.png)

Seguim el que posa de predeterminat.

![](img/07.png)

Per escollir el volum que volem crear escollim en quin el volem fer.

![](img/08.png)

L’escollim i seguim.

![](img/09.png)

Seguim donant ha següent amb l’opció predeterminada.

![](img/10.png)

Utilitzem el algoritme de xifrat AES i el de Hash el SHA-256 com demanen.

![](img/11.png)

- Establir una contrasenya robusta.

R9v@L3m#Qp72!sD

![](img/12.png)

Ara per seguir tindrem que moure el ratolí fins que la barra estigui verda.

![](img/13.png)

Ho deixem com ens surt a predeterminat.

![](img/14.png)

I ho xifrem.

![](img/15.png)

I ja estaria fet.

Seguidament seleccionem a seleccionar dispositivo.

![](img/16.png)

Escollim la unitat.

![](img/17.png)

I escollim una lletra a on muntar-ho. El muntem.

![](img/18.png)

Li posem la contrasenya que hem establert abans.

![](img/19.png)

I ja el tenim.

![](img/20.png)

- Dins la unitat xifrada, heu de copiar un fitxer de text anomenat EXAMEN_FINAL_SEGURETAT.txt amb preguntes de prova.

Primer de tot creo un .txt amb un examen dins del document.

![](img/21.png)

Copiem el fitxer a la nova unitat.

![](img/22.png)

- Demostrar que, sense muntar la unitat amb la contrasenya, el fitxer és inaccessible.

Dins de VeraCrypt desmuntem l’unitat abans creada.

![](img/23.png)

Comprovem que estigui desmuntat.

![](img/24.png)

#### Tasca 2: Verificació d'Integritat (Hashing)

Nexus distribueix material didàctic i software als alumnes a través del seu servidor web.
Volen estar segurs que els fitxers no han estat alterats per un atacant per incloure malware.

- Utilitzant una eina com CertUtil (Windows), md5sum/sha256sum (Linux) o 7-Zip:

Comprovem el seu funcionament.

![](img/25.png)

- Crear un document de text anomenat nota_final_curs.txt amb el text: "L'alumne ha aprovat amb un 5".

![](img/26.png)

Seguidament creem una carpeta que es digui Xifrat i posem el document creat anteriorment a dins.

![](img/27.png)

- Calcular el Hash SHA-256 del fitxer original.

Copiem la ruta.

![](img/28.png)

I en el powershell posem aquest codi per mirar-ho.

![](img/29.png)

- Modificar el fitxer canviant una sola xifra (ex: "L'alumne ha aprovat amb un 9").

![](img/30.png)

- Tornar a calcular el Hash i comparar els resultats per demostrar com l'empremta digital canvia totalment i revela la manipulació de la nota.

![](img/31.png)

#### Justificació:
Per evitar que ningú pugui llegir la informació si no disposa de la contrasenya, el xifratge s’utilitza per ocultar-la; i, com que amb la clau es pot recuperar el fitxer original, és un procés reversible.La funció hash, el que fa es crear una “empremta digital” del fitxer, i el seu objectiu no és ocultar res. Aquesta empremta serveix per comprovar que el document no ha estat modificat, i no es pot convertir de nou en el contingut original. En essència, protegir i ocultar dades és el que fa el xifratge, mentre que garantir que no han estat alterades és el que aporta el hash.

#### Conclusió:
Per evitar que algú pugui llegir dades sensibles en cas de robatori o pèrdua, és important que Nexus xifri tota la informació que es transporta en USB o discos externs. Cal també utilitzar contrasenyes fortes i mantenir-les guardades de manera segura. A més, per assegurar la integritat de documents importants (com contractes o notes), és recomanable emprar funcions hash, garantint així que ningú els hagi modificat sense permís.
