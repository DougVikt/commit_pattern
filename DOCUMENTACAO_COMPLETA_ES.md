# Documentación Completa sobre Commits Git

---

## Índice

1. [¿Qué es un Commit?](#1-qu%C3%A9-es-un-commit)
2. [¿Para qué sirve un Commit?](#2-para-qu%C3%A9-sirve-un-commit)
3. [¿Por qué usar estandarización (Conventional Commits)?](#3-por-qu%C3%A9-usar-estandarizaci%C3%B3n-conventional-commits)
4. [Estructura Estándar de Conventional Commits](#4-estructura-est%C3%A1ndar-de-conventional-commits)
5. [Tabla Completa de Tipos Oficiales](#5-tabla-completa-de-tipos-oficiales)
6. [Explicación Detallada de Cada Tipo](#6-explicaci%C3%B3n-detallada-de-cada-tipo)
   - [6.1 feat (Feature)](#61-feat-feature)
   - [6.2 fix (Bug Fix)](#62-fix-bug-fix)
   - [6.3 docs (Documentation)](#63-docs-documentation)
   - [6.4 style](#64-style)
   - [6.5 refactor](#65-refactor)
   - [6.6 perf (Performance)](#66-perf-performance)
   - [6.7 test](#67-test)
   - [6.8 build](#68-build)
   - [6.9 ci (Continuous Integration)](#69-ci-continuous-integration)
   - [6.10 chore](#610-chore)
   - [6.11 revert](#611-revert)
7. [Breaking Changes (Cambios Disruptivos)](#7-breaking-changes-cambios-disruptivos)
8. [Scope (Ámbito)](#8-scope-%C3%A1mbito)
9. [Tipos Personalizados Usados por Empresas](#9-tipos-personalizados-usados-por-empresas)
10. [Tabla de Decisión Rápida](#10-tabla-de-decisi%C3%B3n-r%C3%A1pida)
11. [Ejemplo de Historial Profesional](#11-ejemplo-de-historial-profesional)
12. [Beneficios de la Convención](#12-beneficios-de-la-convenci%C3%B3n)
13. [Cómo Configurar en tu Proyecto](#13-c%C3%B3mo-configurar-en-tu-proyecto)
14. [Herramientas de Validación Automática (Git Hooks)](#14-herramientas-de-validaci%C3%B3n-autom%C3%A1tica-git-hooks)
15. [Extensiones VS Code para Ayuda y Automatización](#15-extensiones-vs-code-para-ayuda-y-automatizaci%C3%B3n)

---

## 1. ¿Qué es un Commit?

En Git puro no existe una lista oficial de "tipos de commit". Un commit es una **captura instantánea (snapshot) de los cambios del proyecto** en un momento determinado. Cada commit registra quién hizo el cambio, cuándo se hizo y un mensaje descriptivo sobre lo que se cambió.

El estándar más adoptado actualmente es **Conventional Commits**, utilizado por proyectos open source, GitHub, GitLab, Azure DevOps, Semantic Release, Commitlint y diversas empresas.

---

## 2. ¿Para qué sirve un Commit?

- Registrar el historial de cambios del proyecto
- Documentar **qué** se cambió y **por qué**
- Permitir trazabilidad de bugs, features y decisiones técnicas
- Facilitar la colaboración entre miembros del equipo
- Servir como base para automatización de changelogs y versionado semántico

---

## 3. ¿Por qué usar estandarización (Conventional Commits)?

1. **Automatización**: Herramientas como Semantic Release pueden leer los commits y decidir si deben subir la versión del proyecto (Patch, Minor o Major) automáticamente.
2. **Historial Limpio**: Permite que cualquier desarrollador nuevo entienda lo que pasó en el proyecto solo leyendo los tipos de commit.
3. **Búsqueda Facilitada**: Si necesitas encontrar cuándo se actualizó una dependencia, basta filtrar con `git log --grep="build"`.
4. **Generación de Changelog**: Es posible generar un archivo CHANGELOG.md en segundos, listando todas las nuevas funcionalidades (feat) y correcciones (fix) desde la última versión.
5. **Mejor legibilidad del `git log`**.
6. **Facilita code reviews y onboarding**.
7. **Integración con herramientas como Commitlint, Husky, etc.**

En organizaciones serias, nadie usa "actualicé la pantalla" o "arreglé el bug". El uso de estos prefijos permite que el equipo sepa exactamente lo que otro hizo sin necesidad de leer el código, permite la generación automática de changelogs y activa o no procesos de CI/CD.

---

## 4. Estructura Estándar de Conventional Commits

```
<tipo>(ámbito): descripción

[cuerpo opcional]

[pie opcional]
```

Formato extendido:

```
<tipo>[ámbito opcional]!: <descripción>

[cuerpo opcional]

[pie(s) opcional(es)]
```

**Ejemplo básico:**

```bash
feat(auth): agregar inicio de sesión con Google
```

**Ejemplo completo:**

```bash
feat: cambiar formato de respuesta de la API

BREAKING CHANGE: el campo 'user_id' ahora se llama 'uuid'.
```

### Referenciando Issues

En entornos profesionales, es común vincular el commit a una tarea (Jira, GitHub Issues).

```bash
fix: corregir error de redondeo (#123)
```

---

## 5. Tabla Completa de Tipos Oficiales

**Nota:** `feat` y `fix` tienen impacto directo en SemVer (minor y patch). BREAKING CHANGE (o `!` después del tipo) indica un cambio incompatible (major). Otros tipos están permitidos y recomendados por la convención Angular (la más común).

| Tipo | Propósito | Impacto en SemVer | Ejemplo Práctico de Mensaje |
|------|-----------|-------------------|-----------------------------|
| **`feat`** | Introduce una **nueva funcionalidad** en el código | Minor (ej: 1.2.0 → 1.3.0) | `feat(auth): agrega inicio de sesión con Google` |
| **`fix`** | **Corrige un bug** o problema encontrado en el sistema | Patch (ej: 1.2.3 → 1.2.4) | `fix(api): corrige error 500 al guardar cita` |
| **`docs`** | Cambios **solo en la documentación** (Markdown, README, docstrings, wikis) | Ninguno | `docs(readme): actualiza instrucciones de instalación con Docker` |
| **`style`** | Cambios que **no afectan el sentido del código** (formato, espacios, punto y coma, linting). *¡No confundir con CSS!* | Ninguno | `style(templates): corrige indentación y elimina espacios extras` |
| **`refactor`** | Un cambio en el código que **ni corrige un bug ni agrega una feature** (mejora rendimiento, legibilidad, arquitectura) | Ninguno | `refactor(services): centraliza lógica de validación de fechas` |
| **`perf`** | Un cambio de código estrictamente para **mejorar el rendimiento** | Ninguno | `perf(db): agrega índice en la tabla de consultas` |
| **`test`** | Agrega pruebas faltantes o **corrige/modifica pruebas existentes** | Ninguno | `test(views): agrega pruebas unitarias para el flujo de checkout` |
| **`build`** | Cambios que afectan el **sistema de construcción** (build), herramientas de compilación o dependencias externas (ej: Poetry, npm, Dockerfile) | Ninguno | `build(poetry): agrega biblioteca django-cors-headers` |
| **`ci`** | Cambios en archivos y scripts de **Configuración de Integración Continua** (ej: GitHub Actions, GitLab CI, Travis) | Ninguno | `ci(github): agrega paso de lint en el workflow de pull request` |
| **`chore`** | Tareas rutinarias de mantenimiento que **no modifican archivos de producción o pruebas** (ej: actualizar `.gitignore`, tareas de deploy manuales) | Ninguno | `chore(gitignore): agrega carpetas de VS Code (.vscode)` |
| **`revert`** | Indica la **reversión** de un commit anterior que causó problemas | Ninguno (generalmente sigue el commit revertido) | `revert: feat(auth): agrega inicio de sesión con Google` |

Estos son los tipos recomendados por la especificación Conventional Commits y la convención Angular.

---

## 6. Explicación Detallada de Cada Tipo

### 6.1 feat (Feature)

**Objetivo:** Agregar una nueva funcionalidad para el usuario.

**Cuándo usar:**
- ✅ Nueva pantalla
- ✅ Nueva API
- ✅ Nuevo endpoint
- ✅ Nuevo componente

**Ejemplos:**

```bash
feat(cart): agregar carrito de compras
```

```bash
feat(auth): implementar inicio de sesión con Google
```

```bash
feat(api): crear endpoint de exportación CSV
```

---

### 6.2 fix (Bug Fix)

**Objetivo:** Corregir comportamientos incorrectos.

**Cuándo usar:**
- ✅ Corregir error
- ✅ Corregir validación
- ✅ Corregir excepción
- ✅ Corregir lógica

**Ejemplos:**

```bash
fix(auth): corregir expiración del token
```

```bash
fix(cart): evitar elementos duplicados
```

```bash
fix(payment): corregir cálculo de descuento
```

---

### 6.3 docs (Documentation)

**Objetivo:** Cambiar solo documentación.

**Cuándo usar:**
- ✅ README
- ✅ Wiki
- ✅ Swagger/OpenAPI
- ✅ Comentarios explicativos

**Ejemplos:**

```bash
docs(readme): agregar instrucciones docker
```

```bash
docs(api): documentar endpoint de usuarios
```

```bash
docs: corregir ejemplos de uso
```

---

### 6.4 style

**Objetivo:** Cambios visuales en el código sin cambiar comportamiento.

**Cuándo usar:**
- ✅ Espaciado
- ✅ Indentación
- ✅ Saltos de línea
- ✅ Organización visual

**Ejemplos:**

```bash
style: corregir formato del proyecto
```

```bash
style(component): alinear imports
```

```bash
style(css): reorganizar reglas de estilo
```

---

### 6.5 refactor

**Objetivo:** Mejorar estructura del código sin alterar comportamiento.

**Cuándo usar:**
- ✅ Extraer métodos
- ✅ Separar clases
- ✅ Mejorar arquitectura
- ✅ Reducir duplicación

**Ejemplos:**

```bash
refactor(auth): separar reglas de autenticación
```

```bash
refactor(order): extraer servicio de pago
```

```bash
refactor(api): reorganizar controladores
```

---

### 6.6 perf (Performance)

**Objetivo:** Mejorar rendimiento.

**Cuándo usar:**
- ✅ Consultas lentas
- ✅ Caché
- ✅ Algoritmos más eficientes
- ✅ Menor consumo de memoria

**Ejemplos:**

```bash
perf(database): optimizar consulta de clientes
```

```bash
perf(cache): agregar caché redis
```

```bash
perf(images): reducir tiempo de carga
```

---

### 6.7 test

**Objetivo:** Agregar o corregir pruebas.

**Cuándo usar:**
- ✅ Pruebas unitarias
- ✅ Pruebas de integración
- ✅ Pruebas E2E

**Ejemplos:**

```bash
test(auth): agregar pruebas de autenticación
```

```bash
test(api): cubrir endpoint de usuarios
```

```bash
test(payment): corregir escenario de pago rechazado
```

---

### 6.8 build

**Objetivo:** Cambios en el sistema de build.

**Cuándo usar:**
- ✅ Maven
- ✅ Gradle
- ✅ Webpack
- ✅ Vite
- ✅ Dependencias

**Ejemplos:**

```bash
build: actualizar dependencias
```

```bash
build(npm): actualizar react a v19
```

```bash
build(docker): optimizar imagen de la aplicación
```

---

### 6.9 ci (Continuous Integration)

**Objetivo:** Cambiar pipelines automatizados.

**Cuándo usar:**
- ✅ GitHub Actions
- ✅ GitLab CI
- ✅ Jenkins
- ✅ Azure Pipelines

**Ejemplos:**

```bash
ci: agregar etapa de pruebas
```

```bash
ci(github): configurar deploy automático
```

```bash
ci(jenkins): corregir pipeline de build
```

---

### 6.10 chore

**Objetivo:** Tareas que no afectan funcionalidades.

**Cuándo usar:**
- ✅ Configuraciones
- ✅ Scripts
- ✅ Actualizaciones simples
- ✅ Limpieza

**Ejemplos:**

```bash
chore: actualizar versión de node
```

```bash
chore: eliminar archivos temporales
```

```bash
chore(config): ajustar eslint
```

---

### 6.11 revert

**Objetivo:** Deshacer commit anterior.

**Cuándo usar:**
- ✅ Revertir feature
- ✅ Revertir bug
- ✅ Revertir deploy problemático

**Ejemplos:**

```bash
revert: feat(auth): inicio de sesión vía Google
```

```bash
revert: fix(api): corrección de caché
```

---

## 7. Breaking Changes (Cambios Disruptivos)

Cuando un cambio rompe la compatibilidad con lo que existía (ej: cambiar el nombre de un campo crítico en la base de datos), agregamos una exclamación `!` después del tipo o una nota en el pie del commit.

Esto indica un aumento de versión MAJOR (1.x → 2.x).

### Forma 1 — Con exclamación `!`

```bash
git commit -m "feat(api)!: cambia la estructura de retorno del JSON de autenticación"
```

```bash
feat!: eliminar endpoint heredado
```

### Forma 2 — Con `BREAKING CHANGE` en el pie

```bash
feat(api): eliminar endpoint heredado

BREAKING CHANGE: endpoint /v1/users eliminado
```

### Visión Corporativa

Existe un tipo especial de commit que las organizaciones temen y necesitan señalar claramente: el **Cambio de Compatibilidad**. Esto ocurre cuando cambias algo que hará que el sistema de otro equipo o la aplicación del cliente deje de funcionar si no se actualiza.

**Ejemplo:** `feat(api)!: cambia ruta de /usuarios a /v2/usuarios`

Lo que sucede en la empresa: Este commit señala a los robots de la empresa que la próxima versión del software no puede ser "1.x.x", obligatoriamente tiene que saltar a "2.0.0" (Versionado Semántico).

---

## 8. Scope (Ámbito)

Además del término inicial, las empresas organizadas usan el **ámbito** (entre paréntesis) justo después del prefijo. Esto evita que el historial se convierta en una sopa de letras.

**Estructura:** `tipo(ámbito): mensaje`

**Sin ámbito (Malo):**
```
feat: agregar botón de guardar
```
¿Guardar qué? ¿Dónde?

**Con ámbito (Bueno):**
```
feat(user-profile): agregar botón de guardar
```
Ahora el equipo sabe exactamente en qué parte del sistema se modificó.

**Ejemplos de ámbitos comunes:**
- `(auth)`
- `(database)`
- `(ui)`
- `(checkout)`
- `(payments)`
- `(email-service)`

Mantener el ámbito ayuda al equipo (y a ti mismo en el futuro) a identificar instantáneamente qué parte del proyecto fue impactada, sin siquiera necesitar abrir el código.

---

## 9. Tipos Personalizados Usados por Empresas

Aunque no forman parte de la especificación oficial, muchos equipos utilizan tipos personalizados. Estos tipos son convenciones locales y deben configurarse en herramientas como Commitlint o Commitizen.

| Tipo | Uso |
|------|-----|
| `hotfix` | Corrección urgente en producción |
| `release` | Preparación de release |
| `security` | Correcciones de seguridad |
| `deps` | Actualización de dependencias |
| `config` | Configuraciones |
| `wip` | Work in Progress |
| `init` | Commit inicial |
| `merge` | Merge de ramas |
| `improvement` | Mejoras sin nueva feature |

### Notas sobre tipos extendidos

- **`deps`**: Una variación de `build` o `chore` enfocada solo en actualización de dependencias.
- **`wip`**: (Work In Progress) Indica que el trabajo aún está en progreso (común en ramas de borrador).
- **`init`**: Utilizado específicamente para el commit inicial que inicia el repositorio.

---

## 10. Tabla de Decisión Rápida

| Situación | Tipo |
|-----------|------|
| Nueva funcionalidad | `feat` |
| Corregir bug | `fix` |
| Actualizar README | `docs` |
| Corregir indentación | `style` |
| Mejorar arquitectura | `refactor` |
| Mejorar rendimiento | `perf` |
| Crear pruebas | `test` |
| Actualizar dependencias | `build` |
| Ajustar GitHub Actions | `ci` |
| Actualizar configuraciones | `chore` |
| Deshacer commit | `revert` |
| Romper compatibilidad | `feat!` o `BREAKING CHANGE` |

---

## 11. Ejemplo de Historial Profesional

```bash
feat(auth): implementar inicio de sesión JWT

fix(auth): corregir renovación de token

docs(api): documentar endpoint de autenticación

test(auth): agregar pruebas de inicio de sesión

perf(auth): reducir consultas a la base de datos

refactor(auth): separar capa de servicio

build(docker): actualizar imagen node 22

ci(github): agregar deploy automático

chore(eslint): actualizar reglas de lint

revert: feat(auth): inicio de sesión por Facebook
```

Este conjunto cubre prácticamente **el 100% de los escenarios profesionales encontrados en proyectos Git modernos**, siguiendo el estándar Conventional Commits adoptado por la mayor parte de la industria.

---

## 12. Beneficios de la Convención

- **Generación automática de changelogs** (herramientas como `standard-version`, `semantic-release`)
- **Mejor legibilidad del `git log`**
- **Facilita code reviews y onboarding** de nuevos desarrolladores
- **Integración con herramientas** como Commitlint, Husky, etc.
- **Búsqueda facilitada**: filtrar con `git log --grep="build"` para encontrar cambios específicos
- **Versionado semántico automatizado**: herramientas como Semantic Release pueden leer los commits y decidir si deben subir la versión del proyecto (Patch, Minor o Major) automáticamente

---

## 13. Cómo Configurar en tu Proyecto

1. **Instala `commitlint` + `husky`** para validar commits automáticamente
2. **Usa plantillas o extensiones de VS Code** (ej: Conventional Commits)
3. Configura **Commitlint** con las reglas de tu equipo (tipos permitidos, ámbitos, etc.)
4. Usa **Commitizen** para crear commits interactivamente siguiendo el estándar

---

## 14. Herramientas de Validación Automática (Git Hooks)

En organizaciones de punta, nadie confía en la buena voluntad del programador. Usan **Robots de Git (Git Hooks)**:

1. El dev escribe: `git commit -m "arreglé la pantalla de inicio de sesión"`
2. El robot (herramienta como **Commitlint + Husky**) **bloquea el commit** y muestra un error en el terminal: *"Error: Tu commit no sigue el estándar Conventional Commit. Usa feat:, fix:, etc."*
3. El commit **solo se guarda en Git** si el dev escribe: `git commit -m "fix(login): corrige validación de correo"`
4. Cuando este commit sube a GitHub/GitLab, otro robot lee el `fix:` y automáticamente genera un ticket en Jira/Linear marcando el bug como "Resuelto".

---

## 15. Extensiones VS Code para Ayuda y Automatización

A continuación, las principales extensiones de VS Code que ayudan en la creación de commits estandarizados, desde interfaces visuales hasta generación automática con IA.

### 15.1 Conventional Commits (vivaxy)

**ID:** `vivaxy.vscode-conventional-commits`

Extensión más popular para escribir commits convencionales manualmente con una interfaz visual.

**Funcionalidades:**
- Interfaz visual para llenar tipo, ámbito, descripción, cuerpo y pie
- Atajo: `Ctrl+Shift+P` → "Conventional Commits"
- Auto commit automático al finalizar el formulario (configurable)
- Soporte para Breaking Changes

**Configuraciones relevantes:**

| Configuración | Descripción | Por Defecto |
|---|---|---|
| `conventionalCommits.autoCommit` | Controla si hace el commit automáticamente después de llenar el mensaje | `true` |
| `conventionalCommits.silentAutoCommit` | Auto commit silencioso, sin enfocar el panel de control | `false` |

**Flujo de trabajo recomendado:**
1. Activar la extensión
2. Llenar los campos en la interfaz
3. La extensión automáticamente agrega los archivos, ejecuta el commit y hace push

---

### 15.2 Git Auto Commit Message (MohitJangir)

**ID:** `MohitJangir.git-auto-commit-message`

Genera mensajes de commit automáticos usando IA (Groq, Google Gemini o Anthropic Claude).

**Funcionalidades:**
- Generación con un clic (ícono ✨ en Source Control o Command Palette)
- Funciona con archivos staged, unstaged y untracked
- 3 proveedores de IA: Groq/Llama (gratuito, rápido), Google Gemini (gratuito), Anthropic Claude (pago)
- Cambio automático de modelo al cambiar de proveedor
- Genera mensajes en formato `tipo(ámbito): descripción`
- Claves de API almacenadas en SecretStorage cifrado de VS Code
- Funciona globalmente en cualquier repositorio Git

**Comandos disponibles:**

| Comando | Descripción |
|---|---|
| `Auto Commit: Auto Generate Commit Message` | Genera mensaje de commit a partir de los cambios actuales |
| `Auto Commit: Setup API Key` | Configurar o actualizar la clave de API |
| `Auto Commit: Reset API Key` | Limpiar la clave de API almacenada |

**Configuraciones:**

| Configuración | Por Defecto | Descripción |
|---|---|---|
| `autoCommit.provider` | `groq` | Proveedor de IA: `groq`, `gemini` o `claude` |
| `autoCommit.model` | `meta-llama/llama-4-scout-17b-16e-instruct` | Modelo de IA (auto-switch al cambiar de proveedor) |
| `autoCommit.maxDiffLength` | `10000` | Máximo de caracteres del diff enviados a la IA |

**Modelos disponibles:**

| Modelo | Proveedor | Gratuito | Notas |
|---|---|---|---|
| `meta-llama/llama-4-scout-17b-16e-instruct` | Groq | Sí | Llama más reciente (por defecto) |
| `llama-3.3-70b-versatile` | Groq | Sí | Estable |
| `gemini-2.0-flash` | Gemini | Sí | Rápido y estable |
| `gemini-2.5-flash` | Gemini | Sí | Puede estar sobrecargado |
| `gemini-3-flash-preview` | Gemini | Sí | Gemini más reciente |
| `claude-haiku-4-5-20251001` | Claude | No | Rápido, mejor calidad |
| `claude-sonnet-4-6-20260310` | Claude | No | Equilibrado |
| `claude-opus-4-6-20260310` | Claude | No | Mayor calidad |

---

### 15.3 Conventional Commit Builder (fletch-r)

**ID:** `fletch-r.conventional-commit-builder`

Interfaz simplificada para construir commits siguiendo el estándar Conventional Commits.

**Funcionalidades:**
- Input boxes y selection boxes para escribir mensajes
- Si no hay archivos staged, pregunta qué archivos agregar antes
- Detecta automáticamente números de issue de la rama actual
- Soporte para Gitmoji (emojis en commits)
- Soporte para archivo de configuración `.commitbuilderrc.json` por proyecto
- Auto commit opcional al finalizar

**Configuraciones relevantes:**

| Configuración | Descripción | Por Defecto |
|---|---|---|
| `conventionalCommitBuilder.autoCommit` | Commit automático después de llenar los prompts | `true` |
| `conventionalCommitBuilder.showCommit` | Mostrar mensaje en SCM para revisión antes de commitar | `false` |

---

### 15.4 AI Commit Message Gen (Nolomon)

**ID:** `Nolomon.commit-message-gen-vs-x`

Genera mensajes de commit con IA directamente en la vista de Source Control.

**Funcionalidades:**
- Botón en Source Control para generar mensaje con IA
- Múltiples proveedores y modelos de IA
- Claves de API almacenadas en SecretStorage de VS Code
- Mensajes en formato Conventional Commits

**Comandos:**

| Comando | Descripción |
|---|---|
| `AI Commit: Set Model` | Seleccionar modelo de IA |
| `AI Commit: Set API Key` | Configurar clave de API |
| `AI Commit: Clear API Key` | Limpiar clave de API |

**Consejo:** Para mantener el botón visible sin necesidad de pasar el mouse, agrega a `settings.json`:
```json
"workbench.view.alwaysShowHeaderActions": true
```

---

### 15.5 Gemini Commits (midnightgb)

**ID:** `midnightgb.gemini-commits`

Genera commits convencionales usando Google Gemini AI con análisis de contexto.

**Funcionalidades:**
- Botón de acceso rápido en Source Control
- Análisis contextual del código cambiado (no solo nombres de archivos)
- Soporte para múltiples idiomas (inglés y español)
- Mensajes editables antes de commitar
- Smart Large Diff Handling: maneja automáticamente commits grandes con resúmenes compactos
- Claves de API almacenadas en SecretStorage

**Configuración:**

```json
{
  "geminiCommits.model": "gemini-2.5-flash"
}
```

**Requisitos:** VS Code 1.85.0+, repositorio Git, clave de API Gemini.

**Métodos de uso:**
1. **Botón Source Control**: Haz clic en el ícono ✨ en Source Control
2. **Command Palette**: `Ctrl+Shift+P` → "Generate Commit with Gemini"

---

### 15.6 Git Message Generator (ARGRABBI)

**ID:** `ARGRABBI.git-message-generator-by-arg-rabbi`

Genera mensajes de commit convencionales **sin necesidad de API key** — funciona 100% local.

**Funcionalidades:**
- Sin IA, sin API key — funciona localmente
- Análisis multi-señal (ruta + diff + metadatos)
- Detección inteligente de ámbito (`auth`, `deps`, etc.)
- Mensajes con nivel de confianza (high confidence = mayor precisión)
- Soporte para commits con cuerpo multi-línea
- Comando "Explain" para inspeccionar por qué se generó un mensaje
- Fallback para diffs grandes

**Configuraciones relevantes:**

| Configuración | Por Defecto | Descripción |
|---|---|---|
| `commitGen.maxHeaderLength` | `72` | Tamaño máximo del encabezado |
| `commitGen.includeBody` | `true` | Incluir cuerpo en el mensaje |
| `commitGen.bodyMaxLines` | `12` | Máximo de líneas en el cuerpo |
| `commitGen.messageStyle` | `balanced` | Verbosidad: `concise`, `balanced`, `verbose` |
| `commitGen.showConfidence` | `true` | Notificación de confianza |
| `commitGen.profile` | `balanced` | Perfil: `balanced`, `frontend`, `backend`, `infra` |

---

### 15.7 ZeroDrop (Siranjeevan)

**ID:** `Siranjeevan.zerodrop`

Automatización completa de commit con guardado automático, IA y sincronización.

**Funcionalidades:**
- **Auto-save lifecycle**: Commitea y hace push automáticamente al cerrar VS Code
- **AI commits inteligentes**: Genera mensajes "Conventional Commit" automáticamente usando IA
- **Auto interval**: Guarda automáticamente en intervalos configurables (por defecto: 30 min)
- **Fix de commits por defecto**: Reemplaza mensajes placeholder por mensajes con IA
- **CLI standalone**: Comando `zerodrop run` para backup manual
- Soporta múltiples proveedores: Groq, Google, Hugging Face, Cohere, xAI, Ollama, etc.
- Monitoreo de batería: commitea automáticamente si la batería está baja

**Configuraciones principales:**

| Configuración | Por Defecto | Descripción |
|---|---|---|
| `zeroDrop.enableAutoPush` | `false` | Push automático al cerrar |
| `zeroDrop.enableAICommitMessage` | `true` | Generar mensajes con IA |
| `zeroDrop.aiProvider` | `groq` | Proveedor de IA |
| `zeroDrop.enableAutoInterval` | `false` | Auto-guardado periódico |
| `zeroDrop.intervalMinutes` | `30` | Minutos entre auto-guardados |

**Comandos CLI:**

| Comando | Descripción |
|---|---|
| `zerodrop run` | Backup manual silencioso |
| `zerodrop run --auto-push` | Backup manual con push |
| `zerodrop run --ai` | Backup con generación de mensaje IA |

---

### 15.8 Gemini Conventional Commit Writer (shawnchee)

**ID:** `shawnchee.vscode-gemini-commit-writer`

Extensión enfocada en Gemini (gratuito) para escribir commits convencionales modulares.

**Funcionalidades:**
- 100% gratuito (usa Google Gemini free tier, sin tarjeta de crédito)
- Generación en segundos basada en los cambios staged
- Elección entre commit de una línea o multi-línea (con cuerpo y pie)
- Múltiples modelos: Gemini 2.5 Flash y Flash Lite
- Atajo de teclado: `Ctrl+Alt+G` (Windows/Linux) o `Cmd+Alt+G` (Mac)
- Botón ✨ en Source Control

**Configuraciones:**

| Configuración | Por Defecto | Descripción |
|---|---|---|
| Model | `gemini-2.5-flash` | Modelo Gemini (todos gratuitos) |
| Temperature | `0.1` | Control de creatividad (0.0 = consistente, 1.0 = creativo) |
| Max Output Tokens | `500` | Tamaño máximo del mensaje |
| Max Diff Length | `5000` | Máximo de caracteres del diff analizado |

---

### Resumen Comparativo

| Extensión | Auto Commit | IA | Gratuito | Local | Interfaz Visual |
|---|---|---|---|---|---|
| Conventional Commits (vivaxy) | Sí | No | Sí | Sí | Sí |
| Git Auto Commit Message | No | Sí (Groq/Gemini/Claude) | Parcial | No | No |
| Conventional Commit Builder | Sí | No | Sí | Sí | Sí |
| AI Commit Message Gen | No | Sí (múltiples) | Parcial | No | No |
| Gemini Commits | No | Sí (Gemini) | Parcial | No | No |
| Git Message Generator | No | No | Sí | Sí | No |
| ZeroDrop | Sí | Sí (múltiples) | Parcial | No | No |
| Gemini Commit Writer | No | Sí (Gemini) | Sí | No | No |

---

## 🤝 Colabora con esta guía

Este documento fue construido basado en investigaciones y siempre puede crecer.

**¿Faltó algo? ¿Quieres complementar con más información, ejemplos, consejos o correcciones?**

Contribuye enviando sugerencias, abriendo issues o haciendo un pull request en el repositorio. Toda contribución es bienvenida para hacer esta guía cada vez más completa y útil para la comunidad.

> ✨ **Comparte conocimiento. Crece junto.**

---

> **Fuente:** Investigación compilada de múltiples fuentes sobre Conventional Commits, convención Angular y prácticas de mercado, reunida en un solo archivo.

---
