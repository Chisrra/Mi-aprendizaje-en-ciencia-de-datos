# Numpy
Continuamos trabajando dentro de ipython

## DataNote 1: Arreglos
Empezamos conociendo la libreria numpy, primero debemos importarla libreria con 
`import numpy as np` 
La llamamos `np` por convencion de la comunidad. Si es que no tienes la libreria o te marca error al intentar importarla (como fue mi caso) sólo escribe: 
`pip install numpy`

Para definir arreglos con numpy debemos llabar a la libreria y decirle que queremos crear un arreglo, en este ejemplo creamos un arreglo a partir de una lista y lo guardamos en una variable `a`.
`a = np.array( [1, 2, 3, 4, 5, 6] )`
Podemos acceder a varios de sus metodos como lo son:
- `a.size`: que nos devuelve la longitud del arrelgo.
- `a.ndim`: que nos indica la cantidad de dimensiones del arreglo.
- `a.dtype`: nos dice que tipo de dato almacena el array.
- `a.shape`: nos dice las dimenciones y la cantidad de elementos en cada una de sus dimensiones.

Cabe destacar que una vez se define la longitud de un arreglo ya no se podra modificar.

## DataNote 2: Operaciones
Se pueden hacer diferentes operaciones con los arreglos, como lo son la suma, resta, multiplicación, división, etc. Estas operaciones pueden hacerse entre un arreglo y una constante y entre dos arreglos con la misma forma/shape.

``` ipython
In  [1]: a = np.array( [1, 2, 3, 4, 5, 6] )

In  [2]: b = np.array( [10, 11, 12, 13, 14, 15] )

In  [3]: a + 10
Out [3]: array([11, 12, 13, 14, 15, 16])

In  [4]: a - b
Out [4]: array([-9, -9, -9, -9, -9, -9])
```

## DataNote 3: Tipos de datos
Los arreglos de *numpy* son de tipos de datos especificos y se nos da la posibilidad de definir que tipo de datos queremos que sea nuestro arreglo a la hora de construirlo.

``` ipython
In [1]: a = np.array([1, 2, 3, 4, 5, 6], dtype=float)

In [2]: a
Out[2]: array([1., 2., 3., 4., 5., 6.])

In [3]: a = np.array([1, 2, 3, 4, 5, 6], dtype=str)

In [4]: a
Out[4]: array(['1', '2', '3', '4', '5', '6'], dtype='<U1')

In [5]: a = np.array([1, 2, 3, 4, 5, 6], dtype=complex)

In [6]: a
Out[6]: array([1.+0.j, 2.+0.j, 3.+0.j, 4.+0.j, 5.+0.j, 6.+0.j])
```

## DataNote 4: Otras formas de crear arreglos
A travez de las funciones de numpy podemos crear diferentes arreglos especificos
### np.arange()
Permite crear un arreglo en base a un rango, se puden hacer de dos formas.

#### 1.- Un arreglo secuencial 

``` ipython
In [1]: np.arange(0,10)
Out[1]: array([0, 1, 2, 3, 4, 5, 6, 7, 8, 9])
```

#### 2.- Un arreglo secuancial con saltos

``` ipython
In [1]: np.arange(0, 30, 3)
Out[1]: array([ 0,  3,  6,  9, 12, 15, 18, 21, 24, 27])
```

### np.zeros()
Permite crear un arreglo de tamaño n con sólo ceros, se puede definir el tipo de datos que queremos que sea el arrelgo.

``` ipython
In [1]: np.zeros(10)
Out[1]: array([0., 0., 0., 0., 0., 0., 0., 0., 0., 0.])

In [2]: np.zeros(10, dtype=str)
Out[2]: array(['', '', '', '', '', '', '', '', '', ''], dtype='<U1')
```

### np.ones()
Permite crear un arreglo de tamaño *n* con sólo *unos*, se puede definir el tipo de datos que queremos que sea el arrelgo.

``` ipython
In [1]: np.ones(10)
Out[1]: array([1., 1., 1., 1., 1., 1., 1., 1., 1., 1.])

In [2]: np.ones(10, dtype=int)
Out[2]: array([1, 1, 1, 1, 1, 1, 1, 1, 1, 1])

In [3]: np.ones(10, dtype=str)
Out[3]: array(['1', '1', '1', '1', '1', '1', '1', '1', '1', '1'], dtype='<U1')
```

### np.empty()
Define arreglos de longitud *n* con datos "vacios", también conocidos como basura. Este tipo de arrelos se suelen implementar cuando aún no sabemos que datos vamos a guardar en el arreglo, pero sabemos que vamos a necesitarlo. Se puede definir el tipo de dato

