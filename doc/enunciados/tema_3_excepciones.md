<!--
Posible prompt:
<prompt>
Tengo un cuestionario con preguntas sobre "Excepciones". Debes tener en cuenta que los conocimientos previos que tengo (y por tanto tus respuestas deben ser adaptadas), son:
- C/C++ sin orientación a objetos.
- Temas de Java previos: Clases y Objetos, Encapsulación.

Cada respuesta debe tener entre 2 - 4 párrafos de longitud (sin contar los trozos de código).

Por favor, escribe en impersonal las respuestas.

</prompt>
----
-->
# TEMA 3. Excepciones

## 1. Empecemos un tema sobre control de errores en lenguajes de programación, con algo básico. En C, donde no existen las excepciones, pongamos un ejemplo de una raíz que toma número flotante positivo. Queremos controlar el error si la función recibe un número negativo. El usuario debe ser informado pero desde fuera de la función `raiz` ¿Cómo indicamos ese error?. Enumera dos opciones diferentes de diseñar, poniendo un ejemplo de código de cada una.

### Respuesta:
#include <stdio.h>
#include <math.h>

float raiz(float x) {
    if (x < 0) {
        return NAN;   // Indicamos error
    }
    return sqrtf(x);
}

int main() {
    float numero = -4.0;
    float resultado = raiz(numero);

    if (isnan(resultado)) {
        printf("Error: no se puede calcular la raíz de un número negativo.\n");
    } else {
        printf("Resultado: %.2f\n", resultado);
    }

    return 0;
}


## 2. Brevemente ¿Qué es una **"excepción"**? ¿Con qué objetivo las usa un programador cuando implementa funciones o cuando las llama?

### Respuesta:

Una excepción es un mecanismo para señalar que ha ocurrido una situación anómala o inesperada durante la ejecución de un programa.
No es simplemente un error: es un evento que interrumpe el flujo normal del programa y que puede (y debe) gestionarse de forma controlada.

¿Para qué las usa un programador?
Cuando implementa funciones

El programador lanza excepciones para:

Indicar que una precondición no se cumple (ej: parámetro inválido).
Señalar que ocurrió un fallo que la función no puede resolver por sí sola.
Evitar devolver códigos de error ambiguos.
Separar claramente la lógica normal del manejo de errores.

Ejemplo conceptual:

“Si el divisor es 0, lanzo una excepción en vez de devolver un valor inválido.”

Cuando llama funciones

El programador las usa para:

Capturar y manejar errores sin que el programa termine abruptamente.
Tomar decisiones alternativas si algo falla.
Registrar información del fallo (mensaje, tipo, origen).
Mantener el programa robusto.

## 3. Reescribe el mismo ejemplo de raiz, pero en Java, metiendo ese método en una clase `Calculadora` y llama a dicho método desde el método `main`, mostrando cómo se puede controlar desde fuera.

### Respuesta


## 4. ¿Qué es **"lanzar"** una excepción? ¿Qué es **"controlar"** o **"capturar"** una excepción? ¿Qué es que se **"propague"** una excepción? ¿Qué le va ocurriendo a las funciones en la pila de llamadas por donde se va propagando la excepción? ¿Las funciones que no la controlan se reanudan después de alguna forma? Explica con el mismo ejemplo anterior en Java de la raíz cuadrada.

### Respuesta:
Supongamos que tenemos esta función:

double raiz(double x) {
    if (x < 0) {
        throw new IllegalArgumentException("No se puede calcular la raíz de un número negativo");
    }
    return Math.sqrt(x);
}
1 Lanzar (throw) una excepción

Significado: La función detecta un error y “lanza” una señal que indica que algo salió mal.

En el ejemplo: throw new IllegalArgumentException(...) lanza la excepción cuando x < 0.

Esto detiene inmediatamente la ejecución normal de raiz() y la pasa a quien pueda manejarla.

2 Controlar o capturar (catch) una excepción

Significado: Alguna función que llama a raiz() decide “atrapar” el error para manejarlo sin que el programa termine abruptamente.

Ejemplo:

try {
    double r = raiz(-4);
    System.out.println("Raíz: " + r);
} catch (IllegalArgumentException e) {
    System.out.println("Error: " + e.getMessage());
}

Aquí, el catch captura la excepción y permite que el programa continúe ejecutándose normalmente después del bloque.

3 Propagar una excepción

Significado: Si una función no captura la excepción, ésta “sube” por la pila de llamadas hasta encontrar un manejador que sí la controle.

La pila de llamadas es como una lista de funciones activas: main → otraFunc → raiz.

