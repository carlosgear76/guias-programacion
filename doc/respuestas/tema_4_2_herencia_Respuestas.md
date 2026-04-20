<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Herencia". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación, Excepciones y Composición.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# Tema 4.2. Herencia

## 1. En orientación a objetos, ¿qué es la **herencia** y su relación con "A es-un B"?. Explica las dos implicaciones principales: (1) **compatibilidad de tipos** y (2) **herencia de estado y comportamiento**. Pon un ejemplo en Java muy sencillo, donde un `Soldado` tiene un `nombre` (privado) y un método `saludar()` que muestra su nombre. Hay dos subtipos: un `Artillero`, que es capaz de disparar cohetes y un `Zapador` que pone minas, ambos heredan el atributo nombre y la capacidad de saludar. Además, y de forma específica, el artillero tiene un número de cohetes y el zapador un número de minas, accesibles mediante "getters" específicos. Respecto a la compatibilidad de tipos, aprovechémosla: crea un array de `Soldado`, mete varios de distinto tipo (son todos compatibles con `Soldado`). Recórrela y que todos te saluden.

### Respuesta


## 2. Al crear los soldados concretos, ¿cuántos constructores se ejecutan y en qué orden? ¿Qué significa `super` dentro de un constructor? Si la clase base no tiene visible el constructor sin parámetros, ¿debo llamar a `super` siempre? 

### Respuesta

## 3. Respecto a los objetos de subclases en memoria, los atributos privados de la superclase, ¿forman parte de una instancia de la subclase en memoria? En caso afirmativo ¿implica que se puedan usar desde el código de la subclase? Explícalo con el ejemplo de `Soldado` y alguna de sus subclases.

### Respuesta

## 4. ¿Qué implica en términos de **extensibilidad** de código el hecho de que sean compatibles a nivel de tipos? Ilustra esto añadiendo un nuevo tipo de `Soldado` y demostrando que el código para pedir el saludo a todos los soldados no se modifica.

### Respuesta


## 5. En Java, cuando trabajo con referencias y herencia. ¿Puedo tener una referencia del supertipo que apunte a objetos reales de un subtipo? ¿Puedo invocar con la referencia del supertipo a métodos públicos del subtipo? ¿En qué consiste el **"upcasting"** y el **"downcasting"**? ¿Qué es el `instanceof`? Pon un ejemplo de recorrido de un array de `Soldado`, comprobando que, si el objeto real es un `Artillero`, solicite el número de cohetes que tiene y los imprima.

### Respuesta


## 6. Respecto a la ocultación de información y herencia, ¿qué significa acceso **"protegido"** de métodos y/o atributos? ¿Cómo se implementa en Java? Pon un ejemplo de uso de en la clase `Soldado` para que su nombre sea protegido y pueda usarse en el método de poner bombas del `Zapador`.

### Respuesta


## 7. En los lenguajes orientados a objetos ¿hay una **clase base** para todos los objetos? ¿Ocurre en todos los lenguajes? ¿Qué ocurre en Java?

### Respuesta


## 8. ¿Qué es la **"herencia múltiple"**? ¿Existe en Java herencia múltiple?

### Respuesta


## 9. Las excepciones en los lenguajes orientados a objetos son objetos. Por tanto, se pueden crear excepciones personalizadas. Pon un ejemplo en Java de una excepción personalizada (`UsuarioNoEncontradoException`), que sea *no controlada* y que además este compuesto con un `Usuario`, para saber qué `Usuario` dio el problema. Permite además que se pueda incluir la causa, es decir, sobrecarga el constructor para tener una versión que permita añadir la causa subyacente. 

### Respuesta


## 10. Herencia vs. Composición. Se dice que no se debe emplear herencia simplemente por reutilizar código, es decir, que si quiero reutilizar código simplemente, no debo pensar en herencia como primera opción ¿por qué?

### Respuesta


## 11. Herencia vs. Composición. Se dice que se debe *"favorecer la composición frente a la herencia"*, ¿por qué?

### Respuesta


## 12. Herencia vs. Composición. Se dice que la *"herencia rompe la encapsulación"*, ¿a qué se refiere esto?

### Respuesta


## 13. Pongamos un ejemplo de dos alternativas para lo mismo. Tenemos un `Estudiante` y un `Trabajador`, ambos tienen datos en común: el DNI y el nombre. Modelemos esto de dos formas: uno por herencia, con una superclase `Persona`, y otro con composición, con una clase `DatosPersonales`. Se debe recibir una instancia de `DatosPersonales` en el constructor de la clase `Estudiante` y `Trabajador`.

