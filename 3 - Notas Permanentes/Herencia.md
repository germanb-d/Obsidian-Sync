---
Categoria: Sistemas
Materia: Orientación a Objetos
tags:
  - Teoria
---

# Conceptos Básicos

- **Herencia** y **composición** permiten reutilizar código y estructurar mejor los programas.
- **Herencia simple**: una [[Clase]] hereda de una sola clase padre.
- **Herencia múltiple**: una clase hereda de más de un padre (no permitida con clases en [[Java]], sí con interfaces).
- **Herencia transitiva**: una subclase hereda todo lo que sus clases padre y abuelo tienen.

## Test "es un" (is-a)

Verifica si una relación de herencia es válida:

- Un pájaro **es un** animal → SI
- Un pastel **es una** manzana → NO
- Un gato **es un** mamífero → SI
- Un motor **es un** coche → NO

## Buen Diseño

- Si `Alumno` y `Docente` comparten características, no deben convertirse entre sí. En su lugar, crear una superclase como `Persona`.
- *Evita crear muchas subclases si no es necesario*.

### Ventajas De Usar Herencia

- Reutilización de codigo.
- Mejora la organización del diseño orientado a objetos.

---

## Sobrescritura (Override)

- Permite redefinir el comportamiento de un método heredado.
- Métodos como `toString()` o `equals()` pueden y deben sobrescribirse correctamente.
- **`equals()` Personalizado** compara objetos por contenido, no por referencia.
- Las subclases pueden sobrescribir métodos del padre para agregar o cambiar comportamiento.

### Importante:

- Crear un objeto del **padre** → solo accede a lo definido en el padre.
- Crear un objeto de una **subclase** → accede a lo del padre **y** lo propio.
- Las **variables** no se sobrescriben, solo se ocultan si se declaran de nuevo en la subclase.

---

## Palabras Clave

- **`extends`**: indica que una clase hereda de otra.

```java
public class CuentaAhorros extends Cuenta {
    // CuentaAhorros hereda todo lo público y protegido de Cuenta
}
```

- **`this`**: referencia al objeto actual (subclase).
- **`super`**:
    - Accede a métodos o atributos de la clase padre.
    - Se usa para llamar al constructor del padre desde la subclase.

O sea por ejemplo en vez de hacer:

``` java
public CuentaAhorros(float saldo, float tasaAnual) {
    this.saldo = saldo;
    this.tasaAnual = tasaAnual;
}
```

Se busca hacer:

```java
public CuentaAhorros(float saldo, float tasaAnual) {
    super(saldo, tasaAnual);  // Llama al constructor de Cuenta
}
```

---

### Constructores Heredados

- Los constructores **no se heredan**.
- Si no definís uno en la subclase, Java crea un constructor vacío por defecto.
- Para **reutilizar el constructor del padre**, usa `super(...)`.
- Para reutilizar otro constructor de la misma clase, usa `this(...)`.

#### Orden De Ejecución En la Jerarquía:

1. Se ejecutan primero los constructores del padre hacia la subclase.
2. Luego se ejecutan las instrucciones propias de la subclase.
    
