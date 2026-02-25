<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Encapsulación". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 2. Encapsulación

## 1. En Programación Orientada a Objetos (POO), ¿Qué buscan la **encapsulación** y **la ocultación** de información? Enumera brevemente algunas ventajas de la ocultación de información.

### Respuesta:
La Encapsulación tiene que ver con la Protección de los objetos en el algoritmo.
-Usandola se evitan los estados no validos de los objetos.
-Tambien evita dependencias desde fuera que no se desean.

-Ocultación de información: Restringir el acceso directo a los datos internos de un objeto, permitiendo interactuar con ellos solo mediante métodos públicos.


Ventajas de la ocultación de información

-Mayor seguridad: Evita modificaciones indebidas de los datos.

-Control del acceso: Permite validar datos antes de cambiarlos.

-Menor acoplamiento: Reduce la dependencia entre clases.

-Facilita el mantenimiento: Se pueden cambiar detalles internos sin afectar el código externo.

-Mejor organización: Separa claramente qué es público y qué es interno.

## 2. ¿Qué se entiende por la **interfaz pública** de un objeto o clase en POO? Describe brevemente cómo se relaciona con la ocultación de información.

### Respuesta:
La Interfaz publica se entiende como los miembos de un algotitmo que se ven desde afuera osea es el conjunto de métodos y atributos accesibles desde fuera de la clase.
Es decir, define qué puede hacer el objeto y cómo otros objetos pueden interactuar con él.

Relación con la ocultación de información

La interfaz pública:

Expone solo lo necesario.

Oculta los detalles internos de implementación.

Permite interactuar con el objeto sin conocer cómo funciona por dentro.


## 3. Brevemente: ¿Por qué hay que ser conscientes y diseñar con cuidado la **interfaz pública** de una clase? ¿Es fácil cambiarla?

### Respuesta:
¿Por qué diseñar con cuidado la interfaz pública?

Porque la interfaz pública es el contrato que la clase ofrece al resto del programa.
Todo el código que la usa depende de ella.
Si se diseña mal:

Puede exponer demasiado.

Puede limitar futuras mejoras.

Puede generar dependencias innecesarias.
¿Es fácil cambiarla?

X No.
Cambiar la interfaz pública puede romper el código que ya la utiliza.

## 4. ¿Qué son las **invariantes de clase** y por qué la ocultación de información nos ayuda?

### Respuesta:
Son condiciones o reglas que siempre deben cumplirse para que un objeto esté en un estado válido.
Deben mantenerse verdaderas antes y después de ejecutar cualquier método público.


## 5. Pon un ejemplo de una clase `Punto` en `Java`, con dos coordenadas, `x` e `y`, de tipo `double`, con un método `calcularDistanciaAOrigen`, y que haga uso de la ocultación de información. ¿Cuál es la interfaz pública de la clase `Punto`? ¿Qué significa `public` y `private`?

### Respuesta:
Ejemplo de clase Punto:

public class Punto {

    // Atributos privados (ocultación de información)
    private double x;
    private double y;

    // Constructor
    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    // Getters (acceso controlado)
    public double getX() {
        return x;
    }

    public double getY() {
        return y;
    }

    // Método público para calcular la distancia al origen (0,0)
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(x * x + y * y);
    }
}

La interfaz pública es el conjunto de elementos accesibles desde fuera de la clase.

En este caso, la interfaz pública es:

public Punto(double x, double y)
public double getX()
public double getY()
public double calcularDistanciaAOrigen()

## 6. En Java, ¿A quiénes se pueden aplicar los modificadores `public` o `private`?

### Respuesta:
En Java, los modificadores public y private se pueden aplicar a distintos elementos del programa:

 1. Clases

public → La clase es accesible desde cualquier otro paquete.

private → No se puede usar en clases de nivel superior (solo en clases internas).

2. Atributos (variables de instancia)

public → Accesibles desde cualquier clase.

private → Solo accesibles dentro de su propia clase.

3. Métodos

public → Se pueden invocar desde cualquier clase.

private → Solo se pueden usar dentro de la misma clase.

 4. Constructores

public → Permiten crear objetos desde cualquier clase.

private → Impiden crear objetos desde fuera (por ejemplo, en el patrón Singleton).

## 7. En POO, la visibilidad puede ser pública o privada, pero ¿existen más tipos de visibilidad? ¿Qué ocurre en Java? ¿Y en otros lenguajes?

