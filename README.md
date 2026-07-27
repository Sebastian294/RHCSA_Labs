# RHCSA_Labs

Laboratorio práctico para prepararse al examen **RHCSA (EX200)** sobre **RHEL 9 / Rocky Linux 9**.

Este repositorio proporciona un entorno de laboratorio listo para usar con **Vagrant**, compuesto por dos máquinas virtuales (server + client), y un laboratorio guiado estilo examen real.

## Características

- Dos VMs: `server` y `client`
- Soporte para **VirtualBox** y **KVM/libvirt**
- Box base: `generic/rocky9`
- Disco adicional de 25 GB en cada máquina (para practicar LVM, particiones, etc.)
- Aprovisionamiento automático con herramientas útiles para el administrador
- Laboratorio estilo examen: **Acme Core**

## Requisitos previos

- [Vagrant](https://www.vagrantup.com/)
- Uno de los siguientes hipervisores:
  - **VirtualBox** + plugin `vagrant-vbguest` (opcional)
  - **KVM/libvirt** + plugin `vagrant-libvirt`
- Al menos **4 GB de RAM** libres y **40 GB** de espacio en disco

### Instalación de plugins (recomendado)

```bash
# Para VirtualBox
vagrant plugin install vagrant-vbguest

# Para KVM/libvirt
vagrant plugin install vagrant-libvirt
```
Cómo levantar el laboratorio

Clona el repositorio:

Bashgit clone https://github.com/Sebastian294/RHCSA_Labs.git
cd RHCSA_Labs

Elige el proveedor que vas a usar y copia el Vagrantfile correspondiente:

Bash# Opción A: VirtualBox
cp Vagrantfile/VB_vagrantfile Vagrantfile

# Opción B: KVM / libvirt
cp Vagrantfile/KVM_vagrantfile Vagrantfile

Levanta las máquinas:

Bashvagrant up

Conéctate a las VMs:

Bashvagrant ssh server
vagrant ssh client
Credenciales por defecto:

Usuario: root / vagrant
Contraseña: redhat

IPs y hostnames configurados por Vagrant


Máquina,Hostname,IP
server,server.rhcsa.lab,192.168.56.10
client,client.rhcsa.lab,192.168.56.11




Nota: El laboratorio Acme Core te pide cambiar estos valores (hostname e IP) como parte de la práctica.
Estructura del repositorio
textRHCSA_Labs/
├── Labs/
│   └── Acme_core.md          # Laboratorio principal (estilo examen)
├── Vagrantfile/
│   ├── VB_vagrantfile        # Configuración para VirtualBox
│   └── KVM_vagrantfile       # Configuración para KVM/libvirt
├── LICENSE                   # GPL-3.0
└── README.md
Laboratorio: Acme Core
Ubicación: Labs/Acme_core.md
Este laboratorio simula un escenario real de empresa (Acme Corp) y cubre los siguientes objetivos del examen RHCSA:

Configuración de red e identidad (hostname + IP estática)
Gestión de usuarios y sudo
Almacenamiento y LVM (VG, LV, XFS, montaje persistente)
Permisos, ACLs y enlaces simbólicos
Systemd, servicios y SELinux (Apache en puerto no estándar)
Firewalld
Tareas programadas (cron)
Búsqueda de archivos y auditoría de logs

# Comandos útiles de Vagrant
```bash
vagrant up              # Levantar las VMs
vagrant halt            # Apagar
vagrant reload          # Reiniciar
vagrant destroy -f      # Eliminar completamente
vagrant status          # Ver estado
vagrant ssh server      # Entrar al servidor
vagrant ssh client      # Entrar al cliente
```
