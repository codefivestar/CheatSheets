
# 📘 GDScript Cheat Sheet (Godot Engine)

## 📌 Fundamentos
```gdscript
extends Node2D  # O cualquier tipo de nodo

func _ready():
    print("Hola Mundo")
```

## 🧩 Variables y Tipado
```gdscript
var nombre = "Godot"               # Dinámico
var edad: int = 4                  # Estático
const PI = 3.1416                  # Constante
```

## 🧠 Operadores
```gdscript
+, -, *, /, %, **     # Aritméticos
==, !=, <, >, <=, >=  # Comparación
&&, ||, !             # Lógicos (and, or, not)
```

## 🔁 Control de Flujo
```gdscript
if vida <= 0:
    morir()
elif vida < 50:
    curar()
else:
    atacar()

for i in range(10):
    print(i)

while energia > 0:
    consumir_energia()
```

## 🧱 Funciones
```gdscript
func saludar(nombre):
    print("Hola, %s" % nombre)

func suma(a: int, b: int) -> int:
    return a + b
```

## 🎭 Clases y Herencia
```gdscript
class_name Enemigo

extends Node2D

var salud = 100

func recibir_dano(dano):
    salud -= dano
```

## 🧠 Señales (Signals)
```gdscript
signal golpeado

func recibir_dano(dano):
    emit_signal("golpeado")

# Conexión
$Boton.connect("pressed", self, "_on_Boton_pressed")
```

## 📦 Arrays y Diccionarios
```gdscript
var lista = [1, 2, 3]
lista.append(4)
print(lista[0])

var diccionario = {"nombre": "Heroe", "vida": 100}
print(diccionario["vida"])
```

## 📌 Nodos y Escena
```gdscript
var nodo = get_node("MiNodo")      # También: $"MiNodo"
add_child(mi_nuevo_nodo)
queue_free()                       # Elimina el nodo
```

## 🎮 Movimiento (2D)
```gdscript
var velocidad = Vector2(100, 0)

func _process(delta):
    position += velocidad * delta
```

## 🕹️ Entrada
```gdscript
func _input(event):
    if event.is_action_pressed("ui_accept"):
        print("Aceptar presionado")
```

## 🧪 Debug
```gdscript
print("Debug info")
print_debug("Mensaje de depuración")
assert(valor > 0)
```
