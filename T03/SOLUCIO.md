1. Preparació de l'Entorn i Instal·lació:

- Atureu i deshabiliteu el servei Apache2 per alliberar els ports 80 i 443.

![alt text](image.png)

- Instal·leu el servidor web Nginx.

![](image-1.png)

- Verifiqueu que el servei està actiu i que la pàgina de benvinguda de Nginx es mostra correctament al navegador.

Mirem que estigui activat.

![alt text](image-2.png)

I edittem l'arxiu de configuració de default.

![alt text](image-3.png)

![alt text](image-4.png)

Ara mirem la sintaxi.

![alt text](image-5.png)

Mirem la nostra IP.

![alt text](image-6.png)

I en l'altre màquina, posem la IP en el buscador i veiem la pàgina de benvinguda de Nginx.

![](image-7.png)

2. Configuració de Server Blocks (Multidomini)

- Aprofiteu l'estructura de carpetes ja creada (/var/www/nexus i /var/www/academia). Si cal, ajusteu els permisos (propietari www-data).

![alt text](image-8.png)

- Configureu dos Server Blocks (l'equivalent a VirtualHosts a Nginx) a /etc/nginx/sites-available/.

Primer de tot copiem el arxiu de configuració en els nostres dominis.

![alt text](image-9.png)

Entrem.

![alt text](image-10.png)
![alt text](image-19.png)
![alt text](image-11.png)

I fem el mateix amb el academia.test.

- Creeu els enllaços simbòlics a sites-enabled/ per activar les configuracions. Verifiqueu la sintaxis amb nginx -t abans de reiniciar el servei.

![alt text](image-12.png)
![alt text](image-14.png)
![alt text](image-15.png)
![alt text](image-16.png)

I mostrem que gràcies a l'altre pràctica ja tenim l'altre màquina configurada per accedir a aquests dominis.

![](image-17.png)
![alt text](image-18.png)

3. Personalització d'Errors

- Configureu la directiva error_page 404 dins del bloc de servidor corresponent.

![alt text](image-13.png)

Editem les següents linies:

![alt text](image-20.png)

Reiniciem el servei i fem el mateix amb el academia.

- Assegureu-vos que, quan es demani un fitxer inexistent, es mostri la pàgina d'error personalitzada que vau crear anteriorment.

![alt text](image-21.png)
![alt text](image-22.png)

Seguidament, desde el terminal mirem com veu el error 404 per la connexió erronia.

![alt text](image-23.png)


4. Seguretat i Certificats (HTTPS)
- Reutilitzeu els certificats SSL generats en l'activitat anterior (o genereu-ne de nous si cal).
- Configureu el Server Block per escoltar al port 443 i indiqueu les rutes del certificat (ssl_certificate) i la clau privada (ssl_certificate_key).
- Redirecció forçada: Configureu un bloc de servidor escoltant al port 80 queretorni un codi 301 (Permanent Redirect) cap a la versió HTTPS del domini projectenexus.test o academia.test.
5. Optimització amb HTTP/2
- Habiliteu el protocol HTTP/2 afegint el paràmetre http2 a la directiva listen del bloc SSL.
- Comproveu novament amb les eines de desenvolupador del navegador que el contingut s'està servint amb aquest protocol.
