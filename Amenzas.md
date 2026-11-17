# Amenazas

## Autenticación

### Fuerza bruta

**Definición:** muchos intentos de inicio de sesión contra un servicio; en este caso, SSH.

**Ejemplo:** varios inicios de sesión fallidos con distintas contraseñas para el mismo usuario y desde la misma dirección IP.

**Detección:** si se producen `N` fallos desde la misma IP para el mismo usuario, generar una alerta y considerar bloquear la IP.

### Password spraying

**Definición:** intentos de inicio de sesión con una misma contraseña contra varios usuarios. La IP de origen es la misma.

**Detección:** detectar muchos intentos de inicio de sesión desde una misma IP y generar una alerta; considerar bloquearla.

**Flujo de respuesta:**

`Detección → Alerta → Investigar la IP → Bloquear la IP → Revisar las cuentas afectadas → Comprobar si hubo algún inicio de sesión exitoso`

Si se detecta un inicio de sesión exitoso, generar una alerta.

### Inicio de sesión exitoso tras varios intentos sospechosos

Puede que no se alcance el umbral necesario para detectar un ataque de fuerza bruta o *password spraying*. Aun así, se generará una alerta si se producen `N` fallos antes de un inicio de sesión exitoso, ya que el comportamiento resulta sospechoso.

## Cuentas

Se supervisarán los cambios en el grupo de administradores. Si se añade un usuario, se generará una alerta por tratarse de una acción potencialmente sospechosa.

## Escalamiento de privilegios

Casos que se deben detectar:

1. Usuario normal → `sudo` → modificación de usuarios.
2. Usuario normal → `sudo` → modificación de servicios.
3. Usuario normal → `sudo` → modificación de la configuración de SSH.

## Procesos

Al detectar un proceso nuevo, investigar:

- ¿Quién lo ejecutó?
- ¿Con qué privilegios?
- ¿Desde dónde se ejecutó?
- ¿Qué procesos padre tiene?

Si se detecta algo sospechoso, generar una alerta.

## Red

### Escaneo de puertos

Detectar el uso de herramientas de escaneo de puertos, como `nmap`.

**Detección:** muchas solicitudes desde una misma IP en un intervalo corto generan una alerta.

### Conexiones a muchos hosts

**Detección:** si un host interno intenta conectarse a muchos servidores desconocidos, generar una alerta.

## Archivos

Supervisar los archivos sensibles. Si se modifica alguno, analizar si el cambio es peligroso y generar una alerta cuando corresponda.

## Daemons y servicios

Supervisar los cambios en daemons y mecanismos de inicio, por ejemplo:

- Servicios de `systemd`
- Tareas de `cron`
- `authorized_keys` de SSH
- Scripts de inicio

Si aparece un daemon nuevo, investigar qué hace, quién lo ejecutó y con qué permisos.

## Web

Pendiente de definir.

## Malware

Pendiente de definir.
