---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

# Modificadores Principales En [[Java]]

## 1. `public`

- **Acceso total**: cualquier clase, paquete o subclase puede acceder.
- Se usa en clases, atributos, métodos y constructores.

```java
public class Persona {
    public String nombre;  // accesible desde cualquier lugar
}
```

✅ Útil cuando el miembro debe ser visible globalmente.  
⚠️ Usar con cuidado: puede romper el encapsulamiento si exponés atributos directamente.

---

## 2. `protected`

- Acceso desde:
    - el mismo paquete
    - **subclases** (incluso si están en otro paquete).
- No accesible desde clases externas que no hereden.

```java
class Animal {
    protected void comer() {
        System.out.println("El animal come");
    }
}

class Perro extends Animal {
    public void mostrar() {
        comer(); // permitido porque es subclase
    }
}
```

✅ Útil para dar acceso controlado a subclases.

---

## 3. `default` (package-private)

- Es el nivel de acceso **por defecto** cuando no se escribe nada.
- Accesible solo dentro del **mismo paquete**.

```java
class Persona {   // default, no puse public
    String direccion; // default, accesible solo en el paquete
}
```

✅ Útil para encapsular dentro de un paquete.  
⚠️ No confundir con la palabra reservada `default` de `switch`.

---

## 4. `private`

- Accesible solo dentro de la **misma clase**.
- Ni siquiera las subclases pueden usarlo directamente.

```java
public class Cuenta {
    private double saldo;

    public void depositar(double monto) {
        saldo += monto; // permitido porque estoy en la misma clase
    }
}
```

✅ Útil para **encapsulación** (ocultar implementación interna).

---

## 5. `static`

- El miembro pertenece a la **clase**, no a los objetos.
- Se accede sin crear instancias.
- Compartido entre todos los objetos de la clase.

```java
public class Contador {
    public static int total = 0;

    public Contador() {
        total++; // aumenta al crear cada objeto
    }
}

System.out.println(Contador.total); // acceso sin objetos
```

✅ Útil para atributos/métodos comunes a todas las instancias.  
⚠️ Cuidado: al ser compartido, un cambio afecta a todos los objetos.

---

## 6. `final`

- Significa **no modificable**.
- Aplica de distintas formas:
    - **Variable/atributo**: no se puede reasignar.
    - **Método**: no se puede sobreescribir.
    - **Clase**: no se puede heredar.

```java
// variable final
final int numero = 5;

// método final
class Animal {
    public final void respirar() {
        System.out.println("Respira aire");
    }
}

// clase final
public final class Utilidad {}
```

✅ Útil para definir **constantes** (usualmente junto a `static`).  
⚠️ Una variable `final` debe inicializarse una sola vez.

---

## 7. `abstract`

- **Clase abstracta**: no puede instanciarse, sirve de base para otras clases.
- **Método abstracto**: solo tiene firma, las subclases deben implementarlo.

```java
abstract class Figura {
    abstract double area(); // cada subclase implementa su versión
}

class Circulo extends Figura {
    double radio;
    Circulo(double r) { radio = r; }

    @Override
    double area() {
        return Math.PI * radio * radio;
    }
}
```

✅ Útil para generalizar comportamiento.  
⚠️ Si una clase tiene al menos un método `abstract`, debe declararse `abstract`.

---

# Diferencias Clave

|Modificador|Aplica a|Qué significa|
|---|---|---|
|`public`|clase, método, atributo|Visible desde cualquier parte del programa.|
|`protected`|método, atributo|Visible en el mismo paquete y en subclases.|
|`default`|clase, método, atributo|Visible solo dentro del mismo paquete.|
|`private`|método, atributo|Visible solo dentro de la misma clase.|
|`static`|método, atributo|Pertenece a la clase, no a las instancias.|
|`final`|clase, método, atributo|Inmutable / no se puede sobrescribir / no se puede heredar.|
|`abstract`|clase, método|Debe ser implementado en subclases; no puede instanciarse.|

---

## Reglas Prácticas

- Usa `private` en atributos + getters/setters para **encapsulación**.
- Usa `protected` si querés que las subclases accedan directamente.
- Usa `static final` para **constantes**.
- Usa `abstract` para forzar a las subclases a implementar un comportamiento común.

Muy buena pregunta 👌

El combo `static final` es **muy usado** en Java y tiene un propósito distinto que usar `static` o `final` por separado.

---

# `static final`

## ¿Qué Significa?

- **`static`** : El atributo pertenece a la **clase** (no a los objetos).
- **`final`** : El atributo no puede ser modificado (es constante).
- Juntos: Definen una **constante global** accesible sin necesidad de instanciar la clase.

```java
public class Matematica {
    // Constante accesible desde cualquier parte
    public static final double PI = 3.14159;
    
    // Constante "mensaje" 
    public static final String MENSAJE = "Hola mundo";
}

class Prueba {
    public static void main(String[] args) {
        // Acceso sin crear objetos
        System.out.println(Matematica.PI);
        System.out.println(Matematica.MENSAJE);
    }
}
```

Al estar en `public static final`:

- `public` → accesible desde cualquier parte.
- `static` → pertenece a la clase (se accede como `Clase.CONSTANTE`).
- `final` → valor fijo, no se puede cambiar.

## Diferencia Con Usar Solo Uno

| Modificador    | Qué hace solo                                   | Qué pasa con una constante                 |
| -------------- | ----------------------------------------------- | ------------------------------------------ |
| `static`       | Compartido entre instancias. Puede modificarse. | No es constante, solo un valor global.     |
| `final`        | Inmutable, pero cada objeto tiene su copia.     | No es global, cada objeto guarda su valor. |
| `static final` | Único valor global e inmutable.                 | Constante verdadera.                       |

```java
class Ejemplo {
    static int contador = 0;       // compartido, modificable
    final int id;                  // inmutable, pero distinto en cada objeto
    static final String APP = "UNRN"; // constante global
    
    Ejemplo(int id) {
        this.id = id;
        contador++;
    }
}

public class Main {
    public static void main(String[] args) {
        Ejemplo e1 = new Ejemplo(1);
        Ejemplo e2 = new Ejemplo(2);
        
        System.out.println(Ejemplo.contador); // 2 (compartido y cambió)
        System.out.println(e1.id);            // 1 (inmutable, propio de e1)
        System.out.println(e2.id);            // 2 (inmutable, propio de e2)
        System.out.println(Ejemplo.APP);      // UNRN (constante global)
    }
}
```
