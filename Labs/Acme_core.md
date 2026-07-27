# Contexto Empresarial: Proyecto "Acme Core"

La empresa **Acme Corp** está desplegando un nuevo servidor departamental. Tu tarea es configurar el servidor principal para alojar datos compartidos y un servicio web interno en un puerto no estándar, asegurando que los desarrolladores tengan el acceso correcto. El cliente se utilizará para validar la conectividad.

---

# Objetivos del Laboratorio

## 1. Configuración de Red e Identidad

### Servidor (VM 1)

- Configurar el hostname como:
  - `server.acme.local`
- Asignar la IP estática:
  - `192.168.50.10/24`

### Cliente (VM 2)

- Configurar el hostname como:
  - `client.acme.local`
- Asignar la IP estática:
  - `192.168.50.20/24`

### Validación

- Verificar que ambas máquinas puedan comunicarse entre sí mediante sus direcciones IP.

---

## 2. Gestión de Usuarios y Sudo

En el **server**:

- Crear el grupo:
  - `devops`

- Crear los usuarios:
  - `admin1`
  - `user1`

- Ambos usuarios deben pertenecer al grupo suplementario:
  - `devops`

- Configurar el sistema para que:
  - `admin1` pueda ejecutar cualquier comando mediante `sudo` **sin solicitar contraseña**.

---

## 3. Almacenamiento y LVM

En el **server**, asumiendo que se agregó un nuevo disco (por ejemplo, **5 GB**):

1. Crear un **Volume Group (VG)**:
   - Nombre: `vg_acme`
   - Physical Extent (PE): **8 MiB**

2. Crear un **Logical Volume (LV)**:
   - Nombre: `lv_datos`
   - Tamaño: **50 extents**

3. Formatear el volumen con:
   - Sistema de archivos: `xfs`

4. Montarlo de forma persistente en:
   - `/datos_compartidos`

---

## 4. Permisos, ACLs y Enlaces

En el **server**:

- Cambiar el grupo propietario del directorio:
  - `/datos_compartidos`
  - Grupo: `devops`

- Configurar el directorio para que todos los archivos y subdirectorios nuevos hereden automáticamente el grupo `devops`.

- Configurar **ACLs** para que:
  - `user1` tenga permisos de **solo lectura y ejecución (`r-x`)** sobre el directorio y sobre los nuevos archivos creados.
  - El resto de los miembros del grupo `devops` mantenga acceso completo.

- Crear un enlace simbólico:

| Ubicación | Nombre | Destino |
|-----------|--------|---------|
| `/home/admin1` | `acceso_datos` | `/datos_compartidos` |

---

## 5. Systemd, Servicios y SELinux

En el **server**:

- Instalar el servidor web Apache (`httpd`).

- Configurar Apache para escuchar en el puerto:

  - `8282`

- Ajustar las políticas de **SELinux** para permitir el funcionamiento del servicio en ese puerto.

- Crear un archivo:

  - `index.html`

- Ubicarlo en la raíz de documentos del servidor web con el siguiente contenido:

```html
Servidor Acme OK
```

- Configurar el servicio `httpd` para que:
  - Se inicie automáticamente al arrancar el sistema.

---

## 6. Firewall

En el **server**:

- Configurar **firewalld** para permitir permanentemente el tráfico entrante hacia:

```
8282/tcp
```

### Validación

Desde el **client**, utilizar `curl` para verificar que puede visualizar el contenido de `index.html`.

---

## 7. Tareas Programadas (Cron)

En el **server**:

Crear un **cron job** para el usuario `admin1` que:

- Se ejecute:
  - De lunes a viernes.
  - A las **14:30**.

- Ejecute el comando:

```bash
uptime
```

- Agregue (append) la salida al archivo:

```
/datos_compartidos/registro_cargas.log
```

---

## 8. Búsqueda y Gestión de Logs

### Respaldo de archivos

Buscar todos los archivos dentro de:

```
/etc
```

que cumplan las siguientes condiciones:

- Propietario: `root`
- Tamaño mayor a **2 MB**

Copiarlos al directorio:

```
/root/respaldos/
```

### Auditoría SSH

Buscar todos los eventos relacionados con el servicio **sshd** ocurridos durante el día de hoy (utilizando `journalctl` o `/var/log/secure`) y guardar la salida en:

```
/root/auditoria_ssh.txt
```
