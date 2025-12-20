---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

![[java-interfaces-comparable-tutorial-slides.pdf]]

# Interfaces `Comparable` Y `Comparator`

## `Comparable`

- (java.lang.Comparable)
- Hace que los objetos de una [[Clase]] sean **comparables entre sí**.
- Define un **orden natural** para los objetos.
- Tiene **un solo método**:

```java
public int compareTo(T o);
```

**Retorno**:
- `0` → son iguales
- `<0` → el objeto actual es menor
- `>0` → el objeto actual es mayor

> [!example] Ejemplo
>
> ```java
> public class Persona implements Comparable<Persona> {
>     private String nombre;
>     private int edad;
> 
>     public Persona(String n, int e) {
>         nombre = n;
>         edad = e;
>     }
> 
>     @Override
>     public int compareTo(Persona otra) {
>         return this.edad - otra.edad; // ordena por edad
>     }
> 
>     public String toString() {
>         return nombre + " (" + edad + ")";
>     }
> }
> 
> // Uso
> Persona[] personas = {
>     new Persona("Ana", 20),
>     new Persona("Luis", 18),
>     new Persona("Maria", 25)
> };
> Arrays.sort(personas); // ordena por edad
> ```

Una clase `Comparable` solo puede tener **un criterio de comparación** (el del `compareTo`).

---

## `Comparator`

- (java.util.Comparator)
- Permite definir **distintos criterios de comparación** externos a la clase.
- Tiene **un método**:

```java
public int compare(T o1, T o2);
```

**Retorno**:
- `0` → iguales
- `<0` → `o1` < `o2`
- `>0` → `o1` > `o2`

> [!example] Ejemplo
>
> ```java
> class ComparadorPorNombre implements Comparator<Persona> {
>     @Override
>     public int compare(Persona p1, Persona p2) {
>         return p1.nombre.compareTo(p2.nombre);
>     }
> }
> 
> class ComparadorPorEdad implements Comparator<Persona> {
>     @Override
>     public int compare(Persona p1, Persona p2) {
>         return p1.edad - p2.edad;
>     }
> }
> 
> // Uso
> Arrays.sort(personas, new ComparadorPorNombre()); // ordena por nombre
> Arrays.sort(personas, new ComparadorPorEdad());   // ordena por edad```

Con `Comparator` puedo tener múltiples formas de ordenar la misma clase.

---

# Diferencias

|Aspecto|`Comparable`|`Comparator`|
|---|---|---|
|Paquete|`java.lang`|`java.util`|
|Método|`compareTo(T o)`|`compare(T o1, T o2)`|
|Dónde se define|Dentro de la clase|En una clase externa|
|Orden|Define el **orden natural** de los objetos|Permite **distintos criterios**|
|Cantidad de criterios|Solo uno|Varios, según comparadores distintos|

---

# Puntos Importantes

- `String`, `Integer`, `Double` y muchas clases de Java ya implementan `Comparable`.
- `Arrays.sort()` y `Collections.sort()` usan `Comparable` si la clase lo implementa.
- Para ordenar de distintas maneras, usamos `Comparator` y lo pasamos como segundo parámetro en `sort()`.

## `Comparator` Usa `Comparable`?

La respuesta corta es: **No, no hace falta que tu clase implemente `Comparable` para usar un `Comparator`.**

---

### Relación Entre `Comparable` Y `Comparator`

#### `Comparable`

- Se implementa **dentro de la clase**.
- Define el **orden natural** de los objetos.
- Ejemplo: `String` y `Integer` ya implementan `Comparable`.
- Si hacés `Arrays.sort(personas)` → Java busca si `Persona` implementa `Comparable`.
    - Si lo implementa → usa el `compareTo()`.
    - Si no lo implementa → error en tiempo de ejecución.

---

#### `Comparator`

- Es una **clase externa** que define cómo comparar **dos objetos**.
- No depende de que la clase implemente `Comparable`.
- Se pasa como parámetro a `Arrays.sort()` o `Collections.sort()`.

```java
Arrays.sort(personas, new ComparadorPorNombre());
```

Esto funciona aunque `Persona` **no tenga compareTo()**.

---

### Ejemplo Sin `Comparable`

```java
class Persona {
    String nombre;
    int edad;

    Persona(String n, int e) {
        nombre = n;
        edad = e;
    }

    public String toString() {
        return nombre + " (" + edad + ")";
    }
}

// Comparator externo (no hace falta que Persona implemente Comparable)
class ComparadorPorEdad implements Comparator<Persona> {
    @Override
    public int compare(Persona p1, Persona p2) {
        return p1.edad - p2.edad;
    }
}

public class Test {
    public static void main(String[] args) {
        Persona[] personas = {
            new Persona("Ana", 20),
            new Persona("Luis", 18),
            new Persona("Maria", 25)
        };

        // Ordenar con Comparator
        Arrays.sort(personas, new ComparadorPorEdad());

        for (Persona p : personas) {
            System.out.println(p);
        }
    }
}
```

**Resultado:**

```
Luis (18)
Ana (20)
Maria (25)
```

---

# Conclusión Importante

- `Comparable` → tu clase debe implementarlo si querés un **orden natural único**.
- `Comparator` → no requiere modificar tu clase, podés definir **muchos criterios externos**.
- Podés combinarlos:
    - Definir un `compareTo` por defecto en la clase (ej. por `id`).
    - Crear `Comparator` externos para otros criterios (ej. por `nombre`, por `edad`).

---

<u>Regla práctica</u>

- Si tu clase **tiene un único criterio obvio** de orden (ej: `Integer`, `String`, `Fecha`) → usá `Comparable`.
- Si tu clase puede ordenarse de varias formas (ej: `Persona` → por nombre, edad, apellido, etc.) → usá `Comparator`.
