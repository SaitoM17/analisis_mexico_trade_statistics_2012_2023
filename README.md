# 📊 Análisis "Mexico Trade Statistics 2012 - 2023"
---

## 📚 Tabla de Contenidos

- [🎯 Propósito](#-propósito)
- [📦 Conjunto de Datos](#-conjunto-de-datos)
- [🧪 Desarrollo del Proyecto](#-desarrollo-del-proyecto)
- [🛠️ Tecnologías](#️-tecnologías)
- [⚙️ Instalación](#️-instalación)
- [📈 Conclusiones y Recomendaciones](#conclusiones-y-recomendaciones)
- [👤 Autor](#-autor)
- [📝 Licencia](#-licencia)

---

## 🎯 Propósito

Analizar la evolución del comercio exterior de México entre 2012 y 2023, identificando los principales socios comerciales, productos clave, tendencias de exportación e importación, y patrones económicos relevantes mediante técnicas de análisis de datos.

---

## 📦 Conjunto de Datos

El conjunto de datos utilizado contiene las siguientes columnas:

- `prod_est`: Nombre de la institución responsable de la recopilación de datos.
- `coverage`: Área geográfica a la que se refieren los indicadores estadísticos.
- `type`: Tipo de operación comercial.
- `year`: Año.
- `month`: Mes numérico.
- `concept`: Descripción de los principales agregados de la información.
- `value_usd`: Valor de venta en millones de dólares estadounidenses, valorado en base FOB o CIF.
- `status`: Estado de las cifras según los lineamientos del INEGI.

Fuente: https://www.kaggle.com/datasets/elanderos/mexico-trade-statistics-2012-2023?select=mex_trade_2022.csv.

---

## 🧪 Desarrollo del Proyecto

### **Carga y exploración inicial de los datos**
El análisis del comercio exterior de México, abarcando el período 2012-2023, se inició con la adquisición de los conjuntos de datos de "Official Mexico Trade Statistics (2012-2023)" de Kaggle, publicados por ***e_landeros***. La primera etapa se centró en un análisis exploratorio preliminar (EDA) con el objetivo de comprender la estructura, volumen, variables y la calidad de los datos, incluyendo la identificación de valores nulos, duplicados e inconsistencias.

Como primer paso, se analizó la cantidad de filas y columnas de cada conjunto de datos:
```bash
Filas y columnas de DatFrame df_2012_2020
Filas: 1944
Columnas: 8

Filas y columnas de DatFrame df_2021
Filas: 216
Columnas: 8

Filas y columnas de DatFrame df_2022
Filas: 216
Columnas: 8

Filas y columnas de DatFrame df_2023
Filas: 180
Columnas: 8
```

Durante la exploración preliminar, el uso de la función ``.info()`` en los cuatro conjuntos de datos permitió determinar que todos poseen las mismas columnas y tipos de datos consistentes. Dado que los tipos de datos eran correctos y uniformes, no fue necesaria ninguna transformación en esta etapa.

Se realizó una inspección detallada de las entradas (registros) en cada columna de los cuatro conjuntos de datos para identificar posibles errores. Esta exploración exhaustiva confirmó la ausencia de cualquier tipo de error en los registros.

Asimismo, se llevó a cabo una verificación minuciosa de valores nulos y duplicados en todos los conjuntos de datos:
```bash
Cantidad de valores nulos en conjunto de datos 2012 - 2020
prod_est     0
coverage     0
type         0
year         0
month        0
concept      0
value_usd    0
status       0
dtype: int64

Cantidad de valores nulos en conjunto de datos 2021
prod_est     0
coverage     0
type         0
year         0
month        0
concept      0
value_usd    0
status       0
dtype: int64

Cantidad de valores nulos en conjuntos de datos 2022
prod_est     0
coverage     0
type         0
year         0
month        0
concept      0
value_usd    0
status       0
dtype: int64

Cantidad de valores nulos en conjuntos de datos 2023
prod_est     0
coverage     0
type         0
year         0
month        0
concept      0
value_usd    0
status       0
dtype: int64

Cantidad de duplicados en conjunto de datos 2012 - 2020
0

Cantidad de duplicados en conjunto de datos 2021
0

Cantidad de duplicados en conjunto de datos 2022
0

Cantidad de duplicados en conjunto de datos 2023
0

```

Un punto importante de este EDA fue la identificación de registros con valores negativos en la columna value_usd a lo largo de los cuatro conjuntos de datos. Se determinó que estos valores negativos no constituyen errores, sino que representan meses en los que la balanza comercial fue deficitaria, es decir, las importaciones superaron a las exportaciones. Dada su relevancia económica y su capacidad para reflejar la dinámica comercial real del país en ciertos períodos, estos registros se mantuvieron en el análisis, ya que aportan un valor significativo al estudio del comportamiento del comercio y permiten la detección de patrones de déficit.

En conclusión, este análisis exploratorio preliminar no identificó problemas de calidad significativos en los conjuntos de datos, asegurando una base robusta y fiable para fases de análisis más avanzadas.

*Archivo: 1_eda.ipynb*

### **Limpieza y preprocesamiento**:
   - Manejo de valores nulos, duplicados, formatos y conversiones de fechas.

### **Análisis exploratorio de datos (EDA)**:
   - [Ej. Distribución, correlaciones, agrupaciones, etc.]

### **Visualización de datos**:
   - Uso de gráficos de barras, líneas, cajas, dispersión y mapas de calor.

### **Modelado o reportes (opcional)**:
   - [Si aplica: modelos de ML, clustering, predicciones, etc.]

### **Conclusiones y recomendaciones**:
   - Síntesis de hallazgos clave y propuestas de acción.

---

## 📈 Conclusiones y Recomendaciones

- [Insight 1]
- [Insight 2]
- [Recomendación práctica o estratégica basada en los datos]

---

## 🛠️ Tecnologías

- Python
- Pandas
- Matplotlib
- Seaborn
- Jupyter Notebook / Google Colab
- [Otras herramientas que uses, como Scikit-learn, Plotly, etc.]

---

## ⚙️ Instalación

### 1. Clonar este repositorio:
```bash
git clone https://github.com/tu_usuario/nombre_del_proyecto.git
```
### 2. Uso de un Entorno Virtual para Aislar Dependencias

Para evitar conflictos con versiones de librerías, se recomienda usar entornos virtuales.

####  Crear y Activar un Entorno Virtual

##### Crear el entorno virtual:
```
python -m venv venv
```
##### Activar el entorno:
* #### En Windows:

    ```
    venv\Scripts\activate
    ```

* #### En Mac/Linux::

    ```
    source venv/bin/activate
    ```
#### 3. Instalar dependencias dentro del entorno:
* #### Opición 1:
    ```
    pip install -r requirements.txt
    ```

* #### Opción 2 (De forma manual):
    ```
    pip install numpy pandas matplotlib seaborn scikit-learn
    ```
---

## 👤 Autor

**Said Mariano Sánchez** – *smariano170@gmail.com*  
Este proyecto forma parte de mi portafolio como analista de datos Jr.

---

## 📝 Licencia

Este proyecto está licenciado bajo la **Licencia MIT**. Puedes usarlo, modificarlo y distribuirlo libremente, siempre que menciones al autor original.

---