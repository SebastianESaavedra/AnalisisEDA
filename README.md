# **Producción de petroleo y gas de reservorios convencionales y no convencionales** 
El siguiente dataset contiene producciones de petroleo y gas seccionado por operadora, provincia, formacion y cuenca, entre otros. 
También cuenta con valores de inyecciones de agua, gas y co2, lo que resulta interesante comparar en terminos de reservorios convencionales y no convencionales.


Fuente: https://datos.gob.ar/dataset/energia-produccion-petroleo-gas-por-pozo-capitulo-iv/archivo/energia_2f2834f4-1981-448f-9a3c-1e519d8c10cd


---

# **Importar el dataset a google collab**

Importación de librerias de pandas y seaborn, acceso al google drive y lectura del archivo energy.csv


```python
import seaborn as sns
import pandas as pd
```

```python
from google.colab import drive
drive.mount('/content/drive')
```


```python
df_original = pd.read_csv('/content/drive/My Drive/Colab Notebooks/prod.csv')
```

Creación de los dataframes:
```python
df= df_original[df_original.anio.isin([2022,2020])]
df= df[df.cuenca.isin(['NEUQUINA','CUYANA','GOLFO SAN JORGE'])]
df_neuquina= df[df.cuenca.isin(['NEUQUINA'])]
df_cuyana= df[df.cuenca.isin(['CUYANA'])]
df_sanjorge= df[df.cuenca.isin(['GOLFO SAN JORGE'])]
```




# Exploración general del conjunto de datos


## Explorando el conjunto de datos
Ahora, podemos comenzar a explorar el conjunto de datos utilizando las funciones que hemos discutido anteriormente:


