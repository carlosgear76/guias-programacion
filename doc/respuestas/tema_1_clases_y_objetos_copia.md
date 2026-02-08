<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Clases y Objetos". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: ninguno.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->

# TEMA 1. Clases y objetos

## 1. ¿Cuáles son las cuatro características básicas de la programación orientada a objetos? Describe brevemente cada una

### Respuesta
Las cuatro características básicas de la Programación Orientada a Objetos (POO) son:

Encapsulación
Agrupa los datos y métodos dentro de una clase y oculta la información interna, permitiendo acceder a ella solo de forma controlada. Mejora la seguridad y el mantenimiento del código.

Abstracción
Permite representar solo los aspectos esenciales de un objeto, ocultando los detalles de implementación. Facilita trabajar con conceptos generales mediante interfaces o clases abstractas.

Herencia
Posibilita que una clase herede atributos y métodos de otra, reutilizando código y estableciendo jerarquías entre clases.

Polimorfismo
Permite que un mismo método se comporte de distintas formas según el objeto que lo implemente, haciendo el código más flexible y extensible.


## 2. Cita cuatro lenguajes populares que permitan la programación orientada a objetos

### Respuesta
Cuatro lenguajes populares que permiten la programación orientada a objetos son:

Java

C++

Python

C#

Todos ellos soportan los principios básicos de la POO, aunque con enfoques y niveles de rigidez diferentes.

## 3. Los paradigmas anteriores a la POO, ¿Qué es la **programación estructurada**? y, todavía mejor, ¿Qué es la **programación modular**?

### Respuesta
Antes de la POO, los paradigmas más relevantes fueron estos:

Programación estructurada
Es un paradigma que organiza los programas usando estructuras de control claras (secuencia, selección y repetición), evitando saltos incontrolados como goto. Su objetivo es mejorar la claridad, legibilidad y corrección del código.

Programación modular
Es una evolución de la estructurada que consiste en dividir el programa en módulos independientes, cada uno con una función concreta. Cada módulo puede ocultar su implementación interna y exponer solo una interfaz, lo que facilita el mantenimiento, la reutilización y el trabajo en equipo.

Ambas sentaron las bases conceptuales sobre las que luego se desarrolló la programación orientada a objetos.

## 4. ¿Qué tres elementos definen a un objeto en programación orientada a objetos?

### Respuesta
En programación orientada a objetos, un objeto se define por tres elementos fundamentales:

Atributos: representan el estado del objeto (sus datos).

Métodos: definen su comportamiento (las acciones que puede realizar).

Identidad: lo distingue de otros objetos, incluso si tienen los mismos atributos y métodos.

En resumen: estado, comportamiento e identidad.

## 5. ¿Qué es una clase? ¿Es lo mismo que un objeto? ¿Qué es una instancia? ¿Todos los lenguajes orientados a objetos manejan el concepto de clase?

### Respuesta
¿Qué es una clase?
Una clase es una plantilla o molde que define las características y comportamientos (atributos y métodos) que tendrán los objetos.

¿Es lo mismo que un objeto?
No. Un objeto es una entidad concreta creada a partir de una clase. La clase es la definición; el objeto es el resultado.

¿Qué es una instancia?
Una instancia es un objeto creado a partir de una clase. Decir que un objeto es una instancia de una clase significa que fue generado siguiendo su definición.

