# Seguridad en SSH

## Objetivo

Asegurar el acceso remoto mediante SSH (Secure Shell) es crucial para proteger servidores y sistemas de accesos no autorizados. SSH es uno de los métodos más utilizados para acceder remotamente a servidores, pero si no se configura correctamente, puede ser una puerta abierta para atacantes. El objetivo es reducir la superficie de ataque, evitar accesos no deseados e implementar medidas efectivas de protección.

---

## Archivo de configuración

El archivo principal para configurar SSH es `/etc/ssh/sshd_config`. En este archivo, se definen las reglas y configuraciones de cómo el servidor SSH maneja las conexiones remotas, la autenticación, y el acceso a los usuarios.

Para editar este archivo de configuración:

```bash
sudo nano /etc/ssh/sshd_config
```

---

## Medidas básicas de hardening

Existen varias prácticas para endurecer la seguridad de SSH. A continuación, se 
describen algunas de las más importantes:

### Deshabilitar acceso root

El acceso directo con el usuario root es muy arriesgado, ya que permite a los 
atacantes tener acceso total al sistema si logran obtener las credenciales o 
explotar alguna vulnerabilidad.

Para deshabilitar el acceso como root:
```bash
PermitRootLogin no
```

### Limitar usuarios permitidos

Limitar el acceso solo a los usuarios que realmente necesitan conectarse vía SSH 
reduce las posibilidades de acceso no autorizado. Esto se puede hacer 
especificando qué usuarios están permitidos.

Para limitar el acceso a ciertos usuarios:
```bash
AllowUsers usuario1 usuario2
```

### Autenticación por claves

La autenticación mediante claves es más segura que las contraseñas, ya que evita 
ataques de fuerza bruta y de diccionario. Para habilitar la autenticación por 
claves y deshabilitar las contraseñas, se deben configurar las siguientes 
opciones en el archivo sshd_config.

Deshabilitar la autenticación por contraseña:
```bash
PasswordAuthentication no
```
Habilitar la autenticación por claves públicas:
```bash
PubkeyAuthentication yes
```

### Cambiar puerto

El puerto por defecto de SSH es el 22. Cambiar este puerto es una medida 
sencilla que ayuda a disminuir el riesgo de ataques automatizados, como 
los intentos de acceso por fuerza bruta, ya que los atacantes suelen 
buscar servidores en este puerto predeterminado. Aunque no es una solución 
definitiva, es una capa adicional de seguridad.

Para cambiar el puerto en el que SSH escucha:
```bash
Port 2222
```

---

## Reinicio del servicio

Para reiniciar el servicio SSH:
```bash
sudo systemctl restart sshd
```

### Uso de claves SSH
El uso de claves SSH es más seguro que las contraseñas. Se recomienda generar un 
par de claves y copiar la clave pública al servidor. La clave privada debe 
mantenerse segura y nunca debe ser compartida.

### Evitar contraseñas débiles
Si decides permitir la autenticación por contraseña (aunque no se recomienda), 
asegúrate de que las contraseñas sean fuertes y únicas. Usa una política de 
contraseñas que requiera una combinación de letras, números y caracteres especiales.

### Monitoreo y revisión de logs

Es importante revisar regularmente los registros de acceso SSH para detectar 
intentos de acceso fallidos o actividades sospechosas. Los registros de SSH se 
encuentran en el archivo /var/log/auth.log.

Puedes revisar los logs en tiempo real con el siguiente comando:
```bash
tail -f /var/log/auth.log
```
### Accesos mínimos

Aplica el principio de mínimo privilegio. Limita el acceso SSH a solo los usuarios 
que realmente necesitan acceso al sistema. Además, asegúrate de que estos usuarios 
no tengan más privilegios de los necesarios. Revoca el acceso de usuarios que ya 
no necesiten acceso al servidor.

Para revisar los usuarios con acceso SSH, puedes usar el comando who o w para ver 
quién está conectado actualmente.
