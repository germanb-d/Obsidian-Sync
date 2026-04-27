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