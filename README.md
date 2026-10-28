# NinMagic Cleaner 1.2.0

Aplicación NRO para Nintendo Switch con Atmosphère, interfaz en español y logo original de NinMagic. Cleaner mantiene un canal de actualización propio, separado de NinMagic Cheats y de la página web.

## Cambios de esta versión

- Lee los metadatos NACP normales y comprimidos de juegos instalados y NROs. Evita presentar los datos comprimidos como nombres con símbolos extraños.
- Respeta el idioma de la consola y conserva los nombres originales para asociar instalaciones y NROs. Si el texto no se puede interpretar, muestra el identificador o el nombre del archivo.
- Muestra versiones de aplicaciones instaladas y NROs por separado. En pantalla adapta símbolos como ™ a (TM), manteniendo los acentos.
- Incorpora actualizaciones por HTTPS desde el repositorio independiente `ANE-JV/ninmagic-cleaner`.

## Primera instalación

Extrae el ZIP completo en la raíz de la microSD, uniendo las carpetas `switch` y `config`. El archivo principal debe quedar en:

`switch/NinMagicCleaner/NinMagic-Cleaner.nro`

Las versiones anteriores a la 1.2.0 necesitan esta primera copia mediante PC o NinMagic AIO Updater. Después abre hbmenu manteniendo R al iniciar un juego o una aplicación para usar el modo aplicación. El borrado está bloqueado en modo Álbum/applet.

La carpeta `fuentes` contiene el código correspondiente y no es necesaria para ejecutar Cleaner. El paquete no contiene juegos, partidas, recibos personales ni archivos de configuración de Atmosphère.

## Actualizar desde Cleaner

Al abrir Cleaner se consulta el canal de versiones. Pulsa **R: Actualizar** desde la biblioteca para volver a comprobarlo. Si hay una versión nueva, revisa la versión publicada y pulsa **A: Descargar e instalar**. La aplicación verifica HTTPS, tamaño, SHA-256, estructura NRO, nombre y versión antes de sustituir su archivo. Conserva una copia numerada de la versión anterior.

Una instalación correcta requiere cerrar Cleaner y abrirlo otra vez. Si la publicación coincide con el programa y el NRO instalado, aparece **No hay actualizaciones pendientes**. Un fallo de conexión se muestra como consulta sin comprobar; nunca se presenta como prueba de que estás al día.

El canal oficial está integrado en el NRO:

`https://raw.githubusercontent.com/ANE-JV/ninmagic-cleaner/main/update.txt`

El archivo opcional `config/NinMagicCleaner/update-url.txt` permite indicar otro manifiesto HTTPS. Un archivo presente debe contener una sola URL válida. Las actualizaciones y sus copias se guardan dentro de `config/NinMagicCleaner/app-update/`, separadas de los recibos de limpieza. No se sustituyen juegos, partidas, configuraciones de firmware ni la aplicación NinMagic Cheats.

Si aparece un registro antiguo terminado, la pantalla permite revisarlo antes de confirmar su archivo. Un estado pendiente, incoherente o dañado queda bloqueado. No retires la microSD durante la instalación. Sin red, la consulta inicial puede esperar hasta 40 segundos antes de continuar; Cleaner sigue disponible para limpiar después del aviso.

## Limpiar una aplicación

1. Selecciona el juego o NRO y pulsa A.
2. Elige **Conservar las partidas**, **Borrar todas las partidas** o **Cancelar**. La opción inicial siempre conserva las partidas.
3. Si necesitas vincular otros archivos de esa aplicación, pulsa X desde la elección de partidas. Revisa las rutas exactas y sus tamaños.
4. Revisa la confirmación. Y activa o desactiva los datos SD y mods; la decisión sobre partidas sigue siendo independiente.
5. Suelta los botones y mantén **L + R + X durante dos segundos** para ejecutar el borrado. B vuelve atrás.

En la biblioteca, X filtra Todos/microSD/interna, Y recarga, L abre otras rutas SD, R comprueba actualizaciones, − muestra ayuda y + sale.

## Alcance de la limpieza

Cleaner enumera instalaciones de HOME y NROs dentro de `switch`. Desinstala los contenidos registrados del título: base, actualizaciones y DLC asociados. La operación puede afectar a microSD y memoria interna aunque la biblioteca tenga un filtro de almacenamiento.

Los paquetes NRO se asocian por identificador NACP o por un nombre exacto y único; los casos ambiguos permanecen separados. El perfil de Dead Space 2 detecta su lanzador y datos conocidos. Otras rutas pueden vincularse expresamente mediante el explorador. Una carpeta con varios NROs no se atribuye entera a uno de ellos.

El borrado de partidas exige una elección independiente en cada operación. Incluye las partidas locales del título y los guardados SD identificados. Si un port tiene una ubicación de partidas desconocida, conservar partidas mantiene toda su carpeta de datos. Si el inventario de partidas no puede verificarse por completo, su borrado se bloquea.

No elimina automáticamente cualquier rastro de un juego: no borra historial, tickets, capturas, copias de JKSV/Checkpoint, nube, instaladores sueltos ni carpetas arbitrarias sin atribuir. Nunca borra manualmente las carpetas `Nintendo`. Los directorios del sistema, la propia aplicación y su configuración están protegidos.

Antes de ejecutar se revalida el inventario confirmado. Si falla la desinstalación del contenido, no se continúa borrando sus partidas. Se muestran los errores parciales. Cleaner opera únicamente en el entorno arrancado; no limpia otras emuMMC ni la sysMMC desde una emuMMC distinta.

## Compilar y comprobar

Con devkitPro para Windows, devkitA64, libnx, switch-tools, zlib y libcurl:

```powershell
.\tools\build.ps1 -ExpectedVersion 1.2.0 -Preview
```

La compilación utiliza una carpeta temporal dedicada bajo el perfil del usuario y genera `dist/NinMagic-Cleaner.nro`. No escribe en la consola. Los tests utilizan servicios simulados o carpetas temporales del PC; no borran contenidos de una Switch.

La validación incluye compilación AArch64, NRO/ASET/NACP/RomFS, conservación del logo, metadatos comprimidos, estados de actualización, verificaciones de descarga y recuperación y regresiones de limpieza mediante simulación. No constituye una prueba de ejecución o borrado en una consola real.

## Recursos y licencias

Logo original de NinMagic, reutilizado a petición de su propietario. Tipografía DejaVu Sans, libnx, zlib y libcurl: avisos incluidos en `licencias` dentro de la carpeta de Cleaner y en el archivo de fuentes.
