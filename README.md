# LDAP-MYSQL
# 🌟 Instalación de phpLDAPadmin 🌟

Este documento detalla los pasos necesarios para instalar y configurar phpLDAPadmin en un servidor que utiliza OpenLDAP.

## 📋 Requisitos Previos

Asegúrate de tener un sistema basado en Debian/Ubuntu y acceso de superusuario.

## 🚀 Pasos de Instalación

### 1. Actualizar el Sistema

Ejecuta el siguiente comando para asegurarte de que tu sistema esté actualizado:

```bash
sudo apt update
```

### 2. Instalar OpenLDAP

Instala OpenLDAP y las utilidades necesarias:

```bash
sudo apt install slapd ldap-utils
```

### 3. Configurar OpenLDAP

Configura OpenLDAP ejecutando:

```bash
sudo dpkg-reconfigure slapd
```

**En tu caso, utiliza los siguientes valores:**

- **🌐 Nombre de dominio DNS:** `ahl.local`
- **🏢 Nombre de la organización:** `ahl`
- **🔑 Contraseña:** `usuario`
- **🗑️ Purgar la base de datos:** `YES`
- **📦 Mover la base de datos antigua:** `YES`

### 4. Instalar phpLDAPadmin

Instala phpLDAPadmin con el siguiente comando:

```bash
sudo apt install phpldapadmin
```

### 5. Configurar phpLDAPadmin

Edita el archivo de configuración de phpLDAPadmin:

```bash
sudo nano /etc/phpldapadmin/config.php
```

Realiza las siguientes modificaciones:

- **🔄 Cambiar el host:**

  Busca la línea:

  ```php
  $servers->setValue('server','host', '127.0.0.1');
  ```

  y cámbiala a:

  ```php
  $servers->setValue('server','host', 'localhost');
  ```

- **🗂️ Modificar la base DN:**

  Busca la línea:

  ```php
  $servers->setValue('server','base',array('dc=example,dc=com'));
  ```

  y bórrala. Luego, agrega:

  ```php
  $config->custom->appearance['hide_template_warning'] = true;
  ```

### 6. Configurar PHP

Edita el archivo de configuración de PHP:

```bash
sudo nano /etc/php/8.1/apache2/php.ini
```

Cambia los valores por defecto de las siguientes líneas:

```ini
max_execution_time = -1
max_input_time = -1
memory_limit = -1
post_max_size = 4000M
upload_max_filesize = 3000M
```

### 7. Actualizar la Estructura de phpLDAPadmin

Navega al directorio de phpLDAPadmin y renombra las carpetas:

```bash
cd /usr/share/phpldapadmin/
sudo mv htdocs htdocs.old
sudo mv lib lib.old
```

### 8. 📥 Descargar Archivos Necesarios

Descarga los siguientes archivos y transfiérelos al servidor:

- [Archivo 1](https://drive.google.com/file/d/1KYLHewFJx_Yto2NzmhuFzLdWE5zhLkMW/view)
- [Archivo 2](https://drive.google.com/file/d/1o2Ew2mKz_vgQ5tBrhb5qsCDEpp6FNFqi/view)

**📤 Ejemplo para pasar los archivos:**

```bash
scp ~/Downloads/htdocs.zip ~/Downloads/lib.zip user@192.168.8.45:~
```

### 9. Descomprimir Archivos en el Servidor

Navega al directorio de phpLDAPadmin y descomprime los archivos:

```bash
cd /usr/share/phpldapadmin/
sudo unzip ~/htdocs.zip
sudo unzip ~/lib.zip
```

## ✅ Conclusión

Siguiendo estos pasos, deberías tener phpLDAPadmin instalado y funcionando en tu servidor.
