
# 📦 NPM (Node Package Manager) Cheat Sheet

## 📥 Instalación

### Node.js incluye npm
```bash
node -v
npm -v
```

---

## 📦 Inicializar Proyecto
```bash
npm init              # Preguntas interactivas
npm init -y           # Usa valores por defecto
```

---

## 📁 Instalación de Paquetes

### Dependencias del proyecto
```bash
npm install paquete
npm i paquete         # Alias
```

### Dependencias de desarrollo
```bash
npm install paquete --save-dev
```

### Instalación global
```bash
npm install -g paquete
```

### Actualizar version global
```bash
npm install -g npm@latest
npm install -g npm@11.4.0
```

### Versión específica
```bash
npm install paquete@1.2.3
```

### Múltiples paquetes
```bash
npm install paquete1 paquete2
```

---

## 🔄 Actualización
```bash
npm update
npm update paquete
```

---

## ❌ Eliminación de paquetes
```bash
npm uninstall paquete
```

---

## 📄 Información del paquete
```bash
npm info paquete
```

---

## 🔍 Buscar paquetes
```bash
npm search palabra-clave
```

---

## 🧪 Scripts en package.json
```json
"scripts": {
  "start": "node index.js",
  "dev": "nodemon app.js",
  "test": "jest"
}
```
```bash
npm run dev
npm start     # Atajo para "start"
```

---

## 📁 node_modules y package-lock.json

- `node_modules/`: Contiene las dependencias instaladas.
- `package-lock.json`: Guarda versiones exactas de dependencias.

---

## ✅ Versionado Semántico
- `^1.2.3`: Compatible con versión mayor
- `~1.2.3`: Compatible con versión menor
- `1.2.3`: Exactamente esa versión

---

## 📂 Archivos útiles
- `.npmrc`: Configuración personalizada.
- `.gitignore`: Excluir `node_modules`.

---

## 🛠 Otros Comandos Útiles
```bash
npm list             # Ver dependencias
npm outdated         # Ver paquetes desactualizados
npm ci               # Instalación limpia desde package-lock.json
```

---

## 🧩 Crear Paquete Propio
```bash
npm login
npm publish
```

