---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

# Definición

**Method Lookup** es el proceso de búsqueda que hace Java para determinar **qué implementación de un método ejecutar** cuando se invoca sobre un objeto.
- Siempre depende del **tipo dinámico** del objeto (la [[Clase]] real en memoria), no solo del tipo estático (el declarado en la variable).

> [!example] Ejemplo
>
> ```java
> Animal a = new Perro();
> a.sonido(); // ejecuta Perro.sonido(), no Animal.sonido()
> ```

---

## This Vs Super

- `this` = referencia al **objeto actual** (su tipo dinámico).
    - Al llamar `this.metodo()`, el lookup arranca en la subclase.
    - Si no lo encuentra, sube por la jerarquía hasta la superclase.
- `super` = referencia a la **superclase inmediata**.
    - `super.metodo()` busca directamente en el padre, ignorando la posible redefinición en la subclase.
    - Se usa para invocar implementaciones heredadas o constructores del padre.

> [!warning] A tener en cuenta
> En constructores, `super(...)` debe ser **la primera línea** obligatoriamente.  
> En métodos normales, `super.metodo()` puede ir en cualquier parte del cuerpo.

---

## Generalizar En El Padre

- Se hace por **reutilización de código o de concepto**.
- Si varias subclases repiten la misma secuencia de instrucciones, conviene definir ese método en la superclase.
- Así las subclases lo heredan directamente, sin necesidad de copiar/pegar el mismo código.

> [!example] Ejemplo
>
> ```java
> class Cuenta {
>     void validarMonto(double m) { ... } // común a todas las cuentas
> }
> 
> class CajaDeAhorro extends Cuenta { ... }
> class CuentaCorriente extends Cuenta { ... }
> ```

---

## Polimorfismo Y Method Lookup

- Gracias al [[Polimorfismo]], puedo enviar el **mismo [[POO - Programación Orientada a Objetos#Mensajes Y Métodos|mensaje]]** a distintos objetos y cada uno responderá con su propia versión del método.
- El lookup dinámico se encarga de decidir qué implementación correr.

> [!example] Ejemplo
>
> ```[[Java]]
> List<Animal> animales = List.of(new Perro(), new Gato());
> for (Animal a : animales) {
>     a.sonido(); // "Guau!" o "Miau!" según el objeto real
> }
> ```

Esto se relaciona con el principio **“Tell, don’t ask”**:

- No preguntes “qué tipo sos” para decidir qué hacer.
- Simplemente enviá el mensaje (llamá al método) y dejá que el objeto se encargue.
