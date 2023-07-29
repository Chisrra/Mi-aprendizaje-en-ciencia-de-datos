# Pandas
## DataNote 1: Series
**Pandas** es una libreria que nos permite almacenar y manipular los datos, al igual que la libreria de *numpy* guarda los datos en arreglos unidimensionales, pero *pandas* se caracteriza por almacenar los datos en *Series* y no en *array*.

Las **Series** de *pandas* se caracterizan por asignarle un *indice* a cada uno de sus datos, los *indices* pueden ser de cualquier tipo de dato inmutable(aquellos que no pueden modificar su valor después de crearse). 

Existen varias formas de crear una serie de *pandas*, a continuación te muestro la forma más sencilla de hacerlo.

``` ipython
In [1]: import pandas as pd  #Para buenas practicas renombramos a pandas como pd

In [2]: pd.Series([1, 2, 3, 4, 5])
Out[2]:
0    1
1    2
2    3
3    4
4    5
dtype: int64

In [3]: a = pd.Series([1, 2, 3, 4, 5])
```
La libreria *pandas* también cuenta con varios metodos que nos permiten conocer la estructura de la serie.

``` ipython
In [4]: a.size
Out[4]: 5

In [5]: a.dtype
Out[5]: dtype('int64')

In [6]: a.shape
Out[6]: (5,)

In [7]: a.index #Nos muestra los rangos de los indices
Out[7]: RangeIndex(start=0, stop=5, step=1)
```

Al igual que en los arreglos podemos modificar los valores de los elementos a traves de su index

``` ipython
In [8]: a
Out[8]:
0    1
1    2
2    3
3    4
4    5
dtype: int64

In [9]: a[2]
Out[9]: 3

In [10]: a[2] = 20

In [11]: a[2]
Out[11]: 20
```

Y por último, existen otros parametros que podemos especificar al momento de crear *Series*:

-  `index`: definimos los indices en forma de lista o de indices de *pandas*, debe haber la misma cantidad de indices que de elementos.

``` ipython
In [12]: pd.Series([1, 2, 3, 4, 5], index=['a','b','c','d','e'])
Out[12]:
a    1
b    2
c    3
d    4
e    5
dtype: int64

In [13]: a = pd.Series([1, 2, 3, 4, 5], index=['a','b','c','d','e'])

In [14]: a['b']
Out[14]: 2

In [15]: a['b'] = 15

In [16]: a['b']
Out[16]: 15
```

- `name`: le damos un nombre a la serie, el dato es string.

``` ipython
In [17]: pd.Series([1, 2, 3, 4, 5], index=['a','b','c','d','e'], name='abecedario')
Out[17]:
a    1
b    2
c    3
d    4
e    5
Name: abecedario, dtype: int64
```

- `dtype`: definimos el tipo de datos de los elementos. 

``` ipython
In [18]: pd.Series([1, 2, 3, 4, 5], index=['a','b','c','d','e'], name='abecedario', dtype=float)
Out[18]:
a    1.0
b    2.0
c    3.0
d    4.0
e    5.0
Name: abecedario, dtype: float64
```

## DataNote 2: Creando Series
Una forma alternativa de crear *Series* es a traves de diccionarios, cuando nosotros definimos un diccionario podemos pasarlo como argumento al momento de crear una *Serie* para así crear un objeto *Serie* que tenga los indices/llaves y elementos del diccionario.

``` ipython
In [1]: import pandas as pd

In [2]: a = {
   ...: 'a': 1,
   ...: 'b': 2,
   ...: 'c': 3,
   ...: 'd': 4
   ...: }

In [3]: pd.Series(a)
Out[3]:
a    1
b    2
c    3
d    4
dtype: int64

In [4]: a['b']
Out[4]: 2

In [5]: a = pd.Series(a)

In [6]: a['b']
Out[6]: 2
```

## DataNote 3: Valores núlos
No es raro que en estudios del mundo real haya casos en los que no se pueda obtener información o no pueda representarse sobre un elemento o algun caso, es por ello que debemos ser capaces de representar estos caso. Para lograr lo anterior la libreria de *numpy* nos proporciona un tipo de dato llamado *NaN*(Not a Number). A continuación mostraremos cómo sería la implementación en código.

``` ipython
In [1]: import pandas as pd

In [2]: import numpy as np

In [3]: np.nan
Out[3]: nan

In [4]: pd.Series([1, 2, 3, np.nan, np.nan,6, np.nan, 8, np.nan])
Out[4]:
0    1.0
1    2.0
2    3.0
3    NaN
4    NaN
5    6.0
6    NaN
7    8.0
8    NaN
dtype: float64
```

Existen dos metodos para comprobar si existen elementos `NaN` en las *Series*, estos son `.isnull()` y `.notnull()`, estos metodos nos retornar una *Serie* con valores booleanos que nos dicen, respectivamente, que indice es null y cual no es null.

``` ipython 
In [5]: a = pd.Series([1, 2, 3, np.nan, np.nan,6, np.nan, 8, np.nan])

In [6]: a.isnull()
Out[6]:
0    False
1    False
2    False
3     True
4     True
5    False
6     True
7    False
8     True
dtype: bool

In [7]: a.notnull()
Out[7]:
0     True
1     True
2     True
3    False
4    False
5     True
6    False
7     True
8    False
dtype: bool
```

Como punto extra, podemos extraer los indices y datos que son o no null en nuevas *Series*

``` ipython 
In [8]: a[ a.isnull() ]
Out[8]:
3   NaN
4   NaN
6   NaN
8   NaN
dtype: float64

In [9]: a[ a.notnull() ]
Out[9]:
0    1.0
1    2.0
2    3.0
5    6.0
7    8.0
dtype: float64
```

## DataNote 4: DataFrame

###¿Qué son?
Los *DataFrame* son estructuras de datos tabulares que nos proporciona *pandas*, este tipo de estructura de datos es similar a una tabla de una base de datos o hoja de calculo, donde las cosas estan organizadas en filas y columnas. Cada columna representa una variable o característica de los datos, y cada fila representa una entrada u observación de datos.

Los *DataFrame* son estructuras de datos flexibles; pueden contener diferentes tipos de datos; cuentan con una gran variedad de funciones y métodos para realizar análisis, liempieza y manipulación compleja de los datos. Estas estructuras son perfectas su queremos realizar operaciones de filtrado, ordenamiento, agregación o transformación de datos.

### Creando un DataFrame
A continuación se muestra un código de cómo crear un DataFrame de manera sencilla a traves de un diccionario, tal que las llaves del diccionario serán las columnas del DataFrame y los valores(series de datos) de las llaves la información de entrada/observación de cada renglon.

``` ipython 
In [1]: import pandas as pd

In [2]: productos = {
   ...: 'nombre': ['producto 1', 'producto 2', 'producto 3'],
   ...: 'material': ['material 1', 'material 2', 'material 3'],
   ...: 'costos': [100, 500, 250],
   ...: 'produccion': [True, True, False] }

In [3]: productos
Out[3]:
{'nombre': ['producto 1', 'producto 2', 'producto 3'],
 'material': ['material 1', 'material 2', 'material 3'],
 'costos': [100, 500, 250],
 'produccion': [True, True, False]}
```

