# RHCSA_Labs

Laboratorio práctico para prepararse para el examen **RHCSA (EX200)** sobre **RHEL 9 / Rocky Linux 9**.

Este repositorio proporciona un entorno de laboratorio listo para usar con **Vagrant**, compuesto por dos máquinas virtuales (**server** y **client**) y un laboratorio guiado con formato similar al examen real.

---

## Características

- Dos máquinas virtuales: `server` y `client`
- Soporte para **VirtualBox** y **KVM/libvirt**
- Box base: `generic/rocky9`
- Disco adicional de **25 GB** en cada máquina (para practicar LVM, particiones, etc.)
- Aprovisionamiento automático con herramientas útiles para el administrador
- Laboratorio estilo examen: **Acme Core**

---

## Requisitos previos

- [Vagrant](https://www.vagrantup.com/)
- Uno de los siguientes hipervisores:
  - **VirtualBox** (opcionalmente con el plugin `vagrant-vbguest`)
  - **KVM/libvirt** (con el plugin `vagrant-libvirt`)
- Al menos:
  - **4 GB de RAM** libres
  - **40 GB** de espacio disponible en disco

### Instalación de plugins (recomendado)

```bash
# Para VirtualBox
vagrant plugin install vagrant-vbguest

# Para KVM/libvirt
vagrant plugin install vagrant-libvirt
```

---

# Cómo levantar el laboratorio

## 1. Clonar el repositorio

```bash
git clone https://github.com/Sebastian294/RHCSA_Labs.git
cd RHCSA_Labs
```

## 2. Elegir el proveedor de virtualización

### Opción A: VirtualBox

```bash
cp Vagrantfile/VB_vagrantfile Vagrantfile
```

### Opción B: KVM / libvirt

```bash
cp Vagrantfile/KVM_vagrantfile Vagrantfile
```

## 3. Levantar las máquinas virtuales

```bash
vagrant up
```

## 4. Conectarse a las máquinas

```bash
vagrant ssh server
vagrant ssh client
```

---

## Credenciales por defecto

| Usuario | Contraseña |
|----------|------------|
| `root` | `redhat` |
| `vagrant` | `vagrant` |

---

## IPs y hostnames configurados por Vagrant

| Máquina | Hostname | Dirección IP |
|----------|----------|--------------|
| `server` | `server.rhcsa.lab` | `192.168.56.10` |
| `client` | `client.rhcsa.lab` | `192.168.56.11` |

> **Nota:** El laboratorio **Acme Core** solicita modificar estos valores (hostname e IP) como parte de la práctica.

---

# Estructura del repositorio

```text
RHCSA_Labs/
├── Labs/
│   └── Acme_core.md          # Laboratorio principal (estilo examen)
├── Vagrantfile/
│   ├── VB_vagrantfile        # Configuración para VirtualBox
│   └── KVM_vagrantfile       # Configuración para KVM/libvirt
├── LICENSE                   # GPL-3.0
└── README.md
```

---

# Laboratorio: Acme Core

**Ubicación:** `Labs/Acme_core.md`

Este laboratorio simula un escenario empresarial (**Acme Corp**) y cubre los principales objetivos del examen RHCSA:

- Configuración de red e identidad (hostname e IP estática)
- Gestión de usuarios y sudo
- Almacenamiento y LVM (VG, LV, XFS y montaje persistente)
- Permisos, ACLs y enlaces simbólicos
- Systemd, servicios y SELinux (Apache en un puerto no estándar)
- Firewalld
- Tareas programadas (cron)
- Búsqueda de archivos y auditoría de logs

---

# Comandos útiles de Vagrant

```bash
# Levantar las máquinas virtuales
vagrant up

# Apagar las máquinas
vagrant halt

# Reiniciar las máquinas
vagrant reload

# Eliminar completamente las máquinas
vagrant destroy -f

# Ver el estado de las máquinas
vagrant status

# Conectarse al servidor
vagrant ssh server

# Conectarse al cliente
vagrant ssh client
```
