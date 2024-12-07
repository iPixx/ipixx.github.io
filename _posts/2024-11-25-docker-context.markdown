---
layout: post
title: "Learning Docker - Docker Context"
date: 2024-11-25 22:10:00 +0100
categories: docker
---

# Learning Docker - Docker Context

- Docker context: https://docs.docker.com/engine/context/working-with-contexts/

## Features

- Docker context is a feature that allows you to switch between multiple Docker environments (local, remote, cloud) without changing the Docker CLI commands.
- Docker context supports local, SSH, and Docker API endpoints.
- Docker context can be used to manage multiple Docker environments, such as development, testing, and production.
- Docker context simplifies the management of Docker environments by providing a single configuration file for all contexts.
- Docker context allows you to define custom configurations for each context, such as environment variables, volumes, and networks.

## Commands

- `docker context create`: Create a new Docker context.
- `docker context ls`: List all Docker contexts.
- `docker context use`: Switch to a different Docker context.
- `docker context inspect`: Display detailed information about a Docker context.
- `docker context rm`: Remove a Docker context.

## Examples

- Create a new Docker context:

  ```bash
  docker context create mycontext --docker "host=ssh://user@hostname"
  ```

- List all Docker contexts:
  ```bash
    docker context ls
  ```
- Switch to a different Docker context:

  ```bash
  docker context use mycontext
  ```

- Display detailed information about a Docker context:

  ```bash
  docker context inspect mycontext
  ```

- Remove a Docker context:
  ```bash
  docker context rm mycontext
  ```