Si raiz() lanza la excepción y otraFunc no la captura, entonces sigue subiendo hasta main.

double otraFunc(double x) {
    return raiz(x); // Si x < 0, la excepción se propaga desde aquí
}

La excepción propaga automáticamente, y las funciones que no la controlan no se reanudan. Se “desenrolla” la pila, eliminando cada llamada que no la captura, hasta que se encuentra un catch o termina el programa con error.


## 5. ¿Qué ventajas tiene frente a C, la **"propagación natural"** de las excepciones a través de la pila (*stack*) de llamadas?

### Respuesta:
La propagación natural de excepciones en Java frente a C permite:

Evitar revisar cada llamada: las funciones intermedias no necesitan chequear errores.

Código más limpio: la lógica principal no se mezcla con control de errores.

Seguridad: funciones intermedias no se ejecutan con datos inválidos.

Mayor información: se puede pasar un objeto excepción con detalles, no solo un código.

En C, todo esto se haría manualmente con códigos de error y comprobaciones en cada función.


## 6. En orientación a objetos, ¿las excepciones suelen ser objetos? ¿Qué ventajas tiene esto en términos de encapsulación? ¿Podemos entonces crear excepciones personalizadas?

### Respuesta:
Sí, en orientación a objetos las excepciones son objetos (por ejemplo, en Java heredan de Throwable).

Ventajas de la encapsulación:

La información sobre el error (mensaje, tipo, pila de llamadas) está guardada dentro del objeto, accesible solo mediante métodos.

Permite manejar errores sin exponer detalles internos de la función que los lanza.

Excepciones personalizadas:

Sí, podemos crear nuestras propias clases de excepción para representar errores específicos de nuestra aplicación.


## 7. En relación con las ventajas de la encapsulación, comparando el ejemplo en C con Java. ¿Qué **información esencial** lleva cualquier **objeto excepción** que es muy útil tener cuando se llega a un manejador?

### Respuesta:
En Java, cualquier objeto excepción suele llevar información esencial como:

Tipo de excepción: qué clase de error ocurrió.

Mensaje descriptivo: explicación del error.

Pila de llamadas (stack trace): dónde se lanzó la excepción y por qué camino llegó al manejador.

En C, normalmente solo se tiene un código de error, sin detalles ni rastreo de la pila.


## 8. En Java, sobre el bloque **"try-catch"**, ¿se pueden tener más de un bloque `catch`? ¿cuántos bloques `catch` se ejecutan?

### Respuesta:
Sí, en Java se pueden tener varios bloques catch para un mismo try.

Solo se ejecuta uno: el primero cuyo tipo de excepción coincida con la lanzada.

Los demás bloques catch se ignoran.


## 9. Si las excepciones producen rupturas en el código llamador, ¿cómo podemos garantizar que se ejecuta siempre finalmente un código necesario para cierre de ficheros, liberacion de recursos, antes de que continúe propagándose la excepción? Pon un ejemplo en Java con `finally`, tanto con `catch` como sin él.

### Respuesta:
En Java, usamos el bloque finally para garantizar que cierto código se ejecute siempre, ya sea que se capture la excepción o no. Esto es útil para cerrar ficheros, liberar recursos, etc.

Ejemplo con catch:
import java.io.*;

public class Ejemplo {
    public static void main(String[] args) {
        FileReader fr = null;
        try {
            fr = new FileReader("archivo.txt");
            int c = fr.read();
            System.out.println("Primer caracter: " + c);
        } catch (IOException e) {
            System.out.println("Error al leer el archivo: " + e.getMessage());
        } finally {
            // Este código se ejecuta siempre
            if (fr != null) {
                try { fr.close(); } catch (IOException e) { }
                System.out.println("Archivo cerrado en finally");
            }
        }
        System.out.println("Programa continúa...");
    }
}

Aunque ocurra un IOException y se ejecute el catch, el finally siempre se ejecuta.

Ejemplo sin catch (propagando la excepción):
import java.io.*;

public class Ejemplo {
    public static void main(String[] args) throws IOException {
        FileReader fr = null;
        try {
            fr = new FileReader("archivo.txt");
            int c = fr.read();
            System.out.println("Primer caracter: " + c);
        } finally {
            // Se ejecuta incluso si la excepción se propaga
            if (fr != null) {
                fr.close();
                System.out.println("Archivo cerrado en finally");
            }
        }
        // Si ocurrió excepción, aquí nunca se llega; si no, continúa
        System.out.println("Programa continúa...");
    }
}


