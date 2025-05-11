
# 🍃 MongoDB Cheat Sheet

## 📦 Instalación
```bash
npm install mongodb         # Driver nativo
npm install mongoose        # ODM para Node.js
```

## 🌐 Conexión (Driver Nativo)
```javascript
const { MongoClient } = require('mongodb');
const uri = "mongodb://localhost:27017";
const client = new MongoClient(uri);

async function conectar() {
    await client.connect();
    const db = client.db("mi_basededatos");
    console.log("Conectado a MongoDB");
}
```

## 🔗 Conexión con Mongoose
```javascript
const mongoose = require('mongoose');

mongoose.connect('mongodb://localhost:27017/mi_basededatos', {
    useNewUrlParser: true,
    useUnifiedTopology: true
})
.then(() => console.log('MongoDB conectado'))
.catch(err => console.error(err));
```

## 📄 Definir un Modelo con Mongoose
```javascript
const mongoose = require('mongoose');

const UsuarioSchema = new mongoose.Schema({
    nombre: String,
    edad: Number,
    email: { type: String, unique: true }
});

const Usuario = mongoose.model('Usuario', UsuarioSchema);
```

## ✍️ Crear Documento
```javascript
const nuevoUsuario = new Usuario({ nombre: "Ana", edad: 30 });
await nuevoUsuario.save();
```

## 🔍 Leer Documentos
```javascript
const usuarios = await Usuario.find();
const usuario = await Usuario.findById(id);
const filtrado = await Usuario.findOne({ nombre: "Ana" });
```

## ✏️ Actualizar Documentos
```javascript
await Usuario.updateOne({ _id: id }, { $set: { edad: 35 } });
await Usuario.findByIdAndUpdate(id, { edad: 40 });
```

## ❌ Eliminar Documentos
```javascript
await Usuario.deleteOne({ _id: id });
await Usuario.findByIdAndDelete(id);
```

## 🔍 Consultas Avanzadas
```javascript
Usuario.find({ edad: { $gt: 18 } });          // Mayor que 18
Usuario.find({ nombre: /ana/i });             // Regex (Ana, ana)
Usuario.find().sort({ edad: -1 });            // Ordenar descendente
Usuario.find().limit(10);                     // Limitar resultados
```

## 🔧 Operadores Comunes
```js
$gt, $gte, $lt, $lte   // Comparación
$eq, $ne               // Igual / diferente
$in, $nin              // En un array / no en array
$and, $or, $not        // Lógicos
$exists                // Campo existente
```

## 📁 Crear Índices
```javascript
Usuario.createIndex({ email: 1 }, { unique: true });
```

## ⚙️ Agregaciones
```javascript
Usuario.aggregate([
  { $match: { edad: { $gt: 20 } } },
  { $group: { _id: "$edad", total: { $sum: 1 } } },
  { $sort: { total: -1 } }
]);
```

## 📜 Validaciones en Mongoose
```javascript
const Schema = mongoose.Schema;
const esquema = new Schema({
    nombre: { type: String, required: true },
    edad: { type: Number, min: 0, max: 120 }
});
```
