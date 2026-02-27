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

# Rocket — Workflow de validación y despliegue a GitHub Pages

Este workflow activa a Rocket para que valide el build de Hugo y despliegue el blog a GitHub Pages.

## Objetivo

Rocket comprueba que no hay PRs pendientes con cambios en `blog/`, verifica que el pipeline
de GitHub Actions está correctamente configurado, y monitoriza el deploy hasta completación.

## Cuándo ejecutar

- Cuando quieras lanzar un deploy manual del blog a GitHub Pages.
- Para verificar el estado del pipeline sin hacer cambios.
- Después de resolver un error de build que bloqueó un deploy anterior.

## Agente responsable

**Rocket** (`rocket.agent.md`) — usa las herramientas `github` y `shell`.

## Requisitos previos

Para que Rocket pueda operar, el repositorio debe tener:

1. **GitHub Pages activado** con source en `GitHub Actions` (Settings → Pages).
2. **Workflow permissions** en `Read and write` (Settings → Actions → General).
3. El fichero `.github/workflows/deploy.yml` con los jobs `validate` y `deploy`.

## Uso

### Deploy estándar

```bash
gh aw run .github/aw/rocket.md
```

### Con instrucción específica

```bash
gh aw run .github/aw/rocket.md \
  -F input="Rocket, verifica el estado del pipeline y despliega si todo está en verde"
```

### Solo verificar (sin forzar deploy)

```bash
gh aw run .github/aw/rocket.md \
  -F input="Rocket, comprueba si hay errores en el último build sin lanzar un nuevo deploy"
```

## Flujo que ejecuta Rocket

1. Verifica que no hay PRs abiertos con cambios pendientes en `blog/`.
2. Comprueba que el workflow `deploy.yml` existe en `.github/workflows/`.
3. Activa el workflow de validación (`validate.yml`) y espera su resultado.
4. Si la validación pasa → activa el workflow de deploy (`deploy.yml`).
5. Monitoriza el deploy hasta completación.
6. Reporta la URL final del blog publicado.

## Guardrail clave

Rocket **nunca** despliega si el build de Hugo falla.
Si el build está en rojo, la respuesta de negativa es invariable:

> "No puedo desplegar con un build fallido. Corrige los errores primero."

## Resultado esperado

- Workflow `validate` completado en verde.
- Workflow `deploy` completado en verde.
- Blog accesible en `https://<owner>.github.io/kitten-agent-blog`.
- Comentario en el commit/PR con enlace al run de Actions.
