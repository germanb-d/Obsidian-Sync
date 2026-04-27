Basado en la estructura del parcial de ejemplo y los temas requeridos, aquí tenés un modelo de parcial para practicar:

### **Examen Parcial: Orientación a Objetos II**

**1. Heurística de diseño: Tell Don't Ask**
Dado el siguiente código de un sistema de alquiler de autos:

```java
public class Alquiler {
    private Auto auto;
    private int dias;
    // getters...
}

public class SistemaAlquiler {
    public double calcularPrecioTotal(Alquiler alquiler) {
        double precioBase = alquiler.getAuto().getPrecioDiario() * alquiler.getDias();
        if (alquiler.getAuto().esLujo()) {
            return precioBase * 1.20;
        }
        return precioBase;
    }
}
```
**Se pide:** Refactorizá aplicando **Tell Don't Ask**. Escribí un test unitario que verifique el cálculo correcto del precio para un auto de lujo.

---

**2. Testabilidad: Inyección de Dependencias y Fakes**
La clase `ValidadorDeCredito` utiliza una librería externa `VerazService` que consulta una base de datos centralizada vía web para determinar si un cliente es apto para un préstamo. Esta dependencia impide testear la lógica local de forma aislada.

```java
public class ValidadorDeCredito {
    public boolean esApto(Cliente cliente) {
        VerazWeb service = new VerazWeb(); // Dependencia hardcodeada
        int puntaje = service.consultarPuntaje(cliente.getDni());
        return puntaje > 700;
    }
}
```
**Se pide:**
*   **a.** Refactorizá aplicando **Inyección de Dependencias** y **Dependencia de Abstracciones** para que el servicio sea testable.
*   **b.** Escribí un test unitario que verifique que un cliente **no es apto** (puntaje 500) utilizando un **Fake Object**.

---

**3. Polimorfismo: Eliminar condicionales**
La siguiente lógica calcula el costo de envío según el tipo de transporte.

```java
enum TipoEnvio { MOTO, CAMION, AVION }

public class CalculadorEnvio {
    public double calcularCosto(TipoEnvio tipo, double distancia) {
        if (tipo == TipoEnvio.MOTO) {
            return distancia * 50;
        } else if (tipo == TipoEnvio.CAMION) {
            return distancia * 100 + 500;
        } else if (tipo == TipoEnvio.AVION) {
            return distancia * 500 + 2000;
        }
        return 0;
    }
}
```
**Se pide:** Refactorizá para eliminar los `if` aplicando **Polimorfismo**. Mostrá cómo quedaría el código del cliente (Main) tras el cambio.

---

**4. Java Moderno: Expresiones Lambda**
En el sistema de la biblioteca, se repite el siguiente bloque para registrar logs de cada operación:

```java
public void registrarPrestamo(Libro libro) {
    logger.info("Inicio operacion");
    long inicio = System.currentTimeMillis();
    repositorio.guardar(libro);
    logger.info("Fin operacion: " + (System.currentTimeMillis() - inicio) + "ms");
}
```
**Se pide:** Refactorizá para eliminar la duplicación de código de auditoría mediante el uso de **Lambdas** (usando por ejemplo `Runnable` o una interfaz funcional propia).

¿Te gustaría que resolvamos juntos el **primer ejercicio** para ver cómo aplicar la lógica de "No pedir datos, sino ordenar acciones"?




