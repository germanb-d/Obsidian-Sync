---
Categoria: Sistemas
Materia: Base de Datos 1
Fecha de Entrega:
Terminado: true
Tags:
  - "#Practico"
---

# Práctica Teórica 7

1) Una transacción es un conjunto de operaciones unidas en una única unidad lógica de trabajo. Estas [[Transacciones]] permite quitar gran parte de las cargas del programador, como en el manejo en entornos concurrentes; además permiten una mayor escalabidad de la BD y un mejor manejo de los fallos y las debidas recuperaciones ante este, entre muchas otras ventajas.
2) Se denomina una única unidad lógica de trabajo, en especial por una de sus propiedades que es la atomicidad, la que implica que una transacción se realiza en su totalidad o no se realiza, en caso de quedar una transacción a la mitad y datos sobrescritos se hace su debido UNDO ( retroceder hasta dejar la BD como estaba con anterioridad a la transacción).
3) El aislamiento en el entorno monousuario es en gran parte trivial debido a la falta de [[Transacciones]] en paralelo, esta propiedad de las [[Transacciones]] se vuelve fundamental en entornos concurrentes para evitar fallos y asegurar una buena consistencia.
4) La modificación diferida es más fácil de implementar y menos costosa al hacer todas las escrituras a la vez y evitar la realización de UNDO en caso de caídas. Pero no hay que olvidar que esta es más lenta en su uso que la modificación inmediata.
5) Un ejemplo sencillo podria ser una transferencia del saldo de una cuenta A a una cuenta B.
   A = 100 y B = 150
   A + B = 250
   Quiero transferir 50 pesos de la cuenta A a la cuenta B

```
lock_c(A)
READ(A)
A = A-50 
lock_e(A)
WRITE(A)
lock_c(A)
SE CAE LA BASE DE DATOS ACA
lock_c(B)
READ(B)
B = B+50 
lock_e(B)
WRITE(B)
COMMIT
```

Donde se cae la [[Base de Datos]], se generaría una inconsistencia. Porque al ser modificación inmediata en A quedaría almacenado 50, pero B seguiría siendo 150. A + B = 200

6) Los puntos de verificación o checkpoints se usan para decir: "De acá para atrás está todo bien", por cuál a la hora de revisar la bitácora solo se revisará del checkpoint para delante.

   ¿Con qué frecuencia? Puede ser cuando la memoria se llene y te veas obligado a bajar los datos a disco, cada X tiempo o en gral. Lo que se busca determinar es cual es tu tiempo de tolerancia para la recuperación de una caída, si ves que ante una caída necesitas una rápida recuperación ( baja tolerancia ) tus checkpoints deben ser más seguidos y viceversa.

7) .

	1) En caso de modificacion inmediata: Al revisar la bitácora aquellas [[Transacciones]] que tengan un comienzo y fin (start y commit) se les realiza un REDO, o sea se sobrescriben los datos de la BD por los nuevos valores almacenados en la bitácora. Para las [[Transacciones]] que tienen comienzo, pero no fin (start y no commit) se realiza un UNDO, se sobrescriben los valores de la BD por los valores antiguos almacenados en la bitácora con la intención de dejar la BD consistente a como estaba antes de la transacción.

	2) En caso de modificación diferida: Al revisar la bitácora aquellas [[Transacciones]] que tengan un comienzo y fin (start y commit) se les realiza un REDO igual que en la inmediata. Para las [[Transacciones]] que tienen comienzo, pero no fin (start y no commit) no se hace nada, debido a que no se modificó ningún dato en la BD.

	3) En caso de doble paginación: No sé

8) Se puede llevar un contador de cuantas veces una transacción produce un fallo, permitiendo que al alcanzar X número no se vuelva a ejecutar.

9) .

	1) Usa modificación inmediata, porque guarda dos valores: el antiguo y el nuevo.

	2)   `< T1, dato1, 4>` y  `< T1, dato2, 35>`, así quedarían en forma diferida.

	3) Es una transacción ya comiteada.

	4) Si la transacción estuviera en medio de una operación sería Activa, si ya hubiera completado todas las operaciones y solo le faltaba comitear será parcialmente activa y en caso de tener un  `abort` estaria abortada.

# Práctica Teórica 8

1) Nosotros buscamos ccrear planificaciones equivalentes a una planificacion en serie debido a que en la planificacion en serie no se generan conflictos en el uso de datos. Una planificacion no serializable implicaciria que una transaccion podria pisar a la otra. Ejemplo:

```
   T1: READ (A)
   T2: READ (A)
   T1: WRITE (A)
   T2: WRITE (A)
```

En este ejemplo podemos ver como T 2 Pisa el dato de T 1, es aún más gráfico cuando desarrollamos un grafo de precedencia donde veríamos como se genera un ciclo al cada transacción deber realizarse antes que la otra.

