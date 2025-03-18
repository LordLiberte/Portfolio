
# Configuración del entorno tecnológico

## Entorno virtual
En todo proyecto de programación es importante separar el entorno de desarrollo. En python es posible trabajar con entornos virtuales que separan las dependencias del entorno global donde se ha installado el intérprete. 

> **Info**
>
> Version de python > 3.12

```sh
conda deactivate # solo si se tiene conda
python3 -m venv venv
echo "./venv" >> .gitignore
source ./venv/bin/activate
```

> Enlaces de interés sobre configuración de entornos: 
> - [Built-in Functions venv](https://docs.python.org/3/library/venv.html)
> - [Comparación venv y virtualenv](https://stackoverflow.com/questions/41573587/what-is-the-difference-between-venv-pyvenv-pyenv-virtualenv-virtualenvwrappe)
> - [Documentación virtualenv](https://virtualenv.pypa.io/en/latest/)
> - [Git y Github](https://video.alexanderstreet.com/watch/git-and-github-the-complete-git-and-github-course)
> - [Creación de proyecto de Ciencia de Datos](https://cookiecutter-data-science.drivendata.org/)

## Instalación de librerías

El comando pip es el encargado de instalar las dependencias a utilizar en un programa.

```sh
pip install seaborn
pip install streamlit
pip3 install -U scikit-learn
```

En caso de tener librerías se puede utilizar la instalación por fichero con el listado:

```sh
# guardar listado de dependencias
pip freeze -l > requirements.txt 
# instalar
pip install -r requirements.txt
```

## Estuctura de cartpetas

```
Practica2/
├── data/
│   ├── datos_accidentes.csv
│   └── ...
├── enunciados/
│   ├── 1_configuracion_ds.md
│   └── ...
├── notebooks/
│   ├── EDA.py
│   └── ...
├── visualizacion/
│    ├── stmain.py
│    └── st_pages/
│        ├── main.py
│        └── ...
├── utils/
│   ├── dbconnect.py
│   └── ...
├── README.md
├── .gitignore
└── venv
```

Crear la estructura desde terminal:

```bash
#!/bin/bash
# Ejecutar: bash crea_estructura.sh
# Crear la carpeta y ficheros de enunciados
mkdir -p enunciados
touch enunciados/objetivos_ds.md
# Crear la carpeta de datos
mkdir -p data
# Crear la carpeta de notebooks
mkdir -p notebooks
touch notebooks/carga_datos.ipynb
# Crear carpeta de visualizacion
mkdir -p visualizacion/st_pages
touch visualizacion/stmain.py
touch visualizacion/st_pages/st_eda.py
# Prgramas de uso comun
mkdir -p utils
touch utils/dbconnect.py
touch README.md
echo "\t --Estructura de ciencia de datos creada exitosamente--"
```

> **Warning**
>
> OJO! sólo ejecutar el script una vez al inicio de la práctica

# Python

## Vanilla Python

Declaración de una variable:

```python
# Hello world!!
a = 503124019814
print(f"el valor {a} para la variable")
```

Estructuras de control y funciones:
```python
# funcion para sumar dos elementos
def suma(a,b):
    return a+b

lista = [1,2,3]

for i,value in enumerate(lista):
    lista[i] = suma(value,10)

print(lista)
```

Estructuras de datos:
```python
class Sesion:
    def __init__(self, titulo, fecha, profesor):
        self.titulo = titulo
        self.fecha = fecha
        self.profesor = profesor

    def __str__(self):
        return f"Sesión: {self.titulo}, Fecha: {self.fecha}, Duración: {self.profesor}"

class SesionTeorica(Sesion):
    def __init__(self, titulo, fecha, profesor, tema):
        super().__init__(titulo, fecha, profesor)
        self.tema = tema

    def __str__(self):
        return f"Sesión Teórica: {self.titulo}, Tema: {self.tema}, Fecha: {self.fecha}, Profesor: {self.profesor}"

class SesionPractica(Sesion):
    def __init__(self, titulo, fecha, profesor, actividad):
        super().__init__(titulo, fecha, profesor)
        self.actividad = actividad

    def __str__(self):
        return f"Sesión Práctica: {self.titulo}, Actividad: {self.actividad}, Fecha: {self.fecha}, Profesor: {self.profesor}"

class Asignatura:
    def __init__(self, nombre):
        self.nombre = nombre
        self.sesiones = []

    def agregar_sesion(self, sesion):
        self.sesiones.append(sesion)

    def __str__(self):
        sesiones_str = "\n".join(str(sesion) for sesion in self.sesiones)
        return f"Asignatura: {self.nombre}\nSesiones:\n{sesiones_str}"

# Ejemplo de uso
asignatura = Asignatura("Introducción a la Ciencia de Datos")
sesion1 = SesionTeorica("KDD y CRIPS-DM", "2025-02-13", "Horacio Kuna", "Tema 2")
sesion2 = SesionPractica("Foro y configuración", "2025-02-18", "Benjamin Arroquia Cuadros", "Práctica 1")

asignatura.agregar_sesion(sesion1)
asignatura.agregar_sesion(sesion2)

print(asignatura)
```

Crear una matriz con Python:

```python
matriz = 3, 3
ls_data = []
ls_range = list(range(1000))
for i in range(matriz[0]):
    ls_fila = []
    for columna in range(matriz[1]):
        ls_fila.append(random.choice(ls_range))
    ls_data.append(ls_fila)
print(ls_data)
```



## Numpy

Librería imprescindible para tratamiento de datos y cálculo.

```python
import numpy as np
random_list = np.random.randint(200,size=(10,2))
print(random_list)
```

- NumPy (__Num__ erical __Py__ thon) es la de facto librería estándar para análisis numérico en Python
- Estructura de datos multidimensional eficiente (escrita en C): ndarray
- Colección de funciones para álgebra lineal, estadística descriptiva
- Ayuda al procesamiento de datos (np.where)
- Existen importantes diferencias entre una lista y un numpy array en el uso de operadores.

Operaciones de lgebra: 
```python
import numpy as np
A = np.random.rand(3,3)
B = np.random.rand(3,1)
print(A.T)
print(A @ B)
```

Ejemplo de slice:
```python
data = np.random.randint(100,size=(4,2))
display(data)
print(data[:, 0], data[:, 1])
```

Ejemplo crar datos y redefinir a una matriz:
```python
X = np.linspace(0, 20, 1000)
y = np.sin(x) + 0.2 * X
display(y)
display(data)
X = np.random.randn(100, 2)
X[:, 0]
```

Ejemplo de resolución del ajuste lineal por mínimos cuadrados:
```python
import numpy as np

# Datos de ejemplo
x = np.array([[1, 2], [2, 3], [3, 4], [4, 5], [5, 6]])
y = np.array([2, 3, 5, 7, 11])

X = np.hstack([x, np.ones((x.shape[0], 1))])
coeficientes = np.linalg.lstsq(X, y, rcond=None)[0]
pendiente1, pendiente2, intersección = coeficientes

print(f"Pendiente 1: {pendiente1}")
print(f"Pendiente 2: {pendiente2}")
print(f"Intersección: {intersección}")
```


```python
import matplotlib.pyplot as plt
X = np.random.randn(200, 2)
X[:50] += 4
Y = np.zeros(200)
Y[:50] = 1
plt.scatter(X[:, 0], X[:, 1], c=Y)
```

## Pandas

- Librería (de facto estándar) para estructurar datos tabulares
- Multivariable (string, int, float, bool...)
- Dos clases:
  - Series (1 dimensión)
  - DataFrames (2+ dimensiones)

```python
import pandas as pd

frame = pd.DataFrame(random_list)
print(frame)
```

### Pandas Series
- Datos unidimensionales (similar a NumPy)
- Elementos + índices modificables
- Índices semánticos y posicionales

```python
import pandas as pd
countries = pd.Series(['Spain','Andorra','Gibraltar','Portugal','France'])
print(type(countries))
print(countries.iloc[0])
```

Diferencias entre Pandas Series y diccionario
* Diccionario, es una estructura que relaciona las claves y los valores de forma arbitraria.
* Series, estructura de forma estricta listas de valores con listas de índice asignado en la posición.
* Series, es más eficiente para ciertas operaciones que los dicionarios.
* En las Series los valores de entrada pueden ser listas o Numpy arrays.
* En Series los índices semánticos pueden ser integers o caracteres, en los valores igual.
* Series se podría entender entre una lista y un diccionario Python, pero es de una dimensión.

### DataFrame
- Datos tabulares (filas x columnas)
- Columnas: Series con índices compartidos

```python 
import pandas as pd
# crear un DataFrame a partir de un diccionario de elementos de la misma longitud
diccionario = { "Nombre" : ["Marisa","Laura","Manuel"], 
                "Edad" : [34,29,12] }

# las claves identifican columnas
frame = pd.DataFrame(diccionario, index=['a', 'b', 'c'])
print(frame)
```

# Jupyter notebook

## Markdown

Fichero de texto con extensión .md en la que se recoje documentación de forma estructurada: [Markdown](https://www.markdownguide.org/)

> **Tip**
>
> En programación y en proyectos de Ciencia de Datos es de uso muy extendido. 

## Jupyter notebook en Ciencia de Datos

- Presentaciones, ejercicios, actividades... __todo__ notebooks
- Markdown/HTML + codigo en vivo
- Facilita la colaboración y la presentación interactiva de código
- En la terminal: __jupyter notebook__
- Archivos _.ipynb_
- Documentación https://jupyter.readthedocs.io/en/latest/

# Conclusiones

- Presentación de la práctica 1:
    - El foro tiene que ser un espacio de debate y contribución.
    - El 29 de marzo se corregirá por primera vez el foro.
    - Plazo máximo de primera convocatoria 29/04/2025
    - Plazo máximo de segunda convocatoria 25/06/2025

- Se ha configurado el entorno de trabajo y se presentan las librerías básicas para trabajar con datos.


# Referencias

- Videos disponibles en "Recursos y materiales/2. Vídeos de la asignatura"
- Guía de estudio para la Práctica 2