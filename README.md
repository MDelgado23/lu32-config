# lu32-config

Documentos de configuración que la app **LU32 Radio** lee en runtime.

**Editar un archivo acá y pushear cambia la app sin publicar una versión nueva.**
Se sirven por `raw.githubusercontent.com`, con ~5 minutos de caché de CDN.

> **Este repo tiene que seguir siendo PÚBLICO.**
> `raw.githubusercontent.com` devuelve 404 sobre repos privados, y la app se queda
> sin auspiciantes y sin la palanca para cambiar la URL del stream.

## `app-config.json`

La ruta crítica: es lo que mantiene la radio al aire. La app lo pide al arrancar
con 4 segundos de timeout, y si falla usa los valores hardcodeados del binario.

| Campo | Para qué |
|---|---|
| `streamUrl` | URL del stream de audio. **Tiene que ser `https://`.** Acá se corrige un puerto rotado sin tocar la app. |
| `newsApiBase` | Base de la API de noticias. |
| `stationLogoUrl` | Logo que se muestra en los controles del sistema (pantalla bloqueada, Control Center). |

## `sponsors.json`

Los auspiciantes de la grilla. Documento aparte a propósito: así un auspiciante
nuevo no invalida el etag de la config del stream, ni al revés.

| Campo | Obligatorio | Notas |
|---|---|---|
| `id` | sí | Identificador estable. |
| `pos` | sí | Orden en la grilla. De 10 en 10, para poder intercalar. |
| `name` | sí | |
| `logoUrl` | sí | **`https://` obligatorio.** `http://` se rechaza: lo bloquea ATS en iOS. Spec del logo: 640 × 512 px (5:4), PNG-24 con fondo transparente, máx 150 KB. |
| `website` | no | **`https://` obligatorio.** |
| `address` | no | |

`{ "sponsors": [] }` es válido y significa "radio sin auspiciantes". Renombrar la
clave o mandar un array pelado NO es válido: la app lo trata como deploy roto y
se queda con lo que tenía cacheado.
