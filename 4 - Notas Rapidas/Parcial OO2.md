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





# Nuevos 1 y 2 


¡Claro! Aquí tenés dos ejercicios nuevos siguiendo exactamente la misma lógica de los temas centrales del parcial:

### **Ejercicio A: Heurística "Tell Don't Ask"**

En un sistema de biblioteca, el bibliotecario decide si un socio puede retirar un libro pidiéndole su lista de préstamos actuales:

``` java
public class Bibliotecario {
    public boolean puedeRetirar(Socio socio) {
        // "Pide" la lista y decide desde afuera
        if (socio.getPrestamos().size() > 5) {
            return false;
        }
        return true;
    }
}
```

**Se pide:**

1. Refactorizá para aplicar **Tell Don't Ask**, moviendo la responsabilidad al objeto que tiene los datos.
2. Escribí un test unitario que verifique que un socio con 6 libros no puede retirar más.

---

### **Ejercicio B: Testabilidad con Inyección de Dependencias**

La clase `GeneradorDeInformes` guarda un archivo PDF directamente en el disco rígido usando una clase concreta de Java, lo que hace que el test dependa del sistema de archivos real.

```
public class GeneradorDeInformes {
    public void exportar(String contenido) {
        FileWriter writer = new FileWriter("informe.pdf"); // Dependencia rígida
        writer.write(contenido);
    }
}
```

**Se pide:**

1. Refactorizá aplicando **Inyección de Dependencias** y **Dependencia de Abstracciones** para que el destino del informe sea intercambiable.
2. Escribí un test unitario que use un **Fake Object** (por ejemplo, uno que guarde el contenido en un `String` en memoria) para verificar que el informe se "envió" correctamente sin escribir el disco.

¿Por cuál te gustaría empezar a resolver? Si querés, probá el de **Tell Don't Ask** que es clave para entender cómo "ordenar acciones" en lugar de "pedir datos".

---

Aquí tenés un modelo de parcial integrando todos los temas clave de las fuentes y lo que vinimos practicando:

### **PUNTO 1: Heurística "Tell Don't Ask"**

Dado el siguiente código de un sistema de Ventas:

```
public class ProcesadorVentas {
    public void procesar(Carrito carrito) {
        if (carrito.getProductos().size() > 10) { // Pide la lista y decide
            carrito.aplicarDescuento(0.10);
        }
    }
}
```

**Se pide:** Refactorizá para aplicar **Tell Don't Ask**, moviendo la responsabilidad al objeto que tiene los datos. Escribí el test unitario para un carrito con 11 productos.

---

### **PUNTO 2: Inyección de Dependencias y Fake Objects**

La clase `Notificador` envía correos usando una librería externa `GmailService` que se conecta a internet:

```
public class Notificador {
    public void avisar(String msg) {
        GmailService service = new GmailService(); // Acoplamiento rígido
        service.send(msg);
    }
}
```

**Se pide:**

1. Refactorizá aplicando **Inyección de Dependencias** y **Dependencia de Abstracciones** para que el servicio sea testable.
2. Implementá un **Fake Object** y escribí un test que verifique que el mensaje enviado es el correcto sin usar internet.

---

### **PUNTO 3: Polimorfismo vs. Condicionales**

Refactorizá el siguiente método para eliminar los `if` usando polimorfismo:

```
public double calcularSueldo(Empleado e) {
    if (e.tipo().equals("GERENTE")) {
        return e.base() + 5000;
    } else if (e.tipo().equals("CADETE")) {
        return e.base() + 1000;
    }
    return e.base();
}
```

---

### **PUNTO 4: Diseño en Capas (Layering)**

En el ejercicio 1 del TP 4, tenías un `JFrame` que hacía validaciones y guardaba en la BD. **Se pide:** Explicá qué es un **Humble Object** (como la vista refactorizada) y por qué las validaciones de negocio deben ir en el **Modelo de Dominio** y no en la UI.

¿Querés empezar resolviendo el **Punto 1** o preferís que profundicemos en la teoría de alguno antes?