``` ipython
In [1]: np.empty(20)
Out[1]:
array([4.24399158e-314, 9.88131292e-324, 0.00000000e+000, 0.00000000e+000,
       0.00000000e+000, 0.00000000e+000, 0.00000000e+000, 0.00000000e+000,
       0.00000000e+000, 0.00000000e+000, 0.00000000e+000, 0.00000000e+000,
       0.00000000e+000, 0.00000000e+000, 0.00000000e+000, 0.00000000e+000,
       0.00000000e+000, 0.00000000e+000, 0.00000000e+000, 0.00000000e+000])

In [2]: np.empty(20, dtype=int)
Out[2]:
array([         0, 1072693248,          0, 1072693248,          0,
       1072693248,          0, 1072693248,          0, 1072693248,
                0, 1072693248,          0, 1072693248,          0,
       1072693248,          0, 1072693248,          0, 1072693248])
```

## DataNote 5: Obtener y actualizar elementos
Podemos obtener elementos a traves de sus indices, así como también cambiar su valor, esto se hace por medio de `a[n]`. Si los indices son positivos, se empieza a hacer la lectura de izquierda a derecha desde 0 hasta el tamaño del arreglo menos 1.

``` ipython
In [1]: import numpy as np

In [2]: a = np.random.randint(0, 10, 20)

In [3]: a
Out[3]: array([1, 7, 3, 2, 8, 4, 6, 7, 7, 4, 4, 4, 2, 0, 4, 5, 0, 6, 9, 3])

In [4]: a[0]
Out[4]: 1

In [5]: a[1]
Out[5]: 7

In [6]: a[19]
Out[6]: 3
```

Si utilizamos números negativos la lectura se hara de derecha a izquierda empezando por el *-1*.

``` ipython
In [7]: a[-1]
Out[7]: 3

In [8]: a[-2]
Out[8] 9
```

Para cambiar el valor de algun elemento sólo debemos especificar su indice y especificar el nuevo valor.

``` ipython
In [9]: a[0] = -8

In [10]: a
Out[10]:
array([-8,  7,  3,  2,  8,  4,  6,  7,  7,  4,  4,  4,  2,  0,  4,  5,  0,
        6,  9,  3])
```

## DataNote 6: Subarreglos
Existen varias formas de generar subarreglos en base a los indices o elementos de un arreglo, a continuación te muestro las mas comunes con base al siguiente arreglo `a`.

``` ipython
In [3]: a
Out[3]: array([4, 8, 8, 8, 2, 1, 4, 3, 8, 8, 5, 0, 2, 7, 9, 3, 8, 5, 0, 9])
```

### Por indices y saltos
Podemos obtener un sub arreglo especificando el indice de inicio, el final y los saltos que se haran para generar el sub arreglo. Cabe mencionar que si no se especifica el inicio se entendera que es desde el primer elemento, sino se especifica el final se entendera que seara hasta el último elemento y si no se especifica la cantidad de saltos se harán de 1 en 1.

### Sintaxis `array[inicio:fin:saltos]`
### Ejemplos

``` ipython
In [4]: b = a[1:7:2]

In [5]: b
Out[5]: array([8, 8, 1])

In [6]: c = a[8:15]

In [7]: type(b)
Out[7]: numpy.ndarray

In [8]: type(c)
Out[8]: numpy.ndarray

In [9]: d = a[0::3]

In [10]: d
Out[10]: array([4, 8, 4, 8, 2, 3, 0])
```

### Especificando directamente los indices
Se pueden especificar los indices los cuales se quieren obtener del arreglo para generar el subarreglo correspondiente.

``` ipython
In [11]:  b = a[[8, 9, 10, 11, 12, 13, 14]]

In [12]: b
Out[12]: array([8, 8, 5, 0, 2, 7, 9])
```

### Por valores booleanos
Podemos colocar valores booleanos en los indices para especificar que valores queremos obtener del arreglo para generar el subarreglo correspondiente. El valor `True` significa que queremos obtener ese indice y por consiguiente `False` significara que no. Es importante resaltar que debemos colocar un valor para cada indice sin omitir uno o poner de mas.
``` ipython
In [13]: b[[True, False, True, False, True]]
Out[13]: array([1, 3, 5])

In [14]: b[[True, False, True, False]]
---------------------------------------------------------------------------
IndexError                                Traceback (most recent call last)
Cell In[14], line 1
----> 1 b[[True, False, True, False]]

IndexError: boolean index did not match indexed array along dimension 0; dimension is 5 but corresponding boolean dimension is 4
```

