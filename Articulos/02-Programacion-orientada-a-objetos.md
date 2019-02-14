# Programación orientada a objetos en Swift

Si bien Swift es un lenguaje multiparadigma (lo cual quiere decir que soporta varios paradigmas de programación a la vez), el paradigma de programación que predomina en la industria en este momento es claramente la **programación orientada a objetos** (POO, o OOP por sus siglas en inglés).

Otros lenguajes de programación orientados a objetos son Java, C#, Smalltalk, C++, Objective-C y Typescript, entre otros. El conocimiento en cualquiera de estos lenguajes será útil en este curso, pero no es absolutamente necesario.

## Conceptos de la POO

Recordemos entonces cómo funciona el paradigma de programación orientada a objetos y de qué manera podemos implementar esos conceptos en Swift.

Antes que nada, es importante comprender que POO es un modelo mental. Es una esquema a partir del cual podemos representar un problema en código a partir de unidades simples.

En todo programa de computadora tenemos dos conceptos bien diferenciados: **los datos** y **los procesamientos sobre los datos**. 

Previo a aprender POO, solemos aprender el paradigma estructurado, normalmente a partir del lenguaje C. En este paradigma, tenemos datos almacenados en variables, y funciones que reciben datos y devuelven resultados. **Ambos conceptos conviven por separado**. 

En POO, esto no se cumple. Los datos y los procesamientos coexisten dentro de unidades llamadas **objetos**. Un objeto no es más que datos, y procesamientos (funciones, también llamadas métodos), sobre esos datos. Por ejemplo, podemos tener un objeto "jorge", que tiene como datos, un String nombre, con valor "Jorge", y un String apellido, con valor "Gomez", y un método obtenerNombreCompleto() que devuelva el String "Jorge Gomez". Tanto los datos, como las funciones que operan con esos datos conviven en esa unidad llamada objeto.

### Clases

Una clase es un molde a partir del cual se crean objetos. Así, si teníamos el objeto "jorge", podemos tener la clase Persona, que define el tipo de datos que va a tener jorge, así como los métodos que contendrá.

Definir una clase Persona en Swift es muy sencillo, pero involucra algunos conceptos que debemos analizar.

```swift
// La palabra clave class define una clase
// Noten que escribimos el nombre en mayúscula
class Persona {
    // Definimos los datos, también llamados 
    // variables miembro o atributos,
    // simplemente declarándolos como cualquier variable
    // común y corriente.
    let nombre: String
    let apellido: String

    // con la palabra clave definimos un constructor.
    // Los constructores son funciones que se ejecutan
    // al "instanciar", es decir, crear, el objeto
    // a partir de una clase.
    init(nombre: string, apellido: String) {
        // self es la palabra clave que nos permite referirnos al objeto
        // en el que estamos operando en este momento.
        self.nombre = nombre
        self.apellido = apellido
    }

    // Los métodos se definen como una función cualquiera,
    // pero tienen acceso a cualquier atributo del mismo objeto.
    func obtenerNombreCompleto() -> String {
        // No es necesario el "self", solo es necesario
        // para distinguir el atributo de un parámetro de la función,
        // como en el caso del constructor que vimos recién.
        return "\(nombre) \(apellido)"
    }
}
```

Y esa clase Persona podría usarse así:

```swift
let jorge = Persona(nombre: "Jorge", apellido: "Gomez")
// El punto "." nos permite acceder a los atributos
// o a los métodos de un objeto.
print("La persona se llama \(jorge.obtenerNombreCompleto())")
```

### Herencia

La **herencia** es, junto al **polimorfismo** y el **encapsulamiento**, uno de los tres pilares de la programación orientada a objetos, y es ciertamente una herramienta muy poderosa cuando se trata de diseñar software orientado a objetos. No obstante, es una técnica peligrosa y debe usarse con cuidado.

La herencia nos dice que si tenemos dos clases, y una es "un tipo de" la otra clase, entonces la primera clase "hereda", o "es hija" de la segunda, que se considera la clase "padre", o "superclase". Por ejemplo, un Estudiante es "un tipo de" Persona, entonces tendría sentido que Estudiante "herede" de Persona.

Como consecuencia de la herencia, la clase que hija obtiene todos los atributos y métodos de la clase padre, en adición a los atributos y métodos de la propia clase hija.

Veamos un ejemplo:

```swift
// La clase Persona que explicamos anteriormente
class Persona {
    let nombre: String
    let apellido: String

    init(nombre: string, apellido: String) {
        self.nombre = nombre
        self.apellido = apellido
    }

    func obtenerNombreCompleto() -> String {
        return "\(nombre) \(apellido)"
    }
}

// La clase Estudiante, "hija" de Persona
// La herencia se declara con los dos puntos.
class Estudiante: Persona {
    // Estudiante tiene un legajo en adición con los
    // atributos que hereda de Persona.
    let legajo: String

    // Un constructor al igual que en la clase Persona.
    init(nombre: String, apellido: String, legajo: String) {
        self.legajo = legajo

        // Tenemos acceso a los métodos de la clase padre
        // por medio de la palabra clave "super"
        super.init(nombre: nombre, apellido: apellido)
    }

    func obtenerDescripcion() -> String {
        return "Nombre: \(obtenerNombreCompleto()) ; Legajo: \(legajo)"
    }
}
```

### Polimorfismo

El polimorfismo es el segundo de los pilares de la programación orientada a objetos que vamos a ver, y es quizás el más complicado de comprender para los que se inician.

