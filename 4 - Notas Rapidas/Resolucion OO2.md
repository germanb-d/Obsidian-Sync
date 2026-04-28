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


```