2) La mayor diferencia recae en el uso de checkpoints, en entornos recurrentes pueden que no se generen espacios sin [[Transacciones]] para crear los checkpoint, por esto a la hora de crearlos a la vez se crea una lista de las [[Transacciones]] que están siendo ejecutadas en el momento de crear el checkpoint.Así si se llega a caer la [[Base de Datos]] puedo decir: revisa a partir del checkpoint para delante y para detrás del checkpoint solo revisa las [[Transacciones]] de esta lista.
3) .
	1) Podria demostrar la consistencia diciendo que tanto al ejecutarse T 0 -> T 1 o T 1- > T 0 en ambos casos B u A quedan 1 y 0, o 0 y 1 siendo ambos respuestas consistentes.

```
	b) inconsistente 
	T1: read A
	T0: read A
	T1: read B
	T0: read B
	T0: If A= 0 then B:=B+1
	T1: If B=0 then A:=A+1
	T0: Write(B)
	T1: Write(A)
```

```
c) consistente
T0: Read(A)
T1: Read(A)
T0: Read(B)
T0: If A= 0 then B:=B+1
T0: Write(B)
T1: Read(B)
T1: If B=0 then A:=A+1
T1: Write(A)
```

4) El protocolo de bloqueo de dos fases busca reducir el tiempo que tiene bloqueado de forma exclusiva una transaccion a un dato: Esto lo logra en dos fases
	1) En la fase 1 de crecimiento empezara con un bloqueo compartido para la lectura y la aplicacion de las operaciones necerarias para el dato. Ej: Read (A), A= 100 + A, etc. PAra posteriormente pasar a un bloqueo exclusivo solamente a la hora de modificar el dato con el write.
	2) En la fase de 2 de decrecimiento se van liberando los bloqueos, empezando pasando del bloqueo exclusivo al compoartido y posteriormente a desbloquear el dato. Tambien puede terminar totalmente con los bloqueos con el commit o abort.
5) no se toman lo relacionado con las marcas de tiempo
6) no se toman lo relacionado con las marcas de tiempo
7) En este caso se debe revisar la bitacora aquellas [[Transacciones]] que tengan un comienzo y fin (start y commit) se les realiza un REDO, o sea se sobrescriben los datos de la BD por los nuevos valores almacenados en la bitácora. Para las [[Transacciones]] que tienen comienzo, pero no fin (start y no commit) no se hace nada, debido a que no se modificó ningún dato en la BD.

# Primer Parcial

1) Las 4 propiedaes son:
	1) Atomicidad: Se realiza toda la transaccion o no se realiza, se ve aplicado a la hora de recuperar [[Transacciones]] que estaban a medias por una caida, siempre se decide si volverla a empezar o abortarla pero jamas quedan datos procesados a medias
	2) Consistencia: La BD debe ser consistente, si dos saldos de cuenta suman 100, despues de una transferencia deben seguir siendo 100. Se ve aplicado en el uso de planificaciones que cumplan con serialidad para garantizar esto.
	3) Aislamiento: Aunque trivial en el entornos monousuario en entornos concurrentes se vuevle fundamental para que una [[Transacciones]] no se vean diferidades por la ejecucion de otras [[Transacciones]], esto se logra con el uso de bloqueos.
	4) Durabilidad: Las [[Transacciones]] deben ser permanentes, deben quedar almacenadas y registradas. Ademas del uso de una memoria no volatil para la BD, esto se vuelve fundamental para el procesamiento en memoria volatil donde se usa una bitacora para garantizar la durabilidad de toda transaccion.
2) La diferencia es que en la Parcialmente Cometida se realizaron todas las operaciones pero la transaccion aun no esta comitieada, osea no esta respaldada en una memoria no volatil como la bitacora, caso contrario a la Cometida que si lo esta, llego al commit.
3) Porque si yo primero grabo en la BD y luego en la bitacora podria generar que en una hipotetica caida de la base, al levantar nuevamente la BD tenga datos que fueron almacenados por una transaccion en curso pero al no estar respaldara en la bitacora no hay forma de hacer un UNDO de estos elementos o determinar si ya habia terminado la transaccion o no. Ademas que siempre es mas rapida la escritura en la bitacora que en la BD
4) Cuando nosotros hacemos un read/white la BD busca el dato o lo almacena en el buffer de la BD, en caso de querer usar un dato y no estar ahi lo buscara en disco, pero es fundamental entender que aca no lo controlamoss nosotros, si hacemos un write este se grabara en el buffer la decsion de cuando se traslarada adisco queda en la BD. El imput/output se usa para sacar y almacenar directamente del disco ( la memoria no volatil)
5) .
	1) T 2 realizan REDO porque estaba procesandose a la hora de hacer el checkpoint y tiene el commit
	2) T 1 y T 3 hacen UNDO porque T 1 estaba procesandose a la hora de hacer el checkpoint y T 3 es posterior a este, donde ambas estan en procesamiento.
	3) A = 250, B = 450, C = 500, D = 700, E = 900.
6) La modificacion diferida es de mas facil implementacion, menor velocidad en operacion normal, menor costo de recuoeracion y sin necesidad de UNDO. La modificacion inmediata es de mas dificil implementacion, mayor velocidad en operacion normal, mayor coste de recuperacion y con necesidad de UNDO
7) No se pierden porque estos estan almacenados en la bitacora en disco, lo unico seria sobrescrivir los valores en la BD por los nuevos de la bitacora con REDO.
8) .
	1) x=20, y = 40
	2) y=30, x = 30

