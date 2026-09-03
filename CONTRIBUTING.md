# 🛠️ Guía de Contribución y Estándares de ZeroStack

¡Gracias por contribuir a los proyectos de ZeroStack! Este documento describe las convenciones globales que seguimos en la organización para mantener un desarrollo organizado, un historial limpio y evitar conflictos en el trabajo colaborativo.

## 📋 1. Requisitos Previos

Antes de comenzar a codificar en cualquier repositorio de la organización:

- Tener Git instalado y configurado.
- Contar con el entorno del proyecto configurado (Node.js/Bun, .NET, Flutter, etc., según corresponda).
- Instalar las dependencias (priorizamos **pnpm** para Node y **bun** para scripts).
- Verificar que las herramientas de calidad (Husky, Commitlint, Linters) estén habilitadas y funcionando.

---

## 🌿 2. Estrategia de Ramas (Branching)

Nuestra estructura de ramas sigue un flujo basado en Épicas y Tareas, utilizando siempre **kebab-case** (minúsculas separadas por guiones).

```text
production
└── develop
    └── epic/<modulo>-<funcionalidad>-<ticket>
        ├── feat/<modulo>-<funcionalidad>[-ticket]
        ├── fix/<modulo>-<bug>[-ticket]
        ├── refactor/<modulo>-<tarea>[-ticket]
        └── ...
```

### Ramas Base
- **`production`**: Contiene el código estable que está en vivo. No se permite hacer push directo. Todo cambio llega mediante un PR aprobado.
- **`develop`**: Rama principal de integración. Aquí se fusionan todas las nuevas funcionalidades antes de pasar a producción.

### Ramas de Desarrollo
- **Ramas Épicas (`epic/<modulo>-<funcionalidad>-<ticket>`)**: Nacen desde `develop`. Agrupan múltiples tareas de un mismo módulo. El ticket es OBLIGATORIO.
  *Ejemplo: `epic/admin-dashboard-12`*
- **Ramas de Tareas (`<tipo>/<modulo>-<breve-descripcion>[-ticket]`)**: Nacen de una rama épica y se fusionan de vuelta a ella. El ticket es OPCIONAL.
  *Ejemplo: `feat/auth-login-form`, `fix/shared-date-format`*

---

## 💬 3. Convención de Commits

Utilizamos Conventional Commits, validados automáticamente por Husky y Commitlint. El mensaje debe escribirse en minúsculas, y se permite el uso de mayúsculas para abreviaciones (ej. JWT, CSS, HTML) en inglés o español y sin punto final.

**Formato de mensaje:**
```text
tipo[(scope)]: descripción breve y en imperativo
```
> **Nota:** El `scope` (ámbito) es opcional, pero es un gran aporte si se lo colocan, ya que ayuda a entender rápidamente qué área del proyecto fue modificada.

### Tipos Permitidos
- **`feat`**: Nueva funcionalidad.
- **`fix`**: Corrección de errores o bugs.
- **`docs`**: Cambios únicamente en documentación.
- **`style`**: Cambios de formato (espacios, comas) sin afectar la lógica.
- **`refactor`**: Reestructuración de código sin agregar funcionalidades ni corregir bugs.
- **`chore`**: Mantenimiento, dependencias, scripts, etc.

### Scopes Permitidos (Universales)
Al ser una organización Fullstack, utilizamos scopes genéricos que aplican a cualquier proyecto:

- **`core`**: Lógica principal del dominio, configuraciones base o inicializaciones.
- **`ui`**: Componentes visuales, interfaces y vistas (Frontend/Móvil).
- **`api`**: Controladores, rutas, endpoints y servicios de red (Backend/Frontend).
- **`db`**: Modelos, repositorios, esquemas y migraciones de base de datos.
- **`auth`**: Lógica de autenticación, autorización y seguridad (JWT, Guards, etc.).
- **`shared`**: Utilidades, helpers y código compartido entre múltiples módulos.
- **`deps`**: Modificaciones exclusivas de dependencias (package.json, pnpm-lock.yaml, .csproj).
- **`tools`**: Configuraciones de herramientas de desarrollo (Vite, ESLint, TypeScript, Docker).
- **`ci`**: Integración continua, GitHub Actions, flujos de automatización y Husky.
- **`docs`**: Archivos .md, guías y manuales del repositorio.

### ✅ Ejemplos Válidos
- `feat(ui): create reusable modal component`
- `fix(auth): resolve token expiration bug`
- `chore(deps): update react and dom dependencies`
- `refactor(api): clean up user controller logic`
- `docs(core): update project setup instructions`

### ❌ Ejemplos Inválidos
- `Actualice el controlador` (Falta tipo y scope).
- `feat(Login): add button` (Login tiene mayúscula y no es un scope genérico permitido).
- `fix(api): Fix crash.` (Empieza con mayúscula y termina en punto).

---

## 📝 4. Convención de Pull Requests

El título del PR debe resumir la característica principal entregada: `tipo[(scope_opcional)]: descripción`.

- El scope es opcional si el cambio abarca múltiples áreas (ej. `feat: implement initial clean architecture`).
- Si se centra en un dominio, úsalo (ej. `fix(ui): resolve responsive layout on mobile`).
- La descripción debe enfocarse en qué valor se entrega, no en enumerar los archivos modificados.

---

## 🔀 5. Flujo de Trabajo Cotidiano (Paso a Paso)

1. **Descarga los últimos cambios** de la épica en la que vas a trabajar:
   ```bash
   git checkout epic/auth-module-10
   git pull origin epic/auth-module-10
   ```

2. **Crea tu rama de tarea** a partir de la épica:
   ```bash
   git checkout -b feat/auth-login-form-10
   ```

3. **Desarrolla la funcionalidad** y haz tus commits siguiendo la convención:
   ```bash
   git commit -m "feat(ui): add login form layout"
   ```

4. **Sube tu rama de tarea** al repositorio remoto:
   ```bash
   git push origin feat/auth-login-form-10
   ```

5. **Abre un Pull Request** desde tu rama `feat/...` hacia la rama `epic/...`.

---

## ✅ 6. Checklist antes del Pull Request

- [ ] El proyecto compila y se ejecuta correctamente.
- [ ] No existen errores de linting ni de tipado.
- [ ] Los commits y la rama siguen estrictamente las convenciones de nombres.
- [ ] Se han eliminado archivos temporales, `console.log` o código comentado innecesario.
- [ ] Se ha actualizado la documentación si el cambio lo requería.

---

¡Gracias por ayudarnos a mantener el código de ZeroStack limpio, consistente y profesional! 🚀

> **Consejo sobre los Scopes:** Si en el futuro necesitan un *scope* muy específico para un proyecto en particular (por ejemplo, `android` o `ios` para una app móvil nativa), pueden agregar una regla en el archivo `commitlint.config.js` de ese repositorio en específico, manteniendo este `CONTRIBUTING.md`.