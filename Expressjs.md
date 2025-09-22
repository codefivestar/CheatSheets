
# 🚀 Express.js Cheat Sheet

## 📦 Instalación
```bash
npm install express
npm install -g nodemon  # (opcional) para desarrollo
```

## 🚀 Servidor Básico
```javascript
const express = require('express');
const app = express();
const PORT = 3000;

app.listen(PORT, () => console.log(`Servidor corriendo en puerto ${PORT}`));
```

## 🧭 Rutas Básicas
```javascript
app.get('/', (req, res) => res.send('Hola Mundo'));
app.post('/', (req, res) => res.send('POST recibido'));
app.put('/', (req, res) => res.send('PUT recibido'));
app.delete('/', (req, res) => res.send('DELETE recibido'));
```

## 📂 Rutas en Archivos Separados
```javascript
// routes/users.js
const express = require('express');
const router = express.Router();

router.get('/', (req, res) => res.send('Usuarios'));

module.exports = router;

// app.js
const userRoutes = require('./routes/users');
app.use('/users', userRoutes);
```

## 📦 Middleware
```javascript
app.use(express.json()); // Parsear JSON
app.use(express.urlencoded({ extended: true })); // Formularios

// Middleware personalizado
app.use((req, res, next) => {
    console.log(`${req.method} ${req.url}`);
    next();
});
```

## 📁 Archivos Estáticos
```javascript
app.use(express.static('public'));
```

## 📄 Envío de Respuestas
```javascript
res.send('Hola');               // Texto
res.json({ nombre: 'Juan' });   // JSON
res.status(404).send('No encontrado'); // Código HTTP
```

## 📬 Parámetros y Query
```javascript
app.get('/user/:id', (req, res) => {
    res.send(`ID: ${req.params.id}`);
});

app.get('/search', (req, res) => {
    res.send(`Buscando: ${req.query.q}`);
});
```

## 📚 Controladores
```javascript
// controllers/userController.js
exports.listar = (req, res) => res.send('Lista de usuarios');

// routes/users.js
const userController = require('../controllers/userController');
router.get('/', userController.listar);
```

## 🧪 Manejo de Errores
```javascript
app.use((err, req, res, next) => {
    console.error(err.stack);
    res.status(500).send('¡Algo salió mal!');
});
```

## 🛡️ Seguridad y Utilidades
```bash
npm install cors dotenv helmet morgan
```

```javascript
const cors = require('cors');
const helmet = require('helmet');
const morgan = require('morgan');
require('dotenv').config();

app.use(cors());
app.use(helmet());
app.use(morgan('dev'));
```

## 🌍 Variables de Entorno (.env)
```
PORT=3000
```

```javascript
require('dotenv').config();
const PORT = process.env.PORT;
```

## 🧪 Testeo con Supertest
```bash
npm install --save-dev supertest jest
```

```javascript
// test/app.test.js
const request = require('supertest');
const app = require('../app');

test('GET / devuelve Hola Mundo', async () => {
    const res = await request(app).get('/');
    expect(res.statusCode).toBe(200);
});
```