El polimorfismo nos dice que:

1. Si tenemos un objeto de una clase hija, ese objeto es también del tipo de la clase padre.
2. Una clase hija puede redefinir el comportamiento (los métodos) de su clase padre.
3. Cuando una función nos pide un objeto de una clase determinada, podemos pasarle un objeto de una clase hija en su lugar. Lo mismo sucede si queremos asignar un objeto de una clase hija a una variable de tipo de la clase padre.

Otra forma más sencilla de definir polimorfismo es que si llamo al método `animal.hablar()`, no sé si el animal es un `Pato`, un `Perro` o un `Gato`, lo que sí sabemos es que si el animal era un `Perro`, al hablar dirá "Guau", si el animal es un `Gato`, dirá "Miau", y si es un `Pato` dirá "Cuak!".

Veamos todo esto en un ejemplo para que quede más claro.

```swift
// Definimos algunas clases (esto se llama jerarquía de clases)

class Persona {
    let nombre: String
    init(nombre: String) { self.nombre = nombre }
    func describir() -> String {
        return "\(nombre)"
    }
}

class Estudiante: Persona {
    let legajo: String
    init(nombre: String, legajo: String) { 
        self.legajo = legajo 
        super.init(nombre: nombre)
    }
    // La palabra clave "override" 
    // indica que estamos "sobreescribiendo" este método.
    // Lo que significa que vamos a redefinir la
    // funcionalidad que le habíamos dado en
    // la clase padre.
    override func describir() -> String {
        return "\(super.describir()) ; legajo: \(legajo)"
    }
}

class Empleado: Persona {
    let salario: Double
    init(nombre: String, salario: Double) { 
        self.salario = salario    
        super.init(nombre: nombre)
    }
    override func describir() -> String {
        return "\(super.describir()) ; salario: \(salario)"
    }
}

// A la función "presentar" podemos enviarle cualquier
// tipo de Persona, ya sea un objeto de tipo Persona,
// o un objeto de tipo Estudiante, o un objeto de tipo
// Empleado.
func presentar(a persona: Persona) {
    print("Les presento a \(persona.describir())")
}

let marcelo = Persona(nombre: "Marcelo")
presentar(a: marcelo) // Les presento a Marcelo

let juan = Estudiante(nombre: "Juan", legajo: "123")
presentar(a: juan) // Les presento a Juan ; Legajo: 123
// En este último caso hemos aplicado polimorfismo.
// El comportamiento cambia a partir de la herencia.
```

### Encapsulamiento

El encapsulamiento es el último de los pilares de la programación orientada a objetos que veremos, y quizás el más sencillo de comprender. Se basa en solo permitir el acceso a determinados atributos y métodos para ser llamados desde fuera de la clase que los define.

Para esto usamos los modificadores de acceso de Swift que son:

- **private**: una variable, función o clase privada no puede ser accedida desde fuera de su alcance. Es el modificador de acceso más restrictivo.
- **fileprivate**: una variable o función fileprivate (no aplica a clases), fileprivate no puede ser accedida desde fuera del archivo en el que fue declarada.
- **internal**: una variable, función o clase internal solo puede ser accedida dentro del módulo en el que fue declarada. Es el modificador de acceso por defecto, es decir que de no especificar nada, toda variable, función a clase que declaremos será internal.
- **public**: una variable, función o clase public puede ser accedida desde cualquier otro lugar del código sin restricción.
- **open**: una variable, función o clase public puede ser accedida desde cualquier otro lugar del código sin restricción, y además, si una clase es open, otra clase puede heredar de ella desde otro módulo, y si una función perteneciente a una clase es open, puede ser sobreescrita (override) desde cualquier otro módulo.

Todo esto es un poco confuso puesto de este modo, pero es en realidad muy sencillo de comprender (salvo la parte de los módulos, que pueden ignorar por este curso).

Pasándolo a un ejemplo:

```swift
class Persona {
    private let nombre: String
    let apellido: String

    init(nombre: String, apellido: String) {
        self.nombre = nombre
        self.apellido = apellido
    }
}

let juan = Persona(nombre: "Juan", apellido: "Gomez")

print(juan.apellido) // Imprimirá "Gomez". Es internal.
print(juan.nombre) // ERROR! nombre es private.
```

### Protocolos

Un protocolo es un "contrato" que define requisitos con los que una clase que "implementa" el protocolo debe cumplir. Es lo que en otros lenguajes de programación se llama interface. En la práctica, consiste en una lista de funciones.

```swift
// Un protocolo Hablador define la lista
// de funciones que tiene que implementar una clase para 
// ser un "Hablador", en el caso de este ejemplo, simplemente
// una función que se llame "hablar".
protocol Hablador {
    func hablar() -> String
}

// Declarar que una clase implementa un protocolo
// es igual que declarar una herencia
class Persona: Hablador {
    // Debemos cumplir con lo que especifica el protocolo.
    func hablar() -> String {
        return "Hola!"
    }
}

class Perro: Hablador {
    func hablar() -> String {
        return "Guau!"
    }
}
```

Los protocolos son una excelente manera de implementar el polimorfismo

```swift
func imprimirSonido(de hablador: Hablador) {
    print(hablador.hablar())
}

let persona = Persona()
let perro = Perro()

imprimirSonido(de: persona) // Hola!
imprimirSonido(de: perro) // Guau!
```