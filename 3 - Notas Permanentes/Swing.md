---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

# Definición

Swing es una segunda generación de herramientas para el desarrollo de GUI. Incluida en el [[Java#JDK - Java Development Kit (Plataforma De Desarrollo)|JDK]]

Las componentes Swing reemplazan a las [[AWT|AWT]] y permiten construir [[Interfaces]]

De usuario de alta calidad.

Swing provee múltiples componentes de GUI que no están presentes en el [[AWT]]: fichas, barras de herramientas, tablas, árboles, cajas de diálogo, etc.

**Ventajas de Swing**:

- **Lightweight**: Dibujado en [[Java]], no usa componentes nativos
- **Consistente**: Mismo aspecto en todas las plataformas
- **Más componentes**: JTable, JTree, JTabbedPane, JSplitPane, etc.
- **Personalizable**: Look and Feel configurable (Metal, Nimbus, etc.)
- **Menos bugs**: Una sola implementación para todas las plataformas

# Explicación

Donde hay Contenedores (Container), Componentes (Component) y Layouts

		Un `Container` pueden contener múltiples `Components`, y cada `Component` tiene un container padre. Un `container` también puede contener otro container con components dentro.

El layout se le aplica a los Containers para generar una división, permitiendo cosas como:

![[[[AWT]]-1756334397967.webp|278x284]]

Este podría ser un Contenedor principal, con 5 regiones que a su vez, cada una de ellas podría contener otros contenedores o componentes como botón, lista, etc.

> [!info] Aclaración de container y component
> El container esta clasificado como un tipo de component, por eso más adelante se verá que container hereda de component. Aunque se trata como cosas separadas teoricamente

# Partes

## Contenedores

![[GUI en [[Java]]-1755726057350.webp]]

![[Swing-1759415395277.webp]]

`Container` es una **[[Clase]] abstracta base** de la que heredan `JFrame`, `JPanel`, `JDialog`, etc.

- Tan solo se suele declarar algo de tipo `container` para **dar generalidad**, igual que `Object` lo es para todos los objetos en [[Java]]. Usualmente, se usan sus subclases.
- Sirve cuando no te importa el tipo concreto del contenedor, sino que solo querés trabajar con él como "algo que puede contener componentes".

### ScrollPane

Permite **desplazamiento (scroll)** en caso de que el contenido sea más grande que el área visible.

```java 
JTextArea area = new JTextArea(10, 30);
JScrollPane scroll = new JScrollPane(area);
frame.add(scroll);
```

### Window

Es un contenedor que representa **ventanas de nivel superior** (no dependen de otro contenedor).

No tiene bordes ni controles por defecto.

#### Frame

Una ventana completa con **título, bordes, botones de cerrar/minimizar/maximizar**

Es el **contenedor principal más común** para aplicaciones de escritorio: A paritr de este se puede agregar componentes u otros contenedores tipo Panel.

```java
JFrame frame = new JFrame("Mi ventana");
frame.setSize(400, 300);
frame.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
frame.setVisible(true);
```

#### Dialog

Ventana emergente, generalmente usada para **mensajes o formularios secundarios**.

Puede ser **modal** (bloquea la ventana principal hasta cerrarse) o no modal.

```java
JDialog dialog = new JDialog(frame, "Aviso", true);
dialog.setSize(200, 100);
dialog.add(new JLabel("Hola!"));
dialog.setVisible(true);
```

### Panel

Es un contenedor **más simple**, usado como **área dentro de una ventana** para organizar componentes.

Muy usado dentro del Frame para dividir la ventana en secciones.

```java
JPanel panel = new JPanel();
panel.add(new JButton("Botón 1"));
panel.add(new JButton("Botón 2"));
frame.add(panel);
```

#### Applet

Era un contenedor especial para ejecutar en navegadores (ya obsoleto).

Permitía incrustar aplicaciones [[Java]] en páginas web.

Hoy casi no se usa.

## Layouts

Como su nombre dice, especifica la disposición de los elementos dentro de un contenedor. Los contenedores delegan en los administradores de disposición (layout manager) todo lo relacionado con el posicionamiento, tamaño, espaciado y alineación de las componentes sobre la pantalla.

Cada contenedor contendrá un layout por defecto que podrá cambiase con el método `setLayout()`

Los Layout por defecto son:

![[Swing-1756589849206.webp|639x218]]

![[Swing-1759415427793.webp]]

### Tipos De Layout

#### BorderLayout

Este Layout ofrece un esquema complejo para la ubicación de componentes en un contenedor. Su estructura básica está compuesta por cinco regiones:

- `BorderLayout.NORTH`
- `BorderLayout.SOUTH`
- `BorderLayout.EAST`
- `BorderLayout.WEST`
- `BorderLayout.CENTER`

![[Swing-1756656747322.webp]]

`{[[Java]]} new BorderLayout();` : Constructor por defecto sin espacio entre regiones.

`{[[Java]]} new BorderLayout(hgap,vgap);` : Constructor con espacio entre los componentes.

`{[[Java]]} contenedor.add(button,BorderLayout.NORTH);` Agrega el componente `button` en la región norte del contenedor.

> [!danger] Un componente por región
> Se puede agregar solo un componente por región. Si se agregan más de una en una misma región, solo la última quedará visible

#### FlowLayout

Este layout ubica a las componentes línea por línea. Cada vez que se completa una línea se comienza una nueva. No restringe el tamaño de las componentes que gestiona y admite que tengan el tamaño preferido.

El alineamiento por defecto que el administrador usa para sus componentes es centrado, aunque se puede cambiar para que use alineación a izquierda o a derecha.

**Constructor**

```java
FlowLayout();
FlowLayout(int align);
FlowLayout(int align, int hgap, int vgap); 
```

Los parámetros `hgap` y `vgap` se utilizan para asignar un espaciado horizontal y vertical entre las componentes

Los valores para `align` pueden ser:

```Java
FlowLayout.LEFT
FlowLayout.CENTER
FlowLayout.RIGHT
```

#### GridLayout

Es una grilla/cuadrícula donde tendremos una cantidad de filas y columnas.

El ancho de todas las celdas es idéntico y está determinado por el resultado de la división del ancho disponible por la cantidad de columnas. De la misma manera se obtiene el alto de todas las celdas.

El orden en que los componentes se agregan a la grilla determina la celda que se ocupa. Las celdas se ocupan de izquierda a derecha y de arriba hacia abajo.

`{[[Java]]}new GridLayout(int rows, int cols, int hgap, int vgap);`

- `rows` Son las filas
- `cols` Son las columnas
- `hgap` y `vgap` el espaciado entre los componentes.

Se puede usar el 0 (cero). La cantidad de columnas o la cantidad de filas puede cero e indica un valor flexible.

```java
new GridLayout(0,3); //Indica 3 columnas y filas la cantidad necesaria 

new GridLayout(0,0); //Cantidad flexible de filas y columnas

new GridLayout(3,0); //Indica 3 filas y cantidad flexible de columnas
```

#### CardLayout

#### GridBagLayout

## Components

![[GUI en [[Java]]-1755725462126.webp]]

![[Swing-1759415476379.webp]]

Se le llama Componentes a todo lo que baja de `MenuComponent` y `Component`.

Los componentes básicos de Swing son subclases de “Container” (las [[AWT]] son subclases de `component`) por lo tanto, están capacitadas para contener a otras componentes

> Las componentes de GUI básicas y los contenedores, heredan de Component una cantidad de métodos y variables de instancia.

Los componentes [[JList y JTable]] se explicarán aparte por su extensión.

### Tipos De Componentes Básicos

![[GUI en [[Java]]-1755726018448.webp]]

#### Button - Botón

![[GUI en [[Java]]-1755726246539.webp|0x0]]

La [[Clase]] Button es una [[Clase]] que produce una componente de tipo botón con una etiqueta (texto) que se visualizará.

**Métodos más importantes:**
- `AddActionListener ()`: añade un receptor de eventos de tipo Action producidos por el botón
- `getLabel ()`: devuelve la etiqueta o título del botón.
- `RemoveActionListener ()`: elimina el receptor de eventos y el botón deja de avisar cuando ocurre un evento.
- `SetLabel ()`: fija el título o etiqueta visual del botón

#### ComboBox - Botones De Elección

![[GUI en [[Java]]-1755726287106.webp|241x60]]

Los botones de selección en una lista (choice) permiten el rápido acceso a una lista de elementos. Por ejemplo, podríamos implementar una selección de colores y mantenerla en un botón Choice.

#### CheckBox - Botones De Marcación

![[GUI en [[Java]]-1755726651629.webp|172x57]]

La de comprobación (Checkbox) se utilizan frecuentemente como botones de estado. Proporcionan información del tipo Sí o No (true o false). El estado del botón se devuelve en el argumento `Object` de los eventos `Checkbox`; el argumento es de tipo booleano: verdadero (true) si la caja se ha seleccionado y falso (false) en otro caso.

Tanto el nombre como el estado se devuelven en el argumento del evento, aunque se pueden obtener a través de los métodos getLabel() y getState() del objeto Checkbox.

#### CheckboxGroup - Botones De Selección

![[GUI en [[Java]]-1755726918532.webp|423x61]]

Los botones de comprobación se pueden agrupar para formar una interfaz de botón de radio(CheckboxGroup), que son agrupaciones de botones Checkbox en las que siempre hay un único botón activo.

#### Labels - Etiquetas

![[GUI en [[Java]]-1755796030296.webp|303x202]]

Las etiquetas (Label) proporcionan una forma de colocar texto estático en un panel, para mostrar información que normalmente no varía, al usuario.

#### List - Listas

![[GUI en [[Java]]-1755796105335.webp]]

Las listas (List) aparecen en los [[Interfaces]] de usuario para facilitar a los operadores la manipulación de muchos elementos. Se crean utilizando métodos similares a los de los botones choice. La lista es visible todo el tiempo, utilizándose una barra de desplazamiento para visualizar los elementos que no caben en el área que aparece en la pantalla.

#### TextField - Campos De Texto

![[GUI en [[Java]]-1755796677447.webp|517x302]]

```java
import java.awt.*;
import java.applet.Applet;
public class CAmpoTexto {
    TextField tf1,tf2,tf3,tf4;
    public void init() {
        // Campo de texto vacio 
        tf1 = new TextField();
        // Campo de texto vacio con 20 columnas 
        tf2 = new TextField(20);
        // Texto predefinido 
        tf3 = new TextField ("Hola");
        // Texto predefinido en 30 
        tf4 = new TextField ("Hola", 30);
        add(tf1); add(tf2); add(tf3); add(tf4);
    }
}
```

#### TextArea - Áreas De Texto

![[GUI en [[Java]]-1755796723732.webp|440x342]]

Permite incorporar texto multilínea dentro de zonas de texto (TextArea). Los objetos TextArea se utilizan para elementos de texto que ocupan más de una línea, como puede ser la presentación tanto de texto editable como de solo lectura.

Para las áreas de texto hay que especificar el número de columnas.

#### Scrollbar - Barra De Desplazamiento

![[GUI en [[Java]]-1755796817956.webp]]

En determinada situación se necesitan realizar el ajuste de valores lineales en pantalla, resulta útil el uso de barras de desplazamiento. Proporcionan una forma de trabajar con rangos de valores o de áreas, como el componente TextArea, que proporciona dos barras de desplazamiento automáticamente.

#### JOptionPane - Ventana De Dialogo

Swing también provee una [[Clase]] que automatiza muchas de las actividades que un programador haría para crear ventanas de diálogo: `JOptionPane`. Esta [[Clase]] tiene muchos métodos de [[Clase]] que permiten crear diálogos con íconos, mensajes, campos de entrada y botones.

Todos los diálogos creados con JOptionPane, son modales. Por lo cual bloquean las acciones del padre.

![[Swing-1759358741487.webp]]

```java
JOptionPane.showMessageDialog(
    null, //padre
    "El valor de PI es "+pi, //mensaje
    "Mensaje", // título
    JOptionPane.INFORMATION_MESSAGE); //hay 5 tipos de mensajes
}
```

![[Swing-1759358755185.webp]]

```java
JOptionPane.showConfirmDialog(
	boton, //padre
	"¿Salva antes de salir?", //mensaje
	"Mensaje", //título
	JOptionPane.YES_NO_CANCEL_OPTION, //tipo de opción
	JOptionPane.WARNING_MESSAGE, // tipo de mensaje
	new ImageIcon("duke.gif")); //ícono
}
```

# Ejemplo Calculadora

![[Swing-1756661811390.webp]]

```java
public class CalculadoraTest{
    Frame calculadora;
    Panel display;
    Panel numeros;
    Panel operadores;
    Button uno, dos, tres, cuatro, cinco, seis, siete, ocho, nueve,cero;
    Button mas, menos, por, dividir, igual;
    TextField displayText;
    
    public void launchCalculadora(){
    dispaly.setLayout(new FlowLayout());
    display.add(display.Text);
    numeros.setLayout(new GridLayout(4,3));
    numeros.add(uno);
    numeros.add(dos);
    numeros.add(tres);
    numeros.add(cuatro);
    numeros.add(cinco);
    numeros.add(seis);
    numeros.add(siete);
    numeros.add(ocho);
    numeros.add(nueve);
    numeros.add(cero);
    operadores.setLayout(new GridLayout(0,1));
    operadores.add(mas);
    operadores.add(menos);
    operadores.add(por);
    operadores.add(dividir);
    operadores.add(igual);
    
    calculadora.setLayout (new BorderLayout());
    calculadora.add(display,BorderLayout.NORTH);
    calculadora.add(numeros, BorderLayout.CENTER);
    calculadora.add(operadores, BorderLayout.EAST);
    calculadora.setSize(300,300);
    calculadora.pack();
    calculadora.setVisible(true);
    }
}
```
