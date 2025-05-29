# **Cinammon.net Changelog**

## v1.11.11
### Corregido
* Copias de seguridad con contenido faltante cuando se utiliza un archivo `.cinammonignore`
* Archivos comprimidos originados desde un subdirectorio que no contiene archivos ([#5030](https://github.com/cinammon-net/panel/issues/5030))

## v1.11.10
### Corregido
* Archivos comprimidos que aleatoriamente ignoran archivos y directorios ([#5027](https://github.com/cinammon-net/panel/issues/5027))
* Caída del sistema al eliminar o transferir un servidor ([#5028](https://github.com/cinammon-net/panel/issues/5028))

## v1.11.9
### Cambios
* Los binarios de la versión ahora están construidos con Go 1.21.8
* Actualización de las dependencias de Go

### Corregido
* [CVE-2024-27102](https://www.cve.org/CVERecord?id=CVE-2024-27102)

## v1.11.8
### Cambios
* Los binarios de la versión ahora están construidos con Go 1.20.10 (resuelve [CVE-2023-44487](https://www.cve.org/CVERecord?id=CVE-2023-44487))
* Actualización de las dependencias de Go

## v1.11.7
### Cambios
* Actualización de las dependencias de Go (esto resuelve un problema relacionado con `http: invalid Host header` con Docker)
* Wings ahora está construido con go1.19.11

## v1.11.6
### Corregido
* CVE-2023-32080

## v1.11.5
### Añadido
* Se añadió una opción de configuración para deshabilitar las actualizaciones del archivo `config.yml` de Wings desde el Panel ([commit](https://github.com/cinammon-net/wings/commit/ec6d6d83ea3eb14995c24f001233e85b37ffb87b))

### Cambios
* Wings ahora está construido con Go 1.19.7

### Corregido
* Se corrigió el manejo de archivos comprimidos que contenían nombres de archivos parcialmente coincidentes ([commit](https://github.com/cinammon-net/wings/commit/43b3496f0001cec231c80af1f9a9b3417d04e8d4))

## v1.11.4
### Corregido
* CVE-2023-25168

## v1.11.3
### Corregido
* CVE-2023-25152

## v1.11.2
### Corregido
* Las copias de seguridad restauradas desde almacenamiento remoto (s3) generaban errores debido a un flujo cerrado.
* Corregida la lógica de validación de IP para los registros de actividad, que filtraban IPs válidas en lugar de IPs inválidas.

## v1.11.1
### Cambios
* Los binarios de la versión ahora están construidos con Go 1.18.10
* El tiempo de espera al detener un servidor antes de que comience una transferencia se ha reducido a 15 segundos desde 1 minuto.
* Se eliminaron los protocolos SSH inseguros para su uso con el servidor SFTP.

### Corregido
* Se dejaron conexiones innecesarias de cliente Docker abiertas, causando una fuga lenta de descriptores de archivo.
* Archivos que quedaban abiertos en partes del sistema de archivos del servidor, causando una fuga de descriptores de archivo.
* Se corrompían las direcciones IPv6 debido a una lógica defectuosa para el despojo de puertos en los registros de actividad, las entradas antiguas con IPs mal formadas serán eliminadas automáticamente de la base de datos SQLite local.
* Un servidor que se queda atascado en estado de transferencia ya no se detiene si se agota el tiempo al detenerse al principio de la transferencia.

## v1.11.0
### Añadido (desde 1.7.2)
* Información más detallada devuelta por el endpoint `/api/system` al usar el parámetro de consulta `?v=2`.

### Cambios (desde 1.7.2)
* Se envía el estado de reinstalación por separado del estado de instalación.
* Las versiones de Wings ahora seguirán la versión mayor y menor del Panel.
* Las transferencias ya no se almacenan en disco, ahora se transmiten completamente con solo una pequeña cantidad de memoria usada para el almacenamiento en búfer.
* Los binarios de la versión ya no se comprimen con UPX.
* Se utiliza `POST` en lugar de `GET` para enviar el estado de una transferencia al Panel.

### Corregido (desde 1.7.2)
* Corregido que las IPs salientes de los servidores no se actualizan cuando se cambia la asignación principal de un servidor usando la opción `Force Outgoing IP`.
* Corregido que los servidores se terminaban en lugar de detenerse correctamente cuando se usaba una señal para detener el contenedor en lugar de un comando.
* Corregido que los errores de archivo no encontrado se trataban como un error interno, ahora se tratan como un 404.
* Wings puede ejecutarse con Podman en lugar de Docker, esto sigue siendo experimental y no se recomienda para su uso en producción.
* Ahora se informa correctamente el progreso de los archivos comprimidos.
* Las etiquetas para los contenedores ahora pueden ser configuradas desde el Panel.
* Corregido que los servidores se quedaran bloqueados cuando el nodo de destino de una transferencia se desconectaba.

## v1.11.0-rc.2
### Añadido
* Información más detallada devuelta por el endpoint `/api/system` al usar el parámetro de consulta `?v=2`.

### Cambios
* Enviar el estado de reinstalación por separado del estado de instalación.

### Corregido
* Corregido que las IPs salientes de los servidores no se actualizan cuando se cambia la asignación principal de un servidor usando la opción `Force Outgoing IP`.
* Corregido que los servidores se terminaban en lugar de detenerse correctamente cuando se usaba una señal para detener el contenedor en lugar de un comando.
* Corregido que los errores de archivo no encontrado se trataban como un error interno, ahora se tratan como un 404.

## v1.11.0-rc.1
### Cambios
* Las versiones de Wings ahora seguirán la versión mayor y menor del Panel.
* Las transferencias ya no se almacenan en disco, ahora se transmiten completamente con solo una pequeña cantidad de memoria usada para el almacenamiento en búfer.
* Los binarios de la versión ya no se comprimen con UPX.

### Corregido
* Wings puede ejecutarse con Podman en lugar de Docker, esto sigue siendo experimental y no se recomienda para su uso en producción.
* Ahora se informa correctamente el progreso de los archivos comprimidos.
* Las etiquetas para los contenedores ahora pueden ser configuradas desde el Panel.

## v1.7.5
### Corregido
* CVE-2023-32080

## v1.7.4
### Corregido
* CVE-2023-25168

## v1.7.3
### Corregido
* CVE-2023-25152

## v1.7.2
### Corregido
* El controlador de copias de seguridad de S3 ahora admite Cloudflare R2

### Añadido
* Durante una transferencia de servidor, ahora hay un nuevo estado "Archivado" que muestra el progreso de la creación del archivo de transferencia del servidor.
* Se añadió una opción de configuración para controlar la lista de proxies confiables que se pueden utilizar para determinar la dirección IP del cliente.
* Se añadió una opción de configuración para controlar la configuración del espacio de nombres del usuario de Docker cuando Wings crea contenedores.

### Cambios
* Las versiones ahora se construyen usando `Go 1.18` — ahora la versión mínima requerida para construir Wings es `Go 1.18`.

## v1.7.1
### Corregido
* El analizador YAML se ha actualizado para corregir algunos problemas extraños

### Añadido
* Añadida la opción `Force Outgoing IP` para servidores para asegurar que el tráfico saliente utilice la dirección IP del servidor
* Se añadió una opción para controlar el nivel de compresión gzip para las copias de seguridad

## v1.7.0
### Corregido
* Se corrigió el soporte multiplataforma para la imagen Docker de Wings.

### Añadido
* Se añadió soporte para el seguimiento de acciones de SFTP, acciones de energía, comandos de servidor y cargas de archivos utilizando una base de datos SQLite local y procesando eventos antes de enviarlos al Panel.
* Se añadió soporte para configurar el MTU en la red `pelican0`.

## v1.6.4
### Corregido
* Se corrigió un error que causaba que la limitación de CPU no se aplicara correctamente a los servidores.
* Se corrigió un error que causaba que los archivos comprimidos se descomprimieran sin tener en cuenta las estructuras de carpetas anidadas.

## v1.6.3
### Corregido
* Se corrigió la autenticación de SFTP que fallaba para los usuarios administrativos debido a un ajuste de permisos en el Panel.

## v1.6.2
### Corregido
* Se corrigió que el tamaño de carga de archivos no se aplicaba correctamente.
* Se corrigió un error que impedía listar un directorio cuando contenía un pipe nombrado. También se añadió una comprobación para evitar intentar leer un pipe nombrado directamente.
* Se corrigió un error con la lógica del archivador que incluiría carpetas que tenían el mismo prefijo de nombre. (por ejemplo, solicitar solo `map` también incluiría `map2` y `map3`)
* Las solicitudes al Panel que devuelven un error de cliente (código de respuesta 4xx) ya no activan una retroalimentación exponencial, detienen inmediatamente la solicitud.

### Cambios
* Los campos de limitación de CPU solo se establecen en el contenedor Docker si se han especificado para el servidor, de lo contrario, se dejan vacíos.

### Añadido
* Se añadió la capacidad de definir la ubicación de la carpeta temporal utilizada por Wings — por defecto en `/tmp/pelican`.
* Se añadió la capacidad de autenticarse para SFTP utilizando claves públicas (requiere `Panel@1.8.0`).


## v1.6.1
### Corregido
* Corrige un error que a veces ocurría al iniciar un servidor y que causaba que el bloqueo temporal de la acción de energía nunca se liberara debido a un canal bloqueado.
* Corrige un error que causaba que el uso de CPU de Wings se quedara al 100% cuando un servidor se eliminaba mientras el proceso de instalación estaba en ejecución.

### Cambios
* Se limpia gran parte de la lógica para manejar eventos entre el servidor y el proceso de entorno para facilitar modificaciones futuras.
* Se limpia la lógica de manejo de `StopAndWait` para detener un servidor de manera ordenada antes de terminar el proceso si no responde.

## v1.6.0
### Corregido
* Se ajustó la lógica interna para procesar un evento de inicio de servidor para adjuntarlo al contenedor Docker antes de intentar iniciar el contenedor. Esto debería solucionar problemas donde un servidor se quedaba atascado después de extraer la imagen del contenedor.
* Se corrige un error en la salida de la consola que dejaba caer líneas cuando se enviaban muchas líneas a la vez.

### Cambios
* Se eliminó la lógica de limitación de consola que terminaba una instancia de servidor que enviaba demasiados datos. Esta lógica se ha reemplazado por una lógica más sencilla que solo limita la consola, sin intentar terminar el servidor. Además, este cambio ha reducido la cantidad de go-routines necesarias y simplificado dramáticamente la lógica interna.
* Se eliminó la opción `--profiler` y se reemplazó por `--pprof`, que inicia un servidor interno escuchando en `localhost:6060`, permitiéndote usar las herramientas estándar de `pprof` de Go.
* Se reemplazó el controlador de registros `json` para contenedores Docker por `local` para reducir la sobrecarga al transmitir registros desde las instancias.

## v1.5.6
### Corregido
* Reescribió la lógica del controlador para el bloqueo de las acciones de energía para abordar los problemas que se habían estado presentando cuando un servidor fallaba y no podía iniciarse nuevamente hasta reiniciar Wings.
* Corrige los archivos cargados con SFTP que no eran propiedad del usuario **Cinammon**.
* Corrige el uso excesivo de memoria cuando se enviaban líneas grandes a través del controlador de eventos de la consola.

### Cambios
* Se reemplazó el uso de `encoding/json` en toda la base de código por un codificador más eficiente (`goccy/go-json`) para mejorar el rendimiento general de las operaciones JSON.
* Se añadió una función personalizada `ContainerInspect` para manejar llamadas directas al CLI de Docker y hacer uso de la nueva lógica de codificación JSON. Esto debería reducir la cantidad total de asignaciones de memoria y mejorar el rendimiento en un camino crítico.

## v1.5.5
### Corregido
* Corrige el envío a un canal cerrado cuando se envían registros del servidor a través del websocket.
* Corrige que el comando `wings diagnostics` no subiera contenido.
* Corrige un pánico causado por el bus de eventos que cerraba canales varias veces cuando se eliminaba un servidor.

## v1.5.4
### Corregido
* Corrige las rutas SSL que se convertían incorrectamente a minúsculas en entornos donde la ruta es sensible a mayúsculas y minúsculas.
* Corrige una fuga de memoria debido a la implementación del procesamiento de eventos del servidor.

### Cambios
* Al seleccionar redactar información, ahora también se redactan las URLs de la salida de los registros al ejecutar el comando de diagnóstico.

### Añadido
* Se añade soporte para modificar los porcentajes de sobrecarga de memoria predeterminados en entornos donde los valores predeterminados no son adecuados.
* Se añade soporte para enviar el encabezado `Access-Control-Request-Private-Network` en entornos donde Wings será accedido a través de una red privada. Esto está configurado por defecto en `off`.

## v1.5.3
### Corregido
* Corrige el registro incorrecto de eventos y el manejo de errores durante la autenticación del socket que causaba que el mensaje de error incorrecto se devolviera al cliente, o que no se devolviera ningún error en algunos escenarios. El registro de eventos ahora se retrasa hasta que el socket esté completamente autenticado para evitar registrar oyentes innecesarios.
* Corrige que los signos de dólar siempre se evaluaban como variables de entorno sin forma de escaparlas. Ahora se pueden escapar como `$$`, lo que se transformará en un solo signo de dólar.

### Cambios
* Una conexión websocket a un servidor será cerrada por Wings si se encuentra un error de envío, dejando que el cliente maneje las reconexiones, en lugar de simplemente registrar el error y seguir escuchando nuevos eventos.

## v1.5.2
### Corregido
* Corrige que los servidores no se resincronizaban correctamente con el Panel si ya estaban en ejecución, causando que se detuvieran de manera forzada cuando se terminaban, en lugar de detenerse con la acción configurada.

### Cambios
* Se cambió la implementación del servidor SFTP para usar claves de servidor ED25519 en lugar de claves SHA1 RSA obsoletas.

### Añadido
* Se añade la salida de tiempo de actividad del servidor en el evento de estadísticas emitido al websocket.

## v1.5.1
### Añadido
* Opción de configuración global para activar o desactivar la detección de fallos del servidor (`system.crash_detection.enabled`)
* Especificación de archivo RPM.

## v1.5.0
### Corregido
* Corrige una condición de carrera al establecer el nombre de la aplicación en la salida de la consola para un servidor.
* Corrige que la reinstalación de un servidor causara que el parámetro `file_denylist` de un Egg fuera ignorado hasta que Wings se reiniciara.
* Corrige el analizador de archivos YAML que no configuraba correctamente los valores booleanos.
* Corrige un posible problema en el que la conexión websocket subyacente se cerraba pero el contexto de la solicitud principal aún no se cancelaba, lo que provocaba una escritura sobre una conexión cerrada.
* Corrige una condición de carrera al cerrar todas las conexiones websocket activas cuando se elimina un servidor.
* Corrige la lógica para determinar si el contexto de un servidor se ha cerrado y enviar un mensaje de cierre de websocket a los clientes conectados. Anteriormente, esto se activaba cuando se cerraba la solicitud en sí, y no cuando el contexto del servidor se cerraba.

### Añadido
* Se expone el puerto `8080` en la configuración predeterminada de Docker para dar mejor soporte a las herramientas proxy.

### Cambios
* Las versiones se construyen ahora usando `Go 1.17` — la versión mínima requerida para construir Wings sigue siendo `Go 1.16`.
* Se simplificó la lógica que impulsa las actualizaciones del servidor para solo obtener información del Panel en lugar de tratar de aceptar valores actualizados. Todas las partes de Wings que necesiten los detalles más actualizados del servidor deben llamar a `Server#Sync()` para obtener la última información almacenada.
* `Installer#New()` ya no requiere pasar todos los datos del servidor como un trozo de bytes, sino que se expone una nueva estructura `Installer#ServerDetails` que se puede pasar y acepta un UUID y si el servidor debe iniciarse después de que el instalador termine.

### Eliminado
* Se elimina la lógica complicada (y no utilizada) durante el proceso de instalación del servidor que era un remanente de arquitecturas anteriores de Wings.
* Se elimina el endpoint `PATCH /api/servers/:server` — si antes usabas esta llamada API, debe ser reemplazada por `POST /api/servers/:server/sync`.

## v1.4.7
### Corregido
* El acceso SFTP ahora está correctamente denegado si un servidor está suspendido.
* Se usa correctamente el `start_on_completion` y `crash_detection_enabled` para los servidores.

## v1.4.6
### Corregido
* Las variables de entorno que comienzan con el mismo prefijo ya no se combinan en un solo valor de variable de entorno (omitidas todas excepto la primera).
* El indicador `start_on_completion` para instalaciones de servidores ahora iniciará correctamente el servidor.
* Corrige que los archivos de socket causaban involuntariamente la cancelación de respaldos.
* Los archivos extraídos de un respaldo ahora tienen el modo correcto en los archivos restaurados, en lugar de predeterminarse a `0644`.
* Corrige problemas de logrotate debido a una mala configuración de usuario en algunos sistemas.

### Actualizado
* La versión mínima de Go requerida para compilar Wings ahora es `go1.16`.

### Deprecado
> Estas dos deprecaciones se eliminarán en `Wings@2.0.0`:
* El método `Server.Id()` ha sido reemplazado por `Server.ID()`.
* El campo `directory` en el endpoint `/api/servers/:server/files/pull` está obsoleto y debe actualizarse a `root` para mantener consistencia con otros endpoints.

## v1.4.5
### Cambios
* Se aumentó el límite de procesos para un contenedor de `256` a `512` para abordar casos extremos de algunos juegos que generan muchos procesos.

## v1.4.4
### Añadido
* **[Seguridad]** Se añade soporte para limitar el número total de pids que un contenedor puede tener activos a la vez para evitar que los usuarios malintencionados impacten otras instancias en el mismo nodo.
* Los contenedores de instalación del servidor ahora usan los límites asignados al servidor o una cantidad mínima globalmente definida de memoria y CPU, en lugar de tener recursos ilimitados.

## v1.4.3
Este build se creó para abordar `CVE-2021-33196` en `Go`, lo que requiere una nueva compilación binaria usando la versión más reciente de `go1.15`.

## v1.4.2
### Corregido
* Corrige que el carácter `~` no se recortaba correctamente de los nombres de imágenes de contenedor al crear un servidor.

### Cambios
* Implementación de retroceso exponencial para cargas S3 al trabajar con respaldos. Esto debería resolver muchos problemas con sistemas S3 compatibles que a veces devuelven errores de tipo 5xx que deberían reintentarse automáticamente.
* Se implementa retroceso exponencial para todas las llamadas API al Panel que no devuelven inmediatamente un error 401, 403 o 429. Esto aborda la fragilidad en algunas llamadas API y resuelve fallos de llamadas aleatorias debido a desconexiones o errores aleatorios de resolución DNS.

## v1.4.1
### Corregido
* Corrige un error que provocaba que el proceso de descompresión de archivos pusiera todos los archivos en el directorio base en lugar del directorio en el que deberían estar ubicados.

## v1.4.0
### Corregido
* **[Breaking]** Corrige que `/api/servers` y `/api/servers/:server` no devolvía correctamente toda la información relevante del servidor y el uso de recursos.
* Corrige que Wings leía incorrectamente `WINGS_UID` y no `WINGS_GID` al ejecutarse en entornos contenerizados.
* Corrige un pánico al devolver los contenidos de un archivo que está siendo escrito activamente por otro proceso.
* Se corrige el manejo de archivos que se descomprimen para admitir correctamente archivos `.rar`.
* Corrige el mensaje de error devuelto cuando un servidor se queda sin espacio en disco para que indique correctamente eso, en lugar de indicar que el archivo es un directorio.

### Cambios
* Mejora el manejo de errores y la salida cuando se encuentra un error al extraer una imagen para un servidor.
* Mejora la robustez del código que maneja la sustitución de valores en archivos de configuración para no potencialmente causar un pánico si se encuentra un tipo de reemplazo no string.
* Mejora el manejo de errores en todo el sistema de archivos del servidor.

### Añadido
* Añade la capacidad de establecer el nombre interno de la aplicación en la salida de la respuesta desde la consola usando la clave `app_name` en el archivo `config.yml`.

## v1.3.2
### Corregido
* Establece correctamente el estado interno del servidor como "restaurando" cuando se realiza una restauración para evitar cualquier inicio accidental.

## v1.3.1
### Corregido
* Corrige un error que se devolvía al cliente al intentar reiniciar un servidor cuando el contenedor ya no existía en la máquina.

### Cambios
* Se actualiza la lógica de transferencia de servidores para usar herramientas de archivado de archivos más nuevas, evitando errores frecuentes al transferir archivos vinculados por enlace simbólico.

## v1.3.0
### Corregido
* Corrige el manejo de errores cuando se intenta crear una nueva red Docker.
* Corrige un error de caso extremo que ocurría cuando un usuario activaba una instalación para un servidor que no tenía un directorio de datos presente en el sistema.
* Corrige la falta de retorno de error al intentar obtener los contenidos de un archivo desde Wings.
* Corrige ciertos señales de parada que no se manejaban ni analizaban correctamente por Wings.
* Corrige la configuración de construcción del servidor que no siempre se actualizaba correctamente si se configuraba a su valor cero.
* Corrige una fuga de contexto al esperar que se detenga una instancia de servidor.
* Corrige una posible pánico de la aplicación al cambiar la propiedad de un archivo si hubo un error al obtener los detalles del archivo.
* Corrige que `Filesystem.Chown` tocaba inadvertidamente todos los archivos dentro de un árbol de directorios dado, lo que podría hacer que algunos juegos dispararan una actualización completa pensando que los archivos habían cambiado.
* Corrige que el encabezado `Content-Disposition` no se escapaba correctamente, lo que causaba que algunos navegadores no informaran el nombre correcto del archivo al descargarlo.

### Añadido
* Añade soporte para restaurar respaldos de servidores (incluyendo respaldos remotos) con la capacidad de restablecer el estado actual de archivos para un servidor.
* Añade soporte subyacente para permitir que los Eggs marquen archivos específicos (o patrones) como inaccesibles para los usuarios dentro del administrador de archivos.

### Cambios
* Se refactorizó el subsistema SFTP para ser menos un paquete independiente y más integrado con la lógica subyacente del servidor en Wings. Esto simplificó significativamente la lógica y hace que sea mucho más fácil de entender.
* Se refactorizó gran parte de la lógica de la API subyacente para ser más extensible en el futuro, admitir reintentos automáticos y ser más testeable.
* Se refactorizó gran parte de la lógica del middleware HTTP subyacente para empaquetarla de manera diferente y hacerla más fácil de entender en el código base.
* La variable `TZ` definida por el sistema se usará si está presente en lugar de intentar analizar la zona horaria usando `datetimectl`.
* Mejora el manejo de errores e informes para el proceso de instalación de servidores para mejorar la depuración en el futuro si las cosas se rompen.

## v1.2.3
### Corregido
* **[Seguridad]** Corrige una vulnerabilidad de seguridad restante en el código que maneja las descargas de archivos remotos para servidores en relación con la validación de redirección.

### Añadido
* Añade una clave de configuración en `api.disable_remote_download` que se puede establecer en `true` para deshabilitar completamente el sistema de descargas remotas.

## v1.0.1
### Añadido
* Añade soporte para ARM en las salidas de compilación de Wings.

### Corregido
* Corrige que algunos clientes Docker no tengan habilitada la negociación de versión.
* Corrige que las imágenes locales con prefijo `~` se descarguen desde fuentes remotas en lugar de usar la copia local.
* Corrige que la salida de la consola se rompa con ciertos juegos cuando se envía una longitud de línea excesiva.
* Corrige un error cuando las líneas de consola son demasiado largas, lo que causaba que la consola dejara de actualizarse hasta que el servidor se reiniciara.

### Cambios
* Simplifica la lógica de zona horaria para los contenedores al obtener correctamente la zona horaria del sistema y luego pasarla a los contenedores mediante la variable de entorno `TZ=`.

## v1.0.0
Esta es la primera versión estable oficial de Wings. Ten en cuenta que aunque este changelog es muy corto, técnicamente incluye todas las versiones beta y alfa anteriores.

### Corregido
* Corrige el parser de archivos para que agregue correctamente el carácter de nueva línea a las líneas modificadas.
* Corrige que el uso de disco del servidor no se informe correctamente al API y al websocket.

### Cambios
* Cambia la URL del endpoint de diagnóstico a `peli.cc` en lugar de `hastebin.com`.
* El informe de diagnóstico ahora incluye la hora del sistema para facilitar la depuración de registros e incidencias con contenedores.

## v1.0.0-rc.7
### Corregido
* **[Seguridad]** Previene que el valor de configuración `allowed_mounts` sea establecido por una llamada remota a la API.
* Corrige un error inesperado cuando se intenta hacer una copia de un archivo de archivo.
* Corrige que ciertos errores del sistema de archivos esperados se devuelvan a la API como un error 500 en lugar de un error 4XX.
* Corrige un fallo que provocaba que la Wings se bloqueara cuando no había texto en una línea y el parser intentaba determinar si la línea era un comentario.
* Corrige múltiples operaciones de sistema de archivos para comprobar, incrementar y disminuir correctamente el uso de disco de un servidor.
* Corrige un problema con el uso negativo de espacio en disco al eliminar un archivo debido a un error en la asignación de enteros.
* Los errores de una conexión WebSocket cerrada ya no saturarán la consola.
* Corrige un `.` extra en el script de instalación para los servidores que causaba errores en algunos escenarios.
* Corrige un spam inesperado de errores debido a un cambio en cómo se devuelve `os.ErrNotExist` desde algunas funciones.

### Cambios
* Ya no se emite un trace de pila al advertir que una imagen existe localmente.
* El parser de configuración ahora intenta crear la estructura de directorios para un archivo de configuración si falta.
* Si un nombre de archivo es demasiado largo para el sistema, se devuelve un error amigable al llamante.
* Habilita la negociación de versiones del cliente para Docker para admitir más versiones.
* Ya no se registran errores de espacio en disco en los logs de Wings.
* Los servidores ya no pueden reinstalarse mientras otra acción de encendido o apagado esté en curso, evitando colisiones de datos y problemas con el estado del contenedor.
* Wings ahora usa `1024` en lugar de `1000` bytes al calcular el uso de disco de un servidor para coincidir con cómo lo informa el Panel.
* Los errores JWT en WebSocket ahora se envían de vuelta a la conexión como un tipo de evento específico, lo que permite que se manejen incluso si el temporizador no se ejecuta o se ejecuta pero no se está escuchando.
* La estructura del servidor ya no se encuentra incrustada en el sistema de archivos virtual, lo que facilita las pruebas y la modularización del código base.
* Los WebSockets del servidor ahora se cierran cuando un servidor es eliminado, desconectando a los clientes conectados.

### Eliminado
* **[Seguridad]** Elimina la función `SafeJoin` que podría asumir incorrectamente el estado de un archivo y permitir que un usuario escape del directorio raíz si el desarrollador que implementa la llamada usa `Stat` en lugar de `Lstat`.

## v1.0.0-rc.6
### Corregido
* Corrige la condición de carrera al verificar si el estado en ejecución de un servidor ha cambiado.
* Corrige que los archivos se descompriman erróneamente en el directorio raíz en lugar del directorio al que deberían ser descomprimidos.
* Corrige que la salida de la consola no se envíe al WebSocket en el mismo orden en que se recibió.
* Corrige un error de archivo ocupado que causaba una respuesta 500 cuando se descomprimía un archivo de archivo, en lugar de una respuesta 400 con un mensaje indicando lo que estaba mal.
* Corrige que la imagen de Docker no se actualice correctamente cuando un servidor es iniciado.

### Cambios
* Reemplaza la lógica frágil del bus de eventos por un sistema más robusto y fácil de entender. Esto resuelve todos los problemas restantes de salida de consola y estadísticas que se habían reportado.
* Limpia los mensajes de error de la API para evitar que se registren errores vacíos que no puedan ser procesados.
* Añade soporte para reintentar una escritura de archivo varias veces con un retroceso si el archivo está ocupado cuando ocurre la escritura.

### Añadido
* Los datos de extracción de imágenes Docker se muestran en la consola cuando un administrador está conectado al WebSocket.
* Añade un límite de líneas para detener un servidor si se está enviando demasiada información desde la consola. Esta lógica imita la lógica presente en el antiguo demonio Nodejs, pero con un límite de conteo de líneas 2x (1000 -> 2000) por período.

## v1.0.0-rc.5
### Corregido
* Corrige un error persistente con la salida de consola que no se enviaba correctamente al cliente con las estadísticas del servidor en ciertos escenarios.
* Corrige los banderas de construcción durante el proceso de lanzamiento para reducir el tamaño final del binario a `~5MB`.
* Corrige que Wings devuelva las últimas `16384` líneas del archivo de registro cuando se conecta al WebSocket.
* Corrige que las acciones previas al arranque siempre se ejecutaran para un evento de inicio de servidor, incluso si el servidor ya estaba en ejecución.

### Añadido
* Añade soporte para configurar el tiempo máximo que puede transcurrir entre la comprobación del tamaño del disco del servidor antes de que se considere desactualizado.

## v1.0.0-rc.4
### Corregido
* Corrige que los archivos del servidor sean inaccesibles si la ruta de datos raíz es un enlace simbólico a otra ubicación en la máquina.
* Corrige que algunos datos de salida de consola se escriban en los logs truncando accidentalmente otras líneas debido a secuencias ANSI especiales.
* Corrige que los archivos `server.properties` se dañen por el editor de configuración automático al arrancar un servidor.
* Corrige un cierre de flujo perdido al detener el sondeo de recursos que llevaba a fugas de memoria.
* Corrige los puertos de enlace que se reasignaban incorrectamente al usar `127.0.0.1` con Docker. Ahora se reasignan correctamente a la interfaz `pelican0` para que la red funcione como se espera para el servidor.

### Cambios
* Permite que un valor desactualizado esté presente al iniciar un servidor si se permite que el servidor tenga una cantidad ilimitada de espacio en disco.
* Elimina todas las huellas restantes de la biblioteca de registro `zap` del código base.
* Los servidores ya no se reinician automáticamente como si se hubiera producido un fallo cuando se envía un comando de parada manualmente a través de la consola del servidor.
* Cambia las verificaciones de CORS para permitir `*` como origen remoto.

### Añadido
* Añade un archivo de logrotate generado automáticamente que se escribe en el directorio logrotate normal cuando Wings se inicia por primera vez.
* Añade más registros de depuración dentro de los internos del sondeo de recursos para servidores para rastrear mejor el comportamiento inesperado.
* Añade una verificación de lógica adicional para evitar intentar detener un servidor suspendido si ya está detenido.

## v1.0.0-rc.3
### Corregido
* Los errores durante el proceso de respaldo ahora se reportan correctamente al Panel y se registran en la salida correctamente.
* Los directorios vacíos ya no se agregan a la lista de archivos de respaldo (lo que causaba errores anteriormente).
* Se cubre un caso límite para prevenir errores si un archivo es eliminado mientras un respaldo está en progreso.
* Se corrigió un error que causaba que Wings se bloqueara y fallara si se pasaba un valor inválido de variable de entorno. Estos valores ahora se registran en la salida para mejor detección y se devuelve una cadena vacía en su lugar.
* Se corrigieron las variables de inicio y otra información del servidor que no se actualizaba correctamente al reiniciar un servidor.
* El estado de suspensión de un servidor ahora se devuelve correctamente por la API.
* Se corrige un error al intentar mover o renombrar una carpeta debido a que el destino se creaba accidentalmente antes de que ocurriera el cambio de nombre.
* Se corrige que los scripts de instalación se ejecutaran incluso cuando la casilla para no ejecutarlos en la instalación fue seleccionada en el Panel.

### Cambios
* Se modificó la comprobación del espacio en disco para no bloquearse en tantas partes del código y permitir devolver un valor de caché desactualizado donde sea apropiado.
* El código del paquete SFTP ahora está fusionado en el código base para simplificar su mantenimiento y reducir la complejidad del servidor SFTP.

### Añadido
* Añadida la capacidad de configurar un nodo para omitir la comprobación de permisos de archivo al iniciar un servidor.
* Se añadió un mensaje de salida en la consola para indicar que se está realizando la comprobación del espacio en disco del servidor en lugar de estar en silencio.

## v1.0.0-rc.2
### Corregido
* Se corrigió una degradación de rendimiento significativa debido a las excesivas acciones de `syscall` al determinar los tamaños de los directorios en servidores grandes. Esto antes causaba bloqueos de CPU y E/S en los servidores y ahora debería ser mucho más eficiente y menos impactante en el sistema.
* Se corrigió un fallo al iniciar Wings sin un directorio de registros creado.

### Cambios
* Se cambió el intervalo predeterminado para el cálculo del espacio en disco de cada 60 segundos a cada 2.5 minutos.

## v1.0.0-rc.1
### Corregido
* Los servidores ya no se marcan incorrectamente como detenidos cuando están, de hecho, fuera de línea.
* Ahora se muestra correctamente la versión de la compilación al iniciar Wings.
* Los señales de terminación ahora siempre se pueden enviar a una instancia de servidor incluso si la instancia está actualmente iniciándose o deteniéndose.
* Se eliminó el `chown` de archivos al arrancar Wings para evitar ralentizar innecesariamente el proceso de arranque cuando se trabajan con cientos de servidores en un nodo.
* Se corrigieron múltiples condiciones de carrera en el código que surgieron durante las pruebas y mejoraron la robustez del manejo de energía para las instancias del servidor.
* Se abordaron problemas graves de uso de CPU al generar respaldos y, adicionalmente, se redujo el tiempo necesario para generarlos.

### Cambios
* El servidor interno ahora usa configuraciones TLS más seguras y recomendadas.
* El manejo de entornos ahora está completamente separado del paquete del servidor, permitiendo que los entornos ya no estén fuertemente acoplados al servidor.
* El directorio `/tmp` montado en los contenedores ahora se puede gestionar programáticamente y usa mejores configuraciones predeterminadas para evitar que las personas necesiten editarlo.

### Añadido
* Los registros de Wings ahora se persisten correctamente en el disco.
* Se añadió la capacidad de un huevo para usar coincidencias sin ANSI al determinar si un servidor ha terminado de arrancar.

## v1.0.0-beta.9
### Corregido
* Se corrigió que las estadísticas de uso de recursos del servidor no se devolvieran correctamente por el endpoint de la API.
* Se corrigió una excepción lanzada cuando se intentaba escribir los registros de instalación del servidor.
* Se corrigió el manejo de errores para proporcionar un seguimiento de pila más preciso en más escenarios donde faltaba inicialmente.
* Se corrigió una fuga de memoria y oyentes de eventos zombi al desconectar un WebSocket de un servidor.
* Se corrigió una condición de carrera cuando Wings intentaba registrar/dar de baja suscriptores de eventos.
* Los directorios de datos del servidor ahora tienen correctamente sus permisos establecidos de manera recursiva al arrancar Wings.
* Se corrigió una condición de carrera cuando el flujo de la consola de un servidor no se cerraba completamente antes de que comenzara la siguiente acción de encendido.

### Cambios
* El manejo de energía del servidor ahora se maneja de manera sincrónica. Esto evita errores interminables y condiciones de carrera que surgían si alguien activaba dos procesos de reinicio consecutivos. La nueva lógica impide realizar cualquier otra acción de encendido hasta que la acción en ejecución esté completada.
* El uso de disco del servidor ahora se calcula correctamente al reiniciar el daemon, siempre que exista el directorio de datos del servidor.
* Se limpiaron varios caminos del código dentro del proceso de arranque para que sean menos intensivos en E/S y, en general, más fáciles de entender como desarrollador.
* Se montó información adicional de zona horaria en los contenedores para mejorar la capacidad de los instantes para utilizar la zona horaria correcta.

### Añadido
* Se añadieron endpoints internos básicos de carga de archivos (que actualmente no están expuestos en el Panel).
* Se añadieron eventos de proceso adicionales para el inicio y la finalización de la instalación.
* Ahora se pueden definir orígenes permitidos adicionales para el WebSocket en el archivo de configuración.
* Se añadió la capacidad de autenticarse con un registro de Docker al extraer imágenes.

## v1.0.0-beta.8
### Corregido
* El estado del servidor se sincroniza con el Panel antes de realizar una reinstalación para asegurar que se utilice la información más reciente.
* Wings ya no se bloquea cuando se pasa un valor de variable de entorno no string.
* La autenticación del servidor SFTP ya no intenta contactar al Panel para validar credenciales si el formato ya se sabe que es incorrecto.
* Se devolvieron correctamente algunos rastreos de error que anteriormente faltaban.
* Renombrar un archivo ya no genera un error si la ruta base no existe.
* El espacio en disco ahora se calcula correctamente para un servidor, incluso si se le asigna espacio ilimitado.
* **[Seguridad]** Se previene que los archivos simbólicos cambien el permiso de su archivo de destino cuando se arranca un servidor y el archivo de destino reside fuera del directorio de datos del servidor.
* **[Seguridad]** Se limpian múltiples caminos de código que podrían permitir a un usuario malintencionado afectar archivos fuera de su directorio principal.
* Se corrigieron múltiples condiciones de carrera durante el proceso de arranque de un servidor que podían llevar a estados de datos no deseados.
* Se corrigió un error al intentar eliminar un archivo que apunta a un archivo simbólico fuera del directorio de datos del servidor.
* Eliminar un archivo simbólico ya no intentará eliminar el archivo fuente, solo el enlace simbólico.
* El WebSocket ya no se bloquea al manejar un proceso de larga duración para un usuario.

### Cambios
* El registro de instalación para servidores ahora es más detallado y útil para depurar lo que podría estar fallando.
* Algunos endpoints de la API de gestión de archivos ahora permiten pasar múltiples rutas a la vez para facilitar las acciones masivas.
* Se reestructuró la implementación del recorrido de archivos para no causar un fallo de servidor al trabajar con directorios muy grandes y evitar condiciones de carrera al recorrer directorios de manera recursiva.
* Se reorganizó la estructura de configuración del servidor para hacerla más manejable en el código base y evitar condiciones de carrera adicionales y complejidad al realizar cambios sobre la marcha.

### Añadido
* Se añadió soporte para configurar puntos de montaje adicionales de archivos en un contenedor a través del Panel.
* Se añadió soporte para la generación automática de certificados SSL al arrancar el Daemon.
* Se añadió el comando de diagnóstico de Wings.
* Nuevos endpoints de la API para comprimir y descomprimir archivos en un servidor.

## v1.0.0-beta.7
### Corregido
* Las trazas de pila ahora se muestran solo una vez en la salida de error, en lugar de dos cuando se encuentran ciertos errores.
* Se han corregido otros errores que antes no mostraban traza de pila, ahora se muestran correctamente.
* Se corrige un error donde el espacio disponible en el servidor se activaba cuando se creaba un nuevo servidor desde una configuración remota antes de que esa ubicación de archivo existiera en el disco, lo que provocaba un error.
* Se corrigieron los tiempos de espera de contexto al obtener imágenes Docker del servidor. El tiempo se aumentó de 10 segundos a 15 minutos.
* Los valores de reemplazo del archivo de configuración ahora se des-escapan correctamente al escribir en el disco. `\/no\/more\/slashes`
* Los archivos `.properties` ahora se guardan correctamente en el disco con saltos de línea, en lugar de en una sola línea.
* El comando `./wings configure` ahora puede guardar correctamente la configuración en el disco.
* Las ubicaciones SSL personalizadas ya no se sobrescriben al hacer cambios en la configuración del Nodo desde el Panel.

### Cambiado
* Ahora se adquiere un bloqueo exclusivo al realizar una instalación de servidor para evitar que se disparen dos procesos de instalación al mismo tiempo. Esto también permite que una instalación se cancele correctamente si el servidor es eliminado antes de que se complete.

## v1.0.0-beta.6
### Corregido
* El estado del servidor ya no se envía a todos los clientes conectados al websocket cuando un nuevo cliente se conecta al socket.
* El uso del disco del servidor ahora se envía nuevamente a través del websocket al conectarse.
* La configuración predeterminada para el servidor SFTP ahora se devuelve correctamente como `on` en lugar de `off`.
* El arranque del servidor ya no se bloquea si hay un error al obtener la imagen Docker, siempre que esa imagen exista en el host.
* El websocket ya no se bloquea cuando Wings intenta enviar un error al cliente.
* Se corrigió un bucle de bloqueo cuando se lanza un error durante la fase de pre-arranque del servidor.
* Los errores con `BindJSON` en los endpoints de la API ahora se manejan correctamente y se devuelven.
* Se corrigió la advertencia sobre Gin ejecutándose en modo no-liberación, incluso cuando el binario se ejecuta en modo liberación.

### Cambiado
* Se cambiaron las bibliotecas de registro para mostrar los datos en un formato más claro adecuado para la CLI donde se ejecuta esta aplicación.
* Mensajes de depuración más limpios en modo depuración del enrutador.

## v1.0.0-beta.5
### Corregido
* La ubicación predeterminada de la configuración se ha establecido en `/etc/cinammon/config.yml`; Wings ahora verificará todas las ubicaciones anteriores de la configuración y la moverá automáticamente a la nueva ubicación.
* Eliminar un servidor ya no falla el proceso si el contenedor no se encuentra.
* Se corrigieron los problemas con la verificación de permisos para los subusuarios que se conectan a la instancia SFTP.
* Las copias de seguridad en S3 ahora envían correctamente los datos de hash al panel.
* Los contenedores de instalación del servidor ahora siempre se eliminan, incluso si el proceso de instalación falla para la instancia.
* Archivos y carpetas con caracteres especiales y espacios ya no devuelven un error 404.
* Los servidores que usan huevos con configuraciones incorrectas ya no causan que el demonio falle al arrancar; estas configuraciones incorrectas se omiten y se emite una advertencia en los registros.
* Las variables de entorno pasadas a los contenedores ya no contienen comillas incorrectas alrededor de ellas.
* La coincidencia de índices en arreglos de configuraciones ahora funciona correctamente; `foo[0]` se transforma silenciosamente en la sintaxis correcta `foo.0`.

### Agregado
* Nuevo mensaje de banner de error cuando el demonio no puede localizar el archivo de configuración. Esto debería aclarar mejor lo que el usuario necesita hacer para resolver el problema.
* Se agrega la capacidad de configurar el controlador de red predeterminado utilizado por Docker.

## v1.0.0-beta.4
### Corregido
* Se corrigió un pánico inesperado de puntero nulo cuando se intentaba iniciar algunos servidores recién creados, o cualquier servidor que no tenía un contenedor en el sistema.
* Se corrigió el uso de memoria del proceso, ya que se informaba de manera diferente a la salida de `docker stats`, lo que causaba algo de confusión. Ahora estos números deberían ser más correctos.
* Se corrigió un posible pánico de puntero nulo al detectar un contenedor eliminado como si estuviera fallando.

## v1.0.0-beta.3
### Corregido
* El demonio ya no se bloqueará si alguien solicita un websocket para un servidor eliminado.
* Los directorios temporales ahora se crean correctamente si faltan durante el proceso de instalación del servidor.

### Agregado
* Se añadió soporte para usar Amazon S3 como ubicación de respaldo para los archivos.

### Cambiado
* La sobrecarga de memoria para los contenedores ahora es un 5/10/15% mayor que el límite pasado para tener en cuenta el montón de JVM y evitar fallos.

## v1.0.0-beta.2
### Cambiado
* La funcionalidad de respaldo se ha hecho mucho más modular para facilitar la adición de métodos adicionales en el futuro.
* Los permisos del websocket cambiaron para usar el mismo nombre que en el panel.
* Los límites de memoria duros para los contenedores ahora se ajustan en un 15% (< 2G de memoria), 10% (< 4G de memoria) o 5% para evitar fallos inesperados por falta de memoria para juegos con mucha memoria.
* El ejecutable de Wings ahora es un 80% más pequeño gracias a mejores argumentos de compilación.

### Agregado
* Se agrega soporte para ignorar archivos y directorios al generar un nuevo respaldo.
* Se agregó un caminante de directorios interno con soporte para continuar con el callback.

### Corregido
* Se corrigió la coincidencia de distribuciones de Linux al arrancar el demonio.
* Se corrigió DNS para ser configurable para los contenedores Docker creados para servidores.
* Se corrigió la truncación incorrecta de archivos al hacer modificaciones en los archivos de configuración de un servidor.

## v1.0.0-beta.1
### Agregado
* Se añadió soporte para pasar hilos específicos al entorno Docker cuando se ejecuta un servidor.
* Se añadió soporte para reinstalar un servidor existente.
* Se añadió soporte para reiniciar un servidor.
* Se añade soporte para transferir servidores entre instancias del demonio.
* Se añadió el comando de despliegue automático para obtener la configuración desde el Panel automáticamente.

### Cambiado
* Los archivos del servidor y los respaldos ahora acceden a un endpoint directo con un JWT de un solo uso para evitar que los respaldos grandes se manejen a través del panel.

### Corregido
* Se corrigió una rutina Go que causaba una fuga de memoria y CPU.
* Se corrigió el `chown` incorrecto de los directorios del servidor al arrancar.
* Se corrigieron diversas fugas de memoria y condiciones de carrera.
* Se corrigió el soporte para sistemas basados en Alpine.

## v1.0.0-alpha.2
### Agregado
* Se añadió la capacidad de ejecutar un proceso de instalación para un servidor y notificar al panel cuando se haya completado.
* La salida del proceso de instalación ahora se emite a través de la consola del servidor para que los administradores puedan verla.

### Corregido
* Se corrigieron los errores causados al deserializar datos en una estructura con valores predeterminados.
* La zona horaria ahora se establece correctamente en los contenedores mediante la variable de entorno `TZ=`, en lugar de montar los datos de zona horaria en el sistema de archivos.
* Los datos del servidor ahora se crean correctamente cuando se ejecuta el proceso de instalación.
* El desajuste de tiempo causado por el JWT del socket ahora se maneja de manera más adecuada y es menos probable que cause errores inesperados.
