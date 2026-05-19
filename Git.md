# ⚡ Git Cheat Sheet

> Referencia rápida de los comandos Git más utilizados en el día a día — desde configuración inicial hasta flujos avanzados.

---

## 📦 Instalación

| Plataforma | Enlace |
|------------|--------|
| Windows | https://windows.github.com |
| macOS | https://mac.github.com |
| Linux / POSIX | https://git-scm.com |

---

## ⚙️ Configuración inicial

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu@email.com"
git config --global color.ui auto
git config --global core.editor "code --wait"      # VSCode como editor por defecto
git config --global init.defaultBranch main        # Rama principal por defecto
git config --list                                  # Ver toda la configuración actual
```

---

## 🗂️ Crear y clonar repositorios

```bash
git init                                           # Inicializar repositorio en directorio actual
git init [nombre-carpeta]                          # Crear nuevo repo en carpeta específica
git clone [url]                                    # Clonar repositorio completo
git clone [url] [nombre-local]                     # Clonar con nombre personalizado
git clone -b [rama] [url]                          # Clonar una rama específica
git clone --depth 1 [url]                          # Clonar solo el último commit (shallow clone)
```

---

## 📁 Estado y seguimiento de archivos

```bash
git status                                         # Ver estado del working tree
git status -s                                      # Vista compacta del estado
git add [archivo]                                  # Añadir archivo al staging area
git add .                                          # Añadir todos los cambios
git add -p                                         # Añadir cambios de forma interactiva (por hunks)
git rm [archivo]                                   # Eliminar archivo del repo y del disco
git rm --cached [archivo]                          # Dejar de rastrear sin eliminar del disco
git mv [origen] [destino]                          # Mover o renombrar archivo
```

---

## 💾 Commits

```bash
git commit -m "mensaje descriptivo"                # Commit con mensaje
git commit -am "mensaje"                           # Stage + commit de archivos ya rastreados
git commit --amend -m "nuevo mensaje"              # Modificar el último commit
git commit --amend --no-edit                       # Añadir cambios al último commit sin cambiar el mensaje
git commit --allow-empty -m "mensaje"              # Commit vacío (útil para triggers de CI)
```

### 💡 Buenas prácticas para mensajes de commit

Usa el formato **Conventional Commits**:

```
<tipo>(<scope>): <descripción corta>

[cuerpo opcional]
[footer opcional]
```

| Tipo | Uso |
|------|-----|
| `feat` | Nueva funcionalidad |
| `fix` | Corrección de bug |
| `docs` | Cambios en documentación |
| `style` | Formato, sin cambios de lógica |
| `refactor` | Refactorización de código |
| `test` | Añadir o corregir tests |
| `chore` | Tareas de mantenimiento |

---

## 🌿 Ramas (Branches)

```bash
git branch                                         # Listar ramas locales
git branch -a                                      # Listar ramas locales y remotas
git branch [nombre]                                # Crear nueva rama
git branch -d [nombre]                             # Eliminar rama (seguro)
git branch -D [nombre]                             # Eliminar rama forzado
git branch -m [viejo] [nuevo]                      # Renombrar rama
git branch --merged                                # Ramas ya fusionadas en la actual
git branch --no-merged                             # Ramas no fusionadas aún
git checkout [rama]                                # Cambiar a rama existente
git checkout -b [nueva-rama]                       # Crear y cambiar a nueva rama
git switch [rama]                                  # Cambiar de rama (comando moderno)
git switch -c [nueva-rama]                         # Crear y cambiar a nueva rama (moderno)
```

---

## 🔀 Merge y Rebase

```bash
git merge [rama]                                   # Fusionar rama en la actual (merge commit)
git merge --no-ff [rama]                           # Forzar merge commit aunque fast-forward sea posible
git merge --squash [rama]                          # Aplastar todos los commits de la rama en uno
git merge --abort                                  # Cancelar merge en conflicto

git rebase [rama]                                  # Rebasar rama actual sobre otra
git rebase -i HEAD~[n]                             # Rebase interactivo de los últimos n commits
git rebase --continue                              # Continuar rebase tras resolver conflicto
git rebase --abort                                 # Cancelar rebase
git rebase --skip                                  # Saltar commit durante rebase
```

> ⚠️ **Regla de oro:** nunca hagas `rebase` sobre ramas compartidas en remoto (main, develop, etc.)

---

## 🌐 Remotos

```bash
git remote -v                                      # Ver remotos configurados
git remote add [nombre] [url]                      # Añadir remoto
git remote rename [viejo] [nuevo]                  # Renombrar remoto
git remote remove [nombre]                         # Eliminar remoto
git remote set-url origin [nueva-url]              # Cambiar URL del remoto

