---
layout: post
title: "Learning Docker - Deploy a Docker Stack"
date: 2024-11-30 11:45:00 +0100
categories: docker vps
---

Nel post precedente abbiamo visto come creare un [Docker stack](/2024/11/25/docker-stack.html). In questo post vedremo come fare il deployment un Docker stack su un server remoto.

# Selezionare il corretto docker context

Per fare il deployment di un Docker stack su un server remoto, la nostra VPS, è necessario selezionare il corretto docker context. Un docker context è un insieme di parametri di configurazione che definiscono la connessione a un'istanza di Docker Engine. Per selezionare il docker context corretto, è possibile utilizzare il comando `docker context use`.

```bash
docker context use remote-server
```

Per verificare che il docker context sia stato selezionato correttamente, è possibile utilizzare il comando `docker context ls`.

```bash
docker context ls
```

# Attivare lo swarm mode in Docker

Affinché il nostro server remoto possa eseguire un Docker stack, è necessario attivare lo swarm mode in Docker. Lo swarm mode è una funzionalità di Docker che consente di creare un cluster di server Docker e distribuire i container su di essi.
Per il nostro scopo, è necessario attivare lo swarm mode sul nostro server remoto, che sarà un nodo sia manager che worker, e non è necessario creare un cluster di server Docker.

Per attivare lo swarm mode, è possibile utilizzare il comando `docker swarm init`.

```bash
docker swarm init
```

# Creare un Docker registry

Un registro è un servizio che memorizza e distribuisce immagini Docker. Per fare il deployment di un Docker stack su un server remoto, è necessario creare un registro Docker per memorizzare le immagini dei nostri servizi. E' possibile utilizzare un registro pubblico come Docker Hub o creare un registro privato.

Attiviamo il servizio di registry Docker sul nostro server remoto.

```bash
docker service create --name registry --publish published=5000,target=5000 registry:2
```

e verifichiamo che il servizio sia attivo.

```bash
docker service ls
```

o anche

```bash
curl http://localhost:5000/v2/
{}
```

```bash
curl http://localhost:5000/v2/_catalog
{"repositories":[]}
```

**NOTA IMPORTANTE:** il firewall ufw di Ubuntu è bypassato da Docker e quindi il servizio è accessibile da qualsiasi IP. Questo succede perché Docker e ufw utilizzano iptables in modi che li rendono incompatibili tra loro. [Maggiori informazioni](https://docs.docker.com/engine/network/packet-filtering-firewalls/)
