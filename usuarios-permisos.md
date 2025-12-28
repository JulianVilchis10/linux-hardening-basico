# Gestión de Usuarios y Permisos en Linux

## Objetivo
Aplicar buenas prácticas de seguridad en la gestión de usuarios, grupos y permisos
siguiendo el principio de mínimo privilegio.

---

## Creación y administración de usuarios

### Crear un usuario
Se crea un usuario estándar para evitar el uso del usuario root en tareas diarias.
```bash
sudo adduser usuario_test
```

### Ver información del usuario
Permite verificar UID, GID y grupos asignados al usuario.
```bash
id usuario_test
```

### Eliminar un usuario
Permite remover una cuenta de usuario del sistema. Sirve de manera segura para 
revocar el acceso a la cuenta cuando un usuario deje la organización(grupo).
En entornos productivos se recomienda revisar archivos y procesos asociados 
antes de eliminar la cuenta.
```bash
sudo deluser usuario_test
```
---

## Gestión de grupos

### Crear un grupo
Crea un grupo estándar.
```bash
sudo groupadd grupo_seguridad
```

### Agregar un usuario a un grupo
Añade un nuevo usuario a la organización(grupo)
``` bash
sudo usermod -aG grupo_seguridad usuario_test
```

### Ver grupos de un usuario
Permite verificar en que grupos se encuentra un usuario, los usuarios pueden 
pertenecer a más de un grupo.
```bash
groups usuario_test
```

---

## Permisos de archivos y directorios

### Ver permisos
Muestra los permisos del archivo dividido en grupo, propietario y otros.
Los permisos son de escritura(w), lectura(r), y ejecución(x)
```bash
ls -l archivo.txt
```

### Cambiar los permisos con chmod
Cambia los permisos que tiene cada usuario o grupo. El valor 640 representa 
los permisos asignados lectura(6), escritura(4) y ejecución(0), donde lectura = 4,
escritura = 2 y ejecución = 1.
```bash
chmod 640 archivo.txt
```

### Cambiar de propietario y grupo
Sirve para cambiar de propietario, este comando suele confundirse con chmod aunque 
son completamente distintos, uno otorga o quita permisos mientras que el otro 
cambia el propietario.
```bash
sudo chown usuario_test:grupo_seguridad archivo.txt
```

---
