1. Estructura de datos genérica con void* en C o Object en Java
En C, se puede usar void* para almacenar cualquier tipo de dato en un array, perdiendo la información de tipo. En Java, la clase Object es la raíz de toda jerarquía, por lo que un array de Object puede contener cualquier objeto. A continuación se muestra un ejemplo en Java con un contenedor simple basado en array primitivo:

java
public class ContenedorObject {
    private Object[] elementos;
    private int size;
    public ContenedorObject(int capacidad) {
        elementos = new Object[capacidad];
        size = 0;
    }
    public void agregar(Object o) { elementos[size++] = o; }
    public Object obtener(int i) { return elementos[i]; }
}
Este enfoque permite alojar cualquier tipo, pero sacrifica la seguridad de tipos.

2. Significado de programación genérica
La programación genérica consiste en escribir código (clases, interfaces, métodos) que opera sobre tipos parametrizables, de modo que la misma implementación pueda ser utilizada con diferentes tipos concretos manteniendo la seguridad de tipos en tiempo de compilación. El ejemplo anterior con Object es una forma básica y no segura de genericidad, pero no es programación genérica propiamente dicha porque no hay parámetros de tipo ni verificación en compilación. Los verdaderos mecanismos genéricos (como templates de C++ o generics de Java) permiten especificar el tipo concreto en el momento de uso y garantizan que no haya errores de tipo.

3. Problemas de emplear void* o Object
El principal problema es la pérdida de seguridad de tipos. Al extraer un elemento, se obtiene un Object (o void*) y se requiere un downcasting explícito al tipo original, lo que es propenso a errores en tiempo de ejecución (por ejemplo, ClassCastException). Además, no hay restricción en tiempo de compilación para evitar mezclar tipos distintos dentro de la misma estructura. Esto viola el principio de fail-fast y dificulta el mantenimiento, ya que el programador debe recordar qué tipo se guardó en cada posición. Los mecanismos genéricos resuelven estos problemas moviendo la comprobación al compilador.

4. Parámetros de tipo
Los parámetros de tipo (o variables de tipo) son identificadores que representan un tipo desconocido que se especificará cuando se instancie la clase genérica o se invoque un método genérico. Se declaran entre ángulos (<T>) después del nombre de la clase o método. Permiten que la misma implementación trabaje con diferentes tipos de forma segura: el compilador reemplaza los parámetros por los tipos concretos (en Java mediante type erasure, en C++ mediante instanciación) y verifica que todas las operaciones respeten los tipos. Por ejemplo, class Caja<T> { private T contenido; ... }.

5. Ejemplo en Java (generics) y C++ (templates)
Java:

java
import java.util.ArrayList;
import java.util.List;

List<String> lista = new ArrayList<>();
lista.add("Hola");
lista.add("Mundo");
for (String s : lista) {
    System.out.println(s);  // s es String, sin casting
}
C++:

cpp
#include <vector>
#include <string>
#include <iostream>

std::vector<std::string> lista;
lista.push_back("Hola");
lista.push_back("Mundo");
for (const auto& s : lista) {
    std::cout << s << std::endl;  // s es std::string
}
En ambos casos, la lista solo admite String y los elementos se extraen con el tipo correcto sin necesidad de conversión explícita.

6. Funcionamiento: type erasure (Java) vs instanciación de plantillas (C++)
En Java, el compilador aplica type erasure: elimina los parámetros de tipo y añade conversiones implícitas donde sea necesario. Solo existe una única versión compilada de la clase genérica (p. ej., List se convierte en List de Object). Esto proporciona compatibilidad binaria con código pre-generics, pero impide conocer el tipo en tiempo de ejecución. En C++, cada instanciación de una plantilla con tipos diferentes genera código separado (instanciación de plantilla). Esto permite optimizaciones específicas y mayor flexibilidad, pero puede aumentar el tamaño del código y los tiempos de compilación. Java prioriza la compatibilidad y la portabilidad; C++ prioriza la eficiencia y la expresividad.

7. Clase genérica Par<T,U> en Java
java
public class Par<T, U> {
    private final T primero;
    private final U segundo;
    public Par(T primero, U segundo) {
        this.primero = primero;
        this.segundo = segundo;
    }
    public T getPrimero() { return primero; }
    public U getSegundo() { return segundo; }
}

// Ejemplo de uso: función que devuelve media y desviación típica
public static Par<Double, Double> estadisticas(double[] datos) {
    double suma = 0.0;
    for (double d : datos) suma += d;
    double media = suma / datos.length;
    double var = 0.0;
    for (double d : datos) var += Math.pow(d - media, 2);
    double desv = Math.sqrt(var / datos.length);
    return new Par<>(media, desv);
}
8. Método genérico seleccionaUno vs versión con Object
Con Object (no genérico):

java
public static Object seleccionaUno(Object a, Object b) {
    return Math.random() < 0.5 ? a : b;
}
// Uso: requiere downcasting y permite mezclar tipos diferentes
String s = (String) seleccionaUno("A", "B");  // peligroso
Integer i = (Integer) seleccionaUno(1, "dos"); // compila, pero falla en runtime
Con parámetro de tipo:

java
public static <T> T seleccionaUno(T a, T b) {
    return Math.random() < 0.5 ? a : b;
}
// Uso: sin downcasting y ambos argumentos deben ser del mismo tipo
String s = seleccionaUno("A", "B");  // T es String
Integer i = seleccionaUno(1, 2);     // T es Integer
// seleccionaUno(1, "dos"); // error de compilación: tipos incompatibles
El método genérico evita el downcasting y obliga a que ambos argumentos compartan el mismo tipo concreto, mejorando la seguridad.

9. Restricciones con extends y ejemplo de Punto con Number
Sí, se pueden establecer restricciones (bounds) usando extends. Por ejemplo, <T extends Number> indica que T debe ser una subclase de Number. Solución sin generics (usando Number directamente):

java
public class PuntoNumber {
    private final Number x, y;
    public PuntoNumber(Number x, Number y) { this.x = x; this.y = y; }
    public Number getX() { return x; }
    public Number getY() { return y; }
    public double distancia(PuntoNumber otro) {
        double dx = x.doubleValue() - otro.x.doubleValue();
        double dy = y.doubleValue() - otro.y.doubleValue();
        return Math.sqrt(dx*dx + dy*dy);
    }
}
Solución con generics:

java
public class PuntoGenerico<T extends Number> {
    private final T x, y;
    public PuntoGenerico(T x, T y) { this.x = x; this.y = y; }
    public T getX() { return x; }
    public T getY() { return y; }
    public double distancia(PuntoGenerico<T> otro) {
        double dx = x.doubleValue() - otro.x.doubleValue();
        double dy = y.doubleValue() - otro.y.doubleValue();
        return Math.sqrt(dx*dx + dy*dy);
    }
}
Tras type erasure, T se reemplaza por Number (el límite superior), por lo que el código compilado de PuntoGenerico usa Number en todas partes.

10. Comparación de las dos soluciones
La solución sin generics permite mezclar tipos distintos en las coordenadas: se puede crear new PuntoNumber(10, 3.5) donde x es Integer e y es Double. En cambio, la solución genérica fuerza que ambas coordenadas sean del mismo subtipo concreto de Number (por ejemplo, ambos Integer o ambos Double). El getX en la primera solución devuelve Number (requiere downcasting para operaciones específicas). En la solución genérica, getX devuelve exactamente el tipo T (por ejemplo, Integer o Double), lo que evita conversiones y permite usar métodos propios del tipo concreto sin perder información.

11. Mejora con generics para evitar instanceof en Punto
Se declara la interfaz con un parámetro de tipo P<T extends P<T>> (patrón self-referential generic):

java
public interface Punto<T extends Punto<T>> {
    double distanciaA(T p);
}

public class Punto2D implements Punto<Punto2D> {
    private final double x, y;
    public Punto2D(double x, double y) { this.x = x; this.y = y; }
    @Override
    public double distanciaA(Punto2D p) {
        return Math.hypot(x - p.x, y - p.y);
    }
}

public class Punto3D implements Punto<Punto3D> {
    private final double x, y, z;
    public Punto3D(double x, double y, double z) { this.x = x; this.y = y; this.z = z; }
    @Override
    public double distanciaA(Punto3D p) {
        double dx = x - p.x, dy = y - p.y, dz = z - p.z;
        return Math.sqrt(dx*dx + dy*dy + dz*dz);
    }
}
Así, el método distanciaA recibe siempre el tipo concreto del punto, eliminando la necesidad de instanceof y downcasting.

12. Covarianza, contravarianza e invarianza: arrays vs generics
String[] es subtipo de Object[] porque los arrays en Java son covariantes: si A es subtipo de B, entonces A[] es subtipo de B[]. Esto permite, por ejemplo, asignar String[] a Object[], pero puede provocar ArrayStoreException en tiempo de ejecución si se intenta almacenar un Integer en ese array. En cambio, List<String> no es subtipo de List<Object> porque los tipos genéricos son invariantes: aunque String sea subtipo de Object, List<String> no tiene relación de subtipo con List<Object>. Esto evita errores de tipo en tiempo de ejecución, trasladando la comprobación al compilador. La invarianza es la opción más segura. La covarianza permitiría más flexibilidad pero con riesgos; la contravarianza (al revés) también es posible mediante wildcards.

13. Wildcards: ? extends T y ? super T
Un wildcard (?) representa un tipo desconocido. List<? extends T> significa una lista de algún subtipo de T (incluido T). Solo se puede leer (los elementos se tratan como T), pero no añadir (excepto null). Se usa cuando se quiere consumir datos de una estructura. List<? super T> significa una lista de algún supertipo de T. Se puede añadir elementos de tipo T (o subtipos), pero al leer solo se garantiza que sean Object. Se usa para llenar estructuras.

Ejemplo con ? extends Number (suma):

java
public static double sumar(List<? extends Number> lista) {
    double suma = 0.0;
    for (Number n : lista) suma += n.doubleValue();
    return suma;
}
Ejemplo con ? super Integer (añadir enteros):

java
public static void añadirEnteros(List<? super Integer> lista) {
    for (int i = 1; i <= 10; i++) lista.add(i);
}