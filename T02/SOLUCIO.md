Primer de tot posem les màquines en xarxa nat, perquè es puguin veure entre elles.

Les IP de les dues màquines.

![](img/01.png)
![](img/02.png)

Prova de connectivitat.

![](img/03.png)
![](img/04.png)
![](img/05.png)

Seguidament instal·lem el servei Apache.

![](img/06.png)

Mirem que estigui activat.

![](img/07.png)

I mirem els seus permisos.

![](img/08.png)
![](img/09.png)

Després creem les dues carpetes pels dominis que fem.

![](img/10.png)

Creem un index.html per configurar.

![](img/11.png)
![](img/12.png)

Reiniciem el servei per aplicar els canvis.

![](img/13.png)

Comprovació que s’ha creat.

![](img/14.png)

I igual pel academia.test (faig demostració de la comprovació, és a dir que tots els anteriors passos també els he fet).

![](img/15.png)

Ara configurem dos virtualhosts dins de sites-available fent servir de base el 000-default.conf. Ho fem copiant-lo.

![](img/16.png)

I configurem els dos arxius posant com a adreça el projectenexus.test

![](img/17.png)

Igual amb academia.test

![](img/18.png)

Seguidament activem els llocs amb a2ensite.

![](img/19.png)

Per poder-ho comprovar dins de l’altre màquina editem el arxiu de hosts per poder entrar als dos llocs desde aquesta màquina.

![](img/20.png)

Provem d’entrar als dos llocs.

![](img/21.png)
![](img/22.png)

Ara configurarem la pàgina d’error de 404.

![](img/23.png)

Posem els missatges que volem que surtin.

![](img/24.png)

I reiniciem el servei.

![](img/25.png)

Comprovació.

![](img/26.png)

I el mateix amb l’altre. 

Comprovació.

![](img/27.png)

Per poder-ho fer entrarem al arxiu de .conf del projectenexus i academia.

![](img/28.png)

I afegim aquesta línia.

![](img/29.png)

Reiniciem el servei.

![](img/30.png)

I fem el mateix amb l’altre. 

Seguidament, revisem que ens surti en el zorin (podem observar que no és recomanable posar accents, ja que no surten bé).

![](img/31.png)
![](img/32.png)

Ara per habilitar el SSL, per fer-ho copiem l'arxiu TLS.

![](img/33.png)

Ara generarem un certificat autosignat pels dos dominis amb openssl amb una validesa de 365 dies i una clau de RSA de 2048 bits.

![](img/34.png)
![](img/35.png)

I configurem el virtualhost segur amb les claus generades anteriorment.

![](img/36.png)
![](img/37.png)
![](img/38.png)

I igual amb l’altre.

Ara farem una redirecció forçada, configurant el servidor perquè qualsevol petició HTTP (port 80) als dos dominis es redirigeixi automàticament a HTTPS (port 443).

![](img/39.png)

Mirem que estigui bé.

![](img/40.png)

Ho fem amb l’altre.

![](img/41.png)

Fem la comprovació.

![](img/42.png)
![](img/43.png)

Ara editem l’arxiu .conf per forçar una pàgina segura.

![](img/44.png)
![](img/45.png)
![](img/46.png)

I igual amb l’altre.

Comprovació.

![](img/47.png)
![](img/48.png)

Seguidament, configurem el ssl.conf per posar directives sobre els directoris.

![](img/49.png)
![](img/50.png)
![](img/51.png)

Igual amb l’altre.

Comprovació.

![](img/52.png)
![](img/53.png)

Ara habilitem el protocol http/2.

![](img/54.png)

Seguidament, configurem la directiva de protocols dels virtualhost.

![](img/55.png)
![](img/56.png)
![](img/57.png)

I fem el mateix amb l’altre.

Ara fem la demostració que el protocol està actiu fent servir la comanda curl o inspeccionant la xarxa amb el navegador.

![](img/58.png)