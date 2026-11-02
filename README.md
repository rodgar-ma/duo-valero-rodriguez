# Dúo Valero-Rodríguez · web

Web del Dúo Valero-Rodríguez, piano a cuatro manos: el dúo, sus discos, agenda de conciertos, multimedia, noticias y contacto, en español, inglés e italiano.

Astro 7 · EmDash · TypeScript · CSS propio · Cloudflare Workers

## Requisitos

- Node.js 22.23.4 o posterior (la que pide Astro 7; ver `engines` en `package.json`)
- pnpm 12.14.0 (fijado en `packageManager` en `package.json`)

## Arrancar

```bash
pnpm install
pnpm approve-builds   # solo la primera vez, si pnpm lo pide
pnpm dev              # http://localhost:4321/
```

## Comandos

| Comando        | Qué hace                      |
| -------------- | ----------------------------- |
| `pnpm dev`     | Servidor local                |
| `pnpm build`   | Compila la web en `dist/`     |
| `pnpm preview` | Sirve la compilación en local |
| `pnpm check`   | Tipos y formato               |
| `pnpm format`  | Formatea el código            |

## Ramas y despliegue

Nada se despliega desde un ordenador: lo hace GitHub Actions.

| Cuándo                   | Workflow     | Qué hace                                                                                 |
| ------------------------ | ------------ | ---------------------------------------------------------------------------------------- |
| Cada pull request a main | `ci.yml`     | Tipos, formato y compilación; si pasan, despliega en `https://dev.duovalerorodriguez.es` |
| Merge a `main`           | `deploy.yml` | Compila y despliega en `https://duovalerorodriguez.es`                                   |

- `main` está protegida: solo se cambia con una pull request y con las comprobaciones en verde.
- Una rama por tarea, con prefijo (`feat/`, `fix/`, `chore/`, `ci/`, `docs/`) y commits en formato [Conventional Commits](https://www.conventionalcommits.org/).
- `dev` es un solo entorno compartido: muestra la última pull request que se ha desplegado.
- Cada entorno es un Worker distinto (ver `wrangler.jsonc`). Dev tiene su propia base de datos (D1), medios (R2) y sesiones (KV), separados de los de producción.
- Hasta el lanzamiento, todas las respuestas llevan `X-Robots-Tag: noindex` (en `public/_headers`) para que los buscadores no indexen la web a medias.
- GitHub necesita los secretos `CLOUDFLARE_API_TOKEN` y `CLOUDFLARE_ACCOUNT_ID`.

## Estructura

```text
public/             archivos que se sirven tal cual (_headers, favicon)
src/pages/          rutas
.github/workflows/  comprobaciones y despliegues
wrangler.jsonc      configuración de los Workers de producción y dev
```

## Contenido

El contenido (conciertos, discos, noticias, vídeos…) no está en el repositorio: se edita en el panel de EmDash, en `/_emdash/admin`, y se guarda en Cloudflare D1 y R2.

Hasta que los músicos entreguen el contenido real, la web usa datos de prueba, marcados con `[prueba]`.
