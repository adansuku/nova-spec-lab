# AGEX-007: Refactor completo — Renombrar framework a "DevSpec"

## Épica
Migrar toda la estructura, comandos, referencias y documentación del framework de la nomenclatura actual (agex / sdd-*) a la nueva identidad: **DevSpec**.

## Contexto
- **DevSpec** = el producto/framework (lo que instalas y usas)
- **AX (Agent Experience)** = el concepto/filosofía detrás
- DevSpec implementa AX: define cómo los agentes de IA entienden, navegan y evolucionan tu codebase

## Alcance

### 1. Estructura de carpetas
| Antes | Después |
|---|---|
| `.spec/` | `.devspec/` |
| `.spec/commands/` | `.devspec/workflow/` |
| `.spec/skills/` | `.devspec/skills/` |
| `.spec/config.yml` | `.devspec/config.yml` |
| `.docs/` (raíz) | `.devspec/memory/` |
| `.docs/services/` | `.devspec/memory/services/` |
| `.docs/adr/` | `.devspec/memory/adr/` |
| `.docs/specs/` | `.devspec/memory/specs/` |
| `.docs/glossary.md` | `.devspec/memory/glossary.md` |
| `.docs/changes/` | `.devspec/changes/` |
| `.docs/changes/archive/` | `.devspec/changes/archive/` |
| `.docs/backlog/` | `.devspec/backlog/` |
| (nuevo) | `.devspec/guardrails/` (placeholder para AGEX-006) |

### 2. Renombrar comandos
| Antes | Después | Verbo |
|---|---|---|
| `/sdd-start` | `/ds-init` | Inicializar ticket |
| `/sdd-spec` | `/ds-define` | Cerrar requisitos y redactar spec |
| `/sdd-plan` | `/ds-plan` | Generar plan ejecutable |
| `/sdd-do` | `/ds-build` | Implementar |
| `/sdd-review` | `/ds-review` | Code review |
| `/sdd-wrap` | `/ds-ship` | Cerrar, archivar, commit |
| `/sdd-status` | `/ds-status` | Inspección del estado |

### 3. Archivos a renombrar
| Antes | Después |
|---|---|
| `sdd-start.md` | `ds-init.md` |
| `sdd-spec.md` | `ds-define.md` |
| `sdd-plan.md` | `ds-plan.md` |
| `sdd-do.md` | `ds-build.md` |
| `sdd-review.md` | `ds-review.md` |
| `sdd-wrap.md` | `ds-ship.md` |
| `sdd-status.md` | `ds-status.md` |

### 4. Actualizar contenido interno
- Todas las referencias a `/sdd-*` dentro de los archivos → `/ds-*`
- Todas las referencias a `.spec/` → `.devspec/`
- Todas las referencias a `.docs/` → `.devspec/memory/` o `.devspec/changes/` según contexto
- Referencias a "agex" como nombre del framework → "DevSpec"
- Mantener "AX (Agent Experience)" como concepto donde se mencione la filosofía
- `config.yml`: actualizar rutas y nombre del framework
- `CLAUDE.md`: actualizar rutas y referencias
- `README.md`: reescribir con nueva identidad DevSpec
- `INSTALL.md`: actualizar rutas de instalación
- `install.sh`: actualizar todas las rutas y referencias
- `.claude/` symlinks: actualizar para apuntar a `.devspec/` en vez de `.spec/`

### 5. Prefijo de tickets
- Cambiar de `AGEX-` a `DS-` a partir del siguiente ticket
- Este ticket es el último con prefijo AGEX

### 6. Documentación
- README.md: nuevo título "DevSpec — an Agent Experience (AX) framework"
- Subtítulo: "Define how AI agents understand, navigate, and evolve your codebase. Created by Libnova."
- INSTALL.md: actualizar rutas y ejemplos

## Subtareas
- [ ] ST-1: Crear estructura `.devspec/` y mover archivos
- [ ] ST-2: Renombrar archivos de comandos (sdd-*.md → ds-*.md)
- [ ] ST-3: Actualizar contenido interno de todos los comandos (refs a /sdd-* → /ds-*)
- [ ] ST-4: Actualizar contenido interno de todas las skills
- [ ] ST-5: Actualizar config.yml, CLAUDE.md, README.md, INSTALL.md, install.sh
- [ ] ST-6: Actualizar symlinks de .claude/
- [ ] ST-7: Migrar .docs/ → .devspec/memory/ y .devspec/changes/
- [ ] ST-8: Verificación: grep -ri "sdd-\|\.spec/\|\.docs/" debe devolver 0 en archivos activos
- [ ] ST-9: Actualizar CONTEXT.md del framework con nueva estructura
- [ ] ST-10: Commit, merge y push

## Criterios de aceptación
1. `grep -ri "sdd-" . --exclude-dir=.git --exclude-dir=archive` → 0 resultados
2. `grep -ri "\.spec/" . --exclude-dir=.git --exclude-dir=archive` → 0 resultados
3. `grep -ri "\.docs/" . --exclude-dir=.git --exclude-dir=archive` → 0 resultados
4. Todos los comandos funcionan con prefijo `ds-`
5. Los symlinks de `.claude/` apuntan correctamente a `.devspec/`
6. README refleja la nueva identidad
7. install.sh funciona con la nueva estructura
8. Archivos en archive/ se preservan intactos (registro histórico)

## Dependencias
- Absorbe AGEX-006 (refactorizar guardrails) — al crear `.devspec/guardrails/` se monta el placeholder

## Estimación
Media-alta. Toca prácticamente todos los archivos del framework.

## Prioridad
Alta — define la identidad definitiva del producto antes de seguir añadiendo features.

## Notas
- Este es el último ticket con prefijo AGEX
- A partir de aquí, los tickets usan prefijo DS-
- Los archivos en archive/ mantienen las referencias históricas a sdd/agex/libnova