### Respuesta:
Sí. En POO no solo existen public y private. La mayoría de lenguajes orientados a objetos incluyen niveles intermedios de visibilidad.

 En Java

Java tiene cuatro niveles de acceso:

public → accesible desde cualquier clase.

private → solo dentro de la propia clase.

protected → accesible dentro del mismo paquete y también por subclases (aunque estén en otro paquete).

(sin modificador) → llamado package-private (o acceso por defecto): solo accesible dentro del mismo paquete.

En otros lenguajes

Depende del lenguaje:

C++ → public, private, protected.

C# → public, private, protected, internal (visible dentro del mismo ensamblado), y combinaciones como protected internal.

Python → no tiene visibilidad estricta real; usa convenciones:

_variable → uso interno (convención).

__variable → name mangling (protección parcial).

Kotlin → public, private, protected, internal.

## 8. Responde: Los miembros de instancia privados de un objeto están ocultos para (a) otras clases o (b) otras instancias, aunque sean de la misma clase. Pon un ejemplo añadiendo un método `calcularDistanciaAPunto(Punto otro)` y explica la respuesta.

### Respuesta:
(a) otras clases
No están ocultos para otras instancias de la misma clase.
En Java, private significa “solo accesible dentro de la propia clase”, no “solo accesible por esta instancia”.
Ejemplo
public class Punto {

    private double x;
    private double y;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;
    }

    public double calcularDistanciaAPunto(Punto otro) {
        double dx = this.x - otro.x;  // ✔ Acceso permitido
        double dy = this.y - otro.y;  // ✔ Acceso permitido
        return Math.sqrt(dx * dx + dy * dy);
    }
}

Explicación

Aunque x e y son private, el método puede acceder a otro.x y otro.y porque:

El acceso ocurre dentro de la clase Punto

Todas las instancias de una misma clase pueden acceder a los miembros privados de otras instancias de esa misma clase

Lo que no podría hacerse es esto desde otra clase:

Punto p = new Punto(1,2);
System.out.println(p.x); // X Error

## 9. ¿Qué son los métodos "getter" y "setter" en los lenguajes orientados a objetos?

### Respuesta:
En programación orientada a objetos, los getter y setter son métodos usados para acceder y modificar atributos privados de una clase de forma controlada.

Forman parte del principio de encapsulación (ocultar el estado interno y exponer solo lo necesario).

 Getter:

Es un método que devuelve el valor de un atributo privado.
Permite leer el valor sin acceder directamente al atributo.

Setter:

Es un método que modifica el valor de un atributo privado.
Permite cambiar el valor de forma controlada.

## 10. Cuando nos referimos a que la ocultación de información mejora la "seguridad" del programa, ¿nos referimos a que no pueda ser "hackeado"?

### Respuesta:

No.

Cuando en POO se dice que la ocultación de información mejora la “seguridad”, no se refiere a que el programa no pueda ser hackeado.

Se refiere a seguridad interna del diseño, es decir:

Evitar que otras partes del programa modifiquen datos de forma incorrecta.

Proteger el estado interno del objeto.

Reducir errores y comportamientos inesperados.

Mantener coherencia e invariantes.

Ejemplo: si un atributo debe ser siempre positivo, hacerlo private y controlarlo con un setter evita que otra clase le asigne un valor inválido.


## 11. ¿Qué diferencia hay entre **miembro de instancia** y **miembro de clase**? ¿Los miembros de clase también se pueden ocultar?

### Respuesta:
Diferencia
1) Miembro de instancia

Pertenece a cada objeto creado.

Cada instancia tiene su propia copia.

En Java no lleva static.

2) Miembro de clase

Pertenece a la clase en sí, no a los objetos.

Es compartido por todas las instancias.

En Java se declara con static.

¿Se pueden ocultar los miembros de clase?

Sí.
Los miembros static también pueden ser:

public

private

protected

package-private

## 12. Brevemente: ¿Tiene sentido que los constructores sean privados?

### Respuesta:
Sí, tiene sentido en ciertos casos.

Un constructor private impide que se creen objetos desde fuera de la clase. Se usa, por ejemplo:

 Patrón Singleton → garantizar que solo exista una instancia.

 Clases utilitarias (solo métodos static) → evitar que alguien las instancie.

 Métodos fábrica → controlar cómo y cuándo se crean los objetos.


