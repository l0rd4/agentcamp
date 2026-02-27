# 🐱 Kitten Agent Blog — AgentCamp 2026

Repositorio de trabajo del workshop **AgentCamp 2026: Kitten Squad**. Contiene los agentes, workflows de Copilot, acciones de CI/CD y la estructura del blog Hugo que los asistentes van a construir durante la sesión.

> 🌐 **Guía del workshop**: [https://squad.azurebrains.com/bienvenida-workshop.html](https://squad.azurebrains.com/bienvenida-workshop.html)  
> 🔑 **Código de acceso**: `KITTEN26`

---

## 👥 Para los asistentes del workshop

Este repositorio es vuestra **referencia y plantilla de trabajo**. Os lo hemos dado con acceso `write` para que podáis explorarlo, ejecutar los agentes y apoyar a los participantes durante las actividades.

---

## ⚙️ Requisitos previos

Antes del workshop, asegúrate de tener instalado y configurado lo siguiente:

- **VS Code** (versión más reciente)
- **GitHub Copilot** (plan Individual o Business activo)
- **Extension: GitHub Copilot** + **GitHub Copilot Chat**
- **Git** configurado con tu cuenta de GitHub
- **Node.js** (para Hugo extended) o **Hugo Extended v0.124+**
- **Azure CLI** (solo si trabajas con el blog en Azure)

```bash
# Verificar Hugo
hugo version  # debe ser Extended

# Verificar Azure CLI
az version
```

---

## 📁 Estructura del repositorio

```
kitten-agent-blog/
│
├── .github/
│   ├── agents/              # 🤖 Definiciones de agentes personalizados
│   │   ├── astro.agent.md         # Agente principal del squad
│   │   ├── whiskers.agent.md      # Especialista en contenido
│   │   ├── luna.agent.md          # Experta en diseño y UI
│   │   ├── rocket.agent.md        # DevOps y despliegues
│   │   ├── azure-architect.agent.md
│   │   ├── azure-foundry.agent.md
│   │   └── image-generator.agent.md
│   │
│   ├── aw/                  # 💬 Workflows de GitHub Copilot (gh-aw)
│   │   ├── squad-intro.md         # Presentación del squad
│   │   ├── astro.md
│   │   ├── whiskers.md
│   │   ├── luna.md
│   │   └── squad.md
│   │
│   └── workflows/           # ⚡ GitHub Actions
│       ├── deploy.yml             # Despliegue automático a Azure
│       └── validate.yml           # Validación de PR
│
├── assets/                  # 🌐 Guía del workshop (sitio estático)
│   ├── bienvenida-workshop.html   # Página pública de bienvenida
│   ├── gate.html                  # Página de acceso con contraseña
│   ├── index.html                 # Dashboard del workshop
│   ├── actividad-01-setup.html
│   ├── actividad-02-agentes.html
│   ├── actividad-03-hugo.html
│   ├── actividad-04-whiskers.html
│   ├── actividad-05-luna.html
│   ├── actividad-06-rocket.html
│   ├── actividad-07-squad.html
│   ├── cierre.html
│   └── *.png                      # Ilustraciones de personajes
│
├── blog/                    # 📝 Blog Hugo (lo construyen los participantes)
│   ├── hugo.toml
│   ├── content/
│   │   ├── _index.md
│   │   └── posts/
│   │       └── 2026-02-27-bienvenidos.md
│   └── layouts/
│
└── mcp.json                 # Configuración de MCP servers del workspace
```

---

## 🤖 Agentes disponibles

Los agentes están en `.github/agents/` y se invocan desde **Copilot Chat** en VS Code con `@agent-name`.

| Agente | Archivo | Rol |
|--------|---------|-----|
| **Astro** | `astro.agent.md` | Coordinador del squad, visión general |
| **Whiskers** | `whiskers.agent.md` | Creación de contenido para el blog |
| **Luna** | `luna.agent.md` | Diseño, UI, estética del blog |
| **Rocket** | `rocket.agent.md` | DevOps, CI/CD, despliegues |
| **Azure Architect** | `azure-architect.agent.md` | Infraestructura Azure |
| **Azure Foundry** | `azure-foundry.agent.md` | AI Foundry, modelos |
| **Image Generator** | `image-generator.agent.md` | Generación de imágenes con IA |

### Cómo usarlos

1. Abre **Copilot Chat** en VS Code (`Ctrl+Alt+I`)
2. En el modo **Agent**, selecciona el agente deseado
3. O escríbelo directamente: `@whiskers genera un post sobre GitHub Copilot`

---

## 💬 Workflows de Copilot (gh-aw)

Los workflows en `.github/aw/` definen conversaciones guiadas que los participantes pueden lanzar para obtener ayuda contextual durante las actividades.

| Workflow | Uso |
|----------|-----|
| `squad-intro.md` | Presentación inicial del Kitten Squad |
| `astro.md` | Flujo con Astro para planificar el blog |
| `whiskers.md` | Flujo para crear contenido con Whiskers |
| `luna.md` | Flujo de diseño con Luna |
| `squad.md` | Flujo colaborativo completo |

---

## 📝 Blog Hugo

El blog de ejemplo está en `blog/`. Los participantes lo construyen desde cero en la **Actividad 3** y lo expanden con ayuda de Whiskers y Luna en actividades posteriores.

```bash
# Levantar el blog en local
cd blog
hugo server -D

# Acceder en: http://localhost:1313
```

### Crear un nuevo post

```bash
cd blog
hugo new posts/mi-primer-post.md
# Editar el archivo en content/posts/mi-primer-post.md
```

---

## ⚡ GitHub Actions

| Workflow | Trigger | Descripción |
|----------|---------|-------------|
| `deploy.yml` | Push a `main` / `master` | Despliega el blog a Azure Storage |
| `validate.yml` | Pull Request | Valida Bicep y estructura del blog |

Para que el despliegue funcione, configura estos **secrets** en el repo:

- `AZURE_CLIENT_ID` — App Registration para OIDC
- `AZURE_TENANT_ID`
- `AZURE_SUBSCRIPTION_ID`
- `AZURE_STORAGE_ACCOUNT` — nombre del storage account destino

---

## 🗺️ Actividades del workshop

| # | Actividad | Objetivo |
|---|-----------|----------|
| 01 | Setup | Clonar repo, configurar VS Code y agentes |
| 02 | Agentes | Crear y personalizar tu propio agente |
| 03 | Hugo | Inicializar el blog con Copilot |
| 04 | Whiskers | Generar contenido con el agente escritor |
| 05 | Luna | Personalizar diseño con el agente de UI |
| 06 | Rocket | Configurar CI/CD y despliegue automático |
| 07 | Squad | Orquestar todos los agentes en equipo |

---

## 🆘 Soporte durante el workshop

Si un participante se bloquea, los recursos de apoyo son:

1. **Guía online**: [https://squad.azurebrains.com](https://squad.azurebrains.com/gate.html) → código `KITTEN26`
2. **Este repositorio**: referencia de archivos y estructura final
3. **Copilot Chat**: los propios agentes pueden guiar a los participantes paso a paso

---

*Workshop creado con ❤️ por el equipo de Azure Brains — AgentCamp 2026*