Al igual que en las *Series* podemos definir los indices de los renglones(entradas/observaciones) del DataFrame.

``` ipython 
In [4]: pd.DataFrame(productos)
Out[4]:
       nombre    material  costos  produccion
0  producto 1  material 1     100        True
1  producto 2  material 2     500        True
2  producto 3  material 3     250       False

In [5]: pd.DataFrame(productos, index = ['pA', 'pB', 'pC'])
Out[5]:
        nombre    material  costos  produccion
pA  producto 1  material 1     100        True
pB  producto 2  material 2     500        True
pC  producto 3  material 3     250       False
```

### Accediento a los datos
Para acceder a los datos del *DataFrame* podemos hacerlo a traves de llaves o atributos y cómo punto adicional, con los *DataFrame* podemos obtener todos los valores de una columna especifica de forma sencilla.

``` ipython
In [6]: data = pd.DataFrame(productos)
```

#### Llaves
``` ipython
In [7]: data["material"]
Out[7]:
0    material 1
1    material 2
2    material 3
Name: material, dtype: object 

In [8]: data["material"][2]
Out[8]: 'material 3'
```

#### Atributos
``` ipython
In [9]: data.nombre
Out[9]:
0    producto 1
1    producto 2
2    producto 3
Name: nombre, dtype: object
```
#### Columnas y valores
Los *DataFrame* cuentan con metodos que nos permiten obtener los nombres de las columnas y los valores del data Frame

##### Columnas

``` ipython
In [10]: data.columns
Out[10]: Index(['nombre', 'material', 'costos', 'produccion'], dtype='object')
```

##### Valores

``` ipython
In [11]: data.values
Out[11]:
array([['producto 1', 'material 1', 100, True],
       ['producto 2', 'material 2', 500, True],
       ['producto 3', 'material 3', 250, False]], dtype=object)
```

## DataNote 5: Columnas del DataFrame
Recordemos que en *pandas* las columnas de los *data frame* son *Series*, por lo cual podemos hacer cambios en estas, como modificar, agregar o eliminar. Estaremos utilizando el *data frame* de *productos*.


### Agregar columnas
Para agregar columnas es tan sencillo como crear una *Serie* y asignarla al *data frame*, por medio de la sintaxis `_dataFrame_[_columna nueva_] = _serie_`.

``` ipython
In [1]: import pandas as pd

In [2]: store -r productos

In [3]: productos
Out[3]:
        nombre    material  costos  produccion
pA  producto 1  material 1     100        True
pB  producto 2  material 2     500        True
pC  producto 3  material 3     250       False

In [4]: unidades = pd.Series([200, 100, 0])

In [5]: unidades
Out[5]:
0    200
1    100
2      0
dtype: int64

In [6]: productos["unidades"] = unidades

In [7]: productos
Out[7]:
        nombre    material  costos  produccion  unidades
pA  producto 1  material 1     100        True       NaN
pB  producto 2  material 2     500        True       NaN
pC  producto 3  material 3     250       False       NaN
```

Podemos ver que pese a que se agrego la nueva columna `unidades` todos sus valores son `NaN`, esto se debe a que la *Serie* `unidades` que creamos no coincide en ninguno de los indices de `productos`, por lo cual debemos hacer una modificación en los indices de `unidades` para que coindidan con `productos`.

``` ipython
In [8]: unidades = pd.Series([200, 100, 0], index = ['pA', 'pB', 'pC'])

In [9]: productos["unidades"] = unidades

In [10]: productos
Out[10]:
        nombre    material  costos  produccion  unidades
pA  producto 1  material 1     100        True       200
pB  producto 2  material 2     500        True       100
pC  producto 3  material 3     250       False         0
```

### Renombrar columnas
Para renombrar las columnas solo debemos acceder al metodo `rename` de nuestro *data frame* y especificar por medio de un diccionario en el atributo `columns` las columas que deseamos renombrar y el nuevo nombre.

``` ipython
In [11]: productos.rename(
    ...: columns = {'nombre':'producto'}
    ...: )
Out[11]:
      producto    material  costos  produccion  unidades
pA  producto 1  material 1     100        True       200
pB  producto 2  material 2     500        True       100
pC  producto 3  material 3     250       False         0

In [12]: store productos #Almaceno el data frame para utilizarlo en otros ejemplos
Stored 'productos' (DataFrame)
```

### Eliminar columnas
Para eliminar columnas debemos usar la palabra reservada `del` y,seprado por un espacio, especificar la columna que deseamos eliminar.

``` ipython
In [13]: del productos["unidades"]

In [14]: productos
Out[14]:
        nombre    material  costos  produccion
pA  producto 1  material 1     100        True
pB  producto 2  material 2     500        True
pC  producto 3  material 3     250       False
```

## DataNote 6: Leer archivos csv
Al igual que en *numpy* la libreria de *pandas* también nos ofrece la posibilidad de leer archivos csv a traves del metodo `pd.read_csv(_path_)`. La mejor estructura de datos para guardar estos archivos es en un *data frame*.

