---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

# ¿Qué Es “Tell, don’t ask”?

Es un **principio de diseño orientado [[POO - Programación Orientada a Objetos|a objetos]]** que dice:

> **En lugar de preguntarle a un objeto por sus datos para tomar una decisión afuera, dile al objeto qué hacer.**

---

## 🚫 El Enfoque Que Rompe la Regla (Ask then Tell)

```java
class Cuenta {
    private double saldo;

    public double getSaldo() { return saldo; }
    public void setSaldo(double saldo) { this.saldo = saldo; }
}

// Código de afuera
if (cuenta.getSaldo() >= 100) {
    cuenta.setSaldo(cuenta.getSaldo() - 100);
}
```

Acá el código externo:

1. **Pregunta** al objeto (`getSaldo()`).
2. Toma una decisión.
3. **Le dice qué hacer** (`setSaldo(...)`).

**Problema**:
- Se rompe el encapsulamiento.
- La lógica de negocio está fuera de la clase.
- Si mañana cambia la regla, hay que modificar todo el código cliente.
---

## ✅ El Enfoque Correcto (Tell, don’t ask)

```java
class Cuenta {
    private double saldo;

    public void extraer(double monto) {
        if (saldo >= monto) {
            saldo -= monto;
        } else {
            System.out.println("Fondos insuficientes");
        }
    }
}

// Código de afuera
cuenta.extraer(100);
```

Acá el objeto **recibe una orden (Tell)** y **decide internamente** cómo cumplirla.

- El código cliente no necesita saber cómo funciona `extraer`.
- La lógica queda encapsulada dentro de la clase.
- Si cambia la regla, se modifica solo dentro de `Cuenta`.

---

## 🔎 Relación Con [[Polimorfismo]] Y [[Method Lookup]]

- _Tell don’t ask_ funciona mejor cuando usás **polimorfismo**.
- Ejemplo:

    ```java
    List<Figura> figuras = Arrays.asList(new Circulo(), new Cuadrado());
    for (Figura f : figuras) {
        f.dibujar();   // simplemente "digo", no "pregunto qué tipo sos"
    }
    ```

- No pregunto “¿sos círculo o cuadrado?” para decidir cómo dibujar.
- Simplemente **envío el mensaje (`dibujar()`)** → y el **lookup dinámico** se encarga de que cada objeto ejecute lo que le corresponde.

---

✅ **En resumen:**  
_Tell don’t ask_ = **decile al objeto qué hacer, no le preguntes para hacerlo vos por él**.

- Evita romper encapsulamiento.
- Centraliza la lógica dentro de la [[Clase]].
- Se apoya en el [[Polimorfismo]] y el [[Method Lookup]].
