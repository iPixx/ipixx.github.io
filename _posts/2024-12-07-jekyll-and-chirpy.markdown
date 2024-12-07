---
title: "Jekyll and Chirpy"
date: 2024-12-07 00:00:00 +0000
categories: [jekyll, jekyll-theme]
tags: [jekyll, chirpy, jekyll-theme]
---
[Chirpy](https://chirpy.cotes.page/) è un tema Jekyll per la creazione di blog personali di natura tecnica.

È progettato e sviluppato da [Cotes Chung](https://cotes.info/) ed è disponibile gratuitamente e può essere utilizzato per creare blog personali, progetti open source, documentazione tecnica e altro ancora.

Una interessante guida si trova [qui](https://www.osotechie.com/posts/Blog-as-Code-Part1/).


## Installazione

1. Prerequisiti:
   - [Ruby](https://www.ruby-lang.org/en/downloads/)
   - [RubyGems](https://rubygems.org/pages/download)
   - [Jekyll](https://jekyllrb.com/docs/installation/)

2. Creare un nuovo repository su GitHub usando il progetto [starter](https://github.com/cotes2020/chirpy-starter) come template.
Accedi a GitHub e naviga al progetto [starter](https://github.com/cotes2020/chirpy-starter). Clicca sul pulsante "Use this template" e poi seleziona "Create a new repository".
Dai un nome al nuovo repository `<username>.github.io`, sostituendo `username` con il tuo nome utente GitHub in minuscolo.

3. Clonare il repository di Chirpy:

   ```bash
   git clone git@github.com:<username>/<username>.github.io.git
    ```
4. Navigare nella cartella del repository:

   ```bash
   cd <username>.github.io
   ```
5. Installare le dipendenze di Chirpy:

   ```bash
   bundle install
   ```
6. Avviare il server di sviluppo:

   ```bash
    bundle exec jekyll serve --livereload
    ```
7. Aprire il browser e visitare `http://localhost:4000`.