```python
# Explorando el conjunto de datos
print(df.shape)
print(df.dtypes)
print(df.head())
print(df.info())
print(df.describe())
print(df.isnull().sum())
```

    (60447, 25)
    idempresa                  object
    anio                        int64
    mes                         int64
    prod_pet                  float64
    prod_gas                  float64
    prod_agua                 float64
    iny_agua                  float64
    iny_gas                   float64
    iny_co2                   float64
    iny_ptros                 float64
    tef                       float64
    vida_util                 float64
    empresa                    object
    formprod                   object
    formacion                  object
    idareapermisoconcesion     object
    areapermisoconcesion       object
    idareayacimiento           object
    areayacimiento             object
    tipo_de_recurso            object
    proyecto                   object
    sub_tipo_recurso           object
    cuenca                     object
    provincia                  object
    fecha_data                 object
    dtype: object
         idempresa  anio  mes  prod_pet  prod_gas  prod_agua  iny_agua  iny_gas  \
    1411      Z001  2020    1       0.0       0.0        0.0       0.0      0.0   
    1412      Z001  2020    1       0.0       0.0        0.0       0.0      0.0   
    1413      Z001  2020    1       0.0       0.0        0.0       0.0      0.0   
    1414      Z001  2020    1       0.0       0.0        0.0       0.0      0.0   
    1415      Z001  2020    1       0.0       0.0        0.0       0.0      0.0   
    
          iny_co2  iny_ptros  ...  idareapermisoconcesion  \
    1411      0.0        0.0  ...                     ABO   
    1412      0.0        0.0  ...                     ABO   
    1413      0.0        0.0  ...                     AGR   
    1414      0.0        0.0  ...                    BLLO   
    1415      0.0        0.0  ...                    Z042   
    
                       areapermisoconcesion idareayacimiento  \
    1411  BLANCO DE LOS OLIVOS - BLOQUE "A"              ABO   
    1412  BLANCO DE LOS OLIVOS - BLOQUE "A"              ABO   
    1413                      GENERAL ROCA               AGR   
    1414                    PUESTO SURVELIN             PUSU   
    1415                           DON JOSE             Z122   
    
                           areayacimiento tipo_de_recurso      proyecto  \
    1411  BLANCO DE LOS OLIVOS-BLOQUE "A"    CONVENCIONAL  Sin Proyecto   
    1412  BLANCO DE LOS OLIVOS-BLOQUE "A"    CONVENCIONAL  Sin Proyecto   
    1413                     GENERAL ROCA    CONVENCIONAL  Sin Proyecto   
    1414                  PUESTO SURVELIN    CONVENCIONAL  Sin Proyecto   
    1415                         DON JOSE    CONVENCIONAL  Sin Proyecto   
    
         sub_tipo_recurso    cuenca  provincia  fecha_data  
    1411              NaN  NEUQUINA  Rio Negro  2020-01-31  
    1412              NaN  NEUQUINA  Rio Negro  2020-01-31  
    1413              NaN  NEUQUINA  Rio Negro  2020-01-31  
    1414              NaN  NEUQUINA  Rio Negro  2020-01-31  
    1415              NaN  NEUQUINA  Rio Negro  2020-01-31  
    
    [5 rows x 25 columns]
    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 60447 entries, 1411 to 556095
    Data columns (total 25 columns):
     #   Column                  Non-Null Count  Dtype  
    ---  ------                  --------------  -----  
     0   idempresa               60447 non-null  object 
     1   anio                    60447 non-null  int64  
     2   mes                     60447 non-null  int64  
     3   prod_pet                60447 non-null  float64
     4   prod_gas                60447 non-null  float64
     5   prod_agua               60447 non-null  float64
     6   iny_agua                60447 non-null  float64
     7   iny_gas                 60447 non-null  float64
     8   iny_co2                 60447 non-null  float64
     9   iny_ptros               60447 non-null  float64
     10  tef                     60447 non-null  float64
     11  vida_util               9126 non-null   float64
     12  empresa                 60447 non-null  object 
     13  formprod                59919 non-null  object 
     14  formacion               59584 non-null  object 
     15  idareapermisoconcesion  60399 non-null  object 
     16  areapermisoconcesion    60399 non-null  object 
     17  idareayacimiento        60447 non-null  object 
     18  areayacimiento          60447 non-null  object 
     19  tipo_de_recurso         60447 non-null  object 
     20  proyecto                60447 non-null  object 
     21  sub_tipo_recurso        4634 non-null   object 
     22  cuenca                  60447 non-null  object 
     23  provincia               60447 non-null  object 
     24  fecha_data              60447 non-null  object 
    dtypes: float64(9), int64(2), object(14)
    memory usage: 12.0+ MB
    None
                   anio           mes       prod_pet       prod_gas     prod_agua  \
    count  60447.000000  60447.000000   60447.000000   60447.000000  6.044700e+04   
    mean    2021.009215      6.501282    1002.175340    1140.890549  1.114784e+04   
    std        0.999966      3.452457    6931.598021   11208.061105  6.368836e+04   
    min     2020.000000      1.000000       0.000000       0.000000 -4.260000e+00   
    25%     2020.000000      4.000000       0.000000       0.000000  0.000000e+00   
    50%     2022.000000      7.000000       0.000000       0.000000  0.000000e+00   
    75%     2022.000000      9.000000      94.129716      44.860000  4.245833e+02   
    max     2022.000000     12.000000  251981.040000  565742.416880  1.058743e+06   
    
               iny_agua       iny_gas  iny_co2     iny_ptros           tef  \
    count  6.044700e+04  60447.000000  60447.0  60447.000000  60447.000000   
    mean   1.137200e+04      1.922774      0.0     27.580212    331.770791   
    std    6.849562e+04    142.169680      0.0   1089.158120   1641.293023   
    min    0.000000e+00      0.000000      0.0      0.000000      0.000000   
    25%    0.000000e+00      0.000000      0.0      0.000000      0.000000   
    50%    0.000000e+00      0.000000      0.0      0.000000      0.000000   
    75%    0.000000e+00      0.000000      0.0      0.000000     90.000000   
    max    1.364515e+06  28878.550000      0.0  74310.400000  47752.100000   
    
             vida_util  
    count  9126.000000  
    mean      0.503616  
    std      13.879929  
    min       0.000000  
    25%       0.000000  
    50%       0.000000  
    75%       0.000000  
    max     383.000000  
    idempresa                     0
    anio                          0
    mes                           0
    prod_pet                      0
    prod_gas                      0
    prod_agua                     0
    iny_agua                      0
    iny_gas                       0
    iny_co2                       0
    iny_ptros                     0
    tef                           0
    vida_util                 51321
    empresa                       0
    formprod                    528
    formacion                   863
    idareapermisoconcesion       48
    areapermisoconcesion         48
    idareayacimiento              0
    areayacimiento                0
    tipo_de_recurso               0
    proyecto                      0
    sub_tipo_recurso          55813
    cuenca                        0
    provincia                     0
    fecha_data                    0
    dtype: int64
    

