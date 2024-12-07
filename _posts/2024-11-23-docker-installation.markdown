---
layout: post
title: "Docker installation"
date: 2024-11-23 12:49:00 +0100
categories: docker
---

Ecco i miei appunti su come ho installato Docker in una VPS.
Credo di aver fatto un milione di errori... pazienza!

[Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/) - dal sito ufficiale Docker

Il primo step suggerito è quello di rimuovere tutti i pacchetti installati nella distribuzione in uso che potrebbero essere in conflitto con la versione ufficiale.

{% highlight shell %}
for pkg in docker.io docker-doc docker-compose docker-compose-v2 podman-docker containerd runc; do sudo apt-get remove $pkg; done
{% endhighlight %}

Nella versione che sto utilizzando, `Ubuntu 24.04 LTS`, tutti questi pacchetti non sono stati trovati e quindi non è stato necessario disinstallarli.

# Install Docker Engine

{% highlight shell %}

# Add Docker's official GPG key:

sudo apt-get update
sudo apt-get install ca-certificates curl
sudo install -m 0755 -d /etc/apt/keyrings
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
sudo chmod a+r /etc/apt/keyrings/docker.asc

# Add the repository to Apt sources:

echo \
 "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
 $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
 sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt-get update
{% endhighlight %}

{% highlight shell %}

# Install Docker Engine:

sudo apt-get install docker-ce docker-ce-cli containerd.io
{% endhighlight %}

{% highlight shell %}

# Verify that Docker Engine is installed correctly by running the hello-world image:

sudo docker run hello-world
{% endhighlight %}

[Post install](https://docs.docker.com/engine/install/linux-postinstall/)