## DataNote 7: Vectorizar funciones
Si nosotros queremos que los elementos de un arreglo sean procesados por una función y a su vez guardar este procesamiento en un arreglo, entonces debemos vectorizar la función. Esto se logra gracias al metodo `numpy.vectorize()` que nos pedira como argumento una función y nos retornara un objeto que actua como una función, pero tomara como argumento arreglos y matrices. Dicho objeto retornara un arreglo procesado por la función.

``` ipython
In [1]: import numpy as np

In [2]: a = np.random.randint(0, 10, 20)

In [3]: a
Out[3]: array([4, 4, 2, 4, 9, 0, 8, 8, 2, 6, 7, 7, 8, 2, 7, 7, 4, 9, 4, 1])

In [4]: def operacion(val):
   ...:     return (val ** 2) + 2
   ...:

In [5]: operacion(2)
Out[5]: 6

In [6]: vectorizacion = np.vectorize(operacion)

In [7]: vectorizacion(a)
Out[7]:
array([18, 18,  6, 18, 83,  2, 66, 66,  6, 38, 51, 51, 66,  6, 51, 51, 18,
       83, 18,  3])

In [8]: vectorizacion = np.vectorize(lambda valor: (valor ** 2) + 2)

In [9]: vectorizacion(a)
Out[9]:
array([18, 18,  6, 18, 83,  2, 66, 66,  6, 38, 51, 51, 66,  6, 51, 51, 18,
       83, 18,  3])
```

## DataNote 8: Copias y vistas
Existen metodos que de *numpy* que nos permiten crear copias y vistas de arreglos.

Las <strong>copias de un arreglo</strong> permiten crear nuevos arreglos con el mismo contenido y son objetos diferentes.

``` ipython
In [1]: import numpy as np

In [2]: a = np.arange(0, 20)

In [3]: a
Out[3]:
array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
       17, 18, 19])

In [4]: a.copy()
Out[4]:
array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
       17, 18, 19])

In [5]: b = a.copy()

In [6]: id(a)
Out[6]: 1881751874576

In [7]: id(b)
Out[7]: 1881751837776

In [8]: a is b
Out[8]: False

```

Las <strong>vistas de arreglos</strong> permiten crear referencias/punteros al arreglo original, de forma que los cambios que se hagan en alguno de los dos objetos se vera reflejado en el otro. Cabe destacar que estos no son los mismo objetos, pero su contenido base sí lo es.

Existen dos formas de hacer una *vista* de un arreglo, la primer forma es a traves del metodo `.view()` y la otra forma es por medio de la siguiente estructura dentro de corchetes `a[:]`.

``` ipython
In [9]: a.view()
Out[9]:
array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
       17, 18, 19])

In [10]: c = a.view()

In [11]: c
Out[11]:
array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
       17, 18, 19])

In [12]: a[0] = -8

In [13]: c
Out[13]:
array([-8,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
       17, 18, 19])

In [14]: a is c
Out[14]: False

In [15]: a is c.base
Out[15]: True

In [16]: c = a[:]

In [17]: c
Out[17]:
array([-8,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10, 11, 12, 13, 14, 15, 16,
       17, 18, 19])

In [18]: a is c.base
Out[18]: True
```

## DataNote 9: Matrices
Al igual que con las listas también podemos hacer matrices con arreglos de *numpy*, la forma en la que suele hacerse es creando un arreglo que contenga a otros arreglos o listas.

``` ipython
m = np.array([
 np.arange(1,6),
 np.arange(10,60,10),
 np.arange(100,600,100),
])

m = np.array([
 [1, 2, 3, 4, 5],
 [10, 20, 30, 40, 50],
 [100, 200, 300, 400, 500],
])
```

``` ipython
In [3]: m
Out[3]:
array([[  1,   2,   3,   4,   5],
       [ 10,  20,  30,  40,  50],
       [100, 200, 300, 400, 500]])

In [4]: m.ndim
Out[4]: 2

In [5]: m.shape
Out[5]: (3, 5)
```
Como podemos observar se genera un arreglo de arreglos que tiene dos dimensiones y en esta matrices sus dimenciones/forma es de 3x5 (tres renglones y cinco columnas).

La forma en la que podemos acceder a sus datos practicamente de la misma que la de los arreglos de una dimensión. El procedimiento conciste en especificar primero a que renglon queremos acceder y después en que columna se encuentra el dato, hay dos formas de hacer esto: `[][]` o `[, ]`.

``` ipython
In [6]: m[0][0]
Out[6]: 1

In [7]: m[-1][-1]
Out[7]: 500

In [8]: m[0, 0]
Out[8]: 1

In [9]: m[-1, -1]
Out[9]: 500
```

Al igual que en los arreglos de una dimensión en las matrices podemos obtener sub arreglos por medio de los indices lo cual nos permitira obtener renglones o columas especificas. Recuerde que todos nuestros indices positivos empiezan en **0**.

