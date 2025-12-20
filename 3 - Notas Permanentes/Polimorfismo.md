---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

# Polimorfismo

## Definición

- Capacidad de un objeto de **responder de distintas maneras** a un mismo mensaje (método).
- Permite **usar una misma interfaz** y que cada clase concreta tenga su propia implementación.

> [!example] Ejemplo
>
> ```java
> Animal a1 = new Perro();
> Animal a2 = new Gato();
> 
> a1.sonido(); // "Guau!"
> a2.sonido(); // "Miau!"
> ```

Mismo mensaje (`sonido()`), distinta respuesta según el objeto real.

---

### Tipos Principales En Java

**Polimorfismo de sobrecarga (Overloading):**
- Mismo nombre de método, distinta firma (parámetros distintos).
- Se resuelve en **compilación**.

> [!example] Ejemplo
>
>   ```java
>    int sumar(int a, int b);
>    double sumar(double a, double b);
>    ```

**Polimorfismo de sobreescritura (Overriding):**

- Una subclase redefine un método heredado.
- Se resuelve en **tiempo de ejecución** (dynamic dispatch).

> [!example] Ejemplo
>
>   ```java
>    class Animal { void sonido() {...} }
>    class Perro extends Animal { @Override void sonido() {...} }
>    ```

---

## Relación Con [[Method Lookup]]

- Cuando envío un mensaje (`obj.metodo()`), la JVM hace un **lookup dinámico**:
    
    1. Busca en la [[Clase]] del objeto real (tipo dinámico).
    2. Si no está, sube en la jerarquía de clases.

---

## Ventajas

- Reutilización de código.
- Flexibilidad y extensibilidad del sistema.
- Permite aplicar el principio [[Tell don't ask]] → le digo al objeto qué hacer sin preocuparme por su tipo concreto.
