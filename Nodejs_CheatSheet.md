
# 🚀 Node.js Cheat Sheet

## 📦 Inicialización y Módulos
```bash
npm init -y             # Crear package.json
npm install express     # Instalar Express
npm install -g nodemon  # Instalar nodemon globalmente
```

## 📁 Estructura de Proyecto Típica
```
/project-root
│
├── app.js
├── routes/
│   └── users.js
├── controllers/
│   └── userController.js
├── models/
│   └── user.js
└── package.json
```

## 📄 Crear un Servidor Básico
```javascript
const http = require('http');

const server = http.createServer((req, res) => {
    res.write('Hola Mundo');
    res.end();
});

server.listen(3000, () => console.log('Servidor en puerto 3000'));
```

## 🌐 Express.js Básico
```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send('Hola desde Express');
});

app.listen(3000, () => console.log('Servidor en Express'));
```

## 🧾 Middleware
```javascript
app.use(express.json()); // Parsear JSON
app.use(express.urlencoded({ extended: true })); // Formularios

app.use((req, res, next) => {
    console.log(`${req.method} ${req.url}`);
    next();
});
```

## 🔄 Rutas con Express
```javascript
app.get('/users', userController.listar);
app.post('/users', userController.crear);
app.put('/users/:id', userController.actualizar);
app.delete('/users/:id', userController.eliminar);
```

## 📂 Módulos y Exportación
```javascript
// suma.js
module.exports = function(a, b) {
    return a + b;
};

// app.js
const suma = require('./suma');
console.log(suma(2, 3));
```

## 💾 Leer/Escribir Archivos
```javascript
const fs = require('fs');

// Leer
fs.readFile('archivo.txt', 'utf8', (err, data) => {
    if (err) throw err;
    console.log(data);
});

// Escribir
fs.writeFile('archivo.txt', 'Hola mundo', (err) => {
    if (err) throw err;
    console.log('Archivo guardado');
});
```

## 📡 HTTP con Fetch (desde el cliente)
```javascript
fetch('/api/datos')
    .then(res => res.json())
    .then(data => console.log(data));
```

## 🐞 Debug y Logs
```javascript
console.log('Mensaje');
console.error('Error');
```

## 🧪 Test con Jest
```bash
npm install --save-dev jest
```

```javascript
// suma.js
function suma(a, b) {
    return a + b;
}
module.exports = suma;

// suma.test.js
const suma = require('./suma');
test('2 + 2 = 4', () => {
    expect(suma(2, 2)).toBe(4);
});
```

## 🌍 Variables de Entorno
```bash
# .env
PORT=3000
```

```javascript
require('dotenv').config();
const port = process.env.PORT;
```
