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

*Archivo: [Análisis Exploratorio de Datos - Inicial](notebooks/1_eda.ipynb)*

### **Limpieza y preprocesamiento**
Durante esta fase, se llevó a cabo un proceso de limpieza y preparación de los conjuntos de datos de comercio exterior. El objetivo principal fue consolidar la información y asegurar su calidad para análisis posteriores.

Como primera acción, se procedió a unir los cuatro conjuntos de datos individuales (df_2012_2020, df_2021, df_2022, df_2023) en un único DataFrame consolidado, denominado df_2012_2023, para facilitar la gestión y el análisis de todos los registros del período.

```Python
df_2012_2023 = pd.concat([df_2012_2020, df_2021, df_2022, df_2023])
filas, columnas = df_2012_2023.shape

print('Filas y columnas del DataFrame 2012 - 2023 (unión de los 4 conjuntos de datos)')
print(f'Filas: {filas}\nColumnas: {columnas}')
```

```bash
Filas y columnas del DataFrame 2012 - 2023 (unión de los 4 conjuntos de datos)
Filas: 2556
Columnas: 8
```
El DataFrame resultante df_2012_2023 ahora contiene 2556 filas y 8 columnas. Se verificaron los tipos de datos de cada columna y se confirmó que eran correctos, lo que eliminó la necesidad de realizar conversiones de tipo.

Tras la consolidación de los datos, se realizó una nueva verificación exhaustiva de valores nulos y duplicados en el DataFrame unificado para garantizar la integridad del conjunto de datos final. Los resultados confirmaron la ausencia total de ambos:

```Python
# Verificar valores nulos
valores_nulos = df_2012_2023.isnull().sum()
print(f'Nulos\n{valores_nulos}')

# Verificar duplicados
duplicados = df_2012_2023.duplicated().sum()
print(f'\nDuplicados: {duplicados}')
```
```bash
Nulos
prod_est     0
coverage     0
type         0
year         0
month        0
concept      0
value_usd    0
status       0
dtype: int64

Duplicados: 0
```
Las columnas prod_est, coverage, type, concept, y status ya habían sido revisadas durante el EDA inicial y no se detectaron errores ni la necesidad de limpieza adicional en sus entradas.

Un punto crucial abordado en esta fase fue el análisis de los valores negativos identificados en la columna value_usd durante el análisis preliminar:
```Python
valores_negativos = df_2012_2023[df_2012_2023['value_usd'] < 0]
print(f'Cantidad de valores negativos: {len(valores_negativos)}')
valores_negativos.head(10)
```
```Bash
Cantidad de valores negativos: 199
```
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>prod_est</th>
      <th>coverage</th>
      <th>type</th>
      <th>year</th>
      <th>month</th>
      <th>concept</th>
      <th>value_usd</th>
      <th>status</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>16</th>
      <td>Trade Balance of Goods of Mexico</td>
      <td>National</td>
      <td>Not applicable</td>
      <td>2012</td>
      <td>1</td>
      <td>Total Trade Balance Exports Total - Imports Total</td>
      <td>-267.418000</td>
      <td>Final Figures</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Trade Balance of Goods of Mexico</td>
      <td>National</td>
      <td>Not applicable</td>
      <td>2012</td>
      <td>1</td>
      <td>Total Trade Balance Exports Total - Imports To...</td>
      <td>-1013.224000</td>
      <td>Final Figures</td>
    </tr>
    <tr>
      <th>35</th>
      <td>Trade Balance of Goods of Mexico</td>
      <td>National</td>
      <td>Not applicable</td>
      <td>2012</td>
      <td>2</td>
      <td>Total Trade Balance Exports Total - Imports To...</td>
      <td>-267.776000</td>
      <td>Final Figures</td>
    </tr>
    <tr>
      <th>71</th>
      <td>Trade Balance of Goods of Mexico</td>
      <td>National</td>
      <td>Not applicable</td>
      <td>2012</td>
      <td>4</td>
      <td>Total Trade Balance Exports Total - Imports To...</td>
      <td>-366.619000</td>
      <td>Final Figures</td>
    </tr>
    <tr>
      <th>89</th>
      <td>Trade Balance of Goods of Mexico</td>
      <td>National</td>
      <td>Not applicable</td>
      <td>2012</td>
      <td>5</td>
      <td>Total Trade Balance Exports Total - Imports To...</td>
      <td>-532.382000</td>
      <td>Final Figures</td>
    </tr>
    <tr>
      <th>107</th>
      <td>Trade Balance of Goods of Mexico</td>
      <td>National</td>
      <td>Not applicable</td>
      <td>2012</td>
      <td>6</td>
      <td>Total Trade Balance Exports Total - Imports To...</td>
      <td>-166.668000</td>
      <td>Final Figures</td>
    </tr>
    <tr>
      <th>124</th>
      <td>Trade Balance of Goods of Mexico</td>
      <td>National</td>
      <td>Not applicable</td>
      <td>2012</td>
      <td>7</td>
      <td>Total Trade Balance Exports Total - Imports Total</td>
      <td>-409.644000</td>
      <td>Final Figures</td>
    </tr>
    <tr>
      <th>125</th>
      <td>Trade Balance of Goods of Mexico</td>
      <td>National</td>
      <td>Not applicable</td>
      <td>2012</td>
      <td>7</td>
      <td>Total Trade Balance Exports Total - Imports To...</td>
      <td>-1224.047000</td>
      <td>Final Figures</td>
    </tr>
    <tr>
      <th>142</th>
      <td>Trade Balance of Goods of Mexico</td>
      <td>National</td>
      <td>Not applicable</td>
      <td>2012</td>
      <td>8</td>
      <td>Total Trade Balance Exports Total - Imports Total</td>
      <td>-981.812999</td>
      <td>Final Figures</td>
    </tr>
    <tr>
      <th>143</th>
      <td>Trade Balance of Goods of Mexico</td>
      <td>National</td>
      <td>Not applicable</td>
      <td>2012</td>
      <td>8</td>
      <td>Total Trade Balance Exports Total - Imports To...</td>
      <td>-1844.143000</td>
      <td>Final Figures</td>
    </tr>
  </tbody>
