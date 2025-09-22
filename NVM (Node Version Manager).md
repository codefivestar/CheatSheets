
# 🧠 NVM (Node Version Manager) Cheat Sheet

## 📦 Instalación

### Linux / macOS
```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
```

# en lugar de reiniciar la shell
```bash
\. "$HOME/.nvm/nvm.sh"
```

### Windows
Usar [`nvm-windows`](https://github.com/coreybutler/nvm-windows):
- Descargar desde: https://github.com/coreybutler/nvm-windows/releases

---

## 🔍 Verificar instalación
```bash
nvm --version
```

---

## 📥 Instalar versiones de Node.js
```bash
nvm install node         # Última versión estable
nvm install --lts        # Última versión LTS
nvm install 18.17.0      # Versión específica
```

---

## 🔁 Cambiar de versión
```bash
nvm use 18.17.0
nvm use node             # Usar última versión
```

---

## 💾 Listar versiones
```bash
nvm ls                   # Locales
nvm ls-remote            # Disponibles para instalar
```

---

## 🗑️ Eliminar versión
```bash
nvm uninstall 16.20.0
```

---

## 🧩 Establecer versión predeterminada
```bash
nvm alias default 18.17.0
```

---

## 🔄 Usar archivo `.nvmrc`
```bash
# Contenido del archivo .nvmrc
18.17.0

# Usarlo
nvm use                  # Detecta la versión de .nvmrc
```

---

## ✅ Comprobar versión activa
```bash
node -v
nvm current
```

---

## 🛠 Tips
- NVM no funciona con sudo.
- Ideal para manejar múltiples versiones entre proyectos.
- Compatible con herramientas como `npx`, `npm`, `yarn`.

