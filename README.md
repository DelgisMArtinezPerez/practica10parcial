# Laboratorio: Ansible + Docker 

## Objetivo de la práctica

El objetivo de esta práctica es crear un pequeño laboratorio con dos servidores Linux (contenedores Docker basados en `ubuntu:24.04`) y administrarlos de forma automatizada utilizando **Ansible**. Se busca reforzar conceptos como:

- Creación de entornos de prueba con Docker Compose.
- Configuración de un inventario de Ansible (`inventory.ini`) usando la conexión tipo `docker`.
- Verificación de conectividad mediante el módulo `ping`.
- Escritura de un playbook que use módulos (`debug`, `file`, `copy`), variables/facts (`ansible_hostname`, `ansible_distribution`), bucles (`loop`) y condicionales (`when`).

## Estructura del repositorio
```text
ansible-lab/
├── docker-compose.yml
├── inventory.ini
├── playbook.yml
└── README.md
```

## Requisitos previos

- Docker y Docker Compose instalados.
- Ansible instalado en la máquina host.

## 1. Iniciar los contenedores

```bash
cd ansible-lab
docker compose up -d
docker ps
```

## 2. Instalar Python en cada contenedor

```bash
docker exec -it server1 bash -c "apt update && apt install -y python3"
docker exec -it server2 bash -c "apt update && apt install -y python3"
```

## 3. Verificar la conexión con Ansible

```bash
ansible docker -i inventory.ini -m ping
```

## 4. Ejecutar el playbook

```bash
ansible-playbook -i inventory.ini playbook.yml
```

El playbook realiza, en ambos servidores:

1. Muestra el nombre del host.
2. Muestra el sistema operativo.
3. Crea el directorio `/tmp/ansible-demo`.
4. Crea el archivo `info.txt` con el nombre del servidor y el sistema operativo.
5. Crea, mediante un `loop`, los subdirectorios `logs`, `backup` y `config`.
6. Muestra un mensaje únicamente cuando el sistema operativo es Ubuntu.

## 5. Captura de pantalla de la ejecución exitosa

<img width="816" height="539" alt="image" src="https://github.com/user-attachments/assets/882da070-0322-498d-966a-37a706866d6c" />


<img width="883" height="493" alt="image" src="https://github.com/user-attachments/assets/43432d99-cfea-4f30-9fe5-60364516383b" />


## Link del repositorio en GitHub

https://github.com/DelgisMArtinezPerez/practica10parcial


## 6. Limpieza (opcional)

```bash
docker compose down
```