## 13. ¿Cómo se indican los **miembros de clase** en Java? Pon un ejemplo, en la clase `Punto` definida anteriormente, para que incluya miembros de clase que permitan saber cuáles son los valores `x` e `y` máximos que se han establecido en todos los puntos que se hayan creado hasta el momento.

### Respuesta:
¿Cómo se indican los miembros de clase en Java?

Se indican con la palabra clave static.
Eso significa que el miembro pertenece a la clase, no a cada objeto, y es compartido por todas las instancias.

Ejemplo con Punto

Añadimos dos miembros de clase para guardar los valores máximos de x e y creados hasta el momento:

public class Punto {

    private double x;
    private double y;

    // Miembros de clase (static)
    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    public Punto(double x, double y) {
        this.x = x;
        this.y = y;

        // Actualizamos los máximos
        if (x > maxX) {
            maxX = x;
        }
        if (y > maxY) {
            maxY = y;
        }
    }

    // Métodos de clase para consultar los máximos
    public static double getMaxX() {
        return maxX;
    }

    public static double getMaxY() {
        return maxY;
    }
}

## 14. Como sería un método factoría dentro de la clase `Punto` para construir un `Punto` a partir de dos coordenadas, pero que las redondee al entero más cercano. Escribe sólo el código del método, no toda la clase ¿Has usado `static`? 

### Respuesta:
public static Punto crearPuntoRedondeado(double x, double y) {
    int xRedondeado = (int) Math.round(x);
    int yRedondeado = (int) Math.round(y);
    return new Punto(xRedondeado, yRedondeado);
}

Sí, se uso usado static, porque un método factoría pertenece a la clase y debe poder invocarse sin necesidad de tener previamente un objeto Punto


## 15. Cambia la implementación de `Punto`. En vez de dos `double`, emplea un array interno de dos posiciones, intentando no modificar la interfaz pública de la clase.

### Respuesta:
public class Punto {

    // Implementación interna con un array
    private double[] coords = new double[2]; // coords[0] = x, coords[1] = y

    // Miembros de clase para máximos
    private static double maxX = Double.NEGATIVE_INFINITY;
    private static double maxY = Double.NEGATIVE_INFINITY;

    // Constructor
    public Punto(double x, double y) {
        coords[0] = x;
        coords[1] = y;

        // Actualizar máximos
        if (x > maxX) maxX = x;
        if (y > maxY) maxY = y;
    }

    // Getters
    public double getX() {
        return coords[0];
    }

    public double getY() {
        return coords[1];
    }

    // Distancia al origen
    public double calcularDistanciaAOrigen() {
        return Math.sqrt(coords[0] * coords[0] + coords[1] * coords[1]);
    }

    // Distancia a otro punto
    public double calcularDistanciaAPunto(Punto otro) {
        double dx = coords[0] - otro.coords[0];
        double dy = coords[1] - otro.coords[1];
        return Math.sqrt(dx * dx + dy * dy);
    }

    // Métodos de clase para máximos
    public static double getMaxX() { return maxX; }
    public static double getMaxY() { return maxY; }

    // Método factoría con redondeo
    public static Punto crearPuntoRedondeado(double x, double y) {
        int xRedondeado = (int) Math.round(x);
        int yRedondeado = (int) Math.round(y);
        return new Punto(xRedondeado, yRedondeado);
    }
}


## 16. Si un atributo va a tener un método "getter" y "setter" públicos, ¿no es mejor declararlo público? ¿Cuál es la convención más habitual sobre los atributos, que sean públicos o privados? ¿Tiene esto algo que ver con las "invariantes de clase"?

### Respuesta:
Si los hago publicos para garantizar la invariante de clase.


## 17. ¿Qué significa que una clase sea **inmutable**? ¿qué es un método modificador? ¿Un método modificador es siempre un "setter"? ¿Tiene ventajas que una clase sea inmutable?

### Respuesta:
Inmutable -> Su estado no cambia, un metodo modificador es cualquier metodo modificador que cambia el estado interno.
Por ejemplo: un Setter.

Ventajas de la inmutabilidad

Seguridad y consistencia: no hay riesgo de que otras partes del programa cambien los objetos inesperadamente.

Simplicidad: más fácil de razonar sobre ellos, depurar y mantener.

