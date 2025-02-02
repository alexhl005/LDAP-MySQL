# LDAP-MYSQL

# Instalación de phpLDAPadmin

Este documento detalla los pasos necesarios para instalar y configurar phpLDAPadmin en un servidor que utiliza OpenLDAP.

## Requisitos Previos

Asegúrate de tener un sistema basado en Debian/Ubuntu y acceso de superusuario.

## Pasos de Instalación

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

### 4. Instalar phpLDAPadmin

Instala phpLDAPadmin con el siguiente comando:

```bash
sudo apt install phpldapadmin
```

### 5. Configurar phpLDAPadmin

Edita el archivo de configuración de phpLDAPadmin:

```bash
sudo vi /etc/phpldapadmin/config.php
```

Realiza las siguientes modificaciones:

- **Establecer el servidor a localhost:**

  Busca la línea que comienza con `$servers->setValue('server','host',` y cambia el valor a `'localhost'`.

- **Establecer el DN base:**

  Busca la línea que comienza con `$servers->setValue('server','base',` y establece el valor a tu DN base LDAP. Por ejemplo:

  ```php
  $servers->setValue('server','base',array('dc=example,dc=com'));
  $config->custom->appearance['hide_template_warning'] = true;
  ```

### 6. Reiniciar el Servidor Apache

Reinicia el servidor Apache para aplicar los cambios:

```bash
sudo systemctl restart apache2
```

Puedes acceder a phpLDAPadmin en la siguiente URL:

```
http://ip/phpldapadmin
```

## Transferencia de Archivos

### Para mover archivos del local al servidor

Utiliza el siguiente comando:

```bash
sudo scp -i /home/ubuntu/keypath/"keyname"  /home/ubuntu/filepath/"filename"   ubuntu@178.08.09803:/home/ubuntu
```

### Para mover archivos del servidor al local

Utiliza el siguiente comando:

```bash
sudo scp -i /home/ubuntu/keypath/"keyname" ubuntu@178.08.09803:/home/ubuntu/filepath/"filename"   /home/user/localpath/download/
```

## Configuración del Firewall

Permite el tráfico de OpenLDAP a través del firewall:

```bash
sudo ufw allow "OpenLDAP LDAP"
```

## Aumentar el Tamaño de Carga en phpMyAdmin

Edita el archivo de configuración de PHP:

```bash
sudo vi /etc/php/8.1/apache2/php.ini
```

Ajusta los siguientes parámetros:

```ini
max_execution_time = -1
max_input_time = -1
memory_limit = -1
post_max_size = 4000G 
upload_max_filesize = 3000G
```

## Actualizar la Estructura de phpLDAPadmin

Navega al directorio de phpLDAPadmin y renombra las carpetas:

```bash
cd /usr/share/phpldapadmin/
mv htdocs htdocs.old
mv lib lib.old
```

## Conclusión

Siguiendo estos pasos, deberías tener phpLDAPadmin instalado y funcionando en tu servidor. Para más detalles sobre la configuración, consulta la [documentación oficial de phpLDAPadmin](http://phpldapadmin.sourceforge.net/).