> **Obtener Renglones** 

``` ipython
In [10]: m[:2]
Out[10]:
array([[ 1,  2,  3,  4,  5],
       [10, 20, 30, 40, 50]])

In [11]: m[:2][0]
Out[11]: array([1, 2, 3, 4, 5])

In [12]: m[:2][1]
Out[12]: array([10, 20, 30, 40, 50])
```

> **Obtener columnas**
``` ipython
In [13]: m
Out[13]:
array([[  1,   2,   3,   4,   5],
       [ 10,  20,  30,  40,  50],
       [100, 200, 300, 400, 500]])

In [14]: m[:, 2]
Out[14]: array([  3,  30, 300])

In [15]: m[1:, 2]
Out[15]: array([ 30, 300])

In [16]: m[:, 2:4]
Out[16]:
array([[  3,   4],
       [ 30,  40],
       [300, 400]])
```

## DataNote 10: Metodos de agregación
Existen varios metodos agregación que pueden ser aplicados a los arreglos y matrices con *numpy*.

> **Matriz**
``` ipython
In [1]: import numpy as np

In [2]: m = np.array([
   ...:  np.arange(1,6),
   ...:  np.arange(10,60,10),
   ...:  np.arange(100,600,100),
   ...: ])

In [3]: m
Out[3]:
array([[  1,   2,   3,   4,   5],
       [ 10,  20,  30,  40,  50],
       [100, 200, 300, 400, 500]])

In [4]: m.std()
Out[4]: 157.21323099535866

In [5]: m.sum()
Out[5]: 1665

In [6]: m.min()
Out[6]: 1

In [7]: m.max()
Out[7]: 500

In [8]: m.mean()
Out[8]: 111.0
```

> **Arreglos**
``` ipython
In [9]: m[1].sum()
Out[9]: 150

In [10]: m[2].max()
Out[10]: 500

In [11]: m[:, 3].mean()
Out[11]: 148.0
```

> **Sub arreglos**
``` ipython
In [12]: m[:, 3:].min()
Out[12]: 4
```

> **Nota**
Recomiendo guardar nuestra matriz `m` para poder reutilizarla en otras instancias de ipython sin tener que volverla a crear.

`%store m`

## DataNote 11: Transposición
La transposicion es un atributo de nuestros arreglos de *numpy* el cual nos devuelve un arreglos transpuesto (intercambio de filar por columnas). La complejidad de este proceso es de `O(1)`.

``` ipython
In [1]: import numpy as np

In [2]: store -r m

In [3]: m
Out[3]:
array([[  1,   2,   3,   4,   5],
       [ 10,  20,  30,  40,  50],
       [100, 200, 300, 400, 500]])

In [4]: m.T
Out[4]:
array([[  1,  10, 100],
       [  2,  20, 200],
       [  3,  30, 300],
       [  4,  40, 400],
       [  5,  50, 500]])

In [5]: m.shape
Out[5]: (3, 5)

In [6]: m.T.shape
Out[6]: (5, 3)
```

Cómo vemos esto nos devuelve nuestra matriz original, pero tranpuesta. Esto tine la utilidad que nos permite simplificar algunos procesos o hacerlos más entendibles para nosotros los programadores, por ejemplo si quisieramos obtener la suma de todos los elementos de la cuarta columna de nuestra matriz `m`.

``` ipython
In [7]: m[:, 3].sum()
Out[7]: 444

In [8]: m.T[3].sum()
Out[8]: 444
```

## DataNote 12: Filtros y condiciones
La libreria de *numpy* nos permite aplicarles operaciones lógicas a nuestros arreglos, esto nos permite generar arreglos rapidamente en base a los operadores booleanos que utilicemos, a continuación te muestro un ejemplo:

``` ipython
In [1]: import numpy as np

In [2]: a = np.random.randint(0, 200, 50)

In [3]: a > 65
Out[3]:
array([ True,  True,  True,  True, False,  True, False,  True,  True,
       False, False, False, False, False,  True,  True,  True, False,
        True,  True, False,  True,  True,  True, False,  True,  True,
        True,  True, False, False,  True,  True,  True, False,  True,
        True, False,  True, False,  True,  True,  True,  True,  True,
        True,  True,  True,  True,  True])
```

Podemos observar como al aplicar la condición de `a > 65` nos devuelve un arreglo con la misma forma que el original, pero con valores booleanos donde se cumplio la condición de que el valor fuera mayor que 65. Este nuevo arreglo puede ser utilizado de varias formas, como por ejemplo generar un sub arreglo que tenga todos los elementos que cumplieron la condición.

