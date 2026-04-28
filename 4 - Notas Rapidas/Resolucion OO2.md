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
Libro Prestamos[]; //supongo que prestamos es de clase 

}

public boolean puedeRetirar

```