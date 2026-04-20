1. Ejemplo en C con struct para línea de dos puntos
En C, la composición se logra anidando estructuras. Por ejemplo, se define un struct Punto con coordenadas x e y, y un struct Linea que contiene dos puntos. La distancia entre puntos se calcula mediante la fórmula euclidiana, y la longitud de la línea es la distancia entre sus dos puntos.

c
struct Punto { double x, y; };
struct Linea { struct Punto p1, p2; };

double distancia(struct Punto a, struct Punto b) {
    double dx = a.x - b.x, dy = a.y - b.y;
    return sqrt(dx*dx + dy*dy);
}
double longitud(struct Linea l) { return distancia(l.p1, l.p2); }
2. Transformación a Java con orientación a objetos y encapsulación
En Java, la clase Punto se declara inmutable haciendo sus atributos private final y sin métodos modificadores. La clase Linea recibe dos puntos en el constructor y los almacena también como final, garantizando que no se puedan cambiar una vez creada. El método distancia pertenece a Punto y la longitud se delega en Linea.

java
public final class Punto {
    private final double x, y;
    public Punto(double x, double y) { this.x = x; this.y = y; }
    public double distancia(Punto otro) {
        double dx = this.x - otro.x, dy = this.y - otro.y;
        return Math.sqrt(dx*dx + dy*dy);
    }
}

public final class Linea {
    private final Punto p1, p2;
    public Linea(Punto p1, Punto p2) { this.p1 = p1; this.p2 = p2; }
    public double longitud() { return p1.distancia(p2); }
}
3. Multiplicidad en la composición
La multiplicidad indica cuántas instancias de una clase participan en la relación con otra. En el ejemplo Linea-Punto, la multiplicidad de Linea hacia Punto es 2 (cada línea tiene exactamente dos puntos). De Punto hacia Linea la multiplicidad es 0..* (un punto puede pertenecer a ninguna o muchas líneas), aunque en una composición pura no suele modelarse la navegabilidad inversa.

4. Composición fuerte (composición propia) y composición débil (agregación)
La composición fuerte (llamada simplemente composición) implica que el ciclo de vida de las partes está ligado al del todo: si el contenedor se destruye, las partes también. La composición débil o agregación permite que las partes sobrevivan al contenedor. En la práctica, en la composición fuerte el contenedor crea y destruye las partes; en la débil, las partes se pasan desde fuera y pueden ser compartidas.

5. Diferencia entre composición y dependencia
Cuando una clase solo recibe otra como parámetro, la devuelve, la crea dentro de un método o la usa como variable local, se habla de dependencia, no de composición. La composición implica que la clase contenedora tiene un campo del tipo de la otra clase, y normalmente gestiona su ciclo de vida. La dependencia es una relación más débil y temporal.

6. Dos formas de programar la relación entre Linea y Punto
Composición fuerte (los puntos pertenecen exclusivamente a la línea):

java
public class LineaFuerte {
    private final Punto p1, p2;
    public LineaFuerte(double x1, double y1, double x2, double y2) {
        p1 = new Punto(x1, y1);
        p2 = new Punto(x2, y2);
    }
}
Composición débil (los puntos se pasan desde fuera):

java
public class LineaDebil {
    private final Punto p1, p2;
    public LineaDebil(Punto p1, Punto p2) {
        this.p1 = p1;
        this.p2 = p2;
    }
}
7. Destrucción de objetos en la composición fuerte de Java
En Java no hay destrucción explícita de objetos; el recolector de basura los elimina cuando dejan de ser alcanzables. En la composición fuerte, si un objeto Linea deja de tener referencias activas, sus objetos Punto también quedan sin referencias externas (a menos que se hayan compartido), por lo que el recolector los eliminará automáticamente. No se necesita un destructor.

8. Ejemplo de composición débil: Departamento y Profesor con array primitivo
Se implementa con un array de Profesor de tamaño máximo 50, ocultando su uso. El director debe ser siempre uno de los profesores. Se lanzan excepciones si se intenta eliminar al director o asignar un director que no está en la lista.

java
public class Departamento {
    private static final int MAX = 50;
    private Profesor[] profesores;
    private int numProfesores;
    private Profesor director;

