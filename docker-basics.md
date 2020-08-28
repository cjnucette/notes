# Docker Basics

## Overview
1. Docker: Container Management System.
2. Images: Blueprint for building container. It is compose by layers.
3. Container: Is a running instance of a docker image.

## Container
A container is a process on the machine that runs in isolation on isolated resources. It is an running instance of an image.

## Images
A running container uses an isolated filesystem. This custom filesystem is provided by a **image**. An image is the definition (blueprint) of what is going to be executed, just like an operating system image.

## Dockerfile file.
It is a text based script that is used to define an image. It consists of a series of explicit steps to create said image.

## `docker build . -t my-image-name:my-tag`
Creates an image using the Dockerfile in the current directory (`.`) with the tag name `my-image-name:my-tag`.

# tutorial -> updating our app

## `docker run -it my-image-name:my-tag /bin/sh`
Runs a docker container interactively `-it` named `my-image-name:my-tag`. And after the container is running executes a shell session `/bin/sh`. The container will run as long the main process is running. Once the main process ends, the container will die. In this case, for example, when you exit the shell.


Another options are:
* `-d` to run a container in detached mode (in the background).
* `-p port-number:port-number` to map a port on the host to a port on the container.
* `-v container-path:host-path` to bind directories.

## `docker ps`
Lists currently running containers.

## `docker images`
Lists images stored in your host