Esto nos dará una idea general del conjunto de datos. Se destaca la funcion para conocer el tipo de datos de cada una de las columnas. 
Se observa que las columnas emporesa, formprod, formacion, idareapermisoconcesion,  areapermisoconcesion y sub_tipo_recurso presentan nulos.






# Visualización de datos
La visualización de datos es una parte importante del EDA, ya que nos permite ver patrones y relaciones que podrían no ser evidentes en una tabla de datos. seaborn ofrece una amplia gama de herramientas para la visualización de datos.

## Diagrama de dispersión (scatter plot)
Una forma común de visualizar la relación entre dos variables numéricas es mediante un diagrama de dispersión. seaborn hace que sea fácil crear un diagrama de dispersión utilizando la función scatterplot:

1) Scatter plot de producción de petroleo (y) vs inyección de agua (x) coloreado por cuenca y seccionado por tipo de recurso.
```python
import matplotlib.pyplot as plt
sns.scatterplot(x="iny_agua", y="prod_pet", data=df, hue='cuenca',style='tipo_de_recurso')
plt.legend(bbox_to_anchor=(1, 1), loc=2, borderaxespad=0)

```








    
![png](output_26_1.png)
    


A partir de este gráfico podemos ver que hay una diferencia entre los reservorios convencionales de los no convencionales (NC). Estos ultimos se distinguen de los convencionales principalmente porque para que se produzcan hidrocarburos no es necesaria la inyección de agua, si no que resultan otros los metodos para su extracción.
Los reservorios convencionales en cambio, muestran una correlación lineal entre la inyeccion de agua y la producción de petroleo. Esto es debido a que mientras se va extrayendo el hidrocarburo, la presión de extracción es cada vez menor. Pero existe justamente este metodo de recuperación mediante la inyección de agua en el reservorio, para que "empuje" en petroleo y facilite su extracción.
Respecto a las tres cuencas visibles, se ve que la unica que posee reservorios NC es la Neuquina. El comportamiento de los registros de San Jorge son similares a los de la Neuquina, pero la cuenca Cuyana necesita mayores niveles de agua para poder extraer sus recursos.


2) Scatter plot de producción de petroleo (y) vs inyección de agua (x) coloreado por formación y seccionado por tipo de recurso, pero solo para datos de la Cuenca Neuquina.


```python
import matplotlib.pyplot as plt
sns.scatterplot(x="iny_agua", y="prod_pet", data=df_neuquina, hue='formacion', style='tipo_de_recurso')
plt.legend(bbox_to_anchor=(1, 1), loc=2, borderaxespad=0)

```








    
![png](output_28_1.png)
    


Pareceria que la unica formacion no convencional que se tiene registro en el dataset es Vaca Muerta. Las demas formaciones convencionales suelen seguir el patron lineal.



3) Scatter plot de producción de petroleo (y) vs producción de gas (x) coloreado por formación y seccionado por tipo de recurso para datos de la Cuenca Neuquina.

```python
import matplotlib.pyplot as plt
sns.scatterplot(x="prod_gas", y="prod_pet", data=df_neuquina, hue='formacion', style='tipo_de_recurso')
plt.legend(bbox_to_anchor=(1, 1), loc=2, borderaxespad=0)
```








    
![png](output_30_1.png)
    


Aqui podemos observar que la producción de petroleo esta en ocaciones vinculada a la producción de gas. Los mayores productores de gas son los NC. Se pueden distinguir por lo menos dos tendencias lineales. 

