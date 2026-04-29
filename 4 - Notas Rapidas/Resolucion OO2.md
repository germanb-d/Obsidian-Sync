``` java
public class auto{

public int costeAlquiler(int Dias){
return PrecioDiario * Dias;
}
}


public class SistemaAlquiler {
    public double calcularPrecioTotal(Alquiler alquiler) {
        double precioBase = alquiler.getAuto().costeAlquiler();
        if (alquiler.getAuto().esLujo()) {
            return precioBase * 1.20;
        }
        return precioBase;
    }
}
```


``` java
public interface auto{
    public double calcularPrecio(int dias);
}

public class autoLujo{
    public static final double AUMENTO = 1.20; 
    private double precioDiario
    @override 
    public double calcularPrecio(int dias){
    return (dias * precioDiario) * AUMENTO  
    }
}

public class autoComun{
private double precioDiario

@override 
   public double calcularPrecio(int dias){
   return (dias * precioDiario)
}


public class Alquiler{
    
    public double costeVehicular(){
        return this.auto.calcularPrecio(this.dias);
    }
}

public class SistemaAlquiler{
public double calcularPrecioTotal(Alquiler alquiler) {
return alquiler.costeVehicular();
}

```


```java
//TEST
Auto auto = new autoLujo("100"); //100 seria para el atributo precioDiario
Alquiler casa1 = new Alquiler(auto, "5"); //5 Dias
SistemaAlquiler SA = new SistemaAlquiler();

AssertEquals("600", SA.calcularPrecioTotal(casa1)); //100x5 = 500 ---- 5000x1.2 = 600

```


2)

```java
public interface Puntajes{
public int devolverPuntaje( int DNI);
}

public class ValidadorDeCredito(Puntajes puntajes){ 
   private Puntajes puntajes;

public boolean esApto(Cliente cliente, Puntajes puntajes){
int puntaje = puntajes.devolverPuntaje(cliente.getDNI);
return puntaje >700
}
}
```


```java
public class fakeWeb implements Puntajes{
int DNI;
@override
public int devolverPuntaje( int DNI){
this.DNI = DNI
return 100;
}


public int comprobarUltimoDNI(){
return DNI;
}
}

class testEsApto {

Cliente pepe = new CLiente(1000); //1000 es el dni
new Puntajes P = new fakeWeb();
new ValidadorDeCredito calculadora = new ValidadorDeCredito(P);

AssertEquals(100, P.devolverPuntaje(pepe.getDNI()))
AssertEquals (pepe.getDNI, P.ComprobarUltimoDNI)
    AssertFalse(calculadora.EsApto(pepe,P))
}

```


# Nuevos 1 y 2 


``` java
public class Socio(){
    public static final LIMITE_PRESTAMOS =5;
    private ArrayList<Libro> Prestamos = new ArrayList(); //supongo que prestamos es de clase Libro

    public boolean puedeRetirarMas(){
        return Prestamos.size() < LIMITE_PRESTAMOS;
      }  
}

public class Bibliotecario {

    public boolean puedeRetirar(Socio socio) {
        // "Pide" la lista y decide desde afuera
       return socio.puedeRetirarMas;
    }
}


// TEST

class testRetiro{
    Socio pepe = new Socio();
        pepe.añadirPrestamo(new Libro("El principito")); //agregaria al array
        pepe.añadirPrestamo(new Libro("El 2"));
        pepe.añadirPrestamo(new Libro("El 3"));
        pepe.añadirPrestamo(new Libro("El 4"));
        pepe.añadirPrestamo(new Libro("El 5"));
        pepe.añadirPrestamo(new Libro("El 6"));
      
        Bibliotecario Pablo = new Bibliotecario();
        
          AssertFalse(Pablo.puedeRetirar(pepe)); 
}
```

B)

