# 🚀 Instalación y Configuración de OpenLDAP y phpLDAPadmin en Ubuntu 🖥️

## ✅ Requisitos Previos
Antes de comenzar, asegúrate de tener privilegios de superusuario y acceso a Internet en tu sistema Ubuntu.

---

## 🔄 1. Actualización del sistema
Ejecuta el siguiente comando para actualizar los paquetes del sistema:
```sh
sudo apt update
```

---

## 📦 2. Instalación de OpenLDAP
Para instalar OpenLDAP y sus herramientas:
```sh
sudo apt install slapd ldap-utils
```

---

## ⚙️ 3. Configuración de OpenLDAP
Ejecuta el siguiente comando para configurar OpenLDAP:
```sh
sudo dpkg-reconfigure slapd
```

### 🔧 Configuración utilizada en este caso:
- **🌐 Nombre de dominio DNS:** ahl.local
- **🏢 Nombre de la organización:** ahl
- **🔑 Contraseña del usuario administrador:** usuario
- **🗑️ Purgar la base de datos:** YES
- **📂 Mover la base de datos antigua:** YES

---

## 🌍 4. Instalación de phpLDAPadmin
Ejecuta el siguiente comando para instalar phpLDAPadmin:
```sh
sudo apt install phpldapadmin
```

---

## 🔧 5. Configuración de phpLDAPadmin
Edita el archivo de configuración de phpLDAPadmin:
```sh
sudo nano /etc/phpldapadmin/config.php
```

Realiza las siguientes modificaciones:
1. 🔍 Busca la línea:
   ```php
   $servers->setValue('server','host','127.0.0.1');
   ```
   y cámbiala por:
   ```php
   $servers->setValue('server','host','localhost');
   ```
2. 🔍 Busca la línea:
   ```php
   $servers->setValue('server','base',array('dc=example,dc=com'));
   ```
   ❌ Elimínala y añade:
   ```php
   $config->custom->appearance['hide_template_warning'] = true;
   ```

---

## ⚙️ 6. Configuración de PHP
Edita el archivo de configuración de PHP:
```sh
sudo nano /etc/php/8.1/apache2/php.ini
```

✏️ Modifica los siguientes valores:
```ini
max_execution_time = -1
max_input_time = -1
memory_limit = -1
post_max_size = 4000M
upload_max_filesize = 3000M
```

---

## 🏗️ 7. Actualización de phpLDAPadmin
Cambia al directorio de phpLDAPadmin:
```sh
cd /usr/share/phpldapadmin/
```
🛠️ Renombra los directorios existentes:
```sh
sudo mv htdocs htdocs.old
sudo mv lib lib.old
```

---

## 📥 8. Descarga y transferencia de archivos
🔗 Descarga los siguientes archivos en tu equipo local:
- [📂 htdocs.zip](https://drive.google.com/file/d/1KYLHewFJx_Yto2NzmhuFzLdWE5zhLkMW/view)
- [📂 lib.zip](https://drive.google.com/file/d/1o2Ew2mKz_vgQ5tBrhb5qsCDEpp6FNFqi/view)

Para transferirlos al servidor, usa el siguiente comando desde tu máquina local:
```sh
scp ~/Downloads/htdocs.zip ~/Downloads/lib.zip user@192.168.8.45:~
```

---

## 📦 9. Instalación de los nuevos archivos
En el servidor, descomprime los archivos en el directorio de phpLDAPadmin:
```sh
cd /usr/share/phpldapadmin/
sudo unzip ~/htdocs.zip
sudo unzip ~/lib.zip
```

---

## 🔄 10. Finalización
Después de completar los pasos anteriores, reinicia el servicio Apache para aplicar los cambios:
```sh
sudo systemctl restart apache2
```

Ahora puedes acceder a phpLDAPadmin a través de tu navegador ingresando:
```
http://localhost/phpldapadmin
```

---

## 🎉 ¡Listo!
Con estos pasos, OpenLDAP y phpLDAPadmin están correctamente instalados y configurados en tu servidor Ubuntu. 🚀
