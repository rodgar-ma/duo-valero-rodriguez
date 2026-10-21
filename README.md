# Dúo Valero-Rodríguez · web

Web del Dúo Valero-Rodríguez, piano a cuatro manos: agenda de conciertos, discografía, multimedia, prensa y contacto, en español, inglés e italiano.

Astro 7 · TypeScript · CSS propio · Cloudflare Workers

## Requisitos

- Node.js 22.23.4 o posterior (la que pide Astro 7; ver `engines` en `package.json`)
- pnpm 12 o posterior
- Cuenta de Cloudflare con acceso al Worker, para desplegar

## Arrancar

```bash
pnpm install
pnpm approve-builds   # solo la primera vez, si pnpm lo pide
pnpm dev              # http://localhost:4321/es/
```

## Comandos

| Comando           | Qué hace                                                                 |
| ----------------- | ------------------------------------------------------------------------ |
| `pnpm dev`        | Servidor local                                                           |
| `pnpm build`      | Compila la web en `dist/`                                                |
| `pnpm preview`    | Sirve la compilación en local                                            |
| `pnpm check`      | Tipos y formato                                                          |
| `pnpm format`     | Formatea el código                                                       |
| `pnpm run deploy` | Compila y despliega en Cloudflare (`pnpm wrangler login` la primera vez) |

`pnpm deploy` sin `run` ejecuta un comando propio de pnpm, no el script del proyecto.

## Estructura

```text
public/          archivos que se sirven tal cual (_redirects, favicon)
src/content/     contenido editable: conciertos, discos, prensa, vídeos…
src/i18n/        idiomas, tabla de rutas y textos de interfaz
src/components/  componentes
src/pages/       rutas
src/styles/      tokens y estilos globales
```

## Contenido

Hasta que los músicos entreguen el contenido real, la web usa datos de prueba, marcados con `[prueba]`.
