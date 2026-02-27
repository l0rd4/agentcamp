---
on:
  workflow_dispatch:
    inputs:
      input:
        description: 'Instrucción para el agente'
        required: false
        type: string

permissions:
  contents: read

safe-outputs:
  create-pull-request: {}

network: defaults
---

# Luna — Workflow de generación de imágenes de portada

Este workflow activa a Luna para que genere imágenes de portada para los artículos
que tienen `image: "pending"` en su frontmatter.

## Objetivo

Luna detecta artículos sin imagen, usa meta-prompting (GPT-4o → DALL-E 3 o SVG)
para generar portadas coherentes con el contenido, y propone los cambios mediante PR.

## Cuándo ejecutar

- Después de mergear uno o más PRs de Whiskers
- Cuando un artículo tiene `image: "pending"` y necesita imagen de portada

## Agente responsable

**Luna** (`luna.agent.md`) — usa las herramientas `filesystem`, `github` y `azure-openai`.

## Detección automática de modo

Luna detecta automáticamente el modo según la disponibilidad del secret:

- ✅ `AZURE_OPENAI_API_KEY` configurado → **Modo DALL-E 3** (imagen real 1792×1024)
- 🔄 Sin `AZURE_OPENAI_API_KEY` → **Modo SVG** (SVG animado, sin coste)

No necesitas especificar el modo manualmente.

## Uso

### Modo estándar (procesa hasta 3 artículos pendientes)

```bash
gh aw run .github/aw/luna.md
```

### Con instrucción específica

```bash
gh aw run .github/aw/luna.md \
  -F input="Luna, genera la imagen de portada para el artículo sobre la misión lunar"
```

### Dry-run (ver prompt generado sin crear imagen)

```bash
gh aw run .github/aw/luna.md \
  -F input="Luna, muéstrame el prompt que generarías para el artículo sobre Marte, sin crear la imagen"
```

## Instrucciones de contexto para Luna

Para cada artículo con `image: "pending"`:

1. Leer el artículo completo
2. Invocar GPT-4o para crear el prompt visual (meta-prompting)
3. Generar imagen con DALL-E 3 HD o SVG animado según disponibilidad
4. Guardar en `blog/static/images/posts/<slug>/cover.webp` (o `.svg`)
5. Actualizar el frontmatter del artículo (reemplazar `image: "pending"`)
6. Crear PR con rama `feature/luna-<slug>`

## Resultado esperado

- Rama: `feature/luna-<slug-del-articulo>`
- PR con imagen adjunta y frontmatter actualizado
- Descripción del PR incluye el prompt generado por GPT-4o y el modo utilizado
- Label `images` aplicado al PR

## Revisión del PR de Luna

Antes de mergear, verifica:
- [ ] La imagen se ve correctamente en el preview del PR
- [ ] El frontmatter ya no tiene `image: "pending"` sino la ruta real
- [ ] La descripción del PR incluye el prompt de GPT-4o

## Configurar el secret para DALL-E 3

```
GitHub repo → Settings → Secrets and variables → Actions → New repository secret
Nombre:  AZURE_OPENAI_API_KEY
Valor:   (proporcionado por el instructor en el evento)
```

## Paso siguiente

Una vez mergeado el PR de Luna, push a master activa automáticamente a Rocket para el deploy.
