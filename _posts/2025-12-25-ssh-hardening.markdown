---
layout: post
title: "SSH Hardening"
date: 2024-12-25
categories: [vps, security, ssh-hardening]
tags: [vps, security, ssh]
---

L'SSH (Secure Shell) è un protocollo di rete che consente di accedere e gestire in modo sicuro i server remoti. È uno strumento essenziale per gli amministratori di sistema e gli sviluppatori che necessitano di accedere ai server remoti per configurarli e gestirli.

Tuttavia, l'SSH è anche uno dei bersagli preferiti degli attaccanti, poiché fornisce un canale sicuro per l'accesso ai server. Per questo motivo, è importante implementare misure di sicurezza per proteggere il servizio SSH e prevenire gli attacchi.

In questo articolo, esploreremo alcune delle best practices per proteggere il servizio SSH e migliorare la sicurezza del server.

## 1. Disabilitare l'accesso root

> Prima di procedere con questa modifica, assicurarsi di avere un utente con privilegi di amministratore che possa accedere al server e utilizzare `sudo`.
{: .prompt-danger }

Una delle prime misure di sicurezza che si dovrebbero adottare è disabilitare l'accesso diretto come utente root. L'accesso come utente root è rischioso, poiché consente agli attaccanti di ottenere l'accesso completo al sistema senza dover autenticarsi.

Per disabilitare l'accesso root, è possibile modificare il file di configurazione SSH `/etc/ssh/sshd_config` e impostare `PermitRootLogin no`. Dopo aver apportato questa modifica, riavviare il servizio SSH per applicare le modifiche.

```bash
# Disabilitare l'autenticazione basata su password
sudo nano /etc/ssh/sshd_config

# Impostare PermitRootLogin no

# Riavviare il servizio SSH
sudo systemctl restart sshd
```

## 2. Utilizzare le chiavi SSH per l'autenticazione

L'autenticazione basata su password è vulnerabile agli attacchi di forza bruta e agli attacchi di phishing. Per migliorare la sicurezza del servizio SSH, è consigliabile utilizzare le chiavi SSH per l'autenticazione.

Per utilizzare le chiavi SSH per l'autenticazione, è necessario generare una coppia di chiavi pubbliche e private sul client e copiare la chiave pubblica sul server. Dopo aver copiato la chiave pubblica sul server, è possibile disabilitare l'autenticazione basata su password nel file di configurazione SSH.

```bash
# Generare una coppia di chiavi SSH sul client
ssh-keygen -t ed25519 -b 4096 -C "comment"

# Copiare la chiave pubblica sul server
ssh-copy-id -i ~/.ssh/id_ed25519 user@hostname
```

Dopo aver copiato la chiave pubblica sul server, è possibile disabilitare l'autenticazione basata su password nel file di configurazione SSH.

```bash
# Disabilitare l'autenticazione basata su password
sudo nano /etc/ssh/sshd_config

# Impostare PasswordAuthentication no

# Riavviare il servizio SSH
sudo systemctl restart sshd
```

> Assicurarsi di testare l'accesso con le chiavi SSH prima di disabilitare l'autenticazione basata su password per evitare di bloccarsi fuori dal server.
{: .prompt-danger }


#### 2.1 Che differenza c'è tra una chiave RSA e una ed25519?

Le chiavi SSH possono essere generate utilizzando diversi algoritmi, tra cui RSA ed Ed25519. Entrambi gli algoritmi sono considerati sicuri, ma ci sono alcune differenze tra di loro.


#### RSA

RSA è uno degli algoritmi di crittografia più utilizzati per la generazione di chiavi SSH. Le chiavi RSA sono supportate da quasi tutti i client e server SSH e offrono un buon livello di sicurezza.

Tuttavia, le chiavi RSA possono essere vulnerabili agli attacchi di forza bruta e agli attacchi di crittanalisi. Per questo motivo, è consigliabile utilizzare chiavi RSA di almeno 2048 o 4096 bit per garantire un livello adeguato di sicurezza.

#### Ed25519

Ed25519 è un algoritmo di firma digitale basato sulla curva ellittica che offre un livello di sicurezza elevato e prestazioni migliori rispetto a RSA. Le chiavi Ed25519 sono più piccole di quelle RSA e richiedono meno risorse computazionali per la generazione e la verifica delle firme.

Le chiavi Ed25519 sono supportate da molti client e server SSH moderni e sono considerate una scelta sicura per l'autenticazione SSH.

In generale, se possibile, è consigliabile utilizzare le chiavi Ed25519 per l'autenticazione SSH, poiché offrono un livello di sicurezza elevato e prestazioni migliori rispetto a RSA.





