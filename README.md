# Uso De Claves Pub Priv SSH

Aquí mostraré una guía de como conectarnos paso a paso al usuario **`Admin`** de otra máquina mediante claves pública y privada utilizando SSH. 

> [!IMPORTANT]
> Debemos asegurarnos de tener permisos y autorizaciones adecuadas para realizar estas acciones en ambas máquinas.

**En la máquina local (donde ejecutaremos el comando SSH):**

1. **Generaremos un par de claves pública y privada:**
   - Ejecutamos el siguiente comando en la terminal:
     ```bash
     ssh-keygen -t rsa -b 2048
     ```
   - Presionamos **`Enter`** para aceptar la ubicación predeterminada del archivo de la clave y proporcionaremos una contraseña y omitiremos dejando en blanco la **`Passphrase`**.

2. **A continuación Copiaremos la clave pública al servidor remoto:**
   - Usaremos el siguiente comando para copiar la clave pública al servidor remoto:
     ```bash
     ssh-copy-id admin@10.0.9.19
     ```
   - Una vez realicemos el paso anterior proporcionaremos la contraseña del usuario **`Admin`** cuando se solicite.

**En la máquina remota:**

3. **Configuraremos la autenticación con la clave:**
   - Nos conectamos al servidor mediante SSH de la siguiente forma:
     ```bash
     ssh admin@10.0.9.19
     ```
   - Una vez introducido el comando ingresamos la contraseña del usuario **`Admin`**.

4. **Configuración de la autenticación con clave si no se copió automáticamente:**
   - En el servidor, si no se copió automáticamente, podemos agregar manualmente la clave pública al archivo `~/.ssh/authorized_keys`:
     ```bash
     cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
     ```

5. **Ajustaremos los permisos:**
   - Nos aseguraremos de que los permisos de los archivos y carpetas en `~/.ssh/` sean seguros:
     ```bash
     chmod 700 ~/.ssh
     chmod 600 ~/.ssh/authorized_keys
     ```

6. **Cerraremos la conexión SSH y probaremos la autenticación con clave:**
   - Nos desconectamos del servidor SSH:
     ```bash
     exit
     ```
   - Vuelvemos a conectarnos utilizando la autenticación con clave:
     ```bash
     ssh -i ~/.ssh/id_rsa admin@dirección_ip_del_servidor
     ```
   - Si todo ha salido de bien deberiamos conectarnos sin ingresar una contraseña.

Ahora, deberiamos poder conectarnos al usuario **`Admin`** en la máquina remota sin introducir la contraseña, utilizando la autenticación con clave. 

> [!NOTE]
> Debemos asegurarnos de usar las claves con seguridad y protegerlas con contraseñas adecuadas si es necesario.