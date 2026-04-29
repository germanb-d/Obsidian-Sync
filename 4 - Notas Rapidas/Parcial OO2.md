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



---


Parcial de Ejemplo

PUNTO 1

Dado el siguiente código:

public class Controlador { private Collection<Juez> jueces;

```
public int calcularCausasTotales() {
    int cantidadCausas = 0;
    for (Juez juez : jueces) {
        for (Causa causa : juez.causas()) {
            cantidadCausas += 1;
        }
    }
    return cantidadCausas;
}
``` 

}

public class Juez { private String nombre; private String apellido; private Collection<Causa> causasACargo;

```
public void agregarCausa(Causa causa) {
    this.causasACargo.add(causa);
}
```

}

Se pide: Refactorice aplicando tell don’t ask. Escriba un test que verifique que el método calcularCausasTotales() funcione.

PUNTO 2

La siguiente clase Clima tiene un método climaEn que recibe una fecha y retorna un record con el tipo de clima (un string que puede ser SOLEADO, NUBLADO, etc) y un entero que representa la velocidad del viento. Para ello se utiliza la librería open source WeatherOnline que consume un servicio web para recuperar esa información de la nube/Web. Esta dependencia no nos permite testear en forma automatizada el método climaEn sin invocar realmente a la librería.

Se pide: a. Refactorice la clase Clima aplicando inyección de dependencias y depender de abstracciones de forma que sea posible inyectar un fake que permita hacer el método testable en forma automatizada. b. Modifique el Main para que siga funcionando de forma correcta, con la invocación al servicio del clima real.

public record ClimaValor(String tipo, Integer velocidadViento) { } interfaz ClimaOnline { String clima(fecha); }

public Weather implements CLimaOnline { public String clima(fecha) {

} }

public class Clima { private ClimaOnline climaOnline; public Clima(ClimaOnline online) { this.climaOnline = online; }

```
public ClimaValor climaEn(LocalDate fecha) {
    String clima = this.climaOnline.clima(fecha); //new WeatherOnline().getWeather(fecha);
    //clima = "SOLEADO|25"
    String[] tipoYNudos = clima.split("|");
    return new ClimaValor(tipoYNudos[0], Integer.valueOf(tipoYNudos[1]));
}
```

}

public class Main { public static void main(String[] args) { var c = new Clima(); var tipoYViento = c.climaEn(LocalDate.of(2024, 05, 10)); System.out.println("Tipo: " + tipoYViento.tipo()); System.out.printl n("Velocidad: " + tipoYViento.tipo()); } }

Además, se pide escribir un test que verifique el funcionamiento de Clima.climaEn() forzando un valor de retorno del servicio de WeatherOnline de “NUBLADO|26” mediante el uso de un fake.

PUNTO 3

La siguiente clase Producto calcula el precio de un producto teniendo en cuenta impuestos, descuentos y envío. Luego se presenta un Main para mostrar cómo se utiliza. Se pide: a. Refactorizar para remover los IFs sobre los tipos de producto aplicando polimorfismo. Verificar de no romper el funcionamiento luego del refactor. b. Modifique el main para que funcione de acuerdo al refactor realizado.

enum TipoProducto { LIBRO, ALIMENTO }

class Producto { public CategoriaProducto tipo; public double precio;

```
public Producto(TipoProducto tipo, double precio) {
    this.tipo = tipo;
    this.precio = precio;
}

public double precioFinal(double descuentoInicial) {
    double impuestos = 0;
    boolean envioGratis = false;
    double descuento = descuentoInicial;
    if (tipo == TipoProducto.LIBRO) {
        impuestos = 0.1;
        if (precio > 100) {
            envioGratis = true;
        }
    } else if (tipo == TipoProducto.ALIMENTO) {
        impuestos = 0.05;
        if (precio > 100) {
            descuento = descuento + 0.15;
        }
        if (precio > 200) {
            envioGratis = true;
        }
    } 
   
    double total = precio * (1 + impuestos) * (1 - descuento);
    if (envioGratis) {
        total -= 10;
    }

    return total;
}
```

}

public class Main { public static void main(String[] args) { var p 1 = new Producto(TipoProducto.LIBRO, 30); var p 2 = new Producto(TipoProducto.ALIMENTO, 130); System.out.println(p 1.precioFinal(10)); System.out.println(p 2.precioFinal(10)); } }