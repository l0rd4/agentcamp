---
on:
  workflow_dispatch:

permissions:
  contents: read

safe-outputs:
  create-pull-request: {}
  
network: defaults
---

# Squad — Workflow de cadena coordinada completa

Este es el workflow del **Gran Reto** del workshop. Activa a todo el squad en cadena:
Whiskers escribe → Luna ilustra → Rocket despliega. Un único input humano.

## Objetivo

Con una sola instrucción, el squad completo produce un artículo nuevo en Internet:
1. **Whiskers** escribe el artículo y crea PR #1
2. **Luna** detecta el artículo nuevo y crea PR #2 con la imagen de portada
3. **Rocket** despliega automáticamente cuando los PRs se mergean a master

## Modo de coordinación

Este workflow funciona en modo **supervisado** por defecto:
- El humano aprueba y mergea cada PR antes de que el siguiente agente actúe
- Esto garantiza visibilidad total y control en cada paso

Para modo automático, activa la regla de auto-merge en los PRs o en la configuración del repo.

## Uso

```bash
gh aw run .github/aw/squad.md \
  --input "Escribe y publica un artículo sobre <TEMA>"
```

### Ejemplos

```bash
# Gran Reto del workshop
gh aw run .github/aw/squad.md \
  --input "Escribe y publica un artículo sobre la primera misión de Whiskers a la Luna"

# Con tema tecnológico
gh aw run .github/aw/squad.md \
  --input "Escribe y publica un artículo sobre los trajes espaciales para gatos de última generación"

# Whiskers elige el tema
gh aw run .github/aw/squad.md \
  --input "Escribe y publica un artículo sorpresa"
```

## Secuencia de ejecución

El workflow pasa el input a Whiskers y establece el contexto de cadena coordinada.

### Fase 1: Whiskers escribe

El agente Whiskers recibe el tema y:
- Genera el artículo completo con frontmatter (incluido `image: "pending"`)
- Crea PR en rama `feature/whiskers-<slug>`
- Espera a que el humano revise y mergee

**Acción humana requerida**: Revisar y mergear el PR de Whiskers.

### Fase 2: Luna ilustra

Tras el merge del PR de Whiskers, Luna se activa automáticamente (o puede activarse manualmente):

```bash
gh aw run .github/aw/luna.md
```

Luna:
- Detecta el artículo nuevo con `image: "pending"`
- Genera la imagen de portada (DALL-E 3 o SVG según disponibilidad)
- Crea PR en rama `feature/luna-<slug>`

**Acción humana requerida**: Revisar y mergear el PR de Luna.

### Fase 3: Rocket despliega

El merge a master activa automáticamente el workflow `deploy.yml` de GitHub Actions.
Rocket valida el build de Hugo y despliega a GitHub Pages.

**Resultado final**: El artículo con imagen de portada está live en Internet.

## Flujo visual

```
👤 Tu input
    ↓
✍️ Whiskers → PR #1 (artículo)
    ↓ (tú mergeas)
🎨 Luna     → PR #2 (imagen)
    ↓ (tú mergeas)
🚀 Rocket   → Deploy automático
    ↓
🌍 Blog live en GitHub Pages
```

## Resultado esperado

Al finalizar la cadena completa:
- Un artículo nuevo visible en `https://<owner>.github.io/kitten-agent-blog`
- Imagen de portada coherente con el contenido
- Historial de commits limpio con PRs de cada agente

## Variante: verificar sin deploy

Si quieres probar la cadena sin llegar al deploy:

```bash
# Solo Whiskers
gh aw run .github/aw/whiskers.md --input "Tu tema"

# Solo Luna (sin mergear Whiskers)
gh aw run .github/aw/luna.md
```

Mergea los PRs manualmente en tu orden preferido.
