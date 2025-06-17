---
# ✅ Checklist de Avance - TP Linux (Debian 12)

---

## 1️⃣ Configuración del entorno

- [x] Generar VM de debian en UTM.
- [x] Blanquear clave `root` y cambiar a “palermo”
- [x] Establecer hostname como `TPServer`

---

## 2️⃣ Servicios

### SSH
- [x] Instalar servicio SSH
- [x] Configurar acceso con clave pública/privada para root

### Apache + PHP
- [x] Instalar Apache
- [x] Instalar PHP (>=7.3)
- [x] Servir `index.php` y `logo.png` desde `/www_dir`

### MariaDB
- [x] Instalar MariaDB
- [x] Importar `db.sql`
- [x] Probar conexión desde `index.php`

---

## 3️⃣ Configuración de Red

- [x] Configurar IP estática `192.168.64.6`
- [x] Incluir ADDRESS, NETMASK y GATEWAY en `/etc/network/interfaces`
- [x] Verificar conectividad local e internet

---

## 4️⃣ Almacenamiento

- [x] Agregar disco de 10 GB
- [x] Crear particiones: `/www_dir` (3 GB), `/backup_dir` (6 GB)
- [x] Formatear y montar (`mkfs.ext4` y `mount`)
- [x] Crear `/www_dir` y `/backup_dir`
- [x] Copiar `index.php` y `logo.png` a `/www_dir`
- [x] Cambiar `DocumentRoot` de Apache a `/www_dir`
- [x] Configurar `fstab` para montaje automático
- [x] Crear archivo `/proc/particion` con el contenido de `/proc/partitions` (vía script)

---

## 5️⃣ Backup

- [x] Crear script `/opt/scripts/backup_full.sh`
- [x] Aceptar argumentos `--origen` y `--destino`
- [x] Incluir ayuda `--help`
- [x] Validar origen y destino existentes y montados
- [x] Generar archivo `nombre_bkp_YYYYMMDD.tar.gz`
- [x] Almacenar backups en `/backup_dir`
- [x] Agregar cronjobs:
  - [x] Todos los días a las 00:00: `/var/log`
  - [x] Lunes, miércoles, viernes a las 23:00: `/www_dir`

---

## 6️⃣ Entregables

- [x] Crear repositorio en GitHub
- [x] Redactar `README.md` con nombres del grupo
- [x] Comprimir y subir a GitHub:
  - [x] `/root`
  - [x] `/etc`
  - [x] `/opt`
  - [x] `/proc`
  - [x] `/www_dir`
  - [x] `/backup_dir`
- [x] Dividir `/var` en partes pequeñas (`split`) si es necesario
- [x] Crear diagrama topológico de la infraestructura.

---
