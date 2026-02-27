---
on:
  workflow_dispatch:

permissions:
  contents: read

network: defaults
---

# Squad Intro — Workflow de presentación del squad

Este workflow presenta al equipo de agentes del Kitten Agent Blog al comenzar el workshop.
Es el primer workflow que ejecutarás para verificar que todo funciona correctamente.

## Objetivo

Verificar que:
1. El entorno de `gh aw` está correctamente instalado
2. Los agentes del squad están accesibles
3. El repositorio tiene la estructura esperada

## Instrucciones para el agente

Cuando se ejecute este workflow, el agente debe:

1. **Saludar al squad** con un mensaje de bienvenida que incluya los 4 miembros: Astro 🏗️, Whiskers ✍️, Luna 🎨, Rocket 🚀

2. **Verificar la estructura del repositorio** comprobando que existen los siguientes ficheros:
   - `.github/agents/astro.agent.md`
   - `.github/agents/whiskers.agent.md`
   - `.github/agents/luna.agent.md`
   - `.github/agents/rocket.agent.md`

3. **Imprimir un resumen** del estado de cada agente (fichero encontrado ✅ o no encontrado ❌)

4. **Verificar el directorio `blog/`** — si existe, indica cuántos posts hay. Si no existe, indica que Astro aún no ha scaffoldeado el proyecto.

5. **Finalizar** con un mensaje motivador para el workshop.

## Ejemplo de output esperado

```
🐱 ¡El Kitten Agent Squad está listo para el AgentCamp 2026!

🏗️ Astro (Arquitecto)  → ✅ Configurado
✍️ Whiskers (Escritor)  → ✅ Configurado
🎨 Luna (Imágenes)     → ✅ Configurado
🚀 Rocket (Publisher)  → ✅ Configurado

📁 Blog Hugo: No inicializado todavía (Astro pendiente)

¡Adelante! El squad está listo para construir. 🚀
```

## Uso

```bash
gh aw run .github/aw/squad-intro.md
```
