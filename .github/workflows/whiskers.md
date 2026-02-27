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

# Whiskers — Workflow de generación de artículos

Este workflow activa a Whiskers para que escriba un nuevo artículo en el blog.

## Objetivo

Whiskers genera un artículo completo en Markdown con el frontmatter Hugo correcto
y lo propone mediante un Pull Request de borrador.

## Cuándo ejecutar

Cada vez que quieras publicar un nuevo artículo en el blog.

## Agente responsable

**Whiskers** (`whiskers.agent.md`) — usa las herramientas `filesystem` y `github`.

## Parámetros de entrada

### Con tema específico

```bash
gh aw run .github/aw/whiskers.md \
  -F input="Escribe un artículo sobre <TEMA>"
```

### Sin tema (Whiskers elige)

```bash
gh aw run .github/aw/whiskers.md
```

Whiskers elegirá un tema relacionado con la vida felina en el espacio.

## Instrucciones de contexto para Whiskers

El artículo debe:
- Tener **mínimo 300 palabras** de cuerpo real
- Usar frontmatter Hugo completo (ver `whiskers.agent.md` para el esquema)
- Incluir **`image: "pending"`** en el frontmatter para que Luna lo procese después
- Pertenecer a una de las categorías aprobadas: `misiones`, `tecnologia`, `vida-gatuna`, `announcements`
- Estar en **español**
- Tener la fecha del artículo igual a la fecha **actual** del sistema (nunca en el futuro)

## Resultado esperado

- Rama: `feature/whiskers-<slug-del-articulo>`
- PR de borrador con el artículo completo
- Label `content` aplicado al PR

## Uso básico

```bash
# Con tema específico
gh aw run .github/aw/whiskers.md \
  -F input="Escribe un artículo sobre las primeras vacaciones de un gato en la Luna"

# Whiskers elige el tema
gh aw run .github/aw/whiskers.md
```

## Revisión del PR

Antes de mergear el PR de Whiskers, verifica:
- [ ] El frontmatter tiene todos los campos obligatorios
- [ ] `image: "pending"` está presente
- [ ] El artículo tiene más de 300 palabras
- [ ] La categoría es una de las aprobadas
- [ ] La fecha no está en el futuro

## Paso siguiente

Una vez mergeado el PR de Whiskers, Luna puede generar la imagen de portada:

```bash
gh aw run .github/aw/luna.md \
  -F input="Luna, genera la imagen para el artículo recién publicado"
```