# Diagrama de barras (bar plot)
Otra forma común de visualizar los datos es mediante un diagrama de barras, que se utiliza para mostrar la distribución de una variable categórica. seaborn hace que sea fácil crear un diagrama de barras utilizando la función `countplot`:


```python
##sns.countplot(x="tipo_de_recurso", data=df)
ax=sns.countplot(x="tipo_de_recurso", data=df)
ax.set_xticklabels(ax.get_xticklabels(),rotation=40)
plt.show()
```


    
![png](output_33_0.png)
    


Esto nos dará un diagrama de barras de la distribución de la variable "tipo_de_recurso" en el conjunto de datos. Podemos ver que el número de observaciones es mayor del tipo Convencional.




```python
a1=sns.displot(df, x='provincia',kde=True)
labels = a1.ax.get_xticklabels()
a1.set_xticklabels(labels,rotation=45)
plt.show()
```


    
![png](output_53_0.png)
    


La provincia dentro de las tres cuencas en tener más registros es Neuquén.



```python
order = df_neuquina['formacion'].sort_values().unique()
ax=sns.countplot(x='formacion', data=df_neuquina, palette='viridis', order=order)
ax.set_xticklabels(ax.get_xticklabels(),rotation=90)
plt.show()
```


    
![png](output_55_0.png)
    


El mayor conteo de registros es cuando una formación no es productiva (no se extrajo petroleo). Entre las formaciones más destacadas se encuentran: Vaca Muerta, Agrio, Quintuco, Centenario, teniendo en cuenta solo a datos de la cuenca neuquina.



# Histograma (histogram)
Un histograma es una forma común de visualizar la distribución de una variable numérica. seaborn hace que sea fácil crear un histograma utilizando la función `histplot`:


```python
sns.histplot(x="iny_agua", bins =5, data=df)
```




    <Axes: xlabel='iny_agua', ylabel='Count'>




    
![png](output_36_1.png)
    


La distribución de inyección de agua está mayoritariamente entre 0 y 0.25 aproximadamente.




# Análisis de correlación
El análisis de correlación es una parte importante del EDA, ya que nos permite ver la relación entre las variables numéricas en el conjunto de datos. Una forma común de analizar la correlación es mediante el cálculo de la matriz de correlación y la visualización de la misma mediante un mapa de calor.

## Matriz de correlación (correlation matrix)
Podemos calcular la matriz de correlación utilizando la función `corr` de pandas:


```python
df.corr()
```

    
    




