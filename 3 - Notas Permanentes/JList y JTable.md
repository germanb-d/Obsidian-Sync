---
Categoria: Sistemas
Materia: Seminario de Lenguajes
tags:
---

![[Clase Swing MVC - List Table.pdf]]

# Que Son

Ambos son componentes de [[Swing]] que se utilizan para funciones similares:

- JList mostrara un listado
- Jtable mostrara una tabla (tipo excel)

## Arquitectura

Ambos componentes constan de una mayor sofisticación entre las que se incluye el aplicar una arquitectura [[MVC - Modelo Vista Controlador|MVC]].

> [!PDF|yellow] [[Clase Swing MVC - List Table.pdf#page=5&selection=23,0,118,1&color=yellow|Clase Swing MVC - List Table, p.5]]
> La arquitectura de las componentes [[Swing]] responde a una versión especializada del patrón MVC. Está basada en 2 objetos: un objeto [[MVC - Modelo Vista Controlador#Modelo|Modelo]] y un objeto encargado del display o apariencia y del manejo de los eventos, que representan la [[MVC - Modelo Vista Controlador#Vista|Vista]]  + el [[MVC - Modelo Vista Controlador#Controlador|Controlador]] en el patrón [[MVC - Modelo Vista Controlador|MVC]].

![[JList y JTable-1759348285700.webp]]

Al crear el componente, el objeto encargado de la UI y el controlador se crea automáticamente (el de color lila en la imagen).

El modelo, por otra parte, se deberá crear manualmente.

# JList

Muestra un listado de elementos.

![[JList y JTable-1759349277652.webp]]

## Crear Una Lista Sin Modelo

Al crear una lista pasándole directamente el array este creará un modelo por defecto, aunque este sera inmutable, no podremos agregar ni eliminar ni modificar elementos.

- `{[[Java]]} JList(Object[] arg0)`
- `{[[Java]]} JList(Vector  arg0))`

## Crear Una Lista Con Modelo

En este caso hay dos alternativas:

Se crea usando el constructor por defecto (el que no tiene argumentos) y luego se le setea un Modelo

```java
JList lista = new JList(); 
lista.setModel(modelo);
```

2. Se crea usando el constructor que tiene un Modelo como argumento

```java
JList lista = new JList(modelo);
```

### Como Se Crea El Modelo

 El modelo se crea implementando la interfaz `ListModel` o utilizando una de sus implementaciones por defecto, como `DefaultListModel`.  Una vez creado los elementos primero se agregan al modelo y luego se pasa el modelo a la lista.

`DefaultListModel` nos provee de ciertas funciones para facilitar el manejo de los modelos. Permitiéndonos hacer cosas como:

```java 
private DefaultListModel modelo = new DefaultListModel();
private JList lista = new JList();
modelo.addElement("Elemento 1");
lista.setModel(modelo);
modelo.deleteElement("Elemento 1");
```

# JTable

Igual que JLIst en cuanto a que si se crea pasando en los parametros directamente los arrays, este creara un modelo automatico pero generara una **inmutable**.

## Creacion

### Crear Una Tabla Sin Modelo

![[JList y JTable-1759357755642.webp]]

Se puede crear directamente pasando el array con el contenido de la tabla y un array con el nombre de las columnas:

`{[[Java]]} JTable(Object[][] rowData, Object[] columnNames)`

`{[[Java]]} JTable(Vector rowData, Vector columnNames)`

### Crear Una Tabla Con Modelo

 En este caso al igual que con la JList se puede crear un modelo con `DefaultTableModel` el cual implementa la [[Interfaces|interface]]  `TableModel`.

```Java 
private JTable tabla = new JTable();
private DefaultTableModel modeloTabla = new DefaultTableModel(/*titulos, 0*/);
tabla.setModel(modeloTabla);
```

Al crear un `DefaultTableModel`, se especifican los títulos de las columnas y los datos iniciales como parámetros. En el ejemplo, se usa el valor 0 para los datos porque se agregarán filas posteriormente.

## Cambiar Tipo De Dato Mostrado

> [!PDF|yellow] [[Clase Swing MVC - List Table.pdf#page=17&selection=8,0,129,1&color=yellow|Clase Swing MVC - List Table, p.17]]
>
> > Los datos de la tabla son mostrados como String porque usamos como modelo una instancia de la [[Clase]] DefaultTableModel. Esta [[Clase]] tiene una manera por defecto de mostrar los datos y es en formato String. Para poder cambiar esto, debemos crear una [[Clase]] que extienda a DefaultTableModel y sobreescribir un método para indicar el tipo de dato de cada celda

```java
package tablas;

import javax.swing.table.DefaultTableModel;

public class ModeloReservas extends DefaultTableModel {

    public ModeloReservas(final Object[][] datos, final String[] titulos) {
        super(datos, titulos);
    }

    @Override
    public Class getColumnClass(final int column) {
        return this.getValueAt(0, column).getClass();
    }
}


```

Ahora a la tabla le podras crear un modelo de este tipo siendo `{[[Java]]}tabla.setModel (new ModeloReservas(datos,titulos))`

 De esta forma, si en alguna columna tienes un `Boolean`, se mostrará como un `JCheckBox`.