### Respuesta
1. Herencia: definición, relación "es-un", compatibilidad y herencia de estado y comportamiento
La herencia permite definir una nueva clase (subclase) a partir de una clase existente (superclase), estableciendo una relación "A es-un B". Esto tiene dos implicaciones principales: (1) compatibilidad de tipos: una instancia de la subclase puede ser tratada como una instancia de la superclase; (2) herencia de estado y comportamiento: la subclase automáticamente posee los atributos y métodos de la superclase (salvo los privados). En el ejemplo, Artillero y Zapador heredan de Soldado el atributo nombre y el método saludar(). Gracias a la compatibilidad, un array de tipo Soldado puede contener objetos de ambas subclases, y al recorrerlo se puede invocar saludar() sin conocer el tipo concreto.

java
public class Soldado {
    private String nombre;
    public Soldado(String nombre) { this.nombre = nombre; }
    public void saludar() { System.out.println("Soy " + nombre); }
}
public class Artillero extends Soldado {
    private int cohetes;
    public Artillero(String nombre, int cohetes) { super(nombre); this.cohetes = cohetes; }
    public int getCohetes() { return cohetes; }
}
public class Zapador extends Soldado {
    private int minas;
    public Zapador(String nombre, int minas) { super(nombre); this.minas = minas; }
    public int getMinas() { return minas; }
}
// Uso:
Soldado[] ejercito = { new Artillero("Juan", 5), new Zapador("Ana", 3) };
for (Soldado s : ejercito) s.saludar();
2. Orden de ejecución de constructores y uso de super
Al crear una instancia de una subclase, primero se ejecuta el constructor de la superclase (explícita o implícitamente) y luego el de la subclase. Dentro de un constructor, super(...) llama a un constructor concreto de la superclase y debe ser la primera instrucción. Si la superclase no tiene un constructor sin parámetros visible, la subclase debe llamar explícitamente a super con los parámetros adecuados; de lo contrario, el compilador intentaría insertar super() y fallaría.

3. Atributos privados de la superclase en la memoria de la subclase
Los atributos privados de la superclase sí forman parte de la memoria de la instancia de la subclase, pero no son accesibles directamente desde el código de la subclase porque la encapsulación los oculta. En el ejemplo, un objeto Artillero contiene internamente el campo nombre heredado de Soldado, pero no puede acceder a él directamente (solo mediante métodos públicos o protegidos de Soldado). Esto garantiza que la superclase controle cómo se manipulan sus propios datos.

4. Extensibilidad gracias a la compatibilidad de tipos
La compatibilidad de tipos permite añadir nuevos subtipos sin modificar el código que opera sobre el supertipo. Por ejemplo, si se crea una nueva clase Francotirador que extiende Soldado, el mismo bucle for (Soldado s : ejercito) s.saludar(); sigue funcionando sin cambios. Esto hace que el sistema sea fácilmente extensible: se pueden agregar comportamientos especializados sin afectar el código cliente que depende únicamente de la interfaz común de Soldado.

5. Referencias de supertipo, upcasting, downcasting e instanceof
En Java, una referencia del supertipo puede apuntar a un objeto de un subtipo (upcasting implícito). Con esa referencia solo se pueden invocar métodos declarados en el supertipo, no los específicos del subtipo. Para invocar métodos específicos se necesita downcasting (conversión explícita), que debe ir precedido de una comprobación con instanceof para evitar ClassCastException. En el ejemplo, al recorrer el array de Soldado, se usa instanceof para detectar artilleros y luego se hace downcasting para obtener el número de cohetes.

java
for (Soldado s : ejercito) {
    s.saludar();
    if (s instanceof Artillero) {
        Artillero a = (Artillero) s;
        System.out.println("Cohetes: " + a.getCohetes());
    }
}
6. Acceso protegido (protected) en herencia
El modificador protected permite que un miembro (atributo o método) sea accesible desde las subclases (incluso si están en paquetes diferentes) y desde clases del mismo paquete, pero no desde cualquier otra clase. En Java se declara con protected. Por ejemplo, si en Soldado se declara protected String nombre;, la subclase Zapador podría acceder directamente a nombre en su método ponerMina(). Sin embargo, sigue siendo recomendable usar private con getters protegidos o públicos para mantener un mejor control.