git fetch                                          # Descargar cambios sin integrar
git fetch [remoto]                                 # Descargar de un remoto específico
git fetch --prune                                  # Eliminar referencias a ramas remotas eliminadas
git pull                                           # fetch + merge de la rama actual
git pull --rebase                                  # fetch + rebase (historial más limpio)
git push                                           # Subir commits al remoto
git push -u origin [rama]                          # Subir y configurar upstream
git push --force-with-lease                        # Push forzado seguro (verifica estado remoto)
git push origin --delete [rama]                    # Eliminar rama en remoto
git push --tags                                    # Subir todos los tags al remoto
```

---

## 🔍 Inspección e historial

```bash
git log                                            # Historial completo
git log --oneline                                  # Una línea por commit
git log --oneline --graph --all                    # Árbol visual de ramas
git log -n [número]                                # Últimos n commits
git log --author="nombre"                          # Commits de un autor específico
git log --since="2 weeks ago"                      # Commits desde fecha
git log --grep="palabra"                           # Buscar en mensajes de commit
git log -S "texto"                                 # Commits que añaden o eliminan ese texto
git log --stat                                     # Resumen de archivos modificados
git log -p                                         # Ver diff completo por commit

git diff                                           # Cambios no staged
git diff --staged                                  # Cambios en staging vs último commit
git diff [rama1]..[rama2]                          # Diferencias entre dos ramas
git diff HEAD~1 HEAD                               # Comparar con el commit anterior

git show [commit]                                  # Ver detalles de un commit
git blame [archivo]                                # Ver quién modificó cada línea
git shortlog -sn                                   # Resumen de commits por autor
```

---

## ⏪ Deshacer cambios

```bash
git restore [archivo]                              # Descartar cambios en working directory (moderno)
git restore --staged [archivo]                     # Quitar del staging (moderno)
git checkout -- [archivo]                          # Descartar cambios (clásico)

git revert [commit]                                # Crear commit que deshace otro (seguro para remoto)
git revert HEAD                                    # Revertir el último commit

git reset HEAD~1                                   # Deshacer último commit, mantener cambios staged
git reset --mixed HEAD~1                           # Deshacer commit y staging, mantener archivos
git reset --hard HEAD~1                            # Deshacer commit y eliminar todos los cambios
git reset --hard origin/[rama]                     # Resetear al estado del remoto
```

> ⚠️ `reset --hard` es destructivo. Úsalo con precaución en ramas compartidas.

---

## 📦 Stash

```bash
git stash                                          # Guardar cambios sin commitear
git stash push -m "descripción"                    # Guardar con mensaje descriptivo
git stash list                                     # Ver todos los stashes
git stash pop                                      # Aplicar el último stash y eliminarlo
git stash apply stash@{n}                          # Aplicar stash específico sin eliminarlo
git stash drop stash@{n}                           # Eliminar stash específico
git stash clear                                    # Eliminar todos los stashes
git stash branch [rama]                            # Crear rama desde el último stash
```

---

## 🏷️ Tags

```bash
git tag                                            # Listar todos los tags
git tag [nombre]                                   # Crear tag ligero en HEAD
git tag -a [nombre] -m "mensaje"                   # Crear tag anotado
git tag -a [nombre] [commit]                       # Tag sobre commit específico
git tag -d [nombre]                                # Eliminar tag local
git push origin [nombre]                           # Subir tag específico
git push origin --tags                             # Subir todos los tags
git push origin --delete tag [nombre]              # Eliminar tag en remoto
git checkout [tag]                                 # Cambiar a un tag (modo detached HEAD)
```

---

## 🍒 Cherry-pick

```bash
git cherry-pick [commit]                           # Aplicar commit específico en rama actual
git cherry-pick [commit1]..[commit2]               # Rango de commits
git cherry-pick -n [commit]                        # Aplicar sin crear commit automático
git cherry-pick --abort                            # Cancelar cherry-pick en conflicto
git cherry-pick --continue                         # Continuar tras resolver conflicto
```

---

## 🔎 Búsqueda (Grep & Bisect)

```bash
git grep "patrón"                                  # Buscar texto en archivos rastreados
git grep -n "patrón"                               # Mostrar número de línea
git grep -i "patrón"                               # Búsqueda sin distinción de mayúsculas