Hilos / concurrencia: objetos inmutables son automáticamente thread-safe (sin sincronización adicional).

Reutilización y caching: se pueden compartir sin riesgo de modificación.



## 18. ¿Es recomendable incluir métodos "setter" siempre y como convención?

### Respuesta: No, no siempre es recomendable incluir setters, y la convención actual en POO dice que no todos los atributos necesitan uno.
Por qué no siempre

Clases inmutables → no tienen setters, porque los objetos no deben cambiar tras crearse.

Preservar invariantes → un setter mal usado puede romper condiciones internas de la clase.

Encapsulación → si un atributo no necesita modificarse desde fuera, mejor no exponer un setter.

## 19. ¿La clase `String` en Java es mutable o inmutable? ¿Qué ocurre al concatenar dos cadenas? ¿Qué debemos hacer si vamos a hacer una operación que implique concatenar muchas veces para construir paso a paso una cadena muy larga?

### Respuesta: La clase String en Java es inmutable.


## 20. En POO ¿Cómo se comparan objetos de una misma clase? ¿Por su contenido o por su identidad? ¿Qué es el método equals en Java? ¿Qué hace por defecto? ¿Cómo se deben comparar dos cadenas en Java? 

### Respuesta:
En POO, la comparación de objetos depende de qué se quiere comparar: su identidad (si son el mismo objeto) o su contenido (valores internos).

Comparación por identidad

Se usa el operador == en Java.

Compara si las referencias apuntan al mismo objeto, no los valores internos.

Punto p1 = new Punto(2, 3);
Punto p2 = new Punto(2, 3);
System.out.println(p1 == p2); // false, son objetos distintos
 Comparación por contenido:

Se usa el método equals().

En Java, equals es un método de la clase Object.

Por defecto, Object.equals() hace lo mismo que == (compara identidad).

p1.equals(p2); // false si no se sobrescribe

Para comparar contenido, una clase debe sobrescribir equals() y definir qué significa que dos objetos sean “iguales”.

Comparar cadenas en Java

No usar == (compara referencias).

Usar equals() para comparar contenido:

String s1 = "hola";
String s2 = new String("hola");
System.out.println(s1.equals(s2)); // true

Para ignorar mayúsculas/minúsculas: s1.equalsIgnoreCase(s2).

## 21. ¿Qué son las clases "wrapper" en un lenguaje de programación orientado a objetos? ¿Cómo se hace? ¿Es un proceso automático? ¿Qué ventajas tienen? ¿Todos los lenguajes orientados a objetos tienen tipos primitivos y necesitan wrappers? 

### Respuesta:
Una clase wrapper (envoltorio) es una clase que encapsula un tipo primitivo para que pueda ser tratado como un objeto.

Permite usar tipos primitivos (int, double, boolean, etc.) donde se requieren objetos, por ejemplo en colecciones (ArrayList, HashMap) que solo aceptan objetos.

Cómo se hace en Java

Java tiene wrappers predefinidos:

Primitivo	 |   Wrapper
int	       |   Integer
double	   |   Double
boolean	   |   Boolean

Se puede crear un wrapper explícitamente:

int n = 5;
Integer obj = Integer.valueOf(n); // envolviendo el primitivo

O desde Java 5, con autoboxing (proceso automático):

Integer obj = n; // autoboxing automático
int m = obj;     // unboxing automático

Ventajas de los wrappers

Permiten usar primitivos como objetos → necesarios en colecciones genéricas.

Métodos útiles → los wrappers incluyen operaciones útiles, p.ej., Integer.parseInt("123").

Constantes y utilidades → por ejemplo Integer.MAX_VALUE, Boolean.TRUE.

Sobre otros lenguajes

No todos los lenguajes OO tienen tipos primitivos.

Por ejemplo:

Java sí → necesita wrappers.

Python → todo es objeto, no hay primitivos separados → no necesita wrappers.

C++ → primitivos existen y se pueden envolver en clases si se quiere, pero no obligatorio.

## 22. ¿En POO qué es un **tipo de dato enumerado**? ¿En Java, un tipo de dato enumerado es una clase? ¿Qué ventajas tienen en términos de encapsulación los enumerados en Java?

### Respuesta:
Qué es un tipo de dato enumerado

Un tipo de dato enumerado (enum) es un tipo que define un conjunto limitado y fijo de valores posibles.