## 10. En Java, el bloque `finally` puede ir sin `catch`? ¿Se ejecuta siempre tanto si ocurre como si no ocurre una excepción? ¿Y si hay un `return` en medio del `try`?

### Respuesta:
Sí, en Java un bloque finally puede ir sin catch.

Se ejecuta siempre, tanto si ocurre una excepción como si no.

Incluso si hay un return en el try, el código de finally se ejecuta antes de que el método realmente retorne.


## 11. En Java, qué son las excepciones **"controladas"** y las **"no controladas"**? ¿Qué papel juega `RuntimeException`? Pon un ejemplo de excepciones típicas controladas y no controladas que incluso nosotros mismos podríamos usar. Haz dos listas con 3 o 4 ejemplos de situación donde se suele preferir una excepción controlada y donde se suele preferir una excepción no controlada.

### Respuesta:
Excepciones controladas (checked): el compilador obliga a capturarlas o declararlas. Suelen representar errores previsibles fuera del control del programa.

Ejemplo: IOException, SQLException.

Excepciones no controladas (unchecked): heredan de RuntimeException; no es obligatorio capturarlas. Representan errores de programación.

Ejemplo: NullPointerException, IllegalArgumentException.

RuntimeException sirve de base para excepciones no controladas.

Ejemplos típicos

Excepciones controladas:

Lectura de un archivo que puede no existir → FileNotFoundException

Conexión a base de datos → SQLException

Parse de un número desde un fichero externo → NumberFormatException (controlada si se decide)

Excepciones no controladas:

División por cero → ArithmeticException

Acceso a un índice inválido en un array → ArrayIndexOutOfBoundsException

Argumento inválido en un método → IllegalArgumentException

Referencia nula → NullPointerException

Regla práctica: usa controladas cuando el error puede ocurrir por factores externos; usa no controladas cuando el error indica fallo de programación.


## 12. ¿Qué es y para qué se usa `throws`? ¿Por qué es alternativa a capturar una excepción controlada?

### Respuesta:
En Java throws es una palabra clave utilizada en la firma de un método para declarar que dicho método puede lanzar una o más excepciones durante su ejecución. Actúa como una advertencia para quien llama al método, indicando que el método no maneja el error internamente y que la responsabilidad de gestionarlo se delega al código superior en la pila de llamadas (caller). 

¿Para qué se usa throws?
Delegación de responsabilidad (Separación de conceptos): Un método de bajo nivel (ej. acceso a base de datos) podría no saber cómo reportar el error al usuario final. Usa throws para pasar la excepción a un método de nivel superior (ej. controlador web) que sí sabe cómo mostrar un mensaje adecuado.

Limpieza del código: Evita tener bloques try-catch repetitivos y vacíos en métodos de bajo nivel, haciendo el código más legible.

Gestión centralizada: Permite capturar múltiples excepciones distintas en un único lugar superior en lugar de gestionarlas individualmente en cada sub-método. 


## 13. Pon un ejemplo en Java de firma de método que incluya `throws`, de una función que abre un fichero pero que declara que no le interesa menejar la excepción de si el fichero no existe, sino que se propague hacia arriba. Eso sí, acuérdate del `finally`.

### Respuesta:

import java.io.FileReader;
import java.io.IOException;

public class Ejemplo {

    // Método 1ue declara que puede lanzar IOException
    public static void abrirArchivo(String ruta) throws IOException {
        FileReader lector = null;
        try {
            lector = new FileReader(ruta); // puede lanzar FileNotFoundException
            // ... leer del fichero
            System.out.println("Fichero abierto correctamente.");
        } finally {
            if (lector != null) {
                lector.close(); // se ejecuta aunque haya excepción
                System.out.println("Fichero cerrado en finally.");
            }
        }
    }

    public static void main(String[] args) {
        try {
            abrirArchivo("archivo.txt");
        } catch (IOException e) {
            System.out.println("Se propagó una excepción: " + e.getMessage());
        }
    }
}


## 14. ¿Podemos poner en `throws` excepciones no controladas, como `RuntimeException`? ¿Debería el método llamador entonces poner `try-catch` en ese caso? ¿Qué sentido tendría?

### Respuesta:
Sí:

Puedes poner RuntimeException en throws, pero no es obligatorio.

El llamador no tiene que usar try-catch para esas excepciones.

El sentido de declararlas es documentar que el método puede lanzarlas, para claridad o análisis estático, pero no cambia nada en tiempo de compilación.