java
public class Soldado {
    protected String nombre;
    public Soldado(String nombre) { this.nombre = nombre; }
}
public class Zapador extends Soldado {
    public void ponerMina() { System.out.println(nombre + " pone una mina"); }
}
7. Clase base universal en lenguajes orientados a objetos
No todos los lenguajes orientados a objetos tienen una clase base única. Por ejemplo, C++ no tiene una clase raíz común. En Java, toda clase extiende implícitamente Object si no se especifica otra superclase. Object proporciona métodos básicos como toString(), equals() y hashCode(). Esto permite tratar cualquier objeto como Object y facilita la creación de colecciones genéricas (antes de los genéricos).

8. Herencia múltiple en Java
La herencia múltiple permite que una clase herede de más de una superclase. Java no permite herencia múltiple de clases para evitar problemas como el "diamante" (ambigüedad cuando dos superclases tienen métodos con la misma firma). En su lugar, Java ofrece herencia múltiple de interfaces (una clase puede implementar varias interfaces) y, desde Java 8, métodos default en interfaces, lo que proporciona parte de la flexibilidad sin los conflictos de estado.

9. Excepción personalizada no controlada con composición
Una excepción personalizada puede ser no controlada (unchecked) extendiendo RuntimeException. Se puede componer con un objeto Usuario para almacenar información adicional. También se puede sobrecargar el constructor para aceptar una causa (otra excepción) mediante super(causa).

java
public class UsuarioNoEncontradoException extends RuntimeException {
    private final Usuario usuario;
    public UsuarioNoEncontradoException(Usuario usuario) {
        super("Usuario no encontrado: " + usuario);
        this.usuario = usuario;
    }
    public UsuarioNoEncontradoException(Usuario usuario, Throwable causa) {
        super("Usuario no encontrado: " + usuario, causa);
        this.usuario = usuario;
    }
    public Usuario getUsuario() { return usuario; }
}
10. Por qué no se debe usar herencia solo para reutilizar código
La herencia crea un acoplamiento fuerte entre la subclase y la superclase. Si solo se busca reutilizar código, la composición suele ser más adecuada porque permite delegar comportamiento sin atar las jerarquías de tipos. La herencia debe reflejar una verdadera relación "es-un" conceptual, no simplemente compartir implementación. Usarla solo por reutilización puede llevar a jerarquías artificiales y frágiles, donde cambios en la superclase afectan involuntariamente a todas las subclases.

11. Favorecer la composición frente a la herencia
La composición ofrece mayor flexibilidad y menor acoplamiento. Con composición, una clase puede cambiar su comportamiento en tiempo de ejecución (por ejemplo, cambiando la referencia al objeto compuesto), mientras que la herencia es estática. Además, la composición respeta mejor la encapsulación porque no expone los detalles internos de la clase usada. La herencia, por el contrario, expone la interfaz de la superclase y a menudo requiere conocer su implementación para extenderla correctamente.

12. La herencia rompe la encapsulación
Decir que "la herencia rompe la encapsulación" significa que una subclase depende de los detalles internos de la superclase para funcionar correctamente. Si la superclase cambia su implementación (por ejemplo, modifica un método que la subclase sobrescribe o usa atributos protegidos), la subclase puede dejar de funcionar. En cambio, la composición solo depende de la interfaz pública del objeto compuesto, lo que aísla mejor los cambios. Por esta razón, se recomienda diseñar clases base pensando explícitamente en la herencia (documentando qué métodos son sobrescribibles) o, preferiblemente, usar composición.

13. Modelado alternativo: herencia vs. composición
Por herencia:

java
public class Persona {
    private String dni, nombre;
    public Persona(String dni, String nombre) { this.dni = dni; this.nombre = nombre; }
}
public class Estudiante extends Persona {
    public Estudiante(String dni, String nombre) { super(dni, nombre); }
}
public class Trabajador extends Persona {
    public Trabajador(String dni, String nombre) { super(dni, nombre); }
}
Por composición:

java
public class DatosPersonales {
    private String dni, nombre;
    public DatosPersonales(String dni, String nombre) { this.dni = dni; this.nombre = nombre; }
}
public class Estudiante {
    private DatosPersonales datos;
    public Estudiante(DatosPersonales datos) { this.datos = datos; }
}
public class Trabajador {
    private DatosPersonales datos;
    public Trabajador(DatosPersonales datos) { this.datos = datos; }
}
La composición permite reutilizar DatosPersonales sin crear una jerarquía rígida, facilitando que un mismo Estudiante pueda también ser Trabajador (algo imposible con herencia simple). Además, los cambios en DatosPersonales no afectan a las clases que lo usan más allá de su interfaz pública.