``` ipython
In [4]: a[a > 65]
Out[4]:
array([160,  84, 158, 128, 106, 154, 119,  97, 181, 114, 156,  94, 149,
       180, 142, 162, 164, 184, 182, 173, 160, 192, 135, 149, 137,  95,
       122,  71, 118, 133, 101,  71, 164, 190, 124])

In [5]: a[a <= 10]
Out[5]: array([7, 1, 2])
```

Esto no esta limitado a una sola condición, nosotros si lo deseamos podemos poner *n* condiciones que cumplir para el nuevo sub arreglo, la sintaxis requeria que las condiciones esten entre `()` y que haya operadores lógicos entre ellas `&`, `|`, `^`.

``` ipython
In [6]: a[ (a > 20) & (a < 100) ]
Out[6]: array([84, 63, 45, 34, 45, 56, 22, 97, 94, 61, 55, 95, 71, 71])

In [7]: a[(a < 10) | (a > 180)]
Out[7]: array([181,   7, 184, 182,   1, 192,   2, 190])
```

Para terminar cabe mencionar que a estos arreglos se les puede aplicar directamente cualquier operador lógico.

> **Nota**
Recomiendo guardar nuestro arreglo `a` para poder reutilizarla en otras instancias de ipython sin tener que volverla a crear.

`%store a`

## DataNote 13: Condiciones
Como vimos en el tema pasado *numpy* nos permite agregarle condiciones a nuestros arreglos. Existen 2 funciones de *numpy* con las que podemos aplicar condicionales a todo el arreglo.
1- La primera se llama `np.all()` y es para comprobrar si una condición se cumple para cada elemento del arreglo, también se nos permite agregar *n* condiciones.

``` ipython
In [1]: import numpy as np

In [2]: store -r a

In [3]: a
Out[3]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])

In [4]: np.all(a > 65)
Out[4]: False

In [5]: np.all(a > 0)
Out[5]: True

In [6]: np.all( (a > 0) & (a < 200) )
Out[6]: True
```

2- La segunda se llama `np.any()` y es para comprobar si en algun caso del arreglo se cumple la condición, también se nos permite agregar *n* condiciones.

``` ipython
In [7]: np.any(a > 65)
Out[7]: True

In [8]: np.any(a < 0)
Out[8]: False

In [9]: np.any( (a < 0) | (a > 180) )
Out[9]: True
```

## DataNote 14: Where y Select
Continuando con el tema de condiciones, *numpy* también nos afrece funciones que nos permiten realizar una o más acciones especificas si se cumple una condición o una serie de condiciones.

Para los ejemplos imaginemos que tenemos una lista de los puntos de calidad de *n* productos y queremos mandar un mensaje cuando tengan un cierto puntaje.

### where()

La función *where* nos permie realizar una acción si se cumple una condición determinada o hacer otra sino se cumple, esto para cada elemento dentro del arreglo. La sintaxis es la siguiente `np.where(_condicion_, _se cumple_, _no se cumple_)`, Esto va agregar valores espefificos cuando se cumplan o no se cumplan. Por ejemplo este código que dira *Este producto cumple con las minimas normas de calidad* si es que tienen un puntaje mayor o igual a 150, de lo contrario mandara un mensaje diciendo que no las cumplen.

``` ipython
In [1]: import numpy as np

In [2]: productos = np.random.randint(50, 200, 10)

In [3]: productos
Out[3]: array([170,  54,  82, 143,  65, 195, 175,  97, 148, 107])

In [4]: np.where(productos >= 150, "Este producto cumple con las minimas normas de calidad", "Este producto no cumple con las minimas
   ...: normas de calidad")
Out[4]:
array(['Este producto cumple con las minimas normas de calidad',
       'Este producto no cumple con las minimas normas de calidad',
       'Este producto no cumple con las minimas normas de calidad',
       'Este producto no cumple con las minimas normas de calidad',
       'Este producto no cumple con las minimas normas de calidad',
       'Este producto cumple con las minimas normas de calidad',
       'Este producto cumple con las minimas normas de calidad',
       'Este producto no cumple con las minimas normas de calidad',
       'Este producto no cumple con las minimas normas de calidad',
       'Este producto no cumple con las minimas normas de calidad'],
      dtype='<U57')
```

### select()
La funcion *select* nos permite establecer una relación entre varias condicionales y varios valores para cada elemento, de forma que en base a la condición que cumpla el elemento será el valor que se asigne a su posición. El primer paso es definir la serie de condiciones, en nuestro caso serán las normas de calidad, y posteriormente definiremos el valor que vamos a querer asignar a cada condicional que definimos; es importante mencionar que la cantidad de valores tiene que ser la misma cantidad que de condicionales definidas. Ls sintaxis de *select* es la sieguiente `np.select(_arreglo de condiciones_, _arreglo de valores_)` 