git bisect start                                   # Iniciar búsqueda binaria de bug
git bisect bad                                     # Marcar commit actual como malo
git bisect good [commit]                           # Marcar commit conocido como bueno
git bisect reset                                   # Finalizar bisect
```

---

## 🗃️ El archivo .gitignore

Excluye archivos que no deben rastrearse (compilados, secretos, dependencias):

```gitignore
# Dependencias
node_modules/
vendor/

# Variables de entorno y secretos
.env
.env.local
*.pem
*.key

# Compilados y builds
dist/
build/
*.dll
*.exe
*.obj

# IDEs y editores
.vscode/
.idea/
*.suo
*.user

# Sistema operativo
.DS_Store
Thumbs.db

# Logs
*.log
logs/
```

> 📌 Plantillas listas para usar: https://github.com/github/gitignore

---

## 🌊 Git Flow — Flujo de trabajo

![Git-flow diagram](/assets/img/git-flow.png "Git-flow diagram")

| Rama | Propósito |
|------|-----------|
| `main` | Código en producción. Solo recibe merges. |
| `develop` | Integración de features. Base para releases. |
| `feature/*` | Nuevas funcionalidades. Sale de `develop`. |
| `release/*` | Preparación de versión. Merge doble a `main` + `develop`. |
| `hotfix/*` | Parches urgentes en producción. Merge doble a `main` + `develop`. |

```bash
# Iniciar Git Flow (requiere git-flow instalado)
git flow init

# Features
git flow feature start nombre-feature
git flow feature finish nombre-feature

# Releases
git flow release start 1.0.0
git flow release finish 1.0.0

# Hotfixes
git flow hotfix start fix-critico
git flow hotfix finish fix-critico
```

---

## ⚡ Alias útiles

Añade estos alias a tu configuración global para acelerar tu flujo:

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm "commit -m"
git config --global alias.lg "log --oneline --graph --all --decorate"
git config --global alias.undo "reset HEAD~1 --mixed"
git config --global alias.unstage "restore --staged"
git config --global alias.last "log -1 HEAD"
git config --global alias.aliases "config --get-regexp alias"
```

Uso: `git lg`, `git st`, `git undo`, etc.

---

## 📊 Comandos de diagnóstico y limpieza

```bash
git gc                                             # Optimizar el repositorio local
git fsck                                           # Verificar integridad del repo
git clean -fd                                      # Eliminar archivos no rastreados y carpetas
git clean -n                                       # Simular clean (previsualizar)
git reflog                                         # Historial de movimientos de HEAD (recuperación)
git reflog expire --expire=now --all               # Limpiar reflog
git count-objects -vH                              # Ver tamaño del repo
```

---

## 🗝️ Glosario

| Término | Definición |
|---------|------------|
| **Repository** | Directorio rastreado por Git que contiene todo el historial del proyecto |
| **Working Tree** | El estado actual de los archivos en tu disco |
| **Staging Area** | Zona intermedia donde preparas los cambios antes del commit |
| **Commit** | Snapshot permanente del proyecto en un momento dado |
| **Branch** | Puntero móvil a un commit específico |
| **HEAD** | Puntero al commit actual o rama activa |
| **Remote** | Repositorio alojado en un servidor (GitHub, GitLab, etc.) |
| **Origin** | Alias por defecto para el remoto desde donde clonaste |
| **Upstream** | La rama remota que rastrea tu rama local |
| **Merge** | Combinar el historial de dos ramas |
| **Rebase** | Reescribir historial aplicando commits sobre otra base |
| **Cherry-pick** | Aplicar un commit específico en otra rama |
| **Stash** | Almacenamiento temporal de cambios sin commitear |
| **Tag** | Referencia inmutable a un commit (usada para versiones) |
| **Fork** | Copia de un repositorio bajo otra cuenta |
| **Pull Request** | Solicitud para fusionar cambios con revisión de código |
| **Detached HEAD** | Estado en que HEAD apunta a un commit, no a una rama |

---

## 🔗 Recursos

- [Documentación oficial de Git](https://git-scm.com/docs)
- [Pro Git Book (gratuito)](https://git-scm.com/book/en/v2)
- [GitHub Git Cheat Sheet (PDF)](https://training.github.com/downloads/github-git-cheat-sheet.pdf)
- [Conventional Commits](https://www.conventionalcommits.org)
- [Plantillas .gitignore](https://github.com/github/gitignore)
- [Visualizador interactivo de Git](https://learngitbranching.js.org)
- [Cómo usar Git Flow](https://www.campingcoder.com/2018/04/how-to-use-git-flow)

---

<div align="center">

**⭐ Si este cheat sheet te fue útil, dale una estrella al repositorio ⭐**

</div>
