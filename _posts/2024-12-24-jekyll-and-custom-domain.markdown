---
layout: post
title: "Jekyll and Custom Domain with GitHub Pages"
date: 2024-12-24
categories: [jekyll, domain]
tags: [jekyll, domain]
---
Una delle azioni più comuni da eseguire dopo aver creato un sito web con Jekyll è quella di associare un dominio personalizzato al sito. Questo articolo spiega come associare un dominio personalizzato a un sito web Jekyll ospitato su GitHub Pages.

## GitHub Pages e dominio personalizzato
GitHub Pages è un servizio di hosting web gratuito offerto da GitHub per ospitare siti web statici. GitHub Pages supporta l'uso di un dominio personalizzato per i siti web ospitati su GitHub Pages. Questo significa che è possibile associare un dominio personalizzato come `www.example.com` o `blog.example.com` al proprio sito web Jekyll ospitato su GitHub Pages.

## Passaggi per associare un dominio personalizzato a un sito web Jekyll su GitHub Pages
Per associare un dominio personalizzato a un sito web Jekyll su GitHub Pages, è necessario seguire i seguenti passaggi:

1. **Acquisire un dominio personalizzato**
    - Acquisire un dominio personalizzato da un registrar di domini.
    - Configurare i record DNS del dominio per puntare a GitHub Pages.

2. **Configurare il dominio personalizzato nel progetto Jekyll**
    - Aggiungere il dominio personalizzato al file di configurazione `_config.yml` del sito Jekyll. Aggiungere il dominio personalizzato come valore della chiave `url` o `baseurl`.
    - Creare un file `CNAME` nella cartella radice del repository GitHub con il dominio personalizzato come contenuto. É un semplice file di testo con il nome del dominio personalizzato.

3. **Configurare il repository GitHub**
    - Aggiungere il dominio personalizzato come `Custom domain` nelle impostazioni del repository GitHub (Settings>Pages).
    - Attendere che GitHub Pages aggiorni la configurazione del dominio personalizzato.
    - Selezionare `Enforce HTTPS` per abilitare la crittografia HTTPS per il dominio personalizzato.

3. **Configurare i record DNS del dominio**
    - Configurare i record DNS del dominio per puntare ai server di GitHub Pages.
    - Creare un record `A` per il dominio principale e un record `CNAME` per il sottodominio `www`.


Una volta completati questi passaggi, il dominio personalizzato sarà associato al sito web Jekyll ospitato su GitHub Pages e sarà accessibile tramite il dominio personalizzato.


