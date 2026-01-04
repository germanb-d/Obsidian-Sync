---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

# ¿Qué Es Una Clase?

Una **clase** es un molde o plantilla que define las características ([[POO - Programación Orientada a Objetos#^a8ad8d|atributos]]) y comportamientos ([[POO - Programación Orientada a Objetos#^38a6db|métodos]]) que tendrán los objetos creados a partir de ella. Es la unidad fundamental de la [[POO - Programación Orientada a Objetos|programación orientada a objetos]] en [[Java]].

```java
public class Persona {
    // Atributos
    private String nombre;
    private int edad;
    
    // Constructor
    public Persona(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
    
    // Métodos
    public void saludar() {
        System.out.println("Hola, soy " + nombre);
    }
}
```

# Tipos De Clases

## 1. Clases Regulares (Top-level)

Son las clases normales que se definen en su propio [[archivo]] `.java`.

```java
public class Vehiculo {
    private String marca;
    private String modelo;
    
    public Vehiculo(String marca, String modelo) {
        this.marca = marca;
        this.modelo = modelo;
    }
    
   public void acelerar() {
        System.out.println("El " + marca + " " + modelo + " está acelerando");
    }
}
```

---

## 2. Clases Inner (Clases Internas)

### 2.1 Clases Inner No Estáticas

Definidas dentro de otra clase. Tienen acceso a todos los miembros de la clase contenedora, incluso los privados.

```java
public class ClaseContenedora {
    private String mensajePrivado = "Mensaje desde clase contenedora";
    
    // Clase inner no estática
    class ClaseInterna {
        public void mostrarMensaje() {
            // Puede acceder a miembros privados de la clase contenedora
            System.out.println(mensajePrivado);
        }
    }
    
    public void usarClaseInterna() {
        ClaseInterna inner = new ClaseInterna();
        inner.mostrarMensaje();
    }
}

// Uso desde otra clase
ClaseContenedora contenedora = new ClaseContenedora();
ClaseContenedora.ClaseInterna inner = contenedora.new ClaseInterna();
```

### 2.2 Ejemplo Práctico: Botón Con ActionListener

```java
import javax.swing.*;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;

public class VentanaPrincipal extends JFrame {
    private JButton boton;
    private int contador = 0;
    
    public VentanaPrincipal() {
        boton = new JButton("Hacer clic");
        boton.addActionListener(new MetodoBoton());
        add(boton);
    }
    
    // Clase inner que implementa ActionListener
    class MetodoBoton implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            contador++; // Puede acceder a variables de la clase contenedora
            System.out.println("Botón presionado " + contador + " veces");
        }
    }
    
    public void crearOtroBoton() {
        JButton otroBoton = new JButton("Otro botón");
        // Puedo reutilizar la clase inner
        otroBoton.addActionListener(new MetodoBoton());
    }
}
```

---

## 3. Clases Abstractas

Son clases que **no se pueden instanciar directamente** y están diseñadas para ser heredadas. Pueden contener métodos abstractos (sin implementación) y métodos concretos (con implementación).

```java
// Clase abstracta
public abstract class Animal {
    protected String nombre;
    protected int edad;
    
    // Constructor
    public Animal(String nombre, int edad) {
        this.nombre = nombre;
        this.edad = edad;
    }
    
    // Método concreto (con implementación)
    public void dormir() {
        System.out.println(nombre + " está durmiendo");
    }
    
    // Método abstracto (sin implementación)
    public abstract void hacerSonido();
    public abstract void moverse();
}

// Clase que hereda de la clase abstracta
public class Perro extends Animal {
    public Perro(String nombre, int edad) {
        super(nombre, edad);
    }
    
    // Implementación obligatoria del método abstracto
    @Override
    public void hacerSonido() {
        System.out.println(nombre + " dice: ¡Guau!");
    }
    
    @Override
    public void moverse() {
        System.out.println(nombre + " corre en cuatro patas");
    }
}

// Uso
// Animal animal = new Animal("Rex", 3); // ✗ Error - no se puede instanciar
Animal perro = new Perro("Max", 2); // ✓ Correcto
perro.hacerSonido(); // "Max dice: ¡Guau!"
perro.dormir(); // "Max está durmiendo"
```

### Características De Las Clases Abstractas:

- No se pueden instanciar con `new`
- Pueden tener constructores
- Pueden tener métodos abstractos y concretos
- Pueden tener variables de instancia
- Una clase que hereda debe implementar todos los métodos abstractos

---

## 4. Clases Estáticas (Static Classes)

### 4.1 Clases Top-level Estáticas

En Java, las clases principales **no pueden ser estáticas**, pero sí pueden tener **miembros estáticos**.

```java
public class Utilidades {
    // Método estático - pertenece a la clase, no a la instancia
    public static double calcularArea(double radio) {
        return Math.PI * radio * radio;
    }
    
    // Variable estática - compartida por todas las instancias
    public static int contadorInstancias = 0;
    
    // Bloque estático - se ejecuta una sola vez al cargar la clase
    static {
        System.out.println("Clase Utilidades cargada");
    }
    
    public Utilidades() {
        contadorInstancias++;
    }
}

// Uso
double area = Utilidades.calcularArea(5.0); // No necesita instancia
System.out.println(Utilidades.contadorInstancias); // Acceso directo
```

### 4.2 Clases Estáticas Anidadas (Static Nested Classes)

Se definen dentro de otra clase pero con la palabra clave `static`. No necesitan una instancia de la clase contenedora para ser creadas.

```java
public class ClaseContenedora {
    private static String mensajeEstatico = "Mensaje estático";
    private String mensajeInstancia = "Mensaje de instancia";
    
    // Clase estática anidada
    static class ClaseEstatica {
        public void mostrarMensaje() {
            System.out.println(mensajeEstatico); // ✓ Puede acceder
            // System.out.println(mensajeInstancia); // ✗ No puede acceder
        }
    }
    
    // Ejemplo práctico: Builder Pattern
    static class PersonaBuilder {
        private String nombre;
        private int edad;
        private String email;
        
        public PersonaBuilder setNombre(String nombre) {
            this.nombre = nombre;
            return this;
        }
        
        public PersonaBuilder setEdad(int edad) {
            this.edad = edad;
            return this;
        }
        
        public PersonaBuilder setEmail(String email) {
            this.email = email;
            return this;
        }
        
        public ClaseContenedora build() {
            return new ClaseContenedora(this);
        }
    }
    
    private ClaseContenedora(PersonaBuilder builder) {
        // Constructor privado que usa el builder
    }
}

// Uso
ClaseContenedora.ClaseEstatica estatica = new ClaseContenedora.ClaseEstatica();
estatica.mostrarMensaje();

// Uso del Builder Pattern
ClaseContenedora persona = new ClaseContenedora.PersonaBuilder()
    .setNombre("Juan")
    .setEdad(25)
    .setEmail("juan@email.com")
    .build();
```

---

## 5. Clases Anónimas

Se crean al instanciar una interfaz o extender una clase sin darle un nombre específico. **No se pueden reutilizar** porque no tienen nombre.

```java
import javax.swing.*;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;

public class EjemploClaseAnonima {
    public void crearBoton() {
        JButton boton = new JButton("Clic aquí");
        
        // Clase anónima que implementa ActionListener
        boton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println("¡Botón presionado con clase anónima!");
            }
        });
        
        // Esta implementación NO se puede reutilizar en otro lugar
        // porque no tiene nombre
    }
    
    // Si quiero el mismo comportamiento en otro botón, 
    // tengo que volver a escribir la clase anónima
    public void crearOtroBoton() {
        JButton otroBoton = new JButton("Otro botón");
        
        otroBoton.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                // Código duplicado - no hay reutilización
                System.out.println("¡Botón presionado con clase anónima!");
            }
        });
    }
}
```

|Tipo de variable|Acceso de lectura|Acceso de escritura|Debe ser final|
|---|---|---|---|
|**Variables de instancia**|✓ Sí|✓ Sí|✗ No|
|**Variables estáticas**|✓ Sí|✓ Sí|✗ No|
|**Variables locales**|✓ Sí|✗ No|✓ Sí (efectivamente)|
|**Parámetros**|✓ Sí|✗ No|✓ Sí (efectivamente)|

---

## 6. Clases Locales

Se definen dentro de un método. Solo son visibles dentro de ese método.

```java
public class EjemploClaseLocal {
    public void metodoConClaseLocal() {
        final String mensaje = "Mensaje local";
        
        // Clase local definida dentro del método
        class ClaseLocal {
            public void mostrarMensaje() {
                System.out.println(mensaje);
            }
        }
        
        // Solo se puede usar dentro de este método
        ClaseLocal local = new ClaseLocal();
        local.mostrarMensaje();
    }
}
```

---

# Comparación

| Aspecto                    | Clase Inner           | Clase Abstracta                       | Clase Estática              | Clase Anónima                                             |
| -------------------------- | --------------------- | ------------------------------------- | --------------------------- | --------------------------------------------------------- |
| **Instanciación**          | ✓ Se puede instanciar | ✗ No se puede instanciar directamente | ✓ Se puede instanciar       | ✓ Se instancia automáticamente                            |
| **[[Herencia]]**           | ✓ Puede heredar       | ✓ Diseñada para ser heredada          | ✓ Puede heredar             | ✓ Hereda o implementa                                     |
| **Reutilización**          | ✓ Se puede reutilizar | ✓ Se reutiliza por [[Herencia]]           | ✓ Se puede reutilizar       | ✗ No se puede reutilizar                                  |
| **Acceso a clase externa** | ✓ Acceso completo     | N/A                                   | ✗ Solo a miembros estáticos | ✓ Acceso a variables final/effectively final y atributos. |
| **Nombre**                 | Tiene nombre          | Tiene nombre                          | Tiene nombre                | No tiene nombre                                           |
| **Uso principal**          | Encapsulación interna | Plantillas/contratos                  | Utilidades independientes   | Implementaciones rápidas                                  |

## Ejemplo Completo: Todos Los Tipos De Clases

```java
import javax.swing.*;
import java.awt.event.ActionListener;
import java.awt.event.ActionEvent;

// Clase abstracta
abstract class Figura {
    protected String color;
    
    public Figura(String color) {
        this.color = color;
    }
    
    public void pintar() {
        System.out.println("Pintando de color " + color);
    }
    
    public abstract double calcularArea();
}

// Clase regular que hereda de abstracta
class Circulo extends Figura {
    private double radio;
    
    public Circulo(String color, double radio) {
        super(color);
        this.radio = radio;
    }
    
    @Override
    public double calcularArea() {
        return Math.PI * radio * radio;
    }
}

// Clase principal con diferentes tipos de clases internas
public class EjemploCompleto extends JFrame {
    private static int contadorEstatico = 0;
    private int contadorInstancia = 0;
    
    public EjemploCompleto() {
        setLayout(new java.awt.FlowLayout());
        
        // Usando clase inner
        JButton botonInner = new JButton("Clase Inner");
        botonInner.addActionListener(new ManejadorInner());
        
        // Usando clase anónima
        JButton botonAnonimo = new JButton("Clase Anónima");
        botonAnonimo.addActionListener(new ActionListener() {
            @Override
            public void actionPerformed(ActionEvent e) {
                System.out.println("Botón anónimo presionado");
            }
        });
        
        // Usando clase estática anidada
        CalculadoraEstatica calc = new CalculadoraEstatica();
        JButton botonCalcular = new JButton("Calcular");
        botonCalcular.addActionListener(e -> {
            double resultado = calc.sumar(5.0, 3.0);
            System.out.println("Resultado: " + resultado);
        });
        
        add(botonInner);
        add(botonAnonimo);
        add(botonCalcular);
        
        // Usando clase abstracta
        Figura circulo = new Circulo("rojo", 5.0);
        circulo.pintar();
        System.out.println("Área del círculo: " + circulo.calcularArea());
        
        setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        pack();
    }
    
    // Clase inner no estática
    class ManejadorInner implements ActionListener {
        @Override
        public void actionPerformed(ActionEvent e) {
            contadorInstancia++; // Puede acceder a variables de instancia
            System.out.println("Contador instancia: " + contadorInstancia);
        }
    }
    
    // Clase estática anidada
    static class CalculadoraEstatica {
        public double sumar(double a, double b) {
            contadorEstatico++; // Solo puede acceder a miembros estáticos
            return a + b;
        }
    }
    
    // Método con clase local
    public void metodoConClaseLocal() {
        final String mensaje = "Clase local";
        
        class ClaseLocal {
            public void mostrar() {
                System.out.println(mensaje);
            }
        }
        
        ClaseLocal local = new ClaseLocal();
        local.mostrar();
    }
    
    public static void main(String[] args) {
        SwingUtilities.invokeLater(() -> {
            new EjemploCompleto().setVisible(true);
        });
    }
}
```
