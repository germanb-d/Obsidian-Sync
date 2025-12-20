---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

# Definición

Es un **paradigma de programación** que organiza el software mediante **objetos** que modelan conceptos del mundo real. Cada objeto tiene:

- **Estado** → representado por sus atributos (datos). ^a8ad8d
- **Comportamiento** → definido por sus métodos (acciones). ^38a6db
- **Identidad** → es único, incluso si dos objetos tienen los mismos valores.
	- Aun si ambas tazas fueran de café con 150 de volumen y 100 de cantidad, ambas tendrían los mismos atributos y métodos, pero seguirían siendo dos objetos diferentes ^kfgnea

> La POO permite pensar el sistema como una colección de "cosas" que interactúan, en vez de funciones o procesos aislados.

---

## Dominio Del Problema

El **dominio** es el conjunto de conceptos y relaciones del **mundo real** que el sistema debe representar.

Ejemplo: En un sistema hospitalario:

- Entidades: `Paciente`, `Médico`, `Cita`
- Relaciones: un médico atiende pacientes
- Reglas de negocio: un paciente no puede agendar sin médico asignado

> Comprender bien el dominio es clave para crear clases y objetos representativos.

---

## Abstracción

La **abstracción** consiste en **reducir la complejidad** ocultando los detalles innecesarios y enfocándose en lo relevante.

Por ejemplo, un “Auto” puede ser visto como:

- Un conjunto de piezas (fabricante)
- Un medio de transporte (usuario)
- Un objeto con velocidad y dirección (simulador)

Cada enfoque depende del **contexto** y define qué atributos y métodos se incluyen.

> La abstracción ayuda a trabajar con conceptos generales sin preocuparnos por los detalles internos.

---

# Objeto

Un **objeto** es una unidad que representa una entidad concreta o abstracta del dominio.

Tiene:

- **Atributos**: características o datos internos (ej: nombre, edad). ^62e845
- **Métodos**: acciones que puede realizar (ej: hablar, caminar).

Ejemplo: Objeto “Taza”

- **Atributos**: capacidad, contenido, color.
- **Métodos**: `llenar()`, `vaciar()`, `beber().`

📌 **Identidad**: Dos objetos pueden tener los mismos atributos, pero son distintos si ocupan lugares diferentes en la memoria.

> [!cite] 1º Principio de programación orientado a objetos
> Un programa orientado a objetos, está organizado como una comunidad de agentes interactuando, llamados objetos. Cada objeto cumple un rol. Cada objeto provee un servicio o ejecuta una acción, que es usada por otros miembros de la comunidad.

---

## Encapsulamiento

Es la práctica de **ocultar los detalles internos** de un objeto y exponer solo lo necesario a través de interfaces (métodos públicos).

Ventajas:

- Seguridad de datos
- Mantenimiento más simple
- Control sobre cómo se accede y modifica el estado

También se basa en el envío de **mensajes** entre objetos, donde uno le “pide” a otro que realice una acción (ej: `objeto.metodo()`).

> [!cite] 2º Principio de programación orientado a objetos
> El encapsulamiento y el ocultamiento de información se complementan, para aislar las diferentes partes de un sistema, permitiendo que el código sea modificado, extendido y que se puedan corregir errores, sin el riesgo de producir efectos colaterales no intencionados.
> Los objetos ponen en práctica estos dos conceptos:
> 1. Se abstrae la funcionalidad y la información relacionada y se encapsulan en un objeto. Este principio basico es llamado [[Tell don't ask]]
> 2. Se decide que funcionalidad e información, podrá ser requerida por otros objetos y el resto se oculta.

---

# Mensajes Y Métodos

> [!cite] 3º Principio de programación orientado a objetos
> Una acción es iniciada cuando un objeto, el emisor, envía un mensaje a un agente responsable de la acción, el receptor. El mensaje representa el requerimiento y es acompañado por información adicional (argumentos) necesaria para cumplir el
> requerimiento. El receptor es el objeto a quien se le envía el mensaje. El receptor en respuesta al mensaje ejecutará un conjunto de acciones o método para satisfacer el requerimiento. ^q7fhfj

Ejemplo:

Juan hace un primer requerimiento al telefonista, quien hace otro requerimiento que conduce a más y más requerimientos, hasta que se resuelve el problema: la pizza le llega a Juan!.

![[POO (Programación Orientada a Objetos)-1758841657865.webp]]

## Mensajes Y Métodos vs. Llamadas a Procedimiento

### Llamadas a Procedimiento (programación estructurada)

- Cuando invocas un procedimiento o función, **no hay receptor**.
- Simplemente, el programa va a ejecutar esas instrucciones.

```c
printf("Hola mundo");
```

Aquí llamamos a `printf` → no hay "objeto receptor", es solo una llamada directa a una función.

---

### Mensajes Y Métodos (POO)

- Siempre hay un **objeto receptor** que recibe el mensaje.
- Tú (emisor) envías un **mensaje** (que en código es una llamada a método con argumentos).
- El objeto receptor decide **cómo interpretar ese mensaje** (qué método usar).
- La respuesta **depende del objeto** que lo reciba.

Ejemplo en Java:

```java
class Telefonista {
    void pedirPizza(String tipo) {
        System.out.println("Ok, pido la pizza de " + tipo);
    }
}

class Doctor {
    void pedirPizza(String tipo) {
        System.out.println("¿Pizza? No entiendo...");
    }
}

// Emisor
public class Main {
    public static void main(String[] args) {
        Telefonista t = new Telefonista();
        Doctor d = new Doctor();

        t.pedirPizza("muzzarella"); // OK
        d.pedirPizza("muzzarella"); // Confusión/Error
    }
}
```

### Relación Con la Imagen

![[POO (Programación Orientada a Objetos)-1758841854283.webp]]

- **Juan (emisor)** manda un **mensaje**: "quiero una pizza".
- Si el receptor es el **telefonista de la pizzería**, entiende y responde: **"OK!"** ✅
- Si el receptor es el **doctor**, no sabe qué hacer → **Error** ❌

La clave es que:

- En **POO** el **mensaje** es siempre el mismo (ej. `pedirPizza("muzzarella")`), pero el **método que se ejecuta depende del receptor** (objeto).

---

✅ En conclusión:

- **Procedimiento** = instrucción directa, sin receptor.
- **Mensaje** = se manda a un objeto, y ese objeto decide qué método usar.
