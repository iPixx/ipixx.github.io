---
layout: post
title: "Aggiungere un utente al gruppo sudo"
date: 2024-11-23 11:00:00 +0100
categories: [linux, shell]
tags: [linux, shell, vps]
---

Una delle prime cose che faccio quando creo un nuovo server è aggiungere un nuovo utente e assegnargli i permessi di sudo. Questo mi consente di eseguire comandi come amministratore senza dover accedere come root.

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
$ su - newuser
```

Una volta connessi con il nuovo utente, provare a eseguire un comando come amministratore utilizzando `sudo`.

```shell
$ sudo <command>
```

Se il comando viene eseguito correttamente, il nuovo utente ha i permessi di sudo.




