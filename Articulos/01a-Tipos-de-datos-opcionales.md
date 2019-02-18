# Tipos de datos opcionales

Todos los que hemos trabajado en lenguajes de programación como Java o C/C++ nos hemos cruzado en algún momento con errores que cerraban nuestros programas por querer utilizar variables que contenían `null` (`nil` en Swift).

En Swift, afortunadamente, contamos con herramientas que nos ayudan a evitar este tipo de inconvenientes: Los tipos de datos opcionales.

Una variable es opcional si puede contener un valor, o `nil`. 

```swift
// Estas dos variables no son opcionales,
// ya que tienen un valor asociado
var nombre: String = "Fernando"
var apellido: String = "Ortiz"

// segundoNombre en cambio es opcional,
// de ahí que contenga el `?` en el tipo String. 
// Una persona puede o no tener segundo nombre.
var segundoNombre: String? = nil

// Esto es válido, porque las variables opcionales
// pueden o no tener valores asociados.
segundoNombre = "Martín"

// ESTO DARÁ UN ERROR!
// NOMBRE NO ES OPCIONAL!
nombre = nil
```

Como se ve en el ejemplo, el signo `?` es el que indica que la variable es opcional, y por lo tanto puede llegar a ser `nil`. Hay una segunda manera de declarar una variable opcional:

```swift
var segundoNombre: String! = "Martín"
```

Con `!`, también podemos declarar una variable opcional. La diferencia entre declarar una variable con `?` y `!` es que cuando trabajamos con variables `?`, Swift nos exige asegurarnos constantemente de que tienen valor, mientras que las variables `!` (o *Implicitly Unwrapped Optionals*), no nos imponen ninguna restricción, y se comportan de la misma manera que estabamos acostumbrados en lenguajes como Java o C++.

## Trabajando con Opcionales

Imaginemos que queremos trabajar con una variable opcional

```swift
let segundoNombre: String? = "Martín"
let otroSegundoNombre: String! = "Pedro"

func saludar(a nombre: String) {
    print("Hola \(nombre)")
}

saludar(a: segundoNombre) // ERROR! segundoNombre es opcional.
saludar(a: otroSegundoNombre) // ESTO FUNCIONA CORRECTAMENTE!
```

Hay varias maneras de solucionar estos errores. La primera es haciendo lo que se conoce como "Unwrap". Hacer un unwrap de una variable opcional implica decidir que estamos **SEGUROS** de que esta variable contiene un valor, y no es `nil`. La recomendación general es no usarlo demasiado, no abusar del unwrap de opcionales, porque hay métodos más seguros de trabajar con opcionales, como veremos luego. Sin embargo, esto existe, se puede hacer, y es bueno conocerlo. Volviendo al ejemplo anterior:

```swift
saludar(a: segundoNombre!) // Ahora sí funcionará!
```

### If-Let

Una de las maneras que nos ayuda a trabajar con opcionales de una manera segura es a través de `if-let`. El funcionamiento es sencillo. La condición del `if`, en este caso, será verdadera si la variable que estamos evaluando tiene valor, y será falsa si la variable es `nil`.

```swift
var segundoNombre: String?

segundoNombre = "Martín"

if let nombre = segundoNombre {
    print("El segundo nombre es \(nombre)")
} else {
    print("No hay segundo nombre")
}
```

### Guard-Let

Hay otra forma similar a if-let, pero que evalúa en forma contraria, como **precondición**. `guard` y `let` se combinan para evaluar precondiciones opcionales.

```swift
func imprimirSegundoNombre(_ segundoNombre: String?) {
    guard let _segundoNombre = segundoNombre else {
        print("No hay segundo nombre")
        return
    }

    print("El segundo nombre es \(_segundoNombre)")
}
```