<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>anio</th>
      <th>mes</th>
      <th>prod_pet</th>
      <th>prod_gas</th>
      <th>prod_agua</th>
      <th>iny_agua</th>
      <th>iny_gas</th>
      <th>iny_co2</th>
      <th>iny_ptros</th>
      <th>tef</th>
      <th>vida_util</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>anio</th>
      <td>1.000000</td>
      <td>-0.000202</td>
      <td>0.013025</td>
      <td>0.006800</td>
      <td>-0.000751</td>
      <td>-0.000787</td>
      <td>-0.011133</td>
      <td>NaN</td>
      <td>-0.002698</td>
      <td>-0.002069</td>
      <td>-0.031473</td>
    </tr>
    <tr>
      <th>mes</th>
      <td>-0.000202</td>
      <td>1.000000</td>
      <td>0.001744</td>
      <td>-0.000721</td>
      <td>-0.000967</td>
      <td>-0.001147</td>
      <td>-0.008994</td>
      <td>NaN</td>
      <td>-0.003171</td>
      <td>-0.002388</td>
      <td>-0.000474</td>
    </tr>
    <tr>
      <th>prod_pet</th>
      <td>0.013025</td>
      <td>0.001744</td>
      <td>1.000000</td>
      <td>0.180251</td>
      <td>0.386070</td>
      <td>0.342225</td>
      <td>0.030938</td>
      <td>NaN</td>
      <td>-0.003661</td>
      <td>0.525194</td>
      <td>-0.004744</td>
    </tr>
    <tr>
      <th>prod_gas</th>
      <td>0.006800</td>
      <td>-0.000721</td>
      <td>0.180251</td>
      <td>1.000000</td>
      <td>0.036217</td>
      <td>0.009652</td>
      <td>0.114844</td>
      <td>NaN</td>
      <td>-0.002578</td>
      <td>0.122306</td>
      <td>-0.003355</td>
    </tr>
    <tr>
      <th>prod_agua</th>
      <td>-0.000751</td>
      <td>-0.000967</td>
      <td>0.386070</td>
      <td>0.036217</td>
      <td>1.000000</td>
      <td>0.945769</td>
      <td>-0.000258</td>
      <td>NaN</td>
      <td>-0.004432</td>
      <td>0.730355</td>
      <td>-0.005122</td>
    </tr>
    <tr>
      <th>iny_agua</th>
      <td>-0.000787</td>
      <td>-0.001147</td>
      <td>0.342225</td>
      <td>0.009652</td>
      <td>0.945769</td>
      <td>1.000000</td>
      <td>-0.002082</td>
      <td>NaN</td>
      <td>-0.004204</td>
      <td>0.703673</td>
      <td>-0.005007</td>
    </tr>
    <tr>
      <th>iny_gas</th>
      <td>-0.011133</td>
      <td>-0.008994</td>
      <td>0.030938</td>
      <td>0.114844</td>
      <td>-0.000258</td>
      <td>-0.002082</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>-0.000342</td>
      <td>0.024033</td>
      <td>-0.000517</td>
    </tr>
    <tr>
      <th>iny_co2</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>iny_ptros</th>
      <td>-0.002698</td>
      <td>-0.003171</td>
      <td>-0.003661</td>
      <td>-0.002578</td>
      <td>-0.004432</td>
      <td>-0.004204</td>
      <td>-0.000342</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>-0.004578</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>tef</th>
      <td>-0.002069</td>
      <td>-0.002388</td>
      <td>0.525194</td>
      <td>0.122306</td>
      <td>0.730355</td>
      <td>0.703673</td>
      <td>0.024033</td>
      <td>NaN</td>
      <td>-0.004578</td>
      <td>1.000000</td>
      <td>-0.004710</td>
    </tr>
    <tr>
      <th>vida_util</th>
      <td>-0.031473</td>
      <td>-0.000474</td>
      <td>-0.004744</td>
      <td>-0.003355</td>
      <td>-0.005122</td>
      <td>-0.005007</td>
      <td>-0.000517</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>-0.004710</td>
      <td>1.000000</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-2c590446-58d0-42b6-a976-2be2b54e829a')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

 
    
  </div>




Esto nos dará una matriz de correlación que muestra la correlación entre todas las variables numéricas en el conjunto de datos.

# Mapa de calor (heatmap)
Podemos visualizar la matriz de correlación utilizando un mapa de calor. seaborn hace que sea fácil crear un mapa de calor utilizando la función `heatmap`:


```python
sns.heatmap(df.corr())
```

    
    






    
![png](output_43_2.png)
    


Esto nos dará un mapa de calor que muestra la correlación entre todas las variables numéricas en el conjunto de datos. Los valores más oscuros indican una correlación más fuerte, mientras que los valores más claros indican una correlación más débil.


## Análisis de correlación
Finalmente, podemos utilizar `corr` de pandas y `heatmap` de seaborn para analizar la correlación entre las variables numéricas en el conjunto de datos:


```python
# Análisis de correlación
corr = df.corr()
sns.heatmap(corr, annot=True, cmap='coolwarm')
```

   



    
![png](output_58_2.png)
    


Se observa una buena correlacion entre la inyección de agua y la producción de agua, probablemente porque parte de lo que se inyecta de agua termina siendo extraida con el tiempo. 
La tasa efectiva (tef) tambien esta muy correlacionada a la producción e inyección de agua, esto puede ser debido a que al inyectar agua, se incrementa la producción de hidrocarburos y por eso, las cantidades medidas producidas se acercan más a las hipoteticamente calculadas (previstas a producir).


## Visualizando y correlación general de los datos
A continuación, aplicamos algunas de las visualizaciones discutidas anteriormente para explorar los datos:


```python
# Visualizando los datos
sns.pairplot(df_neuquina, hue='anio',palette='viridis')
```






    
![png](output_52_1.png)
    