</table>
</div>


Se investigó el tipo de conceptos asociados a estos valores negativos:
```Python
concept = valores_negativos['concept']
concept.value_counts()
```
```Bash
concept
Total Trade Balance Exports Total - Imports Total CIF    115
Total Trade Balance Exports Total - Imports Total         84
Name: count, dtype: int64
```

Adicionalmente, se verificó si existían valores negativos bajo cualquier otro concepto diferente a la balanza comercial:
```Python
# Ver si hay otros conceptos con valores negativos distintos a la balanza comercial
otros_negativos = valores_negativos[~valores_negativos['concept'].str.contains('Trade Balance', case=False)]
print(f'Otros valores negativos fuera del concepto de balanza: {len(otros_negativos)}')
otros_negativos.head()
```
```Bash
Otros valores negativos fuera del concepto de balanza: 0
```
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>prod_est</th>
      <th>coverage</th>
      <th>type</th>
      <th>year</th>
      <th>month</th>
      <th>concept</th>
      <th>value_usd</th>
      <th>status</th>
    </tr>
  </thead>
  <tbody>
  </tbody>
</table>
</div>

Los resultados confirman que los valores negativos en ``value_usd`` corresponden exclusivamente a los conceptos de balanza comercial (``Total Trade Balance Exports Total - Imports Total`` y ``Total Trade Balance Exports Total - Imports Total CIF``). Esto reitera la conclusión del análisis preliminar: estos valores no son errores de origen, sino una representación válida de periodos con déficit comercial (cuando las importaciones superan a las exportaciones), y por lo tanto, se retienen en el conjunto de datos por su relevancia para el análisis económico del país.

Como parte final de la limpieza y el procesamiento, se realizó una búsqueda de valores atípicos (outliers) en la columna ``value_usd`` utilizando el método del rango intercuartílico (IQR):
```Python
Q1 = df_2012_2023['value_usd'].quantile(0.25)
Q3 = df_2012_2023['value_usd'].quantile(0.75)
IQR = Q3 - Q1
outliers = df_2012_2023[(df_2012_2023['value_usd'] < Q1 - 1.5 * IQR) | (df_2012_2023['value_usd'] > Q3 + 1.5 * IQR)]
print(f"Outliers detectados por IQR: {len(outliers)}")
```
```Bash
Outliers detectados por IQR: 0
```
![Detección de Outliers](reports/figures/deteccion_outliers_valores_comerciales.png)
No se identificaron valores atípicos que se consideren relevantes o que pudieran afectar negativamente los objetivos del proyecto.