``` ipython
In [5]: productos = np.append(productos, 199)

In [6]: normasCalidad = [ (productos == 199),
    ...: ( (productos >= 175) & (productos < 199) ),
    ...: ( (productos >= 150) & (productos < 175) ),
    ...: (productos < 150)
    ...: ]

In [7]: mensaje = [
    ...: 'El producto cumple con todas las normas de calidad :D', #Calidad de 199
    ...: 'El producto cumple con la mayoria de las normas de calidad :)', #Calidad entre 175 y 198
    ...: 'El producto cumple con las minimas normas de calidad :|', #Calidad entre 150 y 174
    ...: 'El procuto no cumple con minimas normas de calidad >:T'] #Calidad menor que 150

In [8]: np.select(normasCalidad, mensaje)
Out[8]:
array(['El producto cumple con las minimas normas de calidad :|',
       'El procuto no cumple con minimas normas de calidad >:T',
       'El procuto no cumple con minimas normas de calidad >:T',
       'El procuto no cumple con minimas normas de calidad >:T',
       'El procuto no cumple con minimas normas de calidad >:T',
       'El producto cumple con la mayoria de las normas de calidad :)',
       'El producto cumple con la mayoria de las normas de calidad :)',
       'El procuto no cumple con minimas normas de calidad >:T',
       'El procuto no cumple con minimas normas de calidad >:T',
       'El procuto no cumple con minimas normas de calidad >:T',
       'El producto cumple con todas las normas de calidad :D'],
```

## DataNote 15: Crear y leer archivos

### savetxt() y loadtxt()
La libreria de *numpy* nos permite guardar arreglos en archivos y también podemos obtener arreglos de archivos. a traves de los comandos `np.savetxt()` y `np.loadtxt()`

``` ipython
In [1]: import numpy as np

In [2]: store -r a

In [3]: a
Out[3]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])

In [4]: np.savetxt('arreglo_a.txt', a) #(_nombre y extension del archivo_, _arreglo numpy_)

In [5]: ls

         .
         ..
         1,300 arreglo_a.txt

         <DIR>          env
```

Cómo podemos observar guardamos nuestro arreglo `a` en un archivo *.txt*, ahor si nosotros queremos cargar el arreglo del archivo a nuesto entorno de ipython usamos el comando `np.loadtxt()`

``` ipython
In [6]: load arreglo_a.txt

   ...: 9.700000000000000000e+01
   ...: 1.810000000000000000e+02
   ...: 1.140000000000000000e+02
   ...: 7.000000000000000000e+00
   ...: 1.560000000000000000e+02
   ...: 9.400000000000000000e+01
   ...: 1.600000000000000000e+01
   ...: 1.490000000000000000e+02
   ...: 1.800000000000000000e+02
   ...: 1.420000000000000000e+02
   ...: 6.100000000000000000e+01
   ...: 1.620000000000000000e+02
   ...: 1.640000000000000000e+02
   ...: 1.840000000000000000e+02
   ...: 1.820000000000000000e+02
   ...: 1.000000000000000000e+00
   ...: 1.300000000000000000e+01
   ...: 1.730000000000000000e+02
   ...: 1.600000000000000000e+02
   ...: 1.920000000000000000e+02
   ...: 2.000000000000000000e+01
   ...: 1.350000000000000000e+02
   ...: 1.490000000000000000e+02
   ...: 5.500000000000000000e+01
   ...: 1.370000000000000000e+02
   ...: 2.000000000000000000e+00
   ...: 9.500000000000000000e+01
   ...: 1.220000000000000000e+02
   ...: 7.100000000000000000e+01
   ...: 1.180000000000000000e+02
   ...: 1.330000000000000000e+02
   ...: 1.010000000000000000e+02
   ...: 7.100000000000000000e+01
   ...: 1.640000000000000000e+02
   ...: 1.900000000000000000e+02
   ...: 1.240000000000000000e+02
Out[7]: 124.0
```

Ya hemos cargado el arreglo, pero se ve un poco extraño y eso se debe a que cuando lo guardamos no especificamos como que tipo de dato lo guardamos y es importanto especificarlo porque sino lo guardara como número complejos, como es este caso.

``` ipython
In [10]: np.savetxt('arreglo_a.txt', a, fmt='%i')

In [12]: np.loadtxt('arreglo_a.txt') #sin especificar el tipo de dato que deseamos
Out[12]:
array([160.,  84., 158., 128.,  11., 106.,  63., 154., 119.,  45.,  34.,
        45.,  56.,  22.,  97., 181., 114.,   7., 156.,  94.,  16., 149.,
       180., 142.,  61., 162., 164., 184., 182.,   1.,  13., 173., 160.,
       192.,  20., 135., 149.,  55., 137.,   2.,  95., 122.,  71., 118.,
       133., 101.,  71., 164., 190., 124.])

In [13]: np.loadtxt('arreglo_a.txt', dtype=int) #especificando el tipo de dato que deseamos
Out[13]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])

In [15]: np.all( a == np.loadtxt('arreglo_a.txt', dtype=int) )
Out[15]: True

```