``` java
public interface Almacen{
void guardarInforme(String contenido);

public class PDF implements Almacen{
@Override
void guardarInforme(String contenido){
leWriter writer = new FileWriter("informe.pdf")); //podria pedir el titulo como parametro tambien
        writer.write(contenido);
}
}

public class GeneradorDeInformes(Almacen guardados){ 
private Almacen guardados;

public void exportar(String contenido){
guardados.guardarInforme(contenido);
}
}
}


//TEST

new fakePDF implements Almacen{
private String contenidoGuardado;
@Override
public void guardarInforme(String contenido){
contenidoGuardado = contenido;
}

public String devolverContenido(){
return contenidoGuardado;
}
}

class TestGenerarInforme{

Almacen guardados = new FakePDF; //deberia crear un fake no un almacen
GeneradorDeInformes generador = new GeneradorDeInformes(guardados);
generador.guardarInforme("123");

AssertEquals("123", guardados.devolverContenido())

}

```


---

```java
public class ProcesadorVentas {
    public void procesar(Carrito carrito) {
       carrito.procesarProductos()
    }
}

public class Carrito{
private static final DESCUENTO_MAS10 = 0.10;
private List<Productos> productos = new ArrayList<Productos>();
private double precioTotal;

// Supongo q se le agregan productos y se van sumando al precio;

public void procesarProductos(){
if (productos.size() >10)
    precioTotal = precioTotal - precioTotal*DESCUENTO_MAS10
}
}

//TEST -------------------------

class TestCarrito{
ProcesadorVentas PV = new ProcesadorVentas();
Carrito carrito = new Carrito(/*Parametros*/);

for (int i=0, i<12, i++){
carrito.agregarProducto(new Producto(Galletitas, 100)); 
}

PV.procesar(carrito);

// 100x11 = 1100 ; 1100 - 10% = 990
AssertEquals(carrito.devolverPrecioTotal,990.0, 0.01); //pedia tolerancia con doubles


}
```


# Punto 2


```java
public interface Notificacion{
public void Notificar( String mensaje);
}

public class Mail implements Notificacion{
GmailService service = new GmailService();
@Override 
public void Notificar(String mensaje){
service.send(mensaje);
}
}


public class Notificador {
private Notificacion service;

public Notificador(Notificacion service){
this.service = service;
}

public void avisar(String msg){
service.Notificar(msg);
}

}


//TEST------------------------------------

public class fakeMail implements Notificacion{
public String msjEnviado;

@Override 
public void Notificar(String mensaje){
msjEnviado = mensaje;
}

public String retornarMsj(){
return msjEnviado;
}
}


NotificadorTest{

@Test
public void testRecibeMSJ(){
String msj = "hola";
fakeMail mail = new fakeMail();
Notificador notificador = new Notificador(mail);
notificador.avisar(msj);

assertEquals(msj, mail.retornarMsj());
} 

}
```



# Punto 3 


```java

public interface Empleado{
public int retornarSueldo();
}

public class EmpleadoComun implements Empleado{
private int sueldoBase;

@override
public int retornarSueldo(){
return sueldo base;

}
}

public class Gerente implements Empleado{
pivate static int PAGO_EXTRA = 5000;
private int sueldoBase;

@override
public int retornarSueldo(){
return sueldo base + PAGO_EXTRA;
}
}

public class Cadete implements Empleado{
pivate static int PAGO_EXTRA = 1000;
private int sueldoBase;

@override
public int retornarSueldo(){
return sueldo base + PAGO_EXTRA;
}
}



public double calcularSueldo(Empleado e) {
    return e.retornarSueldo();
}
```


---


Parcial de ejemplo:

1)


```java
public class Juez {
    private String nombre;
    private String apellido;
    private Collection<Causa> causasACargo;
    
    public void agregarCausa(Causa causa) {
        this.causasACargo.add(causa);
    }
     public int devolverCantCausas(){
          return causasACargo.size();
     }
}

public class Controlador {

    private Collection<Juez> jueces;
    
    public int calcularCausasTotales() {
        int cantidadCausas = 0;
        for (Juez juez : jueces) {
              cantidadCausas += juez.devolverCantCausas();
        }

        return cantidadCausas;
    }
}
```

