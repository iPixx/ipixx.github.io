---
layout: post
title: "Docker Swarm Secrets"
date: 2024-12-08
categories: docker swarm secrets
tags: [docker, swarm, secrets]
---
Docker Secrets può essere utilizzato per memorizzare informazioni sensibili come password, chiavi API e certificati in modo sicuro e accessibile solo ai servizi autorizzati.


I secrets sono memorizzati in modo sicuro nel server swarm e vengono montati come file nei container dei servizi, sono crittografati in transito e a riposo e sono disponibili solo per i servizi che ne hanno bisogno e possono essere aggiornati senza dover riavviare i servizi e possono essere revocati in qualsiasi momento.

Docker Secrets è disponibile solo per i container eseguiti come servizi swarm, non per container standalone. Vista la convenienza, è interessante valutare di eseguire uno stack swarm anche nel caso si abbia un singolo nodo, cosa assolutamente possibile come espresso nella documentazione di Docker.


## Creare un Docker secret
Per creare un Docker secret, si usa il comando `docker secret create` seguito dal nome del secret e il valore del secret. É previsto che questo sia acquisito dallo standard input per garantire la sicurezza del secret.

Ad esempio, per creare un secret chiamato `db_password` con il valore `mysecretpassword`, è possibile utilizzare il seguente comando:

```bash
$ docker secret create db_password -
```

Il segno `-` alla fine del comando indica che il valore del secret verrà letto dalla standard input. Dopo aver eseguito il comando, è possibile inserire il valore del secret e premere `CTRL+D` per terminare l'input.

Una soluzione alternativa per creare un secret è utilizzare il comando `printf` per passare il valore del secret al comando `docker secret create`. Ad esempio, per creare un secret chiamato
`db_password` con il valore `mysecretpassword`, è possibile utilizzare il seguente comando:

```bash
$ printf "mysecretpassword" | docker secret create db_password -
```

## Visualizzare i Docker secrets
Per visualizzare i Docker secrets, è possibile utilizzare il comando `docker secret ls`. Questo comando elencherà tutti i secrets presenti nel server swarm, inclusi il nome e la data di creazione di ciascun secret.

```bash
$ docker secret ls
```

## Visualizzare i dettagli di un Docker secret
Per visualizzare i dettagli di un Docker secret, è possibile utilizzare il comando `docker secret inspect` seguito dal nome del secret. Questo comando visualizzerà i dettagli del secret, inclusi il nome, l'ID, la data di creazione e lo stato del secret. Non verrà visualizzato il valore del secret per motivi di sicurezza e in generale non esiste nessun modo per recuperare il valore di un secret.

```bash
$ docker secret inspect db_password
```

## Utilizzare un Docker secret in uno stack swarm
Per utilizzare un Docker secret in uno stack swarm, è possibile specificare il secret nel file di configurazione dello stack. Ad esempio, per utilizzare il secret `db_password` nel servizio `db`, è possibile aggiungere il seguente blocco al file di configurazione dello stack:

```yaml
services:
  db:
    image: mysql
    secrets:
      - db_password
```

In questo modo
- il secret `db_password` verrà montato come file nel container del servizio `db` e sarà accessibile come `/run/secrets/db_password`.
- Il secret sarà disponibile solo per il servizio `db` e non sarà accessibile da altri servizi.

## Rimuovere un Docker secret
Per rimuovere un Docker secret, è possibile utilizzare il comando `docker secret rm` seguito dal nome del secret. Questo comando rimuoverà il secret dal server swarm e lo renderà inaccessibile ai servizi.

```bash
$ docker secret rm db_password
```

## Aggiornare un Docker secret
Per aggiornare un Docker secret, è possibile utilizzare il comando `docker secret update` seguito dal nome del secret e il nuovo valore del secret. Questo comando aggiornerà il valore del secret con il nuovo valore specificato.

```bash
$ printf "newsecretpassword" | docker secret update db_password -
```

## Conclusioni
I Docker secrets sono un modo sicuro e conveniente per memorizzare informazioni sensibili come password, chiavi API e certificati nei servizi swarm. Utilizzando i Docker secrets, è possibile garantire che le informazioni sensibili siano accessibili solo ai servizi autorizzati e che siano crittografate in transito e a riposo. I Docker secrets semplificano la gestione delle informazioni sensibili nei servizi swarm e consentono di aggiornare e revocare i secrets senza dover riavviare i servizi.

## Ulteriori informazioni
Di seguito sono riportati alcuni link alla documentazione ufficiale utili per approfondire Docker secrets:
- [Docker secrets](https://docs.docker.com/engine/swarm/secrets/)
- [Docker secret create](https://docs.docker.com/engine/reference/commandline/secret_create/)
- [Docker secret inspect](https://docs.docker.com/engine/reference/commandline/secret_inspect/)
- [Docker secret ls](https://docs.docker.com/engine/reference/commandline/secret_ls/)
- [Docker secret rm](https://docs.docker.com/engine/reference/commandline/secret_rm/)
- [Docker secret update](https://docs.docker.com/engine/reference/commandline/secret_update/)
- [Docker secret](https://docs.docker.com/engine/reference/commandline/secret/)
