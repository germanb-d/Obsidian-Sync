---
Categoria: Sistemas
Materia: Introduccion a las Bases de Datos
tags:
  - BaseDeDatos
  - Teoria
  - Definicion
---

# ¿Qué Es Un Campo?

Un **campo** es la unidad básica de información dentro de un [[Registro]] en una base de datos. Representa un atributo específico de la entidad que se está almacenando y contiene un tipo particular de dato.

**Características fundamentales de un campo:**
- Es la menor unidad de datos con significado propio dentro de un registro
- Tiene un nombre que lo identifica (como "nombre", "edad", "salario")
- Tiene un tipo de dato específico (texto, número, fecha, etc.)
- Almacena un valor concreto para cada registro

**Ejemplo conceptual:** En un *registro* de "Empleado", los campos podrían ser:

- Campo "ID": contiene el número identificador
- Campo "Nombre": contiene el nombre de la persona
- Campo "Salario": contiene el monto del salario
- Campo "Fecha_ingreso": contiene la fecha de contratación

# Campo Fijo

Un **campo fijo** es aquel que tiene un tamaño predeterminado y constante, independientemente de la cantidad real de datos que contenga.

## Características Del Campo Fijo:

**Tamaño constante:**

- Se asigna un número específico de bytes al campo
- Siempre ocupa exactamente ese espacio, sin importar el contenido
- Si los datos son menores, se rellenan con espacios o caracteres nulos
- Si los datos son mayores, se truncan o rechazan

**Ubicación predecible:**

- Su posición dentro del registro es siempre la misma
- Se puede acceder directamente usando un offset calculado

## Ejemplos De Campos Fijos:

```
Campo "Código_Producto" (10 caracteres fijos):
Producto A: "PROD001   " (7 caracteres + 3 espacios)
Producto B: "PROD002   " (7 caracteres + 3 espacios)

Campo "Precio" (8 caracteres fijos para formato decimal):
Precio A: "00125.50" 
Precio B: "01500.00"

Campo "Fecha" (10 caracteres fijos formato YYYY-MM-DD):
Fecha A: "2025-01-15"
Fecha B: "2025-12-31"
```

## Ventajas De Los Campos Fijos:

- **Acceso directo**: Puedes calcular exactamente dónde está cualquier campo
- **Simplicidad**: Fácil implementación y manejo
- **Rendimiento**: Operaciones más rápidas de lectura y escritura
- **Alineación**: Mejor uso de la memoria y cache del procesador

## Desventajas De Los Campos Fijos:

- **Desperdicio de espacio**: Si los datos reales son menores al tamaño asignado
- **Limitación**: No pueden almacenar datos que excedan el tamaño predefinido
- **Inflexibilidad**: Cambiar el tamaño requiere modificar toda la estructura

# Campo Variable

Un **campo variable** es aquel que puede cambiar de tamaño según la cantidad de datos que necesite almacenar en cada registro.

## Características Del Campo Variable:

**Tamaño dinámico:**

- Ocupa solo el espacio necesario para los datos reales
- Puede crecer o decrecer según el contenido
- Requiere información adicional para saber dónde termina

**Ubicación relativa:**

- Su posición puede variar dentro del registro
- Requiere metadatos o delimitadores para ser localizado

## Métodos De Implementación:

**1. Con indicador de longitud:**

```
Campo "Nombre" variable:
Empleado A: "04Juan" (4 caracteres de nombre)
Empleado B: "09Alejandro" (9 caracteres de nombre)
Empleado C: "03Ana" (3 caracteres de nombre)
```

**2. Con delimitadores:**

```
Campo "Descripción" variable:
Producto A: "Computadora portátil|"
Producto B: "Mouse inalámbrico|"
Producto C: "Teclado mecánico para gaming profesional|"
```

**3. Con terminador nulo:**

```
Campo "Comentarios" variable:
Cliente A: "Cliente frecuente\0"
Cliente B: "Requiere factura\0"
Cliente C: "Descuento especial aplicado por volumen de compras\0"
```

## Ejemplos De Campos Variables:

```
Campo "Dirección" variable:
Cliente 1: "Calle 123"
Cliente 2: "Avenida Libertador 4567, Piso 8, Departamento B"
Cliente 3: "Ruta Nacional 40, Km 25.5"

Campo "Observaciones" variable:
Pedido 1: "Entrega urgente"
Pedido 2: ""  (campo vacío)
Pedido 3: "Cliente prefiere entrega en horario de mañana, tocar timbre dos veces, preguntar por María"
```

## Ventajas De Los Campos Variables:

- **Eficiencia de espacio**: Solo usa el espacio necesario
- **Flexibilidad**: Puede adaptarse a diferentes tamaños de datos
- **Sin truncamiento**: Puede almacenar textos largos sin pérdida
- **Ahorro significativo**: Especialmente útil cuando hay gran variación en el tamaño de los datos

## Desventajas De Los Campos Variables:

- **Complejidad**: Requiere algoritmos más sofisticados para acceso
- **Overhead**: Necesita metadatos adicionales (indicadores, delimitadores)
- **Rendimiento**: Acceso más lento que los campos fijos
- **Fragmentación**: Puede causar problemas de fragmentación externa
