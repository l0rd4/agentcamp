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

# Astro — Workflow de scaffolding del blog Hugo

Este workflow activa a Astro para que genere la estructura base del blog Hugo.

## Objetivo

Astro crea (o verifica) la estructura completa del directorio `blog/` siguiendo
las convenciones del proyecto y propone los cambios mediante un Pull Request.

## Cuándo ejecutar

- Al inicio del workshop, tras verificar con `squad-intro.md`
- Cuando el directorio `blog/` no existe o está vacío
- Cuando se necesita restaurar la estructura base tras pruebas destructivas

## Agente responsable

**Astro** (`astro.agent.md`) — usa las herramientas `filesystem` y `github`.

## Instrucciones de contexto

El blog usa:
- **Hugo Extended** ≥ 0.140
- **Tailwind CSS** vía CDN (sin proceso de build separado)
- **GitHub Pages** como hosting
- Idioma principal: **español**

El `baseURL` en `hugo.toml` debe ser:
```
https://<OWNER>.github.io/kitten-agent-blog
```

Donde `<OWNER>` es el propietario del repositorio actual (consúltalo con `git remote -v`).

## Resultado esperado

Al finalizar, Astro habrá creado:
- Una rama `feature/astro-scaffold`
- Un Pull Request con todos los ficheros de estructura base
- El PR incluye la descripción de cada fichero creado

## Uso

```bash
# Sin instrucción específica
gh aw run .github/aw/astro.md

# Con instrucción específica
gh aw run .github/aw/astro.md \
  -F input="Astro, inicializa el blog Hugo con Tailwind CDN en la carpeta blog/"
```

## Paso siguiente tras mergear el PR

```bash
cd blog && hugo server --buildDrafts
# → Abre http://localhost:1313
```