Ahora bien, si nosotros vamos a guardar matrices o arreglos de más de una dimensión se recomienda que se guarden en archivos *.csv* y se pongan delimitadores *;* para hacer una buena distiención entre cada uno de los elementos.

``` ipython
In [16]: store -r m

In [17]: m
Out[17]:
array([[  1,   2,   3,   4,   5],
       [ 10,  20,  30,  40,  50],
       [100, 200, 300, 400, 500]])

In [18]: np.savetxt('matriz_m.csv', m, fmt='%i', delimiter=';')

In [5]: ls

         .
         ..
         1,300 arreglo_a.txt
	 48 matriz_m.csv
         <DIR>          env

In [22]: load matriz_m.csv

In [23]: # %load matriz_m.csv
    ...: 1;2;3;4;5
    ...: 10;20;30;40;50
    ...: 100;200;300;400;500
    ...:
Out[23]: 500

In [21]: np.all( m == np.loadtxt('matriz_m.csv',delimiter=';' , dtype=int) )
Out[21]: True
```

### save() y load()
Al igual que `np.savetxt()` y `np.loadtxt()` las funciones `np.save()` y `np.load()` nos permiten guardar arreglos de *numpy* en archivos, pero se diferencian porque se guardaran como archivos binarios. Por conveción estos archivos tienen que tener la extensión `.npy`, esto con el proposito de comunicar a nosotros los programadores que el archivo almacena un arreglo de *numpy* en el lenguaje de *python*.

``` ipython
In [1]: import numpy as np

In [2]: store -r a

In [3]: a
Out[3]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])

In [4]: np.save('arreglo_a.npy', a)

In [5]: ls

         .
         ..
	 328 arreglo_a.npy
         1,300 arreglo_a.txt
	 48 matriz_m.csv
         <DIR>          en
```

Si nosotros tratapos de cargar o inspeccionar el archivo a traves de ipython se nos lansara un error, ya que ipython no es capaz de leer estos archivos.

``` ipython
In [6]: load arreglo_a.npy
Traceback (most recent call last):

  File ~\AppData\Local\Programs\Python\Python311\Lib\tokenize.py:334 in find_cookie
    line_string = line.decode('utf-8')

UnicodeDecodeError: 'utf-8' codec can't decode byte 0x93 in position 0: invalid start byte


During handling of the above exception, another exception occurred:

In [7]: pycat arreglo_a.npy
Traceback (most recent call last):

  File ~\AppData\Local\Programs\Python\Python311\Lib\tokenize.py:334 in find_cookie
    line_string = line.decode('utf-8')

UnicodeDecodeError: 'utf-8' codec can't decode byte 0x93 in position 0: invalid start byte
```

Así que si deseamos conocer el contenido del archivo debemos cargarlo a traves de *numpy*, ya que esta libreria es quien creo ese archivo binario y es capaz de entenderlo.

``` ipython
In [8]: np.load('arreglo_a.npy')
Out[8]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])
```

## DataNote 16: Modificando arreglos
Sabemos que los arreglos del tipo *numpy* no pueden ser modificados después de ser creados, es decir, no podemos cambiar su tamaño, añadir elementos, remover elementos, etc. Sin embargo *numpy* ofrece varias funciones que nos permiten ***crear nuevos arreglos*** para haci poder hacer modificaciones.

``` ipython
In [1]: import numpy as np

In [2]: store -r a

In [3]: a
Out[3]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])

In [4]: a.size
Out[4]: 50
```

### insert()
La función `.insert()` crea un arreglo el cual se insertar un nuevo elemento en el indice que nosotros especifiquemos.

**Sintaxis**
`np.insert(_arreglo_, _indice_, _elemento_)`

``` ipython
In [5]: np.insert(a, 0, 50)
Out[5]:
array([ 50, 160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,
        56,  22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61,
       162, 164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55,
       137,   2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])

In [6]: a #Veremos que el arreglo original no cambio
Out[6]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])
```

### append()
La función `.append()` crea un arreglo en el cual se insertar un nuevo elemento al final de dicho arreglo.

**Sintaxis**
`np.append(_arreglo_, _elemento_)`

