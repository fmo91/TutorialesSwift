# Introducción a Swift

**Swift** es el lenguaje más utilizado para desarrollar aplicaciones en iOS hoy en día. Y digo "el más utilizado" porque no es el único. Swift es relativamente moderno, fue [introducido por primera vez](https://www.youtube.com/watch?v=MO7Ta0DvEWA) en 2014, durante la conferencia anual para desarrolladores de Apple. Previamente, las aplicaciones para iOS eran desarrolladas utilizando un lenguaje llamado **Objective-C**.

Si bien Swift es muy distinto a Objective-C, fue muy bienvenido entre la comunidad de desarrolladores. Esto se debe principalmente a que Swift es más sencillo y moderno que su antecesor.

Algunas características de Swift son:

- **Es un lenguaje de programación moderno**: Adopta características de lenguajes de programación que fueron surgiendo en el último tiempo (funciones anónimas, funciones como tipo de dato, tipos de datos opcionales, pattern-matching avanzado, inferencia de tipos, etc.)
- **Es multiparadigma**: Se puede programar funcional, orientado a objetos, orientado a protocolos, o mezclando un poco de cada uno.
- **Es seguro**: Es difícil que falle al ejecutar si compiló con éxito.
- **Es sencillo**: Si bien Swift es un lenguaje enorme, comenzar a desarrollar en él no es algo complicado, y una introducción se puede realizar en algunos minutos.
- **Es de código abierto**: Desde el año 2015, Swift es un lenguaje desarrollado por la comunidad. Cualquiera puede ver su código fuente y modificarlo. Es posible utilizar Swift en MacOS y en Linux.

Ahora sí, superadas las formalidades, veamos un poco de código en Swift.

## Declaración de variables

La declaración de una variable se realiza con la palabra clave `var`:

```swift
var alturaDeLaCasa: Int = 5
```

Algunas cosas para notar en este ejemplo:

- Los nombres de las variables comienzan con minúscula, y luego, cada palabra que contenga luego de la primera comenzará con mayúscula.
- El tipo de dato `Int`, representa a los números enteros, comienza con mayúscula como todos los tipos de datos, y se coloca luego del nombre de la variable, a continuación de los dos puntos.
- La asignación se realiza con el símbolo de `=`.
- En Swift los `;` (punto y coma) son opcionales! Pueden o no ir, dependiendo del gusto del desarrollador, que por lo general los ignora.

Vamos a aprovechar la modernidad de Swift para realizar un pequeño cambio en la declaración de arriba:

```swift
var alturaDeLaCasa = 5
```

Así es, el tipo no tiene que ser especificado en forma obligatoria. El compilador de Swift se da cuenta de que alturaDeLaCasa es un número entero, porque le estamos asignando un valor entero (5). Esta característica de Swift y otros lenguajes se llama **Inferencia de tipos**.

## Declaración de constantes

Así como definimos variables con la palabra clave `var`, definimos constantes con la palabra clave `let`.

De esta manera, esto se permite:

```swift
var alturaDeLaCasa = 5
alturaDeLaCasa = 10
```

Pero esto no:

```swift
let alturaDeLaCasa = 5
alturaDeLaCasa = 10
```

El programa no compilará. Swift acusará un error en la línea en la que reasignamos la variable `alturaDeLaCasa`.
Por lo general, en Swift se prefieren las constantes a las variables, la recomendación general es usar constantes siempre que sea posible, y variables solo en caso de ser necesario.

## Comentarios

Los comentarios en Swift son del mismo estilo que en C, C++, Java, o muchos otros lenguajes. Veamos:

```swift
// Esto es un comentario de una sola línea
var altura: Int = 10

/*
    Este es un comentario multilinea,
    aquí podemos escribir varias líneas para
    dar explicaciones más extensas
*/
altura = 15

/**
    Esto es un comentario de documentación. Noten 
    los dos asteriscos al comienzo del comentario.
    Este tipo de comentarios sirve para documentar un proyecto.
*/
let ancho = 100
```

## Tipos de datos

En Swift, además de `Int`, existen algunos otros tipos de datos que consideramos primitivos:

```swift
/* String es un tipo de dato que
sirve para describir cadenas de texto. */
let nombre: String = "Fernando"

/* Bool es tipo de dato que
sirve para describir valores booleanos,
es decir, verdadero (true) o falso (false) */
let esDesarrollador: Bool = true

// El tipo de dato Int con el que venimos trabajando
let edad: Int = 27

/* Double es un valor decimal, de 64 bits,
Si bien también existe el tipo de dato Float, normalmente
utilizamos Double para todos los casos. */
let altura: Double
```

## Tipos de datos numéricos

Los números en Swift se comportan igual que en muchos otros lenguajes de programación, las operaciones aritméticas son las mismas. Veamos:

```swift
let a: Int = 10
let b: Int = 20
let c: Int = a + b // 30

let d: Double = 1 / 3 // 0.3333...

var e = 10
e += 10 // 40
e -= 20 // 20
e /= 2 // 10

e++ // ERROR! Aunque no lo crean, ++ y -- no funcionan en Swift.
// En vez de eso, debemos usar lo siguiente:
e += 1 // En este caso, incrementaremos e en 1.
```

## String

Las cadenas de texto en Swift son colecciones de caracteres que permiten realizar ciertas operaciones sobre ellos:

```swift
// Se pueden concatenar sumándolos
let nombre = "Fernando"
let comienzoDeSaludo = "Hola"
let saludo = comienzoDeSaludo + " " + nombre

// O lo que es más sencillo, se pueden "interpolar"
let despedida = "Chau, \(nombre)" 
// despedida tendrá como valor "Chau, Fernando"

// La interpolación no se limita a String, 
// sino que se puede interpolar cualquier tipo de dato
// dentro de un String.
let edad = 27
let descripcion = "\(nombre) tiene \(edad) años"
```

Por lo general, preferimos realizar interpolación sobre concatenación siempre que sea posible.

## Array

Además de los tipos de dato que describimos ahí arriba, otro tipo muy común es el `Array`. Un `Array` es una colección de elementos de algún tipo de dato. Por ejemplo:

```swift
// Esto es un Array de Int
let numerosPares = [2, 4, 6, 8]

// Array de String
let nombresConF = "Fernando, Fabián, Federico"

// Si queremos especificar el tipo de dato, podemos escribir
// de esta manera que se trata de un Array de enteros.
let numerosImpares: [Int] = [1, 3, 5]

// O bien así:
let numerosNegativos: Array<Int> = [-1, -2, -3]
```

La otra opción que tenemos es declarar un `Array` vacío y luego colocarle valores dentro:

```swift
// En este caso es importante declarar el tipo de dato,
// porque el compilador no puede inferir el tipo de dato
// que guardará el Array, ya que le asignamos un valor vacío.
//
// También es importante que lo declaremos como var, y no como let
// porque lo modificaremos a continuación, agregándole
// nuevos valores dentro
var numerosPares: [Int] = []

// De esta manera podemos agregar nuevos Int
// en el Array
numerosPares.append(2)
numerosPares.append(4)
numerosPares.append(4)
numerosPares.append(8)
```

## Print

Para facilitar la experimentación en nuestros ejercicios, la función `print` servirá para imprimir una línea por consola. Esto nos permitirá inspeccionar en nuestras variables, y entender cómo se comporta nuestro código.

```swift
print("Hola!") // Imprimirá "Hola!" por la consola.

let nombre = "Fernando"
print("Hola, \(nombre)!") // Imprimirá "Hola, Fernando!" por consola.
```

## Condiciones booleanas

Los valores booleanos son dos: `true` (verdadero) y `false` (falso). Y como en muchos otros lenguajes, se pueden combinar, dando siempre como resultado, otro valor booleano.

```swift
let edad = 27

// >, <, >=, <=, ==, != funcionan exactamente igual que como esperaríamos
let mayorDeEdad: Bool = edad >= 18 

let esMasculino = true

// Solo es jubilado si es masculino, y tiene la edad necesaria
// && es AND, es decir, espera que se cumplan ambas condiciones.
let esJubilado = esMasculino && edad >= 65 

// Con ! podemos negar un booleano. Si era true, pasa a ser false, y viceversa
let esFemenino = !esMasculino 

let canalDeTV = "Fox Sports"

// Con || podemos expresar OR, es decir, que será verdadero
// Si al menos una de las dos condiciones es verdadera.
let esCanalDeportivo = canalDeTV == "Fox Sports" || canalDeTV == "TyC Sports" || canalDeTV = "ESPN"
```

## Control de flujo.

Las estructuras de control de flujo nos sirven para determinar el funcionamiento de nuestro código a partir de condiciones que establezcamos.

### If / Else

Usamos la estructura if (if/else) para describir una selección, es decir, para decidir si un fragmento de código se ejecutará o no a partir de una condición.

```swift
let edad = 17
if edad >= 18 { // SIN PARENTESIS! No es necesario
    print("Es mayor de edad")
}
```

La sentencia `else` permite establecer un camino alternativo en caso de que la condición del if no sea verdadera:

```swift
let edad = 17
let esMayorDeEdad = edad >= 18

if esMayorDeEdad {
    print("Es mayor de edad")
} else {
    print("Es menor")
}
```

### Switch

Usamos `switch` para ejecutar código según el valor de una variable

```swift
let canal = "TyC Sports"

switch canal {
case "TyC Sports", "Fox Sports", "ESPN":
    print("Canal de deportes")
case "TNT", "HBO", "Cinecanal":
    print("Canal de películas")
case "Cronica":
    print("Canal de noticias")
}
```

Cada uno de los `case` puede tener más de un valor, separados por coma.

### While

La estructura `while` repetirá un fragmento de código mientras una condición se cumpla:

```swift
var x = 0
let limite = 10
while x < limite {
    x += 1
    print(x) // Imprimirá los números del 1 al 10
}
```

Una estructura muy similar a `while` es `repeat` (do-while en otros lenguajes):

```swift
var x = 100
let limite = 10
while x < limite {
    x += 1
    print(x) // Esto nunca se ejecutará! Porque x > limite
}

repeat {
    x += 1
    print(x) 
} while x < limite
// Esta segunda expresión se ejecutará una sola vez, porque la condición
// se evalúa después de la primera ejecución del bloque
```

### For

`for` es una estructura que varía un poco su comportamiento a comparación de otros lenguajes. Si estaban acostumbrados a for (int i = 0 ; i < 100 ; i++), en Swift esto cambia completamente. Veamos:

```swift
// El equivalente a for (int i = 0 ; i < 100 ; i++) es:
for i in 0 ..< 100 {
    print (i) // Imprimirá los números del 0 al 99
}

// El otro caso en el que `for` sirve es cuando 
// queremos recorrer los elementos de un Array
let numerosPares = [2, 4, 6, 8]
for numero in numerosPares {
    print(numero) // Imprimirá 2, luego 4, ...
}
```

## Funciones

Una función es un fragmento de código, encerrado entre llaves, que puede tener un nombre, puede recibir valores pasados como argumentos, y puede o no devolver un resultado.

En Swift, la palabra clave para definir una función es `func`.

Veamos el ejemplo más sencillo:

```swift
func saludar() {
    print("Hola!")
}

saludar() // Así se invoca la función
```

A notar en el ejemplo:

- La función se define con `func`.
- La función no recibe argumentos.
- La función no devuelve un resultado (el tipo de dato del resultado es `Void`)

Supongamos que queremos hacer que nuestra función salude a una persona por su nombre:

```swift
func saludar(nombre: String) {
    print("Hola, \(nombre)!")
}

saludar(nombre: "Fernando")
```

- La función recibe un argumento llamado `nombre`. 
- Cuando invocamos a la función, debemos escribir el nombre del argumento.

Pero esto puede quedar un poco más natural:

```swift
func saludar(a nombre: String) {
    print("Hola, \(nombre)!")
}

saludar(a: "Fernando")
```

- El argumento `nombre` ahora tiene dos nombres. Uno para usar internamente (`nombre`) y otro para usar externamente (`a`). 
- Cuando escribimos el cuerpo de la función, usamos el nombre interno del argumento.
- Cuando invocamos a la función, usamos el nombre externo del argumento.

Veamos el ejemplo de una función de suma:

```swift
func sumar(x: Int, y: Int) -> Int {
    return x + y
}

let resultado = sumar(x: 1, y: 5) 
print(resultado) // El resultado es 6
```

- Ahora tenemos dos argumentos. Podemos tener cualquier cantidad de argumentos, separados por coma.
- La función devuelve un `Int`. Para especificar el tipo de dato resultado, usaremos la flechita `->`, seguido del tipo de dato.

Pero como antes, esto no queda muy natural, y podemos dejarlo más legible:

```swift
func sumar(_ x: Int, _ y: Int) -> Int {
    return x + y
}

let resultado = sumar(1, 5)
print(resultado) // El resultado es 6
```

Por último, podemos darle un valor por defecto a los argumentos de una función:

```swift
func incrementar(_ x: Int, incremento: Int = 1) -> Int {
    return x + incremento
}

var a = 1
a = incrementar(a) // a pasa a tener valor 2
a = incrementar(a) // a es 3
a = incrementar(a, incremento: 7) // a es 3 + 7 = 10.
```

## Precondiciones

Las **precondiciones** son condiciones que deben complirse para que una función se pueda ejecutar. En Swift, las precondiciones se declaran con la palabra clave `guard`. Podemos imaginar `guard` como un `if` invertido.

```swift
func dividir(_ dividendo: Int, por divisor: Int) -> Double {
    // Esto se lee como:
    //
    // "Asegurate de que `divisor` sea distinto de 0. Y si no se cumple
    // entonces ejecutá este bloque de código."
    guard divisor != 0 else {
        // Por ahora, devolveremos un -1 como código de error.
        // Luego veremos otras formas mejores de resolver este problema.
        return -1 
    }

    return dividendo / divisor
}

let a = dividir(10, por: 5) // a = 2
let b = dividir(10, por: 0) // b = -1, Es un error.
```

## Links relacionados

Lo que vimos hoy fue un resumen de las características básicas de Swift, y un recorrido por la sintaxis. Swift es un lenguaje muy extenso y es MUCHO MÁS que lo que vimos hoy. Para terminar, algunos enlaces, completamente opcionales esta vez, no es necesario que los lean de punta a punta:

- Documentación oficial: https://docs.swift.org/swift-book/LanguageGuide/TheBasics.html
- Tutorial de introducción a Swift por Ray Wenderlich: https://www.raywenderlich.com/6338-swift-tutorial-part-1-expressions-variables-and-constants