# IPython
IPython es un entorno interactivo para Python, más amigable y mejorado que la consola estándar. Permite ejecutar comandos, probar código, explorar datos y ejecutar programas paso a paso desde la línea de comandos. Además, tiene "comandos mágicos" para tareas comunes como cambiar de directorio, guardar variables y listar comandos disponibles. También ofrece una función de autocompletado para escribir código más rápido.

## DataNote 1: Creando entorno virual
### Descargar Python
Si aún no tienes Python instalado en tu sistema, descarga e instala la versión más reciente de Python desde el [sitio web oficial de python](https://www.python.org/downloads/). Asegúrate de marcar la casilla que dice "Agregar Python X.X a la variable de entorno PATH" durante la instalación.

### Instalar virtualenv (depende de la versión)
En versiones más recientes de Python (3.3 o superior), se incluye el módulo venv para crear entornos virtuales sin instalar paquetes adicionales. Sin embargo, si estás utilizando una versión más antigua de Python o prefieres usar el paquete virtualenv abre la [terminal](https://acortar.link/LM7B1s) y ingrsa el siguiente comando:

`pip install virtualenv`

En mi caso instale python 3.11 por lo que no hubo necesidad de instalar el *virtualenv*.

### Crea una nueva carpeta para tu proyecto
Crea una carpeta en tu sistema para tu proyecto y accede a ella desde la línea de comandos.

### Crea el entorno virtual con venv (Python 3.3 o superior)
Si tienes Python 3.3 o superior, puedes utilizar el módulo venv para crear el entorno virtual ejecutando el siguiente comando:

`python -m venv nombre_del_entorno`

Reemplaza "nombre_del_entorno" con el nombre que deseas para tu entorno virtual. En mi caso y lo convencional es que le pongas el nombre **env**

### Crea el entorno virtual con virtualenv
Si decidiste utilizar virtualenv, puedes crear el entorno virtual de esta manera:

`virtualenv nombre_del_entorno`

Reemplaza "nombre_del_entorno" con el nombre que deseas para tu entorno virtual. En mi caso y lo convencional es que le pongas el nombre **env**

### Activa el entorno virtual
Primer paso tienes que situar la ruta de tu consola en la carpeta donde se encuentra el entorno virtual, no el la carpeta del entorno virtual. Te dejo un link de [Navegar entre carpetas del sistema con CMD](https://youtu.be/ycOzl0coFxA) y [Navegar y Crear carpetas especiales desde la terminal en Linux y Mac](https://youtu.be/1fltrbxIbEk)

En **sistemas Windows** ejecuta:

`nombre_del_entorno\Scripts\activate`

Si al igual que a mi al intentar activar tu entorno virtual la consola te dice:
> No se puedo cargar el archivo _ruta_ porque la ejecución de
scripts está deshabilitada en este sistema.

Significa que las politicas de privacidad impiden la ejecución de scripts, existen dos soluciones y tendras abrir tu consola como administrador.

La primera es cambiar la politica de privacidad para que siempre deje ejecutar scipts.

La segunda, que es la que yo utilice, es hacer que sólo por la sesión actual de la consola permita la ejecución de scripts. A continuación te dejo el comando para permitir sólo en la sesión actual la ejecución de scripts:

``` powershell
Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
nombre_del_entorno\Scripts\activate
```

En **sistemas Unix o MacOS** ejecuta:

`source nombre_del_entorno/bin/activate`

Al activar el entorno virtual, verás que el nombre del entorno virtual aparece al principio de la línea de comandos, lo que indica que estás trabajando dentro del entorno virtual.

### Trabaja dentro del entorno virtual
Dentro del entorno virtual, puedes instalar paquetes de Python utilizando `pip`, y todas las bibliotecas y dependencias se instalarán en el ámbito del entorno virtual sin afectar el sistema global de Python.

Para poder comenzar a trabajar con **ipython** ingresa el siguiente comando:

`pip install ipython`

### Desactiva el entorno virtual
Cuando hayas terminado de trabajar en tu proyecto, puedes desactivar el entorno virtual ejecutando el siguiente comando:

`deactivate`

## DataNote 2: Comandos mágicos ipython
Aprendí los comandos "magicos" de ipython.

Los comandos "mágicos" en IPython son comandos especiales que brindan funcionalidades útiles y facilitan la interacción con el entorno de trabajo. Aquí hay algunos comandos "mágicos" útiles que puedes utilizar:

- `%cd`: Este comando te permite cambiar el directorio de trabajo actual. Simplemente escribe `%cd` seguido de la ruta del directorio al que deseas cambiar. Por ejemplo, `%cd /ruta/del/directorio` te llevará a esa ubicación.

- `%pwd`: Si alguna vez necesitas saber en qué directorio te encuentras, el comando `%pwd` te mostrará la ruta del directorio de trabajo actual.

- `%bookmark`: Esta funcionalidad te permite guardar rutas de directorio para acceder a ellas rápidamente. Por ejemplo, puedes usar `%bookmark mydir` para guardar la ubicación actual con el nombre "mydir". Luego, simplemente escribiendo `%cd -b mydir` podrás cambiar rápidamente al directorio guardado.

- `%store`: Si deseas compartir una variable entre diferentes sesiones de IPython, puedes usar `%store` para guardarla y luego acceder a ella en sesiones futuras. Por ejemplo, `%store mi_variable` guardará la variable llamada "mi_variable", y en otra sesión de IPython, puedes recuperarla usando `%store -r mi_variable`.

`%lsmagic`: ¿Te preguntas si hay más comandos "mágicos" disponibles? El comando `%lsmagic` te mostrará una lista completa de todos los comandos "mágicos" disponibles en tu entorno de IPython.

## DataNote 3: Funciones
Definí una función con sus parametros, tipos de datos, docString, return

``` ipython
 def suma(a: int, b:int) -> int:
    ...:     """Permite sumar dos números enteros."""
    ...:     return a + b
``` 

Llame a la función 
`suma(2,2)`

Y por último solicite a ipython información de la función con `suma?` y si queremos información mas detallacomo, como su código, ponemos doble interrogación `suma??`. Esto también funciona con variables. 

## DataNote 4
Interactuamos con archivos externos desde ipython, por medio de los siguientes comandos:
- %pycat : permite ver el contenido de un archivo.
- %run : permite ejecutar un archivo.
- %load : permite cargar el contenido de un archivo a nuestra consola
- %edit : perimite editar el contenido de un archivo

## DataNote 5
Creamos archivos desde la consola de ipython guardando funciones/código que tengamos cargado en la consola por medio de los siguientes comandos:
- %save _nombre.ext_ _In[#]-In[#]-_ _In[#]_ : crea un archivo con un nombre y extensión cargando el código de los bloques *In*, por ejemplo
	- `%save operaciones.py 6 13-14`
- save -a _nombre.ext_ _In[#]-In[#]-_ _In[#]_ : carga el código de los bloques *In* al final del archivo especificado, por ejemplo
	- `save -a operaciones.py 23`