¿Todos los lenguajes orientados a objetos manejan el concepto de clase?
No. La mayoría sí (Java, C++, C#), pero existen lenguajes orientados a objetos basados en prototipos, como JavaScript, donde no se usan clases tradicionales (aunque hoy exista sintaxis de class, el modelo interno sigue siendo prototípico).


## 6. ¿Dónde se almacenan en memoria los objetos? ¿Es igual en todos los lenguajes? ¿Qué es la **recolección de basura**? 

### Respuesta
¿Dónde se almacenan en memoria los objetos?
Normalmente, los objetos se almacenan en el heap (montón) de memoria. El heap permite crear y destruir objetos dinámicamente durante la ejecución del programa.

¿Es igual en todos los lenguajes?
No. El modelo de memoria depende del lenguaje:

En Java, C# y Python, los objetos se crean en el heap y su gestión es automática.

En C++, los objetos pueden estar en el stack, en el heap o incluso en memoria estática, y la gestión suele ser manual.

En lenguajes con máquinas virtuales, la ubicación y gestión está controlada por el runtime.

¿Qué es la recolección de basura (garbage collection)?
Es un mecanismo automático de gestión de memoria que detecta objetos que ya no tienen referencias y libera la memoria que ocupan.
Su objetivo es evitar fugas de memoria y simplificar el trabajo del programador.

## 7. ¿Qué es un método? ¿Qué es la **sobrecarga de métodos**? 

### Respuesta
¿Qué es un método?
Un método es una función asociada a una clase u objeto que define su comportamiento. Permite realizar acciones, operar sobre los atributos del objeto y representar lo que el objeto “sabe hacer”.

¿Qué es la sobrecarga de métodos?
La sobrecarga de métodos consiste en definir varios métodos con el mismo nombre dentro de una clase, pero con distinta lista de parámetros (número, tipo u orden). El lenguaje decide cuál ejecutar según los argumentos usados en la llamada.


## 8. Ejemplo mínimo de clase en Java, que se llame Punto, con dos atributos, x e y, con un método que se llame `calculaDistanciaAOrigen`, que calcule la distancia a la posición 0,0. Por sencillez, los atributos deben tener visibilidad por defecto. Crea además un ejemplo de uso con una instancia y uso del método

### Respuesta
// Definición de la clase Punto
class Punto {
    // Atributos con visibilidad por defecto (package-private)
    double x;
    double y;
    
    // Constructor por defecto
    Punto() {
        this.x = 0.0;
        this.y = 0.0;
    }
    
    // Constructor con parámetros
    Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    // Método que calcula la distancia al origen (0,0)
    double calculaDistanciaAOrigen() {
        // Usamos el teorema de Pitágoras: √(x² + y²)
        return Math.sqrt(this.x * this.x + this.y * this.y);
    }
}

// Ejemplo de uso
public class Main {
    public static void main(String[] args) {
        // Crear una instancia de Punto con coordenadas (3, 4)
        Punto miPunto = new Punto(3.0, 4.0);
        
        // Acceder a los atributos (visibilidad por defecto permite acceso desde el mismo paquete)
        System.out.println("Coordenadas del punto:");
        System.out.println("x = " + miPunto.x);
        System.out.println("y = " + miPunto.y);
        
        // Llamar al método calculaDistanciaAOrigen
        double distancia = miPunto.calculaDistanciaAOrigen();
        System.out.println("Distancia al origen: " + distancia);
        
        // Comprobación: √(3² + 4²) = √(9 + 16) = √25 = 5.0
        System.out.println("(Comprobación: 3² + 4² = 25, √25 = 5.0)");
        
        // Otro ejemplo con diferentes coordenadas
        Punto otroPunto = new Punto(1.5, 2.5);
        System.out.println("\nOtro punto en (1.5, 2.5):");
        System.out.println("Distancia al origen: " + otroPunto.calculaDistanciaAOrigen());
    }
}


## 9. ¿Cuál es el punto de entrada en un programa en Java? ¿Qué es `static` y para qué vale? ¿Sólo se emplea para ese método `main`? ¿Para qué se combina con `final`?

### Respuesta
Punto de entrada en Java
Es el método public static void main(String[] args)

La JVM lo busca automáticamente para iniciar el programa

¿Qué es static?
Indica que algo pertenece a la clase, no a instancias individuales

Variables estáticas: Compartidas por todos los objetos de la clase

Métodos estáticos: Se pueden usar sin crear objetos (Clase.metodo())

¿Solo para el main? NO
Métodos de utilidad: Math.sqrt(), Collections.sort()

Constantes: static final combinado

Variables compartidas: Contadores, configuraciones globales

Bloques de inicialización: Código que se ejecuta al cargar la clase

static final combinado
Crea CONSTANTES (inmutables y compartidas)

Ejemplo: public static final double PI = 3.141592;

Convención: nombre en MAYÚSCULAS (MAX_USUARIOS, COLOR_ROJO)

En resumen
static = "de la clase" (compartido)

final = "inmutable" (constante)

static final = constante global de la clase

main es estático porque la JVM no crea objetos antes de ejecutar

## 10. Intenta ejecutar un poco de Java de forma básica, con los comandos `javac` y `java`. ¿Cómo podemos compilar el programa y ejecutarlo desde linea de comandos? ¿Java es compilado? ¿Qué es la **máquina virtual**? ¿Qué es el *byte-code* y los ficheros `.class`?

### Respuesta
# 1. Crear archivo .java
# 2. COMPILAR (genera .class):
javac Programa.java

# 3. EJECUTAR:
java Programa

java es complicado, pero en dos pasos:

.java → COMPILA javac → .class (bytecode) → EJECUTA java/JVM → Código máquina
       (tu PC)              (bytecode)            (máquina virtual)       (CPU)

       ¿Qué es la Máquina Virtual (JVM)?
Programa que simula una computadora

Ejecuta bytecode Java en cualquier sistema

"Write once, run anywhere" (Portabilidad total)

¿Qué es bytecode y .class?
Bytecode: Código intermedio (no para humanos, sí para JVM)

.class: Archivo con bytecode (resultado de javac)

NO es código máquina nativo, la JVM lo traduce

## 11. En el código anterior de la clase `Punto` ¿Qué es `new`? ¿Qué es un **constructor**? Pon un ejemplo de constructor en una clase `Empleado` que tenga DNI, nombre y apellidos

### Respuesta
¿Qué es new?
Operador que crea objetos en memoria:

java
Empleado emp = new Empleado();
//     ↑           ↑
//  variable    crea objeto real
 ¿Qué es un constructor?
Método especial que inicializa el objeto al crearlo:

Reglas básicas:
Mismo nombre que la clase

Sin tipo de retorno

Se ejecuta automáticamente con new

 Ejemplo Clase Empleado
java
public class Empleado {
    private String dni;
    private String nombre;
    private String apellidos;
    
    // CONSTRUCTOR POR DEFECTO
    public Empleado() {
        this.dni = "00000000X";
        this.nombre = "Sin nombre";
        this.apellidos = "Sin apellidos";
    }
    
    // CONSTRUCTOR CON PARÁMETROS
    public Empleado(String dni, String nombre, String apellidos) {
        this.dni = dni;           // this.dni = atributo
        this.nombre = nombre;     // nombre = parámetro
        this.apellidos = apellidos;
    }
    
    // CONSTRUCTOR COMPLETO
    public Empleado(String dni, String nombre, String apellidos, double salario) {
        this(dni, nombre, apellidos);  // Llama a otro constructor
        // this.salario = salario;     // Si tuviera salario
    }
}
 Ejemplo de uso
java
public class Main {
    public static void main(String[] args) {
        // Diferentes formas de usar new:
        
        // 1. Constructor por defecto
        Empleado emp1 = new Empleado();
        
        // 2. Constructor con parámetros
        Empleado emp2 = new Empleado("12345678A", "Ana", "García");
        
        // 3. Constructor completo
        Empleado emp3 = new Empleado("87654321B", "Carlos", "López", 2500.0);
    }
}

## 12. ¿Qué es la referencia `this`? ¿Se llama igual en todos los lenguajes? Pon un ejemplo del uso de `this` en la clase `Punto`

### Respuesta
¿Qué es this?
Referencia al objeto actual dentro de una clase.

 Usos principales en Java:
1. Diferenciar atributos de parámetros
java
public Punto(double x, double y) {
    this.x = x;  // this.x = atributo, x = parámetro
    this.y = y;
}
2. Llamar a otro constructor
java
public Punto() {
    this(0, 0);  // Llama al constructor con parámetros
}
3. Devolver el objeto actual
java
public Punto setX(double x) {
    this.x = x;
    return this;  // Para encadenar: p.setX(1).setY(2)
}
 ¿Igual en todos los lenguajes?
NO:

Lenguaje	Keyword	Ejemplo
Java/C++/C#	this	this.x = x
Python	self	self.x = x
PHP	$this	$this->x = $x
JavaScript	this	this.x = x
 Ejemplo en clase Punto:
java
public class Punto {
    private double x, y;
    
    // Constructor con this
    public Punto(double x, double y) {
        this.x = x;  // Necesario aquí
        this.y = y;
    }
    
    // Método que usa this
    public double distanciaA(Punto otro) {
        // this.x accede a este objeto
        // otro.x accede al objeto parámetro
        double dx = this.x - otro.x;
        double dy = this.y - otro.y;
        return Math.sqrt(dx*dx + dy*dy);
    }
    
    // Encadenamiento
    public Punto mover(double dx, double dy) {
        this.x += dx;
        this.y += dy;
        return this;  // Devuelve este mismo objeto
    }
}


## 13. Añade ahora otro nuevo método que se llame `distanciaA`, que reciba un `Punto` como parámetro y calcule la distancia entre `this` y el punto proporcionado

### Respuesta
Método distanciaA para clase Punto
Código del método:

public class Punto {
    private double x, y;
    
    // Constructor
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }
    
    // NUEVO MÉTODO: distancia entre este punto y otro
    public double distanciaA(Punto otro) {
        double dx = this.x - otro.x;   // this = punto actual
        double dy = this.y - otro.y;   // otro = punto recibido
        return Math.sqrt(dx * dx + dy * dy);
    }
    
    // Método existente (ahora puede usar distanciaA)
    public double calculaDistanciaAOrigen() {
        return this.distanciaA(new Punto(0, 0));
    }
}
 Ejemplo de uso:

public class Main {
    public static void main(String[] args) {
        // Crear dos puntos
        Punto p1 = new Punto(3, 4);   // (3,4)
        Punto p2 = new Punto(7, 1);   // (7,1)
        
        // Calcular distancia entre ellos
        double distancia = p1.distanciaA(p2);
        
        System.out.println("Distancia entre " + 
                           "(" + p1.getX() + "," + p1.getY() + ") y " +
                           "(" + p2.getX() + "," + p2.getY() + ") = " + 
                           distancia);
        
        // Cálculo manual para verificar:
        // √[(7-3)² + (1-4)²] = √[4² + (-3)²] = √[16+9] = √25 = 5
        System.out.println("(Verificación: √[(7-3)²+(1-4)²] = √[16+9] = √25 = 5)");
    }
}
Resultado:

Distancia entre (3.0,4.0) y (7.0,1.0) = 5.0
(Verificación: √[(7-3)²+(1-4)²] = √[16+9] = √25 = 5)


## 14. El paso del `Punto` como parámetro a un método, es **por copia** o **por referencia**, es decir, si se cambia el valor de algún atributo del punto pasado como parámetro, dichos cambios afectan al objeto fuera del método? ¿Qué ocurre si en vez de un `Punto`, se recibiese un entero (`int`) y dicho entero se modificase dentro de la función? 