Finalmente, el conjunto de datos consolidado y validado fue guardado en formato CSV para su uso en análisis posteriores:
```Python
df_2012_2023.to_csv('../data/processed/mex_trade_2012_2023_clean.csv', index=False)
print('CSV guardado')
```

*Archivo: [Limpieza y transformación](notebooks/2_lipieza_transformacion.ipynb)*

### **Análisis exploratorio de datos (EDA)**
Con el conjunto de datos limpio y consolidado, se procedió a realizar un análisis exploratorio detallado para obtener una visión profunda del comportamiento del comercio exterior de México, enfocándose en el volumen por tipo de operaciones y su evolución temporal.

**Volumen Total: Tendencias Anuales por Tipo de Operación**

La primera visualización revela las tendencias anuales del volumen total de exportaciones, importaciones y la categoría "Not applicable", ofreciendo una panorámica del flujo comercial del país.

- **Dominio Persistente de las Importaciones (Línea Turquesa):** Las importaciones han representado consistentemente el mayor volumen de valor en USD a lo largo de todo el período (2012-2023). Superando significativamente a las exportaciones en la mayoría de los años, muestran una clara tendencia de crecimiento desde 2012 hasta 2022, alcanzando un pico de aproximadamente $2,461,878 USD en 2022. En 2023, se observa una ligera disminución, cerrando en $2,054,154 USD.
- **Crecimiento Sostenido de las Exportaciones (Línea Azul Oscuro):** Las exportaciones también exhiben una tendencia de crecimiento a lo largo del período, aunque con fluctuaciones. Comenzaron en $1,112,310 USD en 2012 y alcanzaron un pico en 2022 con $1,733,206 USD. Similar a las importaciones, las exportaciones experimentaron una caída en 2023, situándose en $1,480,532 USD.
- **Impacto de "Not applicable" (Línea Verde Claro):** Esta categoría permanece consistentemente en valores negativos y cercanos a cero en todos los años. Sugiere que representa saldos negativos, ajustes o rubros que restan al valor total del comercio, en lugar de un volumen de bienes o servicios transaccionado. Su valor se mantuvo relativamente bajo en comparación con exportaciones e importaciones, oscilando entre -$9,689 USD (2012) y -$75,468 USD (2022). Un valor atípico y el más "positivo" que alcanza es un ligero $58,077 USD en 2020.

**Comportamiento Reciente (2020-2023):**
- **2020 (Año de la Pandemia):** Se observa una caída notable tanto en exportaciones ($1,251,512 USD) como en importaciones ($1,532,528 USD) en 2020, lo cual es esperable debido a las interrupciones en el comercio global causadas por la pandemia de COVID-19.
- **Recuperación Post-Pandemia (2021-2022):** Los años siguientes mostraron una fuerte recuperación, con ambos volúmenes alcanzando sus puntos más altos en 2022, evidenciando la resiliencia del comercio.
- **Ligero Descenso en 2023:** Tanto las exportaciones como las importaciones mostraron una disminución en 2023 en comparación con 2022, lo que podría indicar una desaceleración en el crecimiento comercial al final del período analizado.
![Volumne Total de Exportaciones e Importaciones por Año y Tipo](reports/figures/volumen_total_exportaciones_importaciones_2012_2023.png)


**Composición del Comercio: Conceptos Clave por Valor Acumulado**

Para comprender la estructura interna de estos flujos, se analizó el top de conceptos con mayor valor acumulado por tipo de operación (Imports, Exports, Not applicable) durante el período 2012-2023.

- **Dominio de Importaciones Totales:**
   - **Los conceptos con mayor valor acumulado están ambos relacionados con las Importaciones:** ``"Total Imports CIF (Total Imports + Freight and Insurance of Imports)" encabeza la lista con $5,427,293.28 USD``. Esto indica que al considerar el costo de los bienes más el flete y el seguro, este es el rubro de mayor peso monetario.
   - **"Total Imports"** es el segundo concepto más grande. Esto resalta la magnitud general de las importaciones en el comercio.
- **Volumen Significativo de Exportaciones Totales y No Petroleras:**
   - **"Total Exports" es el tercer concepto más relevante con $5,206,323.57 USD**. Esto muestra que las exportaciones totales tienen un peso considerable en el panorama comercial.
   - **"Non Petroleum (No Petroleras)"** es el cuarto concepto. Su composición (barras azul oscuro para Imports y verde azulado para Exports) indica que tanto las importaciones como las exportaciones de productos no petroleros son sustanciales, siendo las importaciones de productos no petroleros significativamente mayores que las exportaciones de este tipo.
