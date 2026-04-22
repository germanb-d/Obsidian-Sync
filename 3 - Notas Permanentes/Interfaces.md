---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---


![[java-interfaces-comparable-tutorial-slides.pdf]]

# Que Son?

En [[Java]] no se puede heredar de múltiples clases (`extends`), pero se puede implementar múltiples **interfaces**.  
Una interface es un contrato: un conjunto de métodos (sin implementación) y constantes agrupados bajo un nombre.  
Sirve para simular una “herencia múltiple de comportamiento”.

## Definición

```java
public interface UnaInter extends SuperInter1, SuperInter2 {
    // Métodos → implícitamente public y abstract
    void hacerAlgo();

    // Constantes → implícitamente public, static y final
    int MAX_VALOR = 100;
}
```

- Todos los métodos son **[[Modificadores - Nivel de Acceso#7. `abstract`|abstract]]** y **[[Modificadores - Nivel de Acceso#1. `public`|public]]** por defecto.
- Todas las constantes son **public [[Modificadores - Nivel de Acceso#`static final`|static final]]** por defecto.

## Implementación

```java
public class Pajaro implements Volador {
    public void volar() {
        System.out.println("El pájaro vuela");
    }
}
```

Una [[Clase]] puede implementar varias interfaces:

  ```java
   public class Perro implements Mascota, AnimalDomestico { ... }
  ``` 

Si no se implementan todos los métodos → la clase debe declararse **abstract**.

---

# Uso De Interfaces

- Permite **identificar comportamientos comunes** entre clases no relacionadas.
- Facilita el **[[Casting#Upcasting|upcasting]]**: tratar objetos diferentes como si fueran del tipo de la interface.

Ejemplo:

```java
Volador[] seresQueVuelan = new Volador[3];
seresQueVuelan[0] = new Pajaro();
seresQueVuelan[1] = new Avion();
seresQueVuelan[2] = new Murcielago();

for (Volador v : seresQueVuelan) {
    v.volar(); // cada uno usa su propia implementación
}
```

---

## Interfaces vs. Clases Abstractas

| Característica             | Interfaces                                                                                              | Clases Abstractas                                                             |
| -------------------------- | ------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Herencia**               | Una clase puede implementar **múltiples interfaces**                                                    | Una clase solo puede heredar de **una clase abstracta**                       |
| **Métodos**                | Implícitamente `public abstract` (sin implementación) _(desde Java 8 puede tener `default` y `static`)_ | Pueden ser abstractos (sin implementación) o concretos (con implementación)   |
| **Constantes / Atributos** | Solo constantes → implícitamente `public static final`                                                  | Pueden tener atributos con distintos modificadores (private, protected, etc.) |
| **Constructores**          | No pueden tener constructores                                                                           | Pueden tener constructores (para inicializar atributos comunes)               |
| **Uso principal**          | Definir un **contrato de comportamiento** común a clases no relacionadas                                | Definir una **superclase común** con código reutilizable y parcial            |
| **Ejemplo típico**         | `Volador`, `Comparable`, `Serializable`                                                                 | `FiguraGeometrica`, `Empleado`, `Animal`                                      |

---

# Notas Adicionales

- Desde [[Java]] 8, las interfaces permiten métodos **default** (con implementación) y métodos **static**.
- En la teoría (y en la cursada), las interfaces deben considerarse como **contratos sin implementación**.
     
