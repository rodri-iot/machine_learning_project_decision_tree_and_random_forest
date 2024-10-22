# Plantilla de Proyecto de Ciencia de Datos

Esta plantilla está diseñada para impulsar proyectos de ciencia de datos proporcionando una configuración básica para conexiones de base de datos, procesamiento de datos, y desarrollo de modelos de aprendizaje automático. Incluye una organización estructurada de carpetas para tus conjuntos de datos y un conjunto de paquetes de Python predefinidos necesarios para la mayoría de las tareas de ciencia de datos.

## Estructura

El proyecto está organizado de la siguiente manera:

- `app.py` - El script principal de Python que ejecutas para tu proyecto.
- `explore.py` - Un notebook para que puedas hacer tus exploraciones, idealmente el codigo de este notebook se migra hacia app.py para subir a produccion.
- `utils.py` - Este archivo contiene código de utilidad para operaciones como conexiones de base de datos.
- `requirements.txt` - Este archivo contiene la lista de paquetes de Python necesarios.
- `models/` - Este directorio debería contener tus clases de modelos SQLAlchemy.
- `data/` - Este directorio contiene los siguientes subdirectorios:
  - `interim/` - Para datos intermedios que han sido transformados.
  - `processed/` - Para los datos finales a utilizar para el modelado.
  - `raw/` - Para datos brutos sin ningún procesamiento.

## Configuración

**Prerrequisitos**

Asegúrate de tener Python 3.11+ instalado en tu máquina. También necesitarás pip para instalar los paquetes de Python.

**Instalación**

Clona el repositorio del proyecto en tu máquina local.

Navega hasta el directorio del proyecto e instala los paquetes de Python requeridos:

```bash
pip install -r requirements.txt
```

**Crear una base de datos (si es necesario)**

Crea una nueva base de datos dentro del motor Postgres personalizando y ejecutando el siguiente comando: `$ createdb -h localhost -U <username> <db_name>`
Conéctate al motor Postgres para usar tu base de datos, manipular tablas y datos: `$ psql -h localhost -U <username> <db_name>`
NOTA: Recuerda revisar la información del archivo ./.env para obtener el nombre de usuario y db_name.

¡Una vez que estés dentro de PSQL podrás crear tablas, hacer consultas, insertar, actualizar o eliminar datos y mucho más!

**Variables de entorno**

Crea un archivo .env en el directorio raíz del proyecto para almacenar tus variables de entorno, como tu cadena de conexión a la base de datos:

```makefile
DATABASE_URL="your_database_connection_url_here"
```

## Ejecutando la Aplicación

Para ejecutar la aplicación, ejecuta el script app.py desde la raíz del directorio del proyecto:

```bash
python app.py
# or
app_dt.ipynb
```

## Añadiendo Modelos

Para añadir clases de modelos SQLAlchemy, crea nuevos archivos de script de Python dentro del directorio models/. Estas clases deben ser definidas de acuerdo a tu esquema de base de datos.

Definición del modelo de ejemplo (`models/example_model.py`):

```py
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy import Column, Integer, String

Base = declarative_base()

class ExampleModel(Base):
    __tablename__ = 'example_table'
    id = Column(Integer, primary_key=True)
    name = Column(String)

```

## Optimizando el modelo

Hiper parametros para optimización del modelo

```py
hyperparams = {
    'criterion': ['gini', 'entropy', 'log_loss'],  # Función para medir la calidad de una división.
    'splitter': ['best', 'random'],  # Estrategia usada para dividir en nodos.
    'max_depth': [None, 10, 20, 30, 40, 50],  # Profundidad máxima del árbol.
    'min_samples_split': [2, 5, 10],  # Número mínimo de muestras necesarias para dividir un nodo.
    'min_samples_leaf': [1, 2, 5, 10],  # Número mínimo de muestras necesarias en un nodo hoja.
    'max_features': [None, 'sqrt', 'log2'],  # Número de características a considerar cuando se divide.
    'max_leaf_nodes': [None, 10, 20, 30, 40],  # Número máximo de nodos hoja.
    'min_impurity_decrease': [0.0, 0.01, 0.05],  # Umbral para una disminución mínima de la impureza.
    'ccp_alpha': [0.0, 0.01, 0.1],  # Parámetro de complejidad usado para el podado.
}
```

#### Explicación de los hiperparámetros
- `criterion`: Define la métrica para evaluar las divisiones.

   - 'gini': Gini Impurity (por defecto).
   - 'entropy': Información de ganancia usando la entropía.
   - 'log_loss': Entropía cruzada.
- `splitter`:

   - 'best': Escoge la mejor división.
   - 'random': Escoge la división aleatoriamente.
- `max_depth`: Limita la profundidad del árbol. Evita el sobreajuste. Un valor más bajo de max_depth simplifica el modelo.

- `min_samples_split`: Número mínimo de muestras requeridas para dividir un nodo interno.

- `min_samples_leaf`: Número mínimo de muestras que un nodo hoja debe tener.

- `max_features`: Número de características a considerar cuando se busca la mejor división. Puede ser:

   - None: Considera todas las características.
   - 'sqrt': Usa la raíz cuadrada del número de características.
   - 'log2': Usa el logaritmo en base 2 del número de características.
- `max_leaf_nodes`: Restringe el número de nodos hoja. Un valor más bajo limita la cantidad de nodos y ayuda a evitar el sobreajuste.

- `min_impurity_decrease`: Un nodo se dividirá si la disminución de impureza es mayor a este valor.

- `ccp_alpha`: Parámetro de poda para la complejidad del árbol.

## Trabajando con Datos

Puedes colocar tus conjuntos de datos brutos en el directorio data/raw, conjuntos de datos intermedios en data/interim, y los conjuntos de datos procesados listos para el análisis en data/processed.

Para procesar datos, puedes modificar el script app.py para incluir tus pasos de procesamiento de datos, utilizando pandas para la manipulación y análisis de datos.

## Contribuyentes

Esta plantilla fue construida como parte del [Data Science and Machine Learning Bootcamp](https://4geeksacademy.com/us/coding-bootcamps/datascience-machine-learning) de 4Geeks Academy por [Alejandro Sanchez](https://twitter.com/alesanchezr) y muchos otros contribuyentes. Descubre más sobre [los programas BootCamp de 4Geeks Academy](https://4geeksacademy.com/us/programs) aquí.

Otras plantillas y recursos como este se pueden encontrar en la página de GitHub de la escuela.