- **Composición por Tipo de Comercio (Color):** La coloración de las barras (azul oscuro para Imports, verde azulado para Exports, verde claro para Not applicable) permite visualizar la dominancia o combinación de flujos comerciales:
   - **"Manufacturing (Manufactura)"** es un concepto de alto valor, dominado por las importaciones, pero con una contribución notable de las exportaciones, lo que sugiere un intercambio bidireccional importante en este sector.
   - **"Intermediate Goods (Bienes Intermedios)"** es predominantemente una categoría de importaciones, lo que es común en cadenas de suministro que dependen de insumos extranjeros para la producción local.
   - **"Consumer Goods (Bienes de Consumo)"** también es mayoritariamente de importaciones.
   - **"Petroleum (Petróleo)"** tiene contribuciones tanto de importaciones como de exportaciones, siendo las exportaciones de petróleo ligeramente mayores en este caso acumulado.
- **Conceptos de Menor Valor (al final de la lista):** Conceptos como "Crude Oil (Petróleo Crudo)", "Agrarian (Agrario)", y "Freight and insurance of Imports" tienen valores acumulados mucho menores en comparación con los "Totales" o "Manufactura". Las categorías como "Extractive (Extractiva)" y "Other Oil (Otro Petróleo)" son aún menores.
- **Balances Comerciales Negativos:** Las categorías con valores negativos, como **"Total Trade Balance Exports Total - Imports Total CIF" con $-220,969.71 USD**, se encuentran al final de la lista. Estas categorías, con barras de color verde claro (Not applicable), muestran valores negativos, lo cual es esperado, ya que el balance comercial (exportaciones - importaciones) a menudo es negativo en una economía con más importaciones que exportaciones, y se alinea con la observación del gráfico de líneas anterior de que las importaciones superan a las exportaciones.
![Top concept con mayor valor acumulado 2012 - 2023](reports/figures/top_concept_mayor_valor_acumulado_2012_2023.png)

**Participación Porcentual Anual: Reafirmando el Déficit**

La proporción anual del comercio por tipo confirma la hegemonía de las importaciones y la estabilidad de la participación de las exportaciones.

- **Las Importaciones Lideran de Forma Sostenida:** A lo largo de todo el período (2012-2023), las **Importaciones (Imports % - barra naranja)** han sido el motor principal del comercio exterior, representando consistentemente **más del 57% del total anual**. Esta hegemonía subraya una economía con una alta demanda de bienes y servicios del extranjero.
- **Exportaciones: Estabilidad en la Proporción, no en el Volumen:** La participación de las **Exportaciones (Exports % - barra azul)** se ha mantenido sorprendentemente estable, oscilando alrededor del 42%-43% del comercio total cada año. Esto sugiere que, a pesar de las fluctuaciones en el volumen absoluto de exportaciones, su proporción relativa dentro del pastel comercial se ha mantenido constante.
- **La Anomalía de 2020: Un Punto de Inflexión Inesperado:** El año **2020 destaca como una excepción notable**, probablemente influenciada por la pandemia global. En contraste con la tendencia general, la participación de las **Importaciones disminuyó a su punto más bajo (54.24%)**, mientras que las **Exportaciones alcanzaron su pico (43.73%)**. Adicionalmente, la categoría "Not applicable %" (barra verde), que generalmente representa ajustes negativos, se tornó positiva (2.03%) por primera vez. Este cambio abrupto podría indicar que, durante la crisis de 2020, la caída en las importaciones fue más pronunciada que la de las exportaciones, alterando drásticamente las proporciones relativas del comercio total.
![Participación Porcentual Anual de Exportaciones e Importaciones](reports/figures/participacion_porcentual_anual_exportaciones_importaciones_2012_2023.png)

**Patrones Mensuales: Estacionalidad y el Impacto de la Pandemia**

El análisis del valor promedio mensual del comercio, visualizado en un mapa de calor, revela patrones estacionales recurrentes y el impacto disruptivo de eventos globales.

