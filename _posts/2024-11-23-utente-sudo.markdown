---
layout: post
title: "Aggiungere un utente al gruppo sudo"
date: 2024-11-23 11:00:00 +0100
categories: [vps, user access management]
tags: [linux, shell, security]
---

Una delle prime cose che faccio quando creo un nuovo server è aggiungere un nuovo utente e assegnargli i permessi di sudo. Questo mi consente di eseguire comandi come amministratore senza dover accedere come root.

É importante notare che l'accesso come root è rischioso, poiché consente agli attaccanti di ottenere l'accesso completo al sistema senza dover autenticarsi. Per questo motivo, è consigliabile disabilitare l'accesso diretto come utente root e utilizzare un utente con privilegi di amministratore per eseguire i comandi come amministratore.

## Creare un nuovo utente

Per creare un nuovo utente, utilizzare il comando `adduser` seguito dal nome del nuovo utente.

```shell
$ adduser newuser
```

## Aggiungere il nuovo utente al gruppo sudo

Per aggiungere il nuovo utente al gruppo sudo, utilizzare il comando `usermod` con l'opzione `-aG` seguita dal nome del gruppo (`sudo`) del nuovo utente.

```shell
$ usermod -aG sudo newuser
```

## Verificare i permessi di sudo

Per verificare che il nuovo utente abbia i permessi di sudo, accedere al server con il nuovo utente e provare a eseguire un comando come amministratore.

```shell
root@hostname:~# su - newuser
To run a command as administrator (user "root"), use "sudo <command>".
See "man sudo_root" for details.

newuser@hostname:~$ sudo <command>
```

Una volta connessi con il nuovo utente, provare a eseguire un comando come amministratore utilizzando `sudo`.

```shell
$ sudo <command>
```

Se il comando viene eseguito correttamente, il nuovo utente ha i permessi di sudo.




