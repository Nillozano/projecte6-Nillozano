# Nil Lozano i Anthony Milla

## Taula comparativa amb les dades obtingudes

| **Mètrica**               | **Apache prova lleugera** | **Nginx prova lleugera** | **Apache prova d’estrès** | **Nginx prova d’estrès** |
|---------------------------|----------------------------|---------------------------|----------------------------|---------------------------|
| **Time taken for test**   | 2,255 s                    | 0,379 s                   | 15,244 s                   | 2,685 s                   |
| **Transfer rate**         | 158,08 kb/s                | 773,36 kb/s               | 233,82 kb/s                | 1091,07 kb/s              |
| **RPS**                   | 443,48                     | 2639,72                   | 655,98                     | 3724,18                   |
| **Time per request**      | 22,549 ms                  | 3,788 ms                  | 152,444 ms                 | 2,685 ms                  |
| **Completed request**     | 1000                       | 1000                      | 10000                      | 10000                     |
| **Failed request**        | 0                          | 0                         | 0                          | 0                         |

## Conclusions taula comparativa amb les dades obtingudes

- Nginx és **molt més ràpid** que Apache en totes les proves.  
- **Satura menys**: manté la velocitat fins i tot amb molta càrrega.  
- Apache és **molt més lent**, sobretot en l’estrès.  
- Mateixa fiabilitat: **cap dels dos falla** peticions.  
- **Nginx rendeix molt millor**; Apache es torna lent quan hi ha molta feina.

*(La imatge del PDF no es pot inserir directament en `.md` perquè no ve com a fitxer separat.)*