### Respuesta


## 15. ¿Qué es el método `toString()` en Java? ¿Existe en otros lenguajes? Pon un ejemplo de `toString()` en la clase `Punto` en Java

### Respuesta
toString()
¿Qué es?
Método que convierte objeto a String. Se llama automáticamente.

java
Punto p = new Punto(3, 4);
System.out.println(p);  // Implícitamente: p.toString()
¿En otros lenguajes?
SÍ:

Python: __str__()

C#: ToString()

JavaScript: toString()

PHP: __toString()

Ruby: to_s

Ejemplo en clase Punto:

public class Punto {
    private double x, y;
    
    @Override
    public String toString() {
        return "(" + x + ", " + y + ")";
    }
}
Uso:

Punto p = new Punto(3.5, 4.2);
System.out.println(p);           // "(3.5, 4.2)"
String texto = "Punto: " + p;    // "Punto: (3.5, 4.2)"


## 16. Reflexiona: ¿una clase es como un `struct` en C? ¿Qué le falta al `struct` para ser como una clase y las variables de ese tipo ser instancias?


### Respuesta


## 17. Quitemos un poco de magia a todo esto: ¿Como se podría “emular”, con `struct` en C, la clase `Punto`, con su función para calcular la distancia al origen? ¿Qué ha pasado con `this`?

### Respuesta
