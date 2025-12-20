---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

El **casting** forma parte de un mismo concepto general dentro de la  [[POO - Programación Orientada a Objetos]].  Este se divide en:

- **Upcasting** → Subclase → Superclase (automático, seguro).
- **Downcasting** → Superclase → Subclase (manual, peligroso si no se comprueba).

---

# Upcasting

- Es cuando tratamos un objeto de una **subclase** como si fuera de su **superclase**.
- Siempre es **seguro** porque una subclase _es un tipo de_ la superclase.
- Ocurre automáticamente (casting implícito).

## Ejemplo En[[Java]]:

```java
class Animal {
    void hacerSonido() { System.out.println("Algún sonido"); }
}

class Perro extends Animal {
    void hacerSonido() { System.out.println("Guau"); }
    void moverCola() { System.out.println("Moviendo la cola"); }
}

public class Main {
    public static void main(String[] args) {
        Animal a = new Perro(); // Upcasting
        a.hacerSonido(); // "Guau" (se usa el método del Perro gracias al polimorfismo)
        // a.moverCola(); // ❌ Error: no visible, porque 'a' se trata como Animal
    }
}
```

👉 **Idea:** Podés usar al objeto como su [[Clase]] padre, pero perdés acceso directo a los métodos específicos de la subclase.

---

# Downcasting

- Es cuando tratamos un objeto de la **superclase** como si fuera de una **subclase**.
- **No es seguro** automáticamente → requiere casting explícito.
- Solo funciona si el objeto **realmente es una instancia de la subclase**, de lo contrario lanza error en tiempo de ejecución (`ClassCastException`).

## Ejemplo En Java:

```java
Animal a = new Perro(); // realmente es un Perro
Perro p = (Perro) a;    // Downcasting
p.moverCola();          // ✅ ahora podemos usar métodos propios de Perro
```

👉 **Idea:** Permite recuperar las funcionalidades específicas de la subclase.
