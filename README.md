# lu32-config

Documentos de configuración que la app **LU32 Radio** lee en runtime.

**Editar un archivo acá y pushear cambia la app sin publicar una versión nueva.**
Se sirven por `raw.githubusercontent.com`, con ~5 minutos de caché de CDN.

> ## ⚠️ Este repo tiene que seguir siendo PÚBLICO
>
> `raw.githubusercontent.com` devuelve **404 sobre repos privados**. Si este repo
> se hace privado, todas las apps instaladas pierden los auspiciantes **y** la
> palanca para corregir la URL del stream, en todas las plataformas a la vez.
>
> Ya pasó una vez: estos documentos vivían en el repo de la app, ese repo se hizo
> privado, y los dos empezaron a dar 404 sin que nadie se enterara. Por eso hoy
> viven acá, separados: **el repo de la app puede ser privado; este no.**

## Los dos documentos

| Archivo | Qué maneja | Guía |
|---|---|---|
| [`app-config.json`](app-config.json) | URL del stream, API de noticias, logo de la estación | acá abajo |
| [`sponsors.json`](sponsors.json) | La solapa Auspiciantes | **[SPONSORS.md](SPONSORS.md)** |

Están separados a propósito: así un auspiciante nuevo no invalida el etag de la
configuración del stream, ni al revés. **La radio no se entera de que existen los
auspiciantes.**

## `app-config.json`

La ruta crítica: es lo que mantiene la radio al aire. La app lo pide al arrancar
con 4 segundos de timeout. Si da 404, tarda, o viene mal formado, la app usa los
valores que trae hardcodeados y arranca igual — **nunca falla el arranque por
la configuración**.

| Campo | Para qué |
|---|---|
| `streamUrl` | URL del stream de audio. **Tiene que empezar con `https://`.** Acá se corrige un puerto rotado sin tocar la app. |
| `newsApiBase` | Base de la API de noticias. **`https://`.** |
| `stationLogoUrl` | Logo en los controles del sistema: pantalla bloqueada, Control Center. **`https://`.** |

Un campo que no sea string, o que no empiece con `https://`, se descarta solo y
queda el valor hardcodeado. Se pueden mandar los tres, o sólo uno.

### Ojo con el alcance

Las URLs de estos documentos están **hardcodeadas en el binario de la app**. Este
repo llega a las versiones que se publicaron apuntando acá; las apps más viejas
siguen buscando en la dirección anterior y no se enteran de nada de lo que se
edite acá.

## Antes de pushear

Pegá el contenido en <https://jsonlint.com> y fijate que diga *Valid JSON*.
Un archivo roto se ignora entero: la app sigue con lo último que le funcionó.
