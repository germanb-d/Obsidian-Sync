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
    public int calcularPrecio(int dias);
}

public class autoLujo{
    public static final int AUMENTO = 1.20; 
    private int precioDiario
    @override 
    public int calcularPrecio(int dias){
    return (dias * precioDiario) * AUMENTO  
    }
}

public class autoComun{
private int precioDiario

@override 
   public int calcularPrecio(int dias){
   return (dias * precioDiario)
}


public class Alquiler{
    
    private int costeVehicular(int dias, Auto auto){
        
    }
}

```