- **Crecimiento Sostenido a lo Largo de la Década:** Se observa un crecimiento constante y significativo en el valor promedio mensual del comercio a lo largo de los años. Los datos de los años más recientes (2022 y 2023) muestran consistentemente los valores más altos, destacando una expansión general en el volumen o valor del comercio. Este patrón sugiere una economía en constante expansión con un aumento en la actividad comercial global.
- **Patrones Estacionales Recurrentes:** Más allá del crecimiento anual, existen patrones estacionales o mensuales que se repiten. Ciertos meses, como **marzo (3), mayo (5), agosto (8) y octubre (10)**, tienden a mostrar consistentemente un mayor valor promedio, indicando posibles picos de actividad comercial relacionados con ciclos de producción, demanda de temporada o festividades. Por otro lado, los primeros meses del año (Enero y Febrero) y algunos meses intermedios (como Julio) a veces muestran valores ligeramente más bajos.
- **El Impacto Anómalo de 2020:** El año **2020 se destaca como una clara anomalía** en la tendencia de crecimiento. Específicamente, los meses de **Abril (4) con $9,433.74 USD y Mayo (5) con $7,466.27 USD** registraron los valores promedio más bajos de todo el período analizado, representados por colores azul oscuro muy frío. Este descenso abrupto es altamente consistente con el impacto global de la pandemia de COVID-19, que causó interrupciones masivas en las cadenas de suministro y el comercio internacional. Es alentador ver una recuperación gradual en los meses siguientes de 2020 (June en adelante), lo que demuestra la resiliencia del sector.
- **Aceleración del Crecimiento en Años Recientes (2021-2023):** Los años 2021, 2022 y especialmente 2023 han mostrado una aceleración notable en el crecimiento, con valores promedio mensuales que superan consistentemente los $16,000 - $20,000 USD. El **2023 se posiciona como el año de mayor actividad comercial** en el período estudiado, con varios meses superando la marca de los $20,000 USD (e.g., Marzo, Mayo, Agosto, Octubre). Esto subraya una fuerte recuperación y un impulso significativo en la actividad comercial en la era pospandemia.
![Mapa de calor](reports/figures/mapa_calor.png)

*Archivo: [Análisis Descriptivo](notebooks/3_analisis_descriptivo.ipynb)*

### **Balanza Comercial y Tendencia**
***Balance Comercial: Un Déficit Crónico y en Aumento***

Nuestro análisis del balance comercial anual entre 2012 y 2023 revela una realidad innegable: la entidad ha mantenido un déficit comercial persistente en cada uno de estos años. Esto significa que el valor de las importaciones ha superado consistentemente al de las exportaciones.

***La Magnitud y Tendencia del Déficit***

La magnitud de este déficit es considerable, oscilando entre los `-$301,016` y los `-$728,671`. Alarmantemente, hemos observado una tendencia general de incremento en el déficit desde 2012, alcanzando su punto más alto en 2022 con -$728,671.

Un punto de interés es el año 2020, que rompe esta tendencia con el déficit más bajo del período ``( -$301,016)``. Esto coincide con el inicio de la pandemia de COVID-19, sugiriendo que las importaciones pudieron haber caído más drásticamente o las exportaciones mostraron una mayor resiliencia en proporción durante ese año. Sin embargo, en 2023, aunque el déficit se redujo ligeramente respecto a 2022, se mantiene en un nivel elevado de ``-$573,622``.

***Consistencia en los Datos***

Estos hallazgos no son aislados; confirman y refuerzan las observaciones de nuestros análisis previos. Tanto los gráficos de volumen total, que muestran las importaciones consistentemente por encima de las exportaciones, como los de participación porcentual, que indican una mayor proporción de importaciones, respaldan esta interpretación de un déficit comercial crónico.

En síntesis, la entidad enfrenta una dependencia continua y creciente de las importaciones, un factor clave a considerar en su dinámica económica.
![Balanza Comercial Anual(Exportaciones - Importaciones) 2012 -2023](reports/figures/balanza_comercial_anual_exportaciones_importaciones_2012_2023.png)

La balanza comercial de la entidad ha estado en un déficit crónico a lo largo de todo el período 2012-2023. La tendencia principal ha sido un aumento constante de este déficit, con una notable interrupción y reducción temporal en 2020 debido a la pandemia, seguida de un rápido y significativo crecimiento del déficit en 2021 y 2022, alcanzando un máximo histórico en 2022. El año 2023 muestra una ligera moderación, pero el déficit se mantiene en niveles elevados. Esta tendencia subraya una dependencia estructural de las importaciones y un desafío continuo para equilibrar el flujo comercial.
![Tendencia con la Balanza como serie de tiempo](reports/figures/tendencia_balanza_como_serie_tiempo.png)

*Archivo: [Balanza Comercial y Tendencias](notebooks/4_balanza_comercial_tendencia.ipynb)*

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