En este ejemplo utilizare el data set de [Cardiovascular Diseases Risk Prediction Dataset](https://www.kaggle.com/datasets/alphiree/cardiovascular-diseases-risk-prediction-dataset) de CDC.

``` ipython
In [1]: import pandas as pd

In [2]: pd.read_csv("Cardiovascular_Diseases_Risk.csv")
Out[2]:
       General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
0                Poor  Within the past 2 years  ...                         16.0                    12.0
1           Very Good     Within the past year  ...                          0.0                     4.0
2           Very Good     Within the past year  ...                          3.0                    16.0
3                Poor     Within the past year  ...                         30.0                     8.0
4                Good     Within the past year  ...                          4.0                     0.0
...               ...                      ...  ...                          ...                     ...
308849      Very Good     Within the past year  ...                          8.0                     0.0
308850           Fair  Within the past 5 years  ...                         60.0                     4.0
308851      Very Good      5 or more years ago  ...                          8.0                     4.0
308852      Very Good     Within the past year  ...                         12.0                     0.0
308853      Excellent     Within the past year  ...                         12.0                     1.0

[308854 rows x 19 columns]

In [3]: data = pd.read_csv("Cardiovascular_Diseases_Risk.csv")

In [4]: data
Out[4]:
       General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
0                Poor  Within the past 2 years  ...                         16.0                    12.0
1           Very Good     Within the past year  ...                          0.0                     4.0
2           Very Good     Within the past year  ...                          3.0                    16.0
3                Poor     Within the past year  ...                         30.0                     8.0
4                Good     Within the past year  ...                          4.0                     0.0
...               ...                      ...  ...                          ...                     ...
308849      Very Good     Within the past year  ...                          8.0                     0.0
308850           Fair  Within the past 5 years  ...                         60.0                     4.0
308851      Very Good      5 or more years ago  ...                          8.0                     4.0
308852      Very Good     Within the past year  ...                         12.0                     0.0
308853      Excellent     Within the past year  ...                         12.0                     1.0

[308854 rows x 19 columns]
```

Cómo puedes observar nos muestra los primeros y últimos registros del *data frame*. Como nota adicional podemos poner un argumento opcional en `pd.read_csv(_path_)` llamado `index_col = ""` si es que nosotros deseamos que alguna de nuestras columnas sea el indice del *data frame*.

### head() y tail()
Los *data frame* nos ofrecen un metodo para poder ver los primeros y ultimos elementos del data set, estos son `.head()` y `.tail()` respectivamente; podemos pasarle un número entero a estos métodos decir cuantos elementos queremos que se muestre, sino mandamos un número mostrara 5 por defecto.

``` ipython
In [5]: data.head()
Out[5]:
  General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
0           Poor  Within the past 2 years  ...                         16.0                    12.0
1      Very Good     Within the past year  ...                          0.0                     4.0
2      Very Good     Within the past year  ...                          3.0                    16.0
3           Poor     Within the past year  ...                         30.0                     8.0
4           Good     Within the past year  ...                          4.0                     0.0

[5 rows x 19 columns]

In [6]: data.tail(10)
Out[6]:
       General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
308844           Good     Within the past year  ...                          4.0                     2.0
308845           Good     Within the past year  ...                         20.0                     4.0
308846      Very Good     Within the past year  ...                          8.0                     1.0
308847      Very Good      5 or more years ago  ...                          0.0                     0.0
308848           Good  Within the past 5 years  ...                         12.0                     0.0
308849      Very Good     Within the past year  ...                          8.0                     0.0
308850           Fair  Within the past 5 years  ...                         60.0                     4.0
308851      Very Good      5 or more years ago  ...                          8.0                     4.0
308852      Very Good     Within the past year  ...                         12.0                     0.0
308853      Excellent     Within the past year  ...                         12.0                     1.0

[10 rows x 19 columns]
```

## DataNote 7: Limpieza de datos
Es bastante común que en data set del mundo real haya mucha información incompleta o con datos faltantes, es por ello que debemos aprender a hacer una limpieza de nuestros datos. La libreria de pandas nos ofrece dos metodos que nos permiten hacer la limpieza, `.dropna()` y `.fillna()` ambos métodos nos retornan un nuevo *data frame*.

Para provar estos métodos elimine algunos datos entre los primeros 5 registros y 2 columnas del data set [Cardiovascular Diseases Risk Prediction Dataset](https://www.kaggle.com/datasets/alphiree/cardiovascular-diseases-risk-prediction-dataset).

``` ipython
In [1]: import pandas as pd

In [2]: data = pd.read_csv("Cardiovascular_Diseases_Risk.csv")

In [3]: data
Out[3]:
       General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
0                 NaN  Within the past 2 years  ...                           16                      12
1           Very Good     Within the past year  ...                            0                       4
2                 NaN     Within the past year  ...                            3                      16
3                Poor                      NaN  ...                           30                       8
4                Good                      NaN  ...                            4                       0
...               ...                      ...  ...                          ...                     ...
308849      Very Good     Within the past year  ...                            8                       0
308850           Fair  Within the past 5 years  ...                           60                       4
308851      Very Good      5 or more years ago  ...                            8                       4
308852      Very Good     Within the past year  ...                           12                       0
308853      Excellent     Within the past year  ...                           12                       1

[308854 rows x 19 columns]
```

Se puede ver que hay varios datos faltantes.

### dropna()
Este método elimina todos los registros/entradas que tengan algun dato del tipo `NaN`.

``` ipython
In [4]: data.dropna()
Out[4]:
       General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
1           Very Good     Within the past year  ...                            0                       4
5                Good     Within the past year  ...                           12                      12
6                Fair     Within the past year  ...                            8                       0
7                Good     Within the past year  ...                            8                       8
8                Fair     Within the past year  ...                           12                       4
...               ...                      ...  ...                          ...                     ...
308849      Very Good     Within the past year  ...                            8                       0
308850           Fair  Within the past 5 years  ...                           60                       4
308851      Very Good      5 or more years ago  ...                            8                       4
308852      Very Good     Within the past year  ...                           12                       0
308853      Excellent     Within the past year  ...                           12                       1

[308850 rows x 19 columns]
``` 

Vemos que se removieron los registros 0, 2, 3 y 4.

### fillna()
Este método llena todos los datos del tipo `NaN`, esto se puede hacer de dos formas

La primera forma es darle un valor el cual se pondra en todos los datos del tipo `NaN`.

``` ipython
In [5]: data.fillna('val0')
Out[5]:
       General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
0                val0  Within the past 2 years  ...                           16                      12
1           Very Good     Within the past year  ...                            0                       4
2                val0     Within the past year  ...                            3                      16
3                Poor                     val0  ...                           30                       8
4                Good                     val0  ...                            4                       0
...               ...                      ...  ...                          ...                     ...
308849      Very Good     Within the past year  ...                            8                       0
308850           Fair  Within the past 5 years  ...                           60                       4
308851      Very Good      5 or more years ago  ...                            8                       4
308852      Very Good     Within the past year  ...                           12                       0
308853      Excellent     Within the past year  ...                           12                       1

[308854 rows x 19 columns]
```

La segunda forma es proporcionarle un diccionario donde la llave será el nombre de la columna y el valor será el que remplazara los datos del tipo `NaN`.

``` ipython
In [6]: data.fillna({ #columna : nuevo valor,
   ...: 'General_Health':'not specified', 
   ...: 'Checkup':'has not been done'
   ...: })
Out[6]:
       General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
0       not specified  Within the past 2 years  ...                           16                      12
1           Very Good     Within the past year  ...                            0                       4
2       not specified     Within the past year  ...                            3                      16
3                Poor        has not been done  ...                           30                       8
4                Good        has not been done  ...                            4                       0
...               ...                      ...  ...                          ...                     ...
308849      Very Good     Within the past year  ...                            8                       0
308850           Fair  Within the past 5 years  ...                           60                       4
308851      Very Good      5 or more years ago  ...                            8                       4
308852      Very Good     Within the past year  ...                           12                       0
308853      Excellent     Within the past year  ...                           12                       1

[308854 rows x 19 columns]
```

## DataNote 8: Atributo iloc
La forma convencional para acceder a los datos de un *data frame* es a traves de sus columnas, pero gracias al atributo `.iloc` podemos acceder a los registros/entradas del *data frame* por medio de sus indices. El atributo `.iloc` sólo podemos utilizarlo si los indices son del tipo entero.

Para este ejercicio utilizare el data set [Cardiovascular Diseases Risk Prediction Dataset](https://www.kaggle.com/datasets/alphiree/cardiovascular-diseases-risk-prediction-dataset).

``` ipython
In [1]: import pandas as pd

In [2]: data = pd.read_csv("Cardiovascular_Diseases_Risk.csv") #Cargamos el data frame

In [3]: data
Out[3]:
       General_Health  ... FriedPotato_Consumption
0                Poor  ...                      12
1           Very Good  ...                       4
2           Very Good  ...                      16
3                Poor  ...                       8
4                Good  ...                       0
...               ...  ...                     ...
308849      Very Good  ...                       0
308850           Fair  ...                       4
308851      Very Good  ...                       4
308852      Very Good  ...                       0
308853      Excellent  ...                       1

[308854 rows x 19 columns]

In [4]: data["General_Health"] #Acceso convencional por columnas
Out[4]:
0              Poor
1         Very Good
2         Very Good
3              Poor
4              Good
            ...
308849    Very Good
308850         Fair
308851    Very Good
308852    Very Good
308853    Excellent
Name: General_Health, Length: 308854, dtype: object

In [5]: data.iloc[0] #Acceso al primer registro
Out[5]:
General_Health                                     Poor
Checkup                         Within the past 2 years
Exercise                                             No
Heart_Disease                                        No
Skin_Cancer                                          No
Other_Cancer                                         No
Depression                                           No
Diabetes                                             No
Arthritis                                           Yes
Sex                                              Female
Age_Category                                      70-74
Height_(cm)                                         150
Weight_(kg)                                       32.66
BMI                                               14.54
Smoking_History                                     Yes
Alcohol_Consumption                                   0
Fruit_Consumption                                    30
Green_Vegetables_Consumption                         16
FriedPotato_Consumption                              12
Name: 0, dtype: object
```

Como podemos ver accedimos al primer registro y nos devolvio los datos de cada una de sus columnas. Con `.iloc` también podemos crear *sub data frames* indicando el inicio y el fin de los registros que deseamos obtener.

``` ipython
In [6]: data.iloc[2:8]
Out[6]:
  General_Health  ... FriedPotato_Consumption
2      Very Good  ...                      16
3           Poor  ...                       8
4           Good  ...                       0
5           Good  ...                      12
6           Fair  ...                       0
7           Good  ...                       8
```

### Seleccionando columnas
Como nota final, nosotros también podemos seleccionar las columas que nosotros desemos obtener de los registros, hay dos formas

#### Selección a traves de números enteros
En esta forma proporcionaremos una lista de números enteros que indiquen que columnas deseamos, la numeración de las columnas empieza a partir del cero.

``` ipython
In [7]: data.iloc[2:8, [0,2,13]]
Out[7]:
  General_Health Exercise    BMI
2      Very Good      Yes  33.47
3           Poor      Yes  28.73
4           Good       No  24.37
5           Good       No  46.11
6           Fair      Yes  22.74
7           Good      Yes  39.94
```

#### Selección a traves de nombres de las columas
En esta formas abriremos un segundo par de corchetes en el cual proporcionaremos uns lista de string con los nombres de las columnas que deseamos.

``` ipython
In [8]: data.iloc[2:8][ ["General_Health", "Exercise", "BMI"] ]
Out[8]:
  General_Health Exercise    BMI
2      Very Good      Yes  33.47
3           Poor      Yes  28.73
4           Good       No  24.37
5           Good       No  46.11
6           Fair      Yes  22.74
7           Good      Yes  39.94
```

## DataNote 9: Atributo loc
El atributo `.loc` trabaja de la misma manera que el atributo `.iloc`, pero recordemos que este último es para *data frames* con indices del tipo entero. Entonces el atributo `.loc` nos permite obtener las registros/entradas de un *data frame* donde sus indices sean string.

``` ipython
In [1]: import pandas as pd

In [2]: store -r productos

In [3]: productos
Out[3]:
        nombre    material  costos  produccion  unidades
pA  producto 1  material 1     100        True       200
pB  producto 2  material 2     500        True       100
pC  producto 3  material 3     250       False         0

In [4]: productos.loc['pB']
Out[4]:
nombre        producto 2
material      material 2
costos               500
produccion          True
unidades             100
Name: pB, dtype: object

In [5]: productos.loc['pB':]
Out[5]:
        nombre    material  costos  produccion  unidades
pB  producto 2  material 2     500        True       100
pC  producto 3  material 3     250       False         0
```

Observemos que además de obtener una sola entrada podemos obtener un conjunto de estas en un rango determinado, esto nos permitiria generar nuevos *sub data frames*. Cómo punto adicional nosotros podemos especificar que columnas obtener.

``` ipython
In [6]: productos.loc['pB':, ["nombre","material","unidades"]]
Out[6]:
        nombre    material  unidades
pB  producto 2  material 2       100
pC  producto 3  material 3         0
```

## DataNote 10: Condicionales
Es comun que en el mundo real necesitemos obtener ciertos datos que cumplan con ciertas condiciones, es por ello que podemos establecer condicionales con los *data frames* para obtenerlos.

Para este ejercicio utilizaremos el data set [Cardiovascular Diseases Risk Prediction Dataset](https://www.kaggle.com/datasets/alphiree/cardiovascular-diseases-risk-prediction-dataset) y obtendremos los siguientes datos en base a sus condicionales:
- El rango de edad de todos los que tengan buena salud ("Good" y "Very Good").
- Obteber el rango de edad y sexo de todos los que hagan ejercicio.
- Obtener el promedio del BMI de todos los hombres que fumaron y su edad es mayor que 30.

``` ipython
In [1]: import pandas as pd

In [2]: data = pd.read_csv("Cardiovascular_Diseases_Risk.csv")
```

### El rango de edad de todos los que tengan buena salud
``` ipython
In [3]: data["General_Health"] == "Good"
Out[3]:
0         False
1         False
2         False
3         False
4          True
          ...
308849    False
308850    False
308851    False
308852    False
308853    False
Name: General_Health, Length: 308854, dtype: bool

In [4]: data["General_Health"] == "Very Good"
Out[4]:
0         False
1          True
2          True
3         False
4         False
          ...
308849     True
308850    False
308851     True
308852     True
308853    False
Name: General_Health, Length: 308854, dtype: bool
```

Se observa que obtenemos *Series* individuales del estado de salud general "Good" y "Very Good", podemos rescribirlo para tenerlo en una sola linea de código.

``` ipython
In [5]: (data["General_Health"] == "Very Good") | (data["General_Health"] == "Good")
Out[5]:
0         False
1          True
2          True
3         False
4          True
          ...
308849     True
308850    False
308851     True
308852     True
308853    False
Name: General_Health, Length: 308854, dtype: bool
```

La *Serie* retornada contiene datos booleanos que nos indican si se cumple la condición en es registro/entrada o no, entonces sólo necesitamos utilizarlos para obtener los datos, recordemos que en python podemos acceder a los registros/entradas a traves de valores booleanos.

``` ipython
In [6]: data[(data["General_Health"] == "Very Good") | (data["General_Health"] == "Good")
   ...: ]
Out[6]:
       General_Health  ... FriedPotato_Consumption
1           Very Good  ...                       4
2           Very Good  ...                      16
4                Good  ...                       0
5                Good  ...                      12
7                Good  ...                       8
...               ...  ...                     ...
308847      Very Good  ...                       0
308848           Good  ...                       0
308849      Very Good  ...                       0
308851      Very Good  ...                       4
308852      Very Good  ...                       0

[205759 rows x 19 columns]
```

Una vez tenemos todas los registros/entradas que tienen una buena salud, solo falta acceder a su rango de edad, en este caso la columna se llama "Age_Category".

``` ipython
In [7]: data[(data["General_Health"] == "Very Good") | (data["General_Health"] == "Good")
   ...: ]["Age_Category"]
Out[7]:
1         70-74
2         60-64
4           80+
5         60-64
7         65-69
          ...
308847    40-44
308848    55-59
308849    25-29
308851    30-34
308852    65-69
Name: Age_Category, Length: 205759, dtype: object
```

### Obteber el rango de edad y sexo de todos los que hagan ejercicio.
Ahora que ya sabemos establecer condicionales, repitamos el proceso para este caso

``` ipython
In [8]: data[data["Exercise"] == "Yes"]
Out[8]:
       General_Health  ... FriedPotato_Consumption
2           Very Good  ...                      16
3                Poor  ...                       8
6                Fair  ...                       0
7                Good  ...                       8
10               Fair  ...                       2
...               ...  ...                     ...
308849      Very Good  ...                       0
308850           Fair  ...                       4
308851      Very Good  ...                       4
308852      Very Good  ...                       0
308853      Excellent  ...                       1

[239381 rows x 19 columns]
```

Para eliegir ambas columnas debemos abrir el segundo par de corchetes y dentro de estos mandar una lista  de `String` con las columnas "Age_Category" y "Sex".

``` ipython
In [9]: data[data["Exercise"] == "Yes"][ ["Age_Category", "Sex"] ]
Out[9]:
       Age_Category     Sex
2             60-64  Female
3             75-79    Male
6             60-64    Male
7             65-69  Female
10            75-79  Female
...             ...     ...
308849        25-29    Male
308850        65-69    Male
308851        30-34  Female
308852        65-69    Male
308853        45-49  Female

[239381 rows x 2 columns]
```

### Obtener el promedio del BMI de todos los hombres que fumaron y su edad es mayor que 30
En este caso hay más condicionales pero el proceso sigue siendo el mismo.

``` ipython
In [10]: data[ (data["Sex"] == "Male") & (data["Age_Category"] > "30") & (data["Smoking_History"] == "Yes")]["BMI"]
Out[10]:
4         24.37
6         22.74
13        35.87
18        33.00
41        27.98
          ...
308800    22.10
308803    35.00
308810    27.98
308818    20.80
308834    27.89
Name: BMI, Length: 61494, dtype: float64
```

Ahora sólo aplicamos el método `.mean()` para obtener el promedio

``` ipython
In [11]: data[ (data["Sex"] == "Male") & (data["Age_Category"] > "30") & (data["Smoking_History"] == "Yes")]["BMI"].mean()
Out[11]: 28.94131427456337
```

## DataNote 11: Ordenamiento
En los *data frame* se nos ofrece una función de ordenamiento en base a una columna especifica, este es el metodo `.sort_values(_columna_)`. El ordenamiento por defecto es ascendente.

Para pracitcar este método utilizare el data set [Cardiovascular Diseases Risk Prediction Dataset](https://www.kaggle.com/datasets/alphiree/cardiovascular-diseases-risk-prediction-dataset) y se requerira obtener la salud general, la última revisión, el sexo, la altura y peso de las siguientes consultas.

- La mujer con menor estatura
- Los 5 hombres con mayor peso

`[ ["General_Health", "Checkup", "Sex", "Height_(cm)", "Weight_(kg)"] ]`

``` ipython
In [1]: import pandas as pd

In [2]: data = pd.read_csv("Cardiovascular_Diseases_Risk.csv")

In [3]: data
Out[3]:
       General_Health  ... FriedPotato_Consumption
0                Poor  ...                      12
1           Very Good  ...                       4
2           Very Good  ...                      16
3                Poor  ...                       8
4                Good  ...                       0
...               ...  ...                     ...
308849      Very Good  ...                       0
308850           Fair  ...                       4
308851      Very Good  ...                       4
308852      Very Good  ...                       0
308853      Excellent  ...                       1

[308854 rows x 19 columns]
```

### Obtener la mujer con menor estatura
El primer paso será obtener a todas las columnas que nos piden y elegir los registros que sean de sexo femenino, posteriormente aplicaremos el método para ordenarlo ascendentemente.

``` ipython
In [4]: data[ data["Sex"] == "Female" ][ ["General_Health", "Checkup", "Sex", "Height_(cm)", "Weight_(kg)"] ]
Out[4]:
       General_Health                  Checkup     Sex  Height_(cm)  Weight_(kg)
0                Poor  Within the past 2 years  Female          150        32.66
1           Very Good     Within the past year  Female          165        77.11
2           Very Good     Within the past year  Female          163        88.45
7                Good     Within the past year  Female          165       108.86
8                Fair     Within the past year  Female          163        72.57
...               ...                      ...     ...          ...          ...
308838      Excellent     Within the past year  Female          163        55.79
308839           Good     Within the past year  Female          168       113.40
308842           Good     Within the past year  Female          163        74.39
308851      Very Good      5 or more years ago  Female          157        61.23
308853      Excellent     Within the past year  Female          160        81.19

[160196 rows x 5 columns]

In [5]: data[ data["Sex"] == "Female" ][ ["General_Health", "Checkup", "Sex", "Height_(cm)", "Weight_(kg)"] ].sort_values("Height_(cm)")
Out[5]:
       General_Health                  Checkup     Sex  Height_(cm)  Weight_(kg)
192543      Very Good     Within the past year  Female           91        57.61
253618      Excellent     Within the past year  Female           91        79.38
27158            Fair     Within the past year  Female           91        31.75
258933           Good     Within the past year  Female           91        57.61
203737           Good     Within the past year  Female           94        63.50
...               ...                      ...     ...          ...          ...
193402           Fair     Within the past year  Female          213        63.50
44633            Good  Within the past 2 years  Female          221       115.67
115335           Fair     Within the past year  Female          226        81.65
107847           Good     Within the past year  Female          226        81.65
21793       Very Good     Within the past year  Female          229       104.33

[160196 rows x 5 columns]
```

Para obtener el primer registro hay varias formas de hacerlo, la mejor en este caso es utilizar el método `.head()` y pasarle `1` como argumento para que nos devuelva el primer registro, y así habremos obtenido a la mujer con menor estatura.

``` ipython
In [6]: data[ data["Sex"] == "Female" ][ ["General_Health", "Checkup", "Sex", "Height_(cm)", "Weig
   ...: ht_(kg)"] ].sort_values("Height_(cm)").head(1)
Out[6]:
       General_Health               Checkup     Sex  Height_(cm)  Weight_(kg)
192543      Very Good  Within the past year  Female           91        57.61
```

### Obtener las 5 personas con mayor peso
Tenemos que repetir los primeros pasos del ejercicio anterior, seleccionando las columas y ordenando. Pero ahora haremos una modificación en el método `.sort_values(_columa_)` pasandole el argumento opcional `ascending` como `False` para obtener un orden descendente.

``` ipython
In [7]: data[ data["Sex"] == "Male" ][ ["General_Health", "Checkup", "Sex", "Height_(cm)", "Weight
   ...: _(kg)"] ]
Out[7]:
       General_Health                  Checkup   Sex  Height_(cm)  Weight_(kg)
3                Poor     Within the past year  Male          180        93.44
4                Good     Within the past year  Male          191        88.45
5                Good     Within the past year  Male          183       154.22
6                Fair     Within the past year  Male          175        69.85
11               Fair     Within the past year  Male          175        73.48
...               ...                      ...   ...          ...          ...
308847      Very Good      5 or more years ago  Male          163        65.77
308848           Good  Within the past 5 years  Male          168        58.97
308849      Very Good     Within the past year  Male          168        81.65
308850           Fair  Within the past 5 years  Male          180        69.85
308852      Very Good     Within the past year  Male          183        79.38

[148658 rows x 5 columns]

In [8]: data[ data["Sex"] == "Male" ][ ["General_Health", "Checkup", "Sex", "Height_(cm)", "Weight
   ...: _(kg)"] ].sort_values("Weight_(kg)", ascending=False)
Out[8]:
       General_Health               Checkup   Sex  Height_(cm)  Weight_(kg)
89359            Good  Within the past year  Male          185       293.02
70799       Excellent  Within the past year  Male          188       285.76
287501           Poor  Within the past year  Male          191       283.50
227580      Excellent  Within the past year  Male          196       274.42
124131      Very Good  Within the past year  Male          191       273.52
...               ...                   ...   ...          ...          ...
251478           Fair  Within the past year  Male          173        36.29
247011           Good  Within the past year  Male          170        36.29
123497           Fair                 Never  Male          165        36.29
303795           Good  Within the past year  Male          163        34.02
148350           Poor                 Never  Male          137        24.95

[148658 rows x 5 columns]

In [9]: data[ data["Sex"] == "Male" ][ ["General_Health", "Checkup", "Sex", "Height_(cm)", "Weight
   ...: _(kg)"] ].sort_values("Weight_(kg)", ascending=False).head(5)
Out[9]:
       General_Health               Checkup   Sex  Height_(cm)  Weight_(kg)
89359            Good  Within the past year  Male          185       293.02
70799       Excellent  Within the past year  Male          188       285.76
287501           Poor  Within the past year  Male          191       283.50
227580      Excellent  Within the past year  Male          196       274.42
124131      Very Good  Within the past year  Male          191       273.52
```

Observese que para obtener los 5 registros le pasamos como argumento el número 5 al método `.head()`.

## DataNote 12: Búsqueda por rangos
Cuando queramos obtener las entradas que se encuentren entre cierto rango de valores podemos implementar una busqueda por rangos, para este ejemplo utilizare el data set [Cardiovascular Diseases Risk Prediction Dataset](https://www.kaggle.com/datasets/alphiree/cardiovascular-diseases-risk-prediction-dataset) y buscare a las personas que comen entre 0 y 15 vegetales.

``` ipython
In [1]: import pandas as pd

In [2]: data = pd.read_csv("Cardiovascular_Diseases_Risk.csv")

In [3]: data
Out[3]:
       General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
0                Poor  Within the past 2 years  ...                           16                      12
1           Very Good     Within the past year  ...                            0                       4
2           Very Good     Within the past year  ...                            3                      16
3                Poor     Within the past year  ...                           30                       8
4                Good     Within the past year  ...                            4                       0
...               ...                      ...  ...                          ...                     ...
308849      Very Good     Within the past year  ...                            8                       0
308850           Fair  Within the past 5 years  ...                           60                       4
308851      Very Good      5 or more years ago  ...                            8                       4
308852      Very Good     Within the past year  ...                           12                       0
308853      Excellent     Within the past year  ...                           12                       1

[308854 rows x 19 columns]
```

Existen dos formas de hacer la busqueda por rangos.

### Delimitar el espacio de busqueda con condicionales
Podemos establecer condicionales dentro nuestro `data` para así obtener las entradas dentro del rango de valores que buscamos.

``` ipython
In [4]: data[(data["Green_Vegetables_Consumption"] >= 0) & (data["Green_Vegetables_Consumption"] <= 15)]
Out[4]:
       General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
1           Very Good     Within the past year  ...                            0                       4
2           Very Good     Within the past year  ...                            3                      16
4                Good     Within the past year  ...                            4                       0
5                Good     Within the past year  ...                           12                      12
6                Fair     Within the past year  ...                            8                       0
...               ...                      ...  ...                          ...                     ...
308848           Good  Within the past 5 years  ...                           12                       0
308849      Very Good     Within the past year  ...                            8                       0
308851      Very Good      5 or more years ago  ...                            8                       4
308852      Very Good     Within the past year  ...                           12                       0
308853      Excellent     Within the past year  ...                           12                       1

[191638 rows x 19 columns]
```

### Método between()
Los *data frame* cuentan con una función `.between(_left_, _right_)` que permite obtener todas las entradas que se encuentren entre su rango de valores.

``` ipython
In [5]: data[ data["Green_Vegetables_Consumption"].between(0,15) ]
Out[5]:
       General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
1           Very Good     Within the past year  ...                            0                       4
2           Very Good     Within the past year  ...                            3                      16
4                Good     Within the past year  ...                            4                       0
5                Good     Within the past year  ...                           12                      12
6                Fair     Within the past year  ...                            8                       0
...               ...                      ...  ...                          ...                     ...
308848           Good  Within the past 5 years  ...                           12                       0
308849      Very Good     Within the past year  ...                            8                       0
308851      Very Good      5 or more years ago  ...                            8                       4
308852      Very Good     Within the past year  ...                           12                       0
308853      Excellent     Within the past year  ...                           12                       1

[191638 rows x 19 columns]
```

## DataNote 13: Busqueda entre opciones
Hay ocasiones en que buscamos las entradas que se encuentren entre una lista de opciones y no en un rango, esto lo podemos hacer de dos formas: con condicionales o con el método `.isin(_values_)`. 

Para realizar este ejercicio utilizare el data set [Cardiovascular Diseases Risk Prediction Dataset](https://www.kaggle.com/datasets/alphiree/cardiovascular-diseases-risk-prediction-dataset) y realizaremos una consulta para obtener el sexo de todas las personas que sufran problemas del corazón, que su consumo de papas fritas sea mayor a 15 y que su estado de salud sea *"Excellent"*, *"Fair"* o *"Poor"*.

``` ipython
In [1]: import pandas as pd

In [2]: data = pd.read_csv("Cardiovascular_Diseases_Risk.csv")

In [3]: data
Out[3]:
       General_Health                  Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
0                Poor  Within the past 2 years  ...                           16                      12
1           Very Good     Within the past year  ...                            0                       4
2           Very Good     Within the past year  ...                            3                      16
3                Poor     Within the past year  ...                           30                       8
4                Good     Within the past year  ...                            4                       0
...               ...                      ...  ...                          ...                     ...
308849      Very Good     Within the past year  ...                            8                       0
308850           Fair  Within the past 5 years  ...                           60                       4
308851      Very Good      5 or more years ago  ...                            8                       4
308852      Very Good     Within the past year  ...                           12                       0
308853      Excellent     Within the past year  ...                           12                       1

[308854 rows x 19 columns]
```

### Utilizando condicionales
Haciendo una suseción de condicionales entre todas nuestras opciones es la primera forma.

``` ipython
In [4]: data[ (data["Heart_Disease"] == "Yes") & (data["FriedPotato_Consumption"] > 15) & (
   ...: (data["General_Health"] == "Excellent") |
   ...: (data["General_Health"] == "Fair") |
   ...: (data["General_Health"] == "Poor") ) ]
Out[4]:
       General_Health               Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
11               Fair  Within the past year  ...                            8                      30
107              Poor  Within the past year  ...                           30                      30
704              Poor  Within the past year  ...                           12                      30
770              Poor  Within the past year  ...                           30                      60
1097             Fair  Within the past year  ...                            0                      30
...               ...                   ...  ...                          ...                     ...
307258           Fair  Within the past year  ...                           15                      25
307479           Fair  Within the past year  ...                            0                      30
307934           Fair  Within the past year  ...                            0                      90
308256           Fair  Within the past year  ...                           30                      16
308742      Excellent  Within the past year  ...                            4                      16

[1077 rows x 19 columns]
```

Como podemos observar esto funciona, pero escribimos demasiado código y es un poco dificil de leer, además que la dificultad ira aumentando conforme tengamos más opciones.

### Método isin()
El método `isin(_values_)` resibe aquellos valores que nosotros queremos validar si se encuentran tendro una *Serie* o *data frame*, para este ejercicio utilizaremos una lista de `string` para almacenar las opciones y utilizarla en el método `isin(_values_)`.

``` ipython
In [5]: health_check = ["Excellent", "Fair", "Poor"] #Lista de opciones

In [6]: data[ (data["Heart_Disease"] == "Yes") & (data["FriedPotato_Consumption"] > 15) & (data["General_Health"].isin(health_check)) ]
Out[6]:
       General_Health               Checkup  ... Green_Vegetables_Consumption FriedPotato_Consumption
11               Fair  Within the past year  ...                            8                      30
107              Poor  Within the past year  ...                           30                      30
704              Poor  Within the past year  ...                           12                      30
770              Poor  Within the past year  ...                           30                      60
1097             Fair  Within the past year  ...                            0                      30
...               ...                   ...  ...                          ...                     ...
307258           Fair  Within the past year  ...                           15                      25
307479           Fair  Within the past year  ...                            0                      30
307934           Fair  Within the past year  ...                            0                      90
308256           Fair  Within the past year  ...                           30                      16
308742      Excellent  Within the past year  ...                            4                      166

[1077 rows x 19 columns]

In [7]: data[ (data["Heart_Disease"] == "Yes") & (data["FriedPotato_Consumption"] > 15) & (data["General_Health"].isi
   ...: n(health_check)) ]["Sex"] #Los datos que nos pidieron
Out[7]:
11          Male
107       Female
704         Male
770       Female
1097        Male
           ...
307258      Male
307479    Female
307934    Female
308256      Male
308742    Female
Name: Sex, Length: 1077, dtype: object
```

Con esto la consulta se hace de forma óptima, es mucho más legible y dinamico.

## DataNote 14: Métodos de String
En la librería *pandas*, existen métodos que nos ayudan a determinar si un `string` cumple ciertas características. Por ejemplo, podemos verificar si comienza con..., si termina con... o si contiene... Para realizar este ejercicio, utilizaré el conjunto de datos [users](https://github.com/codigofacilito/pandas-python/blob/master/users.csv).

> **Nota**
Para llamar a estos métodos la libreria de `pandas.Series.str`, pero como ya tenemos importado `pandas` y trabajamos sobre objetos del tipo `Serie` llamamos a la libreria escribiendo `.str`.

``` ipython
In [1]: import pandas as pd

In [2]: data = pd.read_csv("users.csv", index_col=0)

In [3]: data
Out[3]:
                 nombre  edad  genero            pais                        email
0      Mr Jerome Thomas    73    male   United States    jerome.thomas@example.com
1         Mr Gary Berry    70    male  United Kingdom       gary.berry@example.com
2       Mr Noham Dubois    40    male          France     noham.dubois@example.com
3     Mrs Naja Johansen    63  female         Denmark    naja.johansen@example.com
4    Mr Damien Marchand    61    male          France  damien.marchand@example.com
..                  ...   ...     ...             ...                          ...
195       Mr Raul Bravo    46    male           Spain       raul.bravo@example.com
196   Miss Maeva Fortin    40  female          Canada     maeva.fortin@example.com
197   Mr Gabriel Berger    40    male          France   gabriel.berger@example.com
198  Mrs Ülkü Tanrıkulu    37  female          Turkey   ulku.tanrikulu@example.com
199     Mr Raff Valkema    60    male     Netherlands     raff.valkema@example.com

[200 rows x 5 columns]
```

### startswith()
El método `str.startswith(_pat_)` recibe como argumento obligatorio el texto que nosotros deseamos comprobar si se encuentra al inicio, este argumento también podría ser una *tuple*.

``` ipython
In [4]: data[ data["email"].str.startswith('n') ]
Out[4]:
                nombre  edad  genero         pais                      email
2      Mr Noham Dubois    40    male       France   noham.dubois@example.com
3    Mrs Naja Johansen    63  female      Denmark  naja.johansen@example.com
6        Mr Noah Olsen    40    male      Denmark     noah.olsen@example.com
77    Mr Norman Carter    23    male    Australia  norman.carter@example.com
114     Ms Nalan Ekici    31  female       Turkey    nalan.ekici@example.com
191      Mr Noah Moore    44    male  New Zealand     noah.moore@example.com
```

### endswith()
El método `str.endswith(_pat_)` recibe como argumento obligatorio el texto que nosotros deseamos comprobar si se encuentra en el final, este argumento también podría ser una *tuple*.

``` ipython
In [5]: data[ data["pais"].str.endswith('k') ]
Out[5]:
                     nombre  edad  genero     pais                          email
3         Mrs Naja Johansen    63  female  Denmark      naja.johansen@example.com
6             Mr Noah Olsen    40    male  Denmark         noah.olsen@example.com
19        Ms Asta Jørgensen    72  female  Denmark     asta.jorgensen@example.com
23      Mrs Tilde Mortensen    42  female  Denmark    tilde.mortensen@example.com
28        Miss Maria Madsen    37  female  Denmark       maria.madsen@example.com
43         Miss Anna Hansen    71  female  Denmark        anna.hansen@example.com
57   Miss Victoria Pedersen    41  female  Denmark  victoria.pedersen@example.com
61     Mr Silas Christensen    57    male  Denmark  silas.christensen@example.com
74      Miss Silje Petersen    29  female  Denmark     silje.petersen@example.com
101       Mr Anton Johansen    56    male  Denmark     anton.johansen@example.com
111        Miss Emma Jensen    39  female  Denmark        emma.jensen@example.com
118       Mrs Frida Nielsen    60  female  Denmark      frida.nielsen@example.com
138        Ms Maria Thomsen    41  female  Denmark      maria.thomsen@example.com
173         Mr Adam Nielsen    30    male  Denmark       adam.nielsen@example.com
177     Mrs Andrea Andersen    45  female  Denmark    andrea.andersen@example.com
179       Miss Clara Møller    58  female  Denmark       clara.moller@example.com
```

### endswith()
El método `str.contains(_pat_)` recibe como argumento obligatorio el texto que nosotros deseamos comprobar si se encuentra en el final, también puede recibir una expresión regular.

``` ipython
In [6]: data[ data["nombre"].str.contains("Nielsen") ]
Out[6]:
                nombre  edad  genero     pais                      email
118  Mrs Frida Nielsen    60  female  Denmark  frida.nielsen@example.com
173    Mr Adam Nielsen    30    male  Denmark   adam.nielsen@example.com
```

## DataNote 15: Agrupamiento
Cuando trabajamos con *data frames* o *data sets* es muy comun que haya ocasiones en las que necesitemos agrupar datos para obtener nueva información. 

La libreria de *pandas* cuenta con un método llamado `.groupby(_by_)`, el argumento obligatorio `_by_` será usado para determinar los grupos del `groupby` esté puede ser un `mappin`, `function`, `str`, `pd.Grouper` o `list of such`. En este caso lo agruparemos por el nombre de la columna (str). Utilizare el conjunto de datos [users](https://github.com/codigofacilito/pandas-python/blob/master/users.csv) para obtener las siguientes consultas:
- Obtener la cantidad de hombres y mujeres del data set
- Obtener cuál es el país con más hombres

``` ipython
In [1]: import pandas as pd

In [2]: data = pd.read_csv("users.csv", index_col=0)

In [3]: data
Out[3]:
                 nombre  edad  genero            pais                        email
0      Mr Jerome Thomas    73    male   United States    jerome.thomas@example.com
1         Mr Gary Berry    70    male  United Kingdom       gary.berry@example.com
2       Mr Noham Dubois    40    male          France     noham.dubois@example.com
3     Mrs Naja Johansen    63  female         Denmark    naja.johansen@example.com
4    Mr Damien Marchand    61    male          France  damien.marchand@example.com
..                  ...   ...     ...             ...                          ...
195       Mr Raul Bravo    46    male           Spain       raul.bravo@example.com
196   Miss Maeva Fortin    40  female          Canada     maeva.fortin@example.com
197   Mr Gabriel Berger    40    male          France   gabriel.berger@example.com
198  Mrs Ülkü Tanrıkulu    37  female          Turkey   ulku.tanrikulu@example.com
199     Mr Raff Valkema    60    male     Netherlands     raff.valkema@example.com

[200 rows x 5 columns]
```

### Obtener la cantidad de hombres y mujeres del data set
La siguiente lista ira describiendo el código bloque a bloque, el número hace referencia al bloque correspondiente.

4- Agrupamos el *data frame* por la columna *"genero"*, esto nos devuelve un objeto del tipo `DataFrameGroupBy` que contiene toda la información de nuestra agrupación.
5- Estamos accediento a la columna *"genero"* de nuestro agrupamiento, esto nos devuelve un objeto del tipo `SeriesGroupBy` que contiene la información de nuestro agrupamiento en la columa de *"genero"*.
6- Le aplicamos el método `.count()` a nuestro objeto `SeriesGroupBy`, este método va a contar el número de valores no nulos de cada grupo, retornandonos así un objeto del tipo `Series` teniendo como llaves los grupos y como valores la cantidad que conto.

``` ipython
In [4]: data.groupby("genero")
Out[4]: <pandas.core.groupby.generic.DataFrameGroupBy object at 0x0000019BF23D77D0>

In [5]: data.groupby("genero")["genero"]
Out[5]: <pandas.core.groupby.generic.SeriesGroupBy object at 0x0000019BF26B01D0>

In [6]: data.groupby("genero")["genero"].count()
Out[6]:
genero
female    106
male       94
Name: genero, dtype: int64
```

### Obtener cuál es el país con más hombres
La siguiente lista ira describiendo el código bloque a bloque, el número hace referencia al bloque correspondiente.

7- Primero filtramos el *data frame* para obtener todas las entradas cuyo genero sea "male", osea hombre.
8- Este *data frame* lo vamos a agrupar por paises porque deseamos conocer su cantidad por país.
9- Una vez hacemos la agrupación, accedemos a la columna *"pais"* y hacemos el `count()`, esto nos retorna una nueva `Serie` con e conteo de los hombres por país.
10- Para poder obtener el país con el mayor número aplicamos el método `.sort_values()` y al parameto opcional `ascending` lo marcamos como `Flse` para obtener el orden descendente.
11- Ya teniendo la agrupación y el conteo hechos, y habiendo ordenedo los valores descententemente sólo necesitamos obtener el primer valor de la `Serie` que sería el país con más hombres. Para esto utilizamos el método `.head()` y pasamos como paremetro `1` para así obtener en una `Serie` el primer registo.

``` ipython
In [7]: data[ data["genero"] == "male" ]
Out[7]:
                 nombre  edad genero            pais                        email
0      Mr Jerome Thomas    73   male   United States    jerome.thomas@example.com
1         Mr Gary Berry    70   male  United Kingdom       gary.berry@example.com
2       Mr Noham Dubois    40   male          France     noham.dubois@example.com
4    Mr Damien Marchand    61   male          France  damien.marchand@example.com
5      Mr Harri Althoff    56   male         Germany    harri.althoff@example.com
..                  ...   ...    ...             ...                          ...
189  Mr Carl Williamson    59   male         Ireland  carl.williamson@example.com
191       Mr Noah Moore    44   male     New Zealand       noah.moore@example.com
195       Mr Raul Bravo    46   male           Spain       raul.bravo@example.com
197   Mr Gabriel Berger    40   male          France   gabriel.berger@example.com
199     Mr Raff Valkema    60   male     Netherlands     raff.valkema@example.com

[94 rows x 5 columns]

In [8]: data[ data["genero"] == "male" ].groupby("pais")
Out[8]: <pandas.core.groupby.generic.DataFrameGroupBy object at 0x0000019BF26BBCD0>

In [9]: data[ data["genero"] == "male" ].groupby("pais")["pais"].count()
Out[9]:
pais
Australia          6
Brazil             4
Canada             7
Denmark            4
Finland            3
France             6
Germany            3
Iran               8
Ireland           10
Netherlands        2
New Zealand        4
Norway             8
Spain              4
Switzerland        3
Turkey             5
United Kingdom     9
United States      8
Name: pais, dtype: int64

In [10]: data[ data["genero"] == "male" ].groupby("pais")["pais"].count().sort_values(ascending=False)
Out[10]:
pais
Ireland           10
United Kingdom     9
Iran               8
Norway             8
United States      8
Canada             7
France             6
Australia          6
Turkey             5
Brazil             4
New Zealand        4
Denmark            4
Spain              4
Germany            3
Finland            3
Switzerland        3
Netherlands        2
Name: pais, dtype: int64

In [11]: data[ data["genero"] == "male" ].groupby("pais")["pais"].count().sort_values(ascending=False).head(1)
Out[11]:
pais
Ireland    10
Name: pais, dtype: int64
```