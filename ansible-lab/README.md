# Laboratorio: Ansible + Docker (Dos servidores Linux)

## Objetivo de la práctica

El objetivo de esta práctica es crear un pequeño laboratorio con dos servidores Linux (contenedores Docker basados en ubuntu:24.04) y administrarlos de forma automatizada utilizando Ansible. Se busca reforzar conceptos como creación de entornos con Docker Compose, configuración de un inventario de Ansible, verificación de conectividad, y escritura de un playbook con módulos, variables, bucles y condicionales.

## Comandos para iniciar los contenedores

docker compose up -d
docker ps

## Instalar Python en cada contenedor

docker exec -it server1 bash -c "apt update && apt install -y python3"
docker exec -it server2 bash -c "apt update && apt install -y python3"

## Comando para verificar la conexión

ansible docker -i inventory.ini -m ping

## Comando para ejecutar el playbook

ansible-playbook -i inventory.ini playbook.yml

El playbook realiza, en ambos servidores:

1. Muestra el nombre del host.
2. Muestra el sistema operativo.
3. Crea el directorio /tmp/ansible-demo.
4. Crea el archivo info.txt con el nombre del servidor y el sistema operativo.
5. Crea, mediante un loop, los subdirectorios logs, backup y config.
6. Muestra un mensaje únicamente cuando el sistema operativo es Ubuntu.

## Captura de pantalla de la ejecución exitosa

![Ejecución exitosa del playbook](screenshot-playbook.png)

## Link del repositorio en GitHub

https://github.com/DelgisMArtinezPerez/practica10parcial