Ejemplo conceptual: los días de la semana, colores, direcciones (NORTE, SUR, ESTE, OESTE).

Permite evitar valores inválidos y hacer el código más legible y seguro.

 Enumerados en Java

En Java, un enum es realmente una clase especial.

Cada valor del enum es una instancia de esa clase.

Ventajas en términos de encapsulación

Ocultan implementación interna: los valores se exponen como constantes, no se puede crear uno nuevo desde fuera.

Control del estado: cada valor del enum es inmutable y seguro.

Evita valores inválidos: no se puede asignar un valor fuera del conjunto definido.

Interfaz pública clara: métodos públicos permiten acceder a información interna sin exponer los atributos directamente.


## 23. Crea un tipo enumerado en Java que se llame `Mes`, con doce posibles instancias y que además proporcione métodos para obtener cuántos días tiene ese mes, el ordinal de ese mes en el año (1-12), empleando atributos privados y constructores del tipo enumerado.

### Respuesta:

public enum Mes {

    ENERO(31, 1),
    FEBRERO(28, 2),
    MARZO(31, 3),
    ABRIL(30, 4),
    MAYO(31, 5),
    JUNIO(30, 6),
    JULIO(31, 7),
    AGOSTO(31, 8),
    SEPTIEMBRE(30, 9),
    OCTUBRE(31, 10),
    NOVIEMBRE(30, 11),
    DICIEMBRE(31, 12);

    // Atributos en privado 
    private final int dias;
    private final int ordinalAnual;

    // Constructor privado del enum (seguridad)
    private Mes(int dias, int ordinalAnual) {
        this.dias = dias;
        this.ordinalAnual = ordinalAnual;
    }

    // Métodos públicos para poder acceder a los atributos
    public int getDias() {
        return dias;
    }

    public int getOrdinalAnual() {
        return ordinalAnual;
    }
}


## 24. Añade a la clase `Mes` del ejercicio anterior cuatro métodos para devolver si ese mes tiene algunos días de invierno, primavera, verano u otoño, indicando con un booleano el hemisferio (norte o sur, parámetro `enHemisferioNorte`). Es decir: `esDePrimavera(boolean esHemisferioNorte)`, `esDeVerano(boolean esHemisferioNorte)`, `esDeOtoño(boolean esHemisferioNorte)`, `esDeInvierno(boolean esHemisferioNorte)`

### Respuesta:

public enum Mes {

    ENERO(31, 1),
    FEBRERO(28, 2),
    MARZO(31, 3),
    ABRIL(30, 4),
    MAYO(31, 5),
    JUNIO(30, 6),
    JULIO(31, 7),
    AGOSTO(31, 8),
    SEPTIEMBRE(30, 9),
    OCTUBRE(31, 10),
    NOVIEMBRE(30, 11),
    DICIEMBRE(31, 12);

    // Atributos en privado
    private final int dias;
    private final int ordinalAnual;

    // Constructor privado del enum (seguridad)
    private Mes(int dias, int ordinalAnual) {
        this.dias = dias;
        this.ordinalAnual = ordinalAnual;
    }

    // Getters
    public int getDias() {
        return dias;
    }

    public int getOrdinalAnual() {
        return ordinalAnual;
    }

    // Métodos para devolver estaciones
    public boolean esDeInvierno(boolean esHemisferioNorte) {
        if (esHemisferioNorte) {
            return this == DICIEMBRE || this == ENERO || this == FEBRERO;
        } else {
            return this == JUNIO || this == JULIO || this == AGOSTO;
        }
    }

    public boolean esDePrimavera(boolean esHemisferioNorte) {
        if (esHemisferioNorte) {
            return this == MARZO || this == ABRIL || this == MAYO;
        } else {
            return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
        }
    }

    public boolean esDeVerano(boolean esHemisferioNorte) {
        if (esHemisferioNorte) {
            return this == JUNIO || this == JULIO || this == AGOSTO;
        } else {
            return this == DICIEMBRE || this == ENERO || this == FEBRERO;
        }
    }

    public boolean esDeOtoño(boolean esHemisferioNorte) {
        if (esHemisferioNorte) {
            return this == SEPTIEMBRE || this == OCTUBRE || this == NOVIEMBRE;
        } else {
            return this == MARZO || this == ABRIL || this == MAYO;
        }
    }
}
