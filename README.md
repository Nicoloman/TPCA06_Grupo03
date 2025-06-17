# TPCA06_Grupo03

## 👥 Integrantes del grupo

- Nicolás Lomanto  
- Rene Lludgar
- Thiago Garcia
- Assael Bussi
- Emanuel Silva

## 🧠 Descripción

Trabajo práctico realizado en una máquina virtual Debian 12 ARM64, cuyo objetivo principal fue configurar servicios básicos de red y servidor, implementar backups automáticos y comprender la administración de sistemas Linux.

---

## ⚙️ Configuración realizada

### 🖥️ Entorno

- SO: Debian 12 (arm64)
- Hostname configurado: `TPServer`
- IP estática configurada:
  - IP: `192.168.64.6`
  - Netmask: `255.255.255.0`
  - Gateway: `192.168.64.1`

---

### 🔐 Usuarios

- `root` → contraseña: `palermo`
- `alumno` → contraseña: `alumno`

---

### 📁 Compartición de archivos

Se montó una carpeta compartida desde UTM para intercambiar archivos adicionales (claves, scripts, etc.):  
```bash
mount -t 9p -o trans=virtio share /mnt/mac
```

---

### 🌐 Conexión remota por SSH

Acceso remoto habilitado al usuario `root` mediante clave privada:

```bash
ssh -i clave_privada.txt root@192.168.64.6
```

---

### 🌍 Servicios instalados

#### 1. Apache + PHP

```bash
sudo apt install apache2 php libapache2-mod-php -y
```

- Se configuró `DocumentRoot` a `/www_dir`
- Se instaló soporte PHP y se creó archivo `test.php` para validar funcionamiento
- Se activó debug con:
```php
error_reporting(E_ALL);
ini_set('display_errors', 1);
```

#### 2. MariaDB

```bash
sudo apt install mariadb-server -y
```

- Se importó la base de datos desde `db.sql`
- Se resolvió error de PHP (`Class "MySQLi" not found`) instalando extensión MySQLi

#### 3. Index personalizado

- Se colocó un `index.php` y un `logo.png` personalizado (logo de UP)

---

### 💾 Almacenamiento y particiones

- Se agregó un segundo disco de **10 GB**
- Se particionó con `fdisk` en:
  - `/dev/vdb1` → 3 GB → `/www_dir`
  - `/dev/vdb2` → 6 GB → `/backup_dir`

#### Montaje:

```bash
mkfs.ext4 /dev/vdb1
mkfs.ext4 /dev/vdb2
mkdir /www_dir
mkdir /backup_dir
```

- Se configuró `/etc/fstab` para montaje automático al inicio.

---

### 🗃️ Script de Backup

Ruta: [`/opt/scripts/backup_full.sh`](adicionales/backup_full.sh)

#### Funcionalidad:
- Acepta argumentos `--origen` y `--destino`
- Crea backups comprimidos (`.tar.gz`) con formato `nombre_bkp_YYYYMMDD`
- Valida existencia y disponibilidad de origen/destino
- Muestra ayuda con `--help` o `-h`

#### Tareas programadas (`cron`):
- Todos los días a las 00:00 → backup de `/var/log`
- Lunes, miércoles y viernes a las 23:00 → backup de `/www_dir`

Ejemplo de ejecución manual:

```bash
/opt/scripts/backup_full.sh -o /var/log -d /backup_dir
```

---

### 📁 Estructura entregada

Se comprimieron individualmente los siguientes directorios en `.tar.gz`:

- `/root`
- `/etc`
- `/opt`
- `/proc`
- `/www_dir`
- `/backup_dir`

---

### 🗺️ Diagrama topológico

![Diagrama Topológico](diagrama_topologia.png)

```
[Usuario] → SSH → [Debian 12 VM - TPServer]
                   ├── Apache (index.php + logo.png)
                   ├── MariaDB (datos importados)
                   ├── /www_dir (3 GB)
                   ├── /backup_dir (6 GB)
                   ├── Cron + Script de Backup
                   └── IP Estática: 192.168.64.6
```

---
