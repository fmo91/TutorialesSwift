# Otras estructuras de datos

Podemos hablar de estructuras de datos como contenedores de datos con funciones asociadas.

Ya hemos visto una estructura de datos muy utilizada en Swift, que es la clase. Sin embargo, Swift tiene varias estructuras de datos presentes en el lenguaje. En este apartado veremos algunas.

## Struct

Las structs son estructuras de datos **muy similares** a las clases:

- Pueden contener atributos.
- Pueden contener métodos.
- Pueden implementar protocolos.

Sin embargo, tienen algunas diferencias básicas:

- Una struct no puede heredar de otra struct o clase o viceversa.
- Las structs tienen un constructor por defecto, que inicializa todos sus atributos.
- **Las structs se pasan por valor y no por referencia**. Esta es la diferencia más importante, y la explicaremos luego.

Veamos una struct sencilla:

```swift
struct Direccion {
    let calle: String
    let numero: String

    func describir() -> String {
        return "\(calle) \(numero)"
    }
}

// Direccion tiene un constructor por defecto.
let casa = Direccion(calle: "Av Rivadavia", numero: "18451")

print(casa.describir()) // Av Rivadavia 18451
```

Veamos a qué nos referimos con "Las structs se pasan por valor y no por referencia".

Supongamos el siguiente ejemplo, con struct:

```swift
struct Persona {
    let nombre: String
}

var fernando = Persona(nombre: "Fernando")
var martin = fernando
martin.nombre = "Martin"
print(fernando.nombre) // Fernando
print(martin.nombre) // Martin
```

Y el siguiente, ahora con clases:

```swift
class Persona {
    let nombre: String
    init(nombre: String) { self.nombre = nombre }
}

var fernando = Persona(nombre: "Fernando")
var martin = fernando
martin.nombre = "Martin"
print(fernando.nombre) // Martin
print(martin.nombre) // Martin
```

Pareciera ser que el ejemplo con clases funciona mal. Y efectivamente, no está realizando lo que esperaríamos que haga. Sin embargo, esto tiene una razón clara. Cuando igualamos a `martin` y `fernando` en el caso de las structs, lo que está sucediendo es que se crea una nueva struct, copia de `fernando`, pero completamente independiente. Si cambiamos los atributos de `martin`, esto no afectará a `fernando`, y viceversa.

En el caso de las clases en cambio, esto no es así, lo que se copia es la **referencia** y no el **valor**, y esto tiene consecuencias prácticas. Cuando igualamos las referencias de `fernando` y de `martin`, los objetos quedan apuntando al mismo espacio de memoria, de modo que si modificamos un atributo de `fernando`, esto también modificará el atributo de `martin`. 

## Enum

Las `enum` existen en muchos lenguajes de programación. Se encuentran presentes en Java, C#, C, y muchos otros. Sin embargo, las enum de Swift son mucho más potentes y merecen una mención especial.

En esencia, una enum es un conjunto de casos que representan valores posibles que puede tomar una determinada variable. Por ejemplo:

```swift
enum TipoDeIdentificacion {
    case dni
    case legajo
    case licenciaDeConducir
}
```

De esa manera tan sencilla estamos definiendo una enum. Para utilizarla, basta con declarar una variable de ese tipo, y luego asignarle cualquiera de esos casos.

```swift
struct Identificacion {
    let tipo: TipoDeIdentificacion
    let numero: String
}

let documento = Identificacion(
    tipo: TipoDeIdentificacion.dni,
    numero: "40100202"
)
```

### Enum con valores asociados

Los casos de la enum pueden tener datos asociados. Esto puede ser útil en ciertos casos. Veamos un ejemplo

```swift
enum Salud {
    case sano
    case enfermo(enfermedad: String)
}

struct Gato {
    let nombre: String
    let estadoDeSalud: Salud
}

let michi = Gato(nombre: "Michi", estadoDeSalud: Salud.sano)
let manchas = Gato(nombre: "Manchas", estadoDeSalud: Salud.enfermo(enfermedad: "Gripe"))
```

### Switch en una enum

Una de las operaciones que más solemos usar sobre enums es el `switch`. Imaginemos que queremos preguntar sobre el estado de salud de los gatos.

```swift
func obtenerDiagnostico(gato: Gato) -> String {
    switch gato.estadoDeSalud {
    case Salud.sano:
        return "El gato está sano"
    // De esta manera manejamos el caso en el que un 
    // case de la enum tenga un dato asociado.
    case Salud.enfermo(let enfermedad):
        return "El gato está enfermo. Tiene \(enfermedad)"
    }
}
```

## Tuple

Las tuplas son estructuras de datos muy limitadas que sirven solo en ciertos casos. Algunas cosas importantes que debemos saber de ellas:

- Son un conjunto de valores asociados, nada más que eso
- No pueden heredar de nada
- Nada puede heredar de ellas
- No pueden contener funciones
- No se pueden extender

```swift
let direccion: (calle: String, numero: String) = (calle: "Rivadavia", numero: "18451")

print(direccion.calle)
print(direccion.numero)
```

### Destructuring

Destructuring es una operación por la cual decomponemos una tupla en las partes que la componen, en distinas variables.

```swift
let (calle, numero) = direccion

print(calle)
print(numero)
```

### Resultados múltiples de una función

Uno de los casos más útiles en los cuales nos puede servir una tupla es para devolver más de un resultado en una función.

```swift
func obtenerRango(base: Int, variacion: Int) -> (Int, Int) {
    return (base - variacion, base + variacion)
}

let (minimo, maximo) = obtenerRango(base: 10, variacion: 2)

print(minimo) // 8
print(maximo) // 12
```

## Typealias

Typealias no es una estructura de datos, sino simplemente una manera de renombrar un tipo ya existente.

```swift
typealias Entero = Int

let x: Entero = 20
```

Así de sencillo. Y a simple vista no parece muy útil, pero es en realidad muy útil cuando hablamos de tuplas.

```swift
typealias Direccion = (calle: String, numero: String)

let casa: Direccion = (calle: "Avenida Rivadavia", numero: "18451")
```

