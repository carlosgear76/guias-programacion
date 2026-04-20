1. Definición de polimorfismo y sobreescritura
El polimorfismo es la capacidad de que objetos de distintas clases respondan de manera diferente al mismo mensaje (invocación de método). Permite tratar objetos de subtipos como si fueran del supertipo, delegando la ejecución concreta en la implementación real del objeto. La sobreescritura (o overriding) consiste en redefinir un método heredado en una subclase, cambiando su comportamiento manteniendo la misma firma (nombre y parámetros). Gracias a la sobreescritura, el polimorfismo puede seleccionar la versión adecuada en tiempo de ejecución.

2. Ligadura dinámica (enlace tardío) y comparación entre lenguajes
La ligadura dinámica significa que la decisión de qué método ejecutar se toma en tiempo de ejecución, basándose en el tipo real del objeto (no en el tipo de la referencia). Es esencial para el polimorfismo porque permite que una referencia de supertipo invoque la versión sobrescrita de la subclase. En C++ se requiere declarar explícitamente el método como virtual; en Java todos los métodos no estáticos, no privados y no final usan ligadura dinámica por defecto. En Python, todos los métodos son inherentemente dinámicos (no se necesita declaración especial), pero se paga en rendimiento y seguridad de tipos.

3. Ejemplo de polimorfismo con Soldado y sobrescritura de saludar
java
class Soldado {
    public void saludar() { System.out.println("Soldado saluda"); }
}
class Zapador extends Soldado {
    @Override public void saludar() { System.out.println("Zapador al ataque"); }
}
class Artillero extends Soldado {
    // no sobrescribe, usa el de Soldado
}
// Uso polimórfico:
Soldado[] ejercito = { new Zapador(), new Artillero() };
for (Soldado s : ejercito) s.saludar();  // imprime "Zapador al ataque" y "Soldado saluda"
La referencia de tipo Soldado llama a saludar(), pero la ejecución muestra el comportamiento del objeto real gracias a la ligadura dinámica.

4. Invocación al método base con super
Cuando se sobrescribe un método, se puede invocar explícitamente la versión de la superclase usando la palabra clave super. Por ejemplo, un Zapador puede querer ejecutar el saludo base y luego añadir su propio mensaje:

java
class Zapador extends Soldado {
    @Override public void saludar() {
        super.saludar();  // invoca el método de Soldado
        System.out.println("ZAPADOR A SUS ÓRDENES");
    }
}
De esta forma se extiende el comportamiento original sin reemplazarlo completamente.

5. Restricciones en sobreescritura, diferencias con sobrecarga y uso de @Override
Al sobrescribir, los parámetros deben coincidir exactamente en tipo y orden; el tipo de retorno puede ser el mismo o un subtipo (covarianza). El modificador de acceso no puede ser más restrictivo (p. ej., no se puede hacer private si el base era public). La sobrecarga es diferente: mismo nombre pero distinta lista de parámetros, y se resuelve en tiempo de compilación. La anotación @Override hace que el compilador verifique que realmente se está sobrescribiendo un método heredado, evitando errores tipográficos o de firma. Es recomendable usarla siempre por claridad y seguridad.

6. Uso cotidiano del polimorfismo en Java
Sí, desde los primeros programas se emplea polimorfismo sin saberlo. Por ejemplo, al sobrescribir toString() en una clase propia, y luego pasar un objeto a System.out.println(), este método llama a toString() polimórficamente. También al sobrescribir equals(Object) se está usando polimorfismo, porque ArrayList.contains() o HashSet dependen de esa sobreescritura. Así que el polimorfismo está presente en los mecanismos básicos del lenguaje.

7. Clases y métodos abstractos
Una clase abstracta no puede instanciarse (no se puede usar new). Puede contener métodos abstractos, que carecen de cuerpo (solo declaración) y deben ser implementados por las subclases concretas. Se declaran con abstract. En el ejemplo, Soldado se vuelve abstracto y se añade atacar():

java
abstract class Soldado {
    public void saludar() { System.out.println("Hola"); }
    public abstract void atacar();
}
class Zapador extends Soldado {
    @Override public void atacar() { System.out.println("Pone mina"); }
}
class Artillero extends Soldado {
    @Override public void atacar() { System.out.println("Dispara cohete"); }
}
No se puede crear un new Soldado(); solo sus subclases concretas.

8. Uso de final en métodos y clases
final en un método impide que las subclases lo sobrescriban, anulando así el polimorfismo para ese método. final en una clase impide que sea extendida (no puede tener subclases). Esto se relaciona con el polimorfismo porque cierra la posibilidad de variación. En la API de Java, String es una clase final, al igual que Math o System. Esto garantiza inmutabilidad y seguridad, pero también impide crear subtipos polimórficos de esas clases.

9. Interfaces en Java
Una interfaz es un contrato que declara métodos públicos (abstractos por defecto) y constantes. A diferencia de las clases abstractas, una interfaz no puede tener estado (atributos de instancia) y una clase puede implementar múltiples interfaces (herencia múltiple de tipos). Las interfaces permiten polimorfismo sin jerarquía de clases rígida. Por ejemplo, Comparable o Serializable. Una clase abstracta puede tener métodos concretos y atributos, pero solo se hereda una.

10. Ejemplo polimórfico con Punto abstracto y Linea
java
abstract class Punto {
    public abstract double calcularDistanciaA(Punto otro);
}
class Punto2D extends Punto {
    private double x, y;
    public Punto2D(double x, double y) { this.x = x; this.y = y; }
    @Override
    public double calcularDistanciaA(Punto otro) {
        if (!(otro instanceof Punto2D))
            throw new IllegalArgumentException("Se esperaba Punto2D");
        Punto2D p = (Punto2D) otro;
        double dx = this.x - p.x, dy = this.y - p.y;
        return Math.sqrt(dx*dx + dy*dy);
    }
}
// Similar para Punto3D
class Linea {
    private Punto p1, p2;
    public Linea(Punto p1, Punto p2) { this.p1 = p1; this.p2 = p2; }
    public double longitud() { return p1.calcularDistanciaA(p2); }
}
Linea no necesita conocer el tipo concreto de punto; el polimorfismo delega el cálculo específico en cada subclase.

11. Herencia de interfaces y herencia múltiple
La herencia de interfaces se logra con extends entre interfaces, permitiendo que una interfaz herede los métodos de otra u otras (herencia múltiple de interfaces). Por ejemplo:

java
interface Fichero {
    String leerContenido();
}
interface FicheroEscribible extends Fichero {
    void escribirContenido(String contenido);
    void eliminar();
}
Una clase puede implementar FicheroEscribible y también otras interfaces. Esto proporciona flexibilidad de diseño sin los problemas de la herencia múltiple de clases (como el conflicto de estado). Java permite que una interfaz extienda múltiples interfaces separadas por comas.

