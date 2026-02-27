# Post LinkedIn — AgentCamp 2026

> 📋 Listo para copiar y pegar en LinkedIn.
> 🖼️ Adjunta la imagen del Kitten Squad (los 4 en sus pedestales).

---

## ✅ VERSIÓN PARA PUBLICAR HOY

🐱🚀 Los gatitos astronautas han vuelto de sus misiones espaciales. Y tienen historias épicas que contar.

El problema: ningún gato escribe sus propias memorias.

Así que el **viernes en AgentCamp 2026** vamos a construir —en 4 horas— el sistema que lo hace por ellos: un blog completamente operado por un **squad de agentes autónomos** construidos sobre **GitHub Copilot** y **GitHub Agentic Workflows**.

---

El squad tiene cuatro miembros. Cada uno tiene su rol, sus herramientas y sus reglas del juego. Lo que no os cuento todavía es cómo son... eso lo descubriréis vosotros mismos cuando empecéis a trabajar con ellos. 🐾

---

Lo que sí os cuento es la arquitectura técnica de lo que vamos a montar:

**`.github/agents/*.agent.md`** — Los agentes se definen en Markdown. Sin YAML de 200 líneas, sin DSLs propietarios. Un fichero de texto con identidad, herramientas disponibles y guardrails explícitos en lenguaje natural.

**`gh aw`** — GitHub Agentic Workflows. El agente corre en un GitHub Actions runner, tiene acceso al repo vía MCP, puede crear ramas, abrir PRs y llamar a APIs externas. El humano da la orden en lenguaje natural. El agente ejecuta.

**Guardrails reales** — No es un chatbot que hace lo que le pides. Cada agente tiene límites concretos implementados en tres capas: permisos del workflow (`permissions:` mínimos), safe-outputs declarados en `gh aw`, y reglas de negocio en el propio `.agent.md`. Ninguno hace push directo a `main`. Nunca.

**Meta-prompting** — El agente de imágenes no llama a DALL-E directamente. Primero usa GPT-4o para leer el artículo y construir un prompt visual de alta calidad. Dos IAs encadenadas, el humano no escribe un solo prompt.

**MCP filesystem + MCP github** — Los agentes no tienen acceso a nada que no les hayas dado explícitamente. Leen ficheros del workspace, crean PRs, abren issues. Punto.

---

Al final de las 4 horas cada asistente tendrá:
✅ Un blog Hugo publicado en GitHub Pages
✅ Artículos escritos por un agente
✅ Imágenes de portada generadas por otro agente
✅ Un pipeline de CI/CD gestionado por un tercer agente
✅ Y habrá aprendido a decirle que no a un agente cuando intenta saltarse las reglas

📅 **Viernes 27 de febrero · 10:00–14:00**
📍 NTT DATA Spain — Novus Building, Hortaleza, Madrid
🎤 Con @María Soto y un servidor

¿Vas a estar por allí? Cuéntamelo en comentarios 👇

#AgentCamp2026 #GitHubCopilot #AIAgents #GitHubActions #MCP #AgenticAI #GitHub #Workshop #Madrid #NTTData #GenerativeAI

---

## VERSIÓN CORTA (alternativa más directa)

🐱🚀 Los gatitos astronautas han vuelto. Tienen historias que contar. Y el viernes les vamos a construir el blog que las publique.

En **AgentCamp 2026** (Madrid) montamos en 4 horas un squad de agentes autónomos con **GitHub Copilot** y **GitHub Agentic Workflows**: scaffolding, redacción, generación de imágenes con DALL-E y CI/CD… todo orquestado por agentes definidos en Markdown, con guardrails reales y sin tocar `main` directamente.

Viernes 27 · 10:00 · NTT DATA Spain. Con @María Soto.

¿Vienes? 👇

#AgentCamp2026 #GitHubCopilot #AIAgents #Workshop #Madrid