```
	1)  
	READ(X)
	X := X + 10
	X := X * 2
	WRITE(X)
	READ(Y)
	Y := Y + 10
	Y := Y * 2
	WRITE(Y)
	
	9)Si es serializable
```

9) .
	1) El proposito principal del bloqueo en dos fases es poder crear una planificacion serializable mediente el uso correcto de los bloqueos:
	2)    En la primera fase de crecimiento se van creando los bloqueos, ya sea compartidos, exclusivos o aumentando de forma progrsiva de uno al otro. Lo principal  es que aca no se cierra ningun bloqueo.
	   En la segunda fase de decrecimiento se van liberando los bloqueos, ya sa de forma directa o decreciendo. Lo principal es que aca no se crea ningun nuevo bloqueo.
	3) Garantiza el Aislamiento de las [[Transacciones]], permitiendo generar un orden correcto que sea equivalente a una planificacion en seri
	4) No soluciona los conflictos en sentido de que estos seguiran estando, solo se ordenan de tal manera para que no sucedan. Ademas de que no arregla errores de logica.
10) .
	1) Se genera un interbloqueo o deadlock.
	2) No puedo dibujar al estar haciendo lo en pc, pero serian dos puntos por cada transaccion y dos aristas donde se apuntarian entre si, porque ambas esperan a la otra.
	3) Primero se deberia buscar prevenirlo ya sea que cada transaccion pida todos los datos al comienzo (mas ineficiente) o darle un orden de "prioridad" a los datos, donde las [[Transacciones]] siempre empezarian por A, luego B, etc. Una vez que ya se dio no queda otra que elegir una "victima" que sera la transaccion que se va a abortar, para elegirla nos podemos basar en varios parametros desde cual tiene menos operaciones, cual usa menos datos, cual es mas rapida, etc.
	4) Creo que en este caso daria igual, pero elegiria T 1 porque para prevenir el proximo deadlock deberia empezar por A?
11) .

```
	a)
	T0: read A 
	T0: A = A-100
	T0: write A
	T0: read B 
	T0: B=B+100
	T0: write B
	
	 T1:  read B 
     T1: B=B-50
     T1: write B
     T1: read C
     T1: C=C+50
     T1: write C
     
     A = 400, B = 350, C = 250
     Total = 1000
     
     b) 
    T0: read A 
    T0: A = A-100
    T0: write A
    T0: read B 
    T0: B=B+100
    T1:  read B 
    T1: B=B-50
    T0: write B
    T1: read C
    T1: C=C+50
    T1: write C
    
    A = 400, B = 250, C =250
    Total = 900
```

12) .
	1) A partir del checkpoint para delante, y para atras del checkpoint la T 0 y T 1 porque estas estaban en proceso al hacer el checkpoint.
	2) Requieren REDO T 0 y T 2
	3) Se ignoran T 1 y T 3
	4) X=150, Z= 300, Y = no lo se (como estaba antes de iniciar la transaccion)
13) .
	1)  El primer Unlock(Producto) lo podria haber hecho antes del nuevo_stock = ....
	   El segundo Unlock(Producto) no es necesario porque ya lo hace el commit
	2) No se
	3) Igual pero cambiando el lugar del primer unlock
	4) no se

# Segundo Parcial

1) .
	1) Esta memoria solo es utilizada en la ejecucion de la transacccion, para la realizacion de operaciones. Es volatil, nos la podriamos imaginar como "la memoria cache"
	2) Esta memoria es utilizada por la BD y maneja una gran cantidad de [[Transacciones]] y datos. Sirve como punto intermedio entre la transaccion y el disco. Al igual que la anterior es volatil, pero esta es mas utilizada como una "memoria Ram". Aca se suelen grabar los datos con Write y leer con Read.
	3) Aca es donde se almacena toda la informacion de la BD de forma permanente, las tablas, los datos, la bitacora, etc. Es no volatil, pero no se busca entrar y salir permanentemente por su falta de velocidad en comparasion con los otros dos tipos de memoria. Se usa con imput para leer datos y con output para grabar datos.
2) .
	1) Se modifica con el WRITE ( A, a 1)
	2) No lo sabemos, es a consideracion de la BD cuando es el mejor momento para bajar los datos de los buffers al disco.
	3) Podria ir apartir de que se hace el write
	4) Podria recien ir a partir del commit
3) Si se diera esto, en caso de una caida esta transaccion al no tener el Commit grabado se le haria un UNDO. Esto tambien podria llevar a una eliminacion en cascada?
4) .
	1) Requieren REDO: T 1 . Es la unica que llega al commit de las [[Transacciones]] a revisar posterior al checkpoint (se encuentra en la lista a la hora de realizar el checkpoint)
	2) Se ignoran T 2 y T 3 porque quedaron a medias
	3) X = 10, Y =