## 15. ¿Cuándo se recomienda usar excepciones controladas, como `IOException`, y cuándo no controladas como `IllegalArgumentException`? ¿Existen en todos los lenguajes ambas opciones? En los que sólo existe una opción, ¿cuál es la más habitual?

### Respuesta:
si:
Excepciones controladas (checked, ej. IOException) → se usan cuando el error es previsible y recuperable, y el llamador puede razonablemente manejarlo (lectura de ficheros, conexión a red, etc.).

Excepciones no controladas (unchecked, ej. IllegalArgumentException) → se usan para errores de programación o condiciones irrecuperables, como pasar un argumento inválido; no tiene sentido obligar a capturarlas.

No todos los lenguajes tienen ambas.

Java distingue ambas.

C# tiene sólo unchecked (Exception), no obliga a try-catch.

Python también tiene sólo unchecked (Exception).

En lenguajes sin checked exceptions, todas las excepciones se tratan como no controladas, y la práctica habitual es lanzar exceptions para errores que el llamador pueda manejar y dejar que el resto propague naturalmente.


## 16. ¿Tiene sentido lanzar excepciones dentro del `catch`? ¿Se puede relanzar la misma excepción capturada? ¿Cuándo tendría sentido hacer esto último? Pon ejemplos de ambos casos.

### Respuesta:
Sí:

Lanzar excepciones dentro de un catch tiene sentido si quieres transformar o propagar un error a un nivel superior.

Se puede relanzar la misma excepción capturada usando throw; (Java: throw e;). Esto tiene sentido cuando quieres hacer algo adicional (como loguear) pero no manejar completamente el error.

Ejemplos:

Lanzar una nueva excepción desde catch:

try {
    int x = Integer.parseInt("abc");
} catch (NumberFormatException e) {
    throw new IllegalArgumentException("Valor no válido", e);
}

(Transforma la excepción a otra más apropiada para la API)

Relanzar la misma excepción:

try {
    int[] arr = new int[1];
    int y = arr[2];
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Índice fuera de rango, registrando...");
    throw e; // vuelve a lanzar la misma excepción
}


## 17. ¿En qué consiste que una excepción sea la **"causa"** de otra excepción? Pon un ejemplo en Java, donde capturemos una excepción de bajo nivel y la encapsulemos en otra personalizada de alto nivel. Cuando una excepción sale por pantalla y tiene una causa, ¿se ve?

### Respuesta:
En Java, una excepción puede tener otra excepción como causa cuando queremos encapsular un error de bajo nivel dentro de un error de más alto nivel que tenga más sentido para el contexto de nuestro programa. Esto se hace usando el constructor de las excepciones que acepta un Throwable como parámetro, que se guarda internamente como la causa. Esto permite:

No perder la información del error original.

Proporcionar un mensaje más adecuado para el nivel de abstracción donde ocurre la excepción.

Propagar la excepción de forma controlada.

Ejemplo en Java

Supongamos que tenemos una función que lee un archivo y queremos lanzar una excepción personalizada si ocurre cualquier problema de E/S:
// Excepción personalizada de alto nivel
class MiExcepcionAltoNivel extends Exception {
    public MiExcepcionAltoNivel(String mensaje, Throwable causa) {
        super(mensaje, causa); // aquí guardamos la causa
    }
}

import java.io.*;

public class EjemploCausa {
    public static void leerArchivo(String ruta) throws MiExcepcionAltoNivel {
        try {
            BufferedReader br = new BufferedReader(new FileReader(ruta));
            String linea = br.readLine();
            br.close();
        } catch (IOException e) {
            // Capturamos la excepción de bajo nivel y la encapsulamos
            throw new MiExcepcionAltoNivel("Error leyendo el archivo", e);
        }
    }

    public static void main(String[] args) {
        try {
            leerArchivo("archivo_inexistente.txt");
        } catch (MiExcepcionAltoNivel e) {
            e.printStackTrace(); // imprime la excepción y su causa
        }
    }
}

MiExcepcionAltoNivel: Error leyendo el archivo
    at EjemploCausa.leerArchivo(EjemploCausa.java:10)
    at EjemploCausa.main(EjemploCausa.java:18)
Caused by: java.io.FileNotFoundException: archivo_inexistente.txt (No such file or directory)
    at java.base/java.io.FileInputStream.open0(Native Method)
    at java.base/java.io.FileInputStream.open(FileInputStream.java:219)
    ...

   Se observa que:

La excepción principal es MiExcepcionAltoNivel.

La causa original (FileNotFoundException) se muestra después de Caused by:.

Así no se pierde información y se puede rastrear el error real.
