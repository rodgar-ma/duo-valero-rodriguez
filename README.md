# Dúo Valero-Rodríguez · web

Web del Dúo Valero-Rodríguez, piano a cuatro manos: el dúo, sus discos, agenda de conciertos, multimedia, noticias y contacto, en español, inglés e italiano.

Astro 7 · EmDash · TypeScript · CSS propio · Cloudflare Workers

## Requisitos

- Node.js 22.23.4 o posterior (la que pide Astro 7; ver `engines` en `package.json`)
- pnpm 12.14.0 (fijado en `packageManager` en `package.json`)
- Cuenta de Cloudflare con acceso al Worker, para desplegar

## Arrancar

```bash
pnpm install
pnpm approve-builds   # solo la primera vez, si pnpm lo pide
pnpm dev              # http://localhost:4321/
```

## Comandos

| Comando        | Qué hace                                                                 |
| -------------- | ------------------------------------------------------------------------ |
| `pnpm dev`     | Servidor local                                                           |
| `pnpm build`   | Compila la web en `dist/`                                                |
| `pnpm preview` | Sirve la compilación en local                                            |
| `pnpm check`   | Tipos y formato                                                          |
| `pnpm format`  | Formatea el código                                                       |
| `pnpm ship`    | Compila y despliega en Cloudflare (`pnpm wrangler login` la primera vez) |

El script de despliegue se llama `ship` porque `pnpm deploy` es un comando propio de pnpm y no ejecutaría el script.

## Estructura

```text
public/          archivos que se sirven tal cual (_headers, favicon)
src/pages/       rutas
```

## Contenido

El contenido (conciertos, discos, noticias, vídeos…) no está en el repositorio: se edita en el panel de EmDash, en `/_emdash/admin`, y se guarda en Cloudflare D1 y R2.

Hasta que los músicos entreguen el contenido real, la web usa datos de prueba, marcados con `[prueba]`.