    public Departamento(Profesor directorInicial) {
        profesores = new Profesor[MAX];
        numProfesores = 0;
        anadirProfesor(directorInicial);
        director = directorInicial;
    }

    public void anadirProfesor(Profesor p) {
        if (numProfesores == MAX) throw new IllegalStateException("Máximo alcanzado");
        profesores[numProfesores++] = p;
    }

    public void eliminarProfesor(int pos) {
        if (pos < 0 || pos >= numProfesores) throw new IndexOutOfBoundsException();
        Profesor p = profesores[pos];
        if (p.equals(director)) throw new IllegalArgumentException("No se puede eliminar al director");
        for (int i = pos; i < numProfesores - 1; i++) profesores[i] = profesores[i+1];
        profesores[--numProfesores] = null;
    }

    public int getNumProfesores() { return numProfesores; }
    public Profesor getProfesor(int pos) { return profesores[pos]; }
    public void setDirector(Profesor nuevo) {
        boolean existe = false;
        for (int i = 0; i < numProfesores; i++) if (profesores[i].equals(nuevo)) existe = true;
        if (!existe) throw new IllegalArgumentException("El director debe ser profesor del departamento");
        director = nuevo;
    }
}
9. Uso de List en lugar de arrays primitivos
Con ArrayList<Profesor> se elimina la necesidad de gestionar manualmente el tamaño, el desplazamiento de elementos al eliminar y la variable numProfesores. El código se simplifica notablemente.

java
import java.util.*;

public class Departamento {
    private List<Profesor> profesores = new ArrayList<>();
    private Profesor director;

    public Departamento(Profesor directorInicial) {
        anadirProfesor(directorInicial);
        director = directorInicial;
    }
    public void anadirProfesor(Profesor p) { profesores.add(p); }
    public void eliminarProfesor(int pos) {
        if (profesores.get(pos).equals(director)) throw new IllegalArgumentException();
        profesores.remove(pos);
    }
    public int getNumProfesores() { return profesores.size(); }
    public Profesor getProfesor(int pos) { return profesores.get(pos); }
    // setDirector similar...
}
Si se devolviera la lista interna directamente (return profesores), se rompería la encapsulación porque el llamante podría modificarla (añadir, eliminar). Para resolverlo, se puede devolver una lista no modificable (Collections.unmodifiableList(profesores)) o una copia defensiva.

10. Composición recursiva: Persona inmutable con madre
Una persona tiene una madre que es otra persona, formando una cadena recursiva. Se declara inmutable usando final y no se proporcionan setters. En el main se crean desde la abuela hasta el nieto.

java
public final class Persona {
    private final String nombre;
    private final Persona madre;
    public Persona(String nombre, Persona madre) { this.nombre = nombre; this.madre = madre; }
    public Persona getMadre() { return madre; }
    public static void main(String[] args) {
        Persona abuela = new Persona("Ana", null);
        Persona madre = new Persona("Luisa", abuela);
        Persona nieto = new Persona("Carlos", madre);
    }
}
Otros ejemplos clásicos: nodos de un árbol (cada nodo tiene hijos que son nodos), sistemas de archivos (carpetas que contienen subcarpetas), o expresiones aritméticas (una expresión puede contener subexpresiones).

11. Relaciones de composición bidireccionales
Una relación bidireccional permite navegar desde cada objeto al otro: un Profesor conoce su Departamento y un Departamento conoce a sus Profesores. Para implementarla, se debe mantener la consistencia: al asignar un profesor a un departamento, se actualiza la referencia inversa. Además, al eliminar un profesor del departamento, se debe romper su vínculo con el departamento. Esto suele hacerse mediante métodos que actualizan ambos extremos, cuidando de no crear referencias cíclicas que impidan el recolector de basura.

java
public class Profesor {
    private Departamento departamento;
    public void setDepartamento(Departamento d) { this.departamento = d; }
}

public class Departamento {
    private List<Profesor> profesores = new ArrayList<>();
    public void anadirProfesor(Profesor p) {
        profesores.add(p);
        p.setDepartamento(this);
    }
}