``` ipython
In [7]: np.append(a, 50)
Out[7]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124,  50])

In [8]: a #Veremos que el arreglo original no cambio
Out[8]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])
```
### delete()
La función `.delete()` crea un arreglo en el cual se elimina un elemento en el indice que nosotros especifiquemos.

**Sintaxis**
`np.delete(_arreglo_, _indice_)`

``` ipython
In [9]: np.delete(a, -1)
Out[9]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190])

In [10]: a
Out[10]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])
```

### resize()
La función `.resize()` crea un arreglo en el cual redimenciona un arreglo a las dimensiones que nosotros especifiquemos.

**Sintaxis**
`np.resize(_arreglo_, _dimensiones_)` o bien `np.resize( _arreglo_, ( _d1_, _d2_ ) )`

``` ipython
In [11]: np.resize(a, 20)
Out[11]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94])

In [12]: a
Out[12]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])
```
### concatenate()
La función `.concatenate()` crea un nuevo arreglo en el cual será la union de todos los arreglos que se le pasen como parametro.

**Sintaxis**
`np.concatenate( [ _a1_, _a2_, ..., _an_ ] )`

``` ipython
In [13]: b = np.arange(0,11)

In [14]: b
Out[14]: array([ 0,  1,  2,  3,  4,  5,  6,  7,  8,  9, 10])

In [15]: np.concatenate( [a, b] )
Out[15]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124,   0,   1,
         2,   3,   4,   5,   6,   7,   8,   9,  10])

In [16]: np.concatenate( [ a, b, [500, 600, 700, 800] ] )
Out[16]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124,   0,   1,
         2,   3,   4,   5,   6,   7,   8,   9,  10, 500, 600, 700, 800])
```

### ¿Qué hago si quiero guardar los cambios que le hice al arreglo?
Si quieres guardar el nuevo arreglo con las modificaciones todo lo que tienes que hacer es guardarlo en una nueva variable o hasta en la misma variable donde tienes el arreglo actual, ejemplos:

``` ipython
In [17]: a = np.append(a, 50)

In [18]: a
Out[18]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124,  50])

In [19]: a = np.delete(a, -1)

In [20]: a
Out[20]:
array([160,  84, 158, 128,  11, 106,  63, 154, 119,  45,  34,  45,  56,
        22,  97, 181, 114,   7, 156,  94,  16, 149, 180, 142,  61, 162,
       164, 184, 182,   1,  13, 173, 160, 192,  20, 135, 149,  55, 137,
         2,  95, 122,  71, 118, 133, 101,  71, 164, 190, 124])
```

## DataNote 17: Ordenamiento
Existe un metodo en la libreria de *numpy* que nos permite ordenar nuestros elementos de forma ascendente, este es el metodo `.sort()`

``` ipython
In [1]: import numpy as np

In [2]: a = np.random.randint(0, 20, 15)

In [3]: a
Out[3]: array([ 3, 15,  5,  6,  9, 11,  5, 18, 17, 12,  1, 10, 16, 12,  1])

In [4]: a.sort()

In [5]: a
Out[5]: array([ 1,  1,  3,  5,  5,  6,  9, 10, 11, 12, 12, 15, 16, 17, 18])
```

Si nosotros queremos que el orden de ordenamiento este de forma descendente sólo es necesario indicar que se itere de forma negativa en el arreglo.

``` ipython
In [6]: a[::-1]
Out[6]: array([18, 17, 16, 15, 12, 12, 11, 10,  9,  6,  5,  5,  3,  1,  1])

In [7]: a = a[::-1]

In [8]: a
Out[8]: array([18, 17, 16, 15, 12, 12, 11, 10,  9,  6,  5,  5,  3,  1,  1])
```

Si nosotros deseamos ordenar nuestro arreglo, pero a su vez no queremos que modifique el original sino que se guarde en una nueva variable lo podemos hacer llamando directamente a la libreria *numpy*.

``` ipython
In [9]: b = np.random.randint(0,20,20)

In [10]: b
Out[10]:
array([ 5, 19, 14, 19,  1, 19, 10, 14,  1,  7,  2, 18, 18,  7,  7,  7,  2, 19,  8,  5])

In [11]: np.sort(b)
Out[11]:
array([ 1,  1,  2,  2,  5,  5,  7,  7,  7,  7,  8, 10, 14, 14, 18, 18, 19, 19, 19, 19])

In [12]: b
Out[12]:
array([ 5, 19, 14, 19,  1, 19, 10, 14,  1,  7,  2, 18, 18,  7,  7,  7,  2, 19,  8,  5])

In [13]: c = np.sort(b)[::-1]

In [14]: c
Out[14]:
array([19, 19, 19, 19, 18, 18, 14, 14, 10,  8,  7,  7,  7,  7,  5,  5,  2, 2,  1,  1])
```

