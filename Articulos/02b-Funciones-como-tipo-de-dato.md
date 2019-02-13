# Funciones como tipo de dato

Las funciones son bloques de código que se escriben bajo un nombre, y suelen usarse para reutilizar funcionalidad.
En Swift, sin embargo, las funciones son un tipo de dato como cualquier otro. Es decir, una cierta variable `f` puede ser de tipo Int, Double, String, o función. Lo que implica, entre muchas otras cosas, que una función pueda recibir una función como argumento, o que una función pueda devolver otra función como resultado.
Las funciones como tipo de dato también se llaman **closures**

## Sintaxis

```swift
// Si una función `sumar` se escribe así:
func sumar(_ x: Int, _ y: Int) -> Int {
    return x + y
}

// Una closure equivalente podría ser así:
let sumar = { (x: Int, y: Int) -> Int in
    return x + y
}

// Y el tipo sería (Int, Int) -> Int
// Por lo que sumar también podría haberse declarado como
// let sumar: (Int, Int) -> Int = ...

// Esto también puede reescribirse en forma más sencilla:
let sumar: (Int, Int) -> Int = { x, y in return x + y }

// O también
let sumar: (Int, Int) -> Int =  { x, y in x + y }

// Swift también permite llamar a los argumentos según
// su orden de aparición en la función.
let sumar: (Int, Int) -> Int = { $0 + $1 }
```

Al tener una función como tipo de dato en una variable, puede ser enviada a otra función. Cuando una función recibe otra función como parámetro, o devuelve una función como resultado.