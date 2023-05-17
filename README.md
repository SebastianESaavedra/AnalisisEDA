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

    Drive already mounted at /content/drive; to attempt to forcibly remount, call drive.mount("/content/drive", force_remount=True).
    


```python
df_original = pd.read_csv('/content/drive/My Drive/Colab Notebooks/prod.csv')
```

    <ipython-input-7-9c27b77d4dfd>:1: DtypeWarning: Columns (0,21) have mixed types. Specify dtype option on import or set low_memory=False.
      df_original = pd.read_csv('/content/drive/My Drive/Colab Notebooks/prod.csv')
    


```python
df= df_original[df_original.anio.isin([2022,2020])]
df= df[df.cuenca.isin(['NEUQUINA','CUYANA','GOLFO SAN JORGE'])]
df_neuquina= df[df.cuenca.isin(['NEUQUINA'])]
df_cuyana= df[df.cuenca.isin(['CUYANA'])]
df_sanjorge= df[df.cuenca.isin(['GOLFO SAN JORGE'])]
df
```





  <div id="df-d97fb7b3-fd89-4870-b172-206bcb4ccca6">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idempresa</th>
      <th>anio</th>
      <th>mes</th>
      <th>prod_pet</th>
      <th>prod_gas</th>
      <th>prod_agua</th>
      <th>iny_agua</th>
      <th>iny_gas</th>
      <th>iny_co2</th>
      <th>iny_ptros</th>
      <th>...</th>
      <th>idareapermisoconcesion</th>
      <th>areapermisoconcesion</th>
      <th>idareayacimiento</th>
      <th>areayacimiento</th>
      <th>tipo_de_recurso</th>
      <th>proyecto</th>
      <th>sub_tipo_recurso</th>
      <th>cuenca</th>
      <th>provincia</th>
      <th>fecha_data</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1411</th>
      <td>Z001</td>
      <td>2020</td>
      <td>1</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>ABO</td>
      <td>BLANCO DE LOS OLIVOS - BLOQUE "A"</td>
      <td>ABO</td>
      <td>BLANCO DE LOS OLIVOS-BLOQUE "A"</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>NEUQUINA</td>
      <td>Rio Negro</td>
      <td>2020-01-31</td>
    </tr>
    <tr>
      <th>1412</th>
      <td>Z001</td>
      <td>2020</td>
      <td>1</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>ABO</td>
      <td>BLANCO DE LOS OLIVOS - BLOQUE "A"</td>
      <td>ABO</td>
      <td>BLANCO DE LOS OLIVOS-BLOQUE "A"</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>NEUQUINA</td>
      <td>Rio Negro</td>
      <td>2020-01-31</td>
    </tr>
    <tr>
      <th>1413</th>
      <td>Z001</td>
      <td>2020</td>
      <td>1</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>AGR</td>
      <td>GENERAL ROCA</td>
      <td>AGR</td>
      <td>GENERAL ROCA</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>NEUQUINA</td>
      <td>Rio Negro</td>
      <td>2020-01-31</td>
    </tr>
    <tr>
      <th>1414</th>
      <td>Z001</td>
      <td>2020</td>
      <td>1</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>BLLO</td>
      <td>PUESTO SURVELIN</td>
      <td>PUSU</td>
      <td>PUESTO SURVELIN</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>NEUQUINA</td>
      <td>Rio Negro</td>
      <td>2020-01-31</td>
    </tr>
    <tr>
      <th>1415</th>
      <td>Z001</td>
      <td>2020</td>
      <td>1</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>Z042</td>
      <td>DON JOSE</td>
      <td>Z122</td>
      <td>DON JOSE</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>NEUQUINA</td>
      <td>Rio Negro</td>
      <td>2020-01-31</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>556091</th>
      <td>ACO</td>
      <td>2022</td>
      <td>12</td>
      <td>2264.02</td>
      <td>90.54</td>
      <td>8569.47</td>
      <td>17786.8</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>CHA</td>
      <td>CHAÑARES HERRADOS</td>
      <td>CHA</td>
      <td>CHAÑARES HERRADOS</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2022-12-31</td>
    </tr>
    <tr>
      <th>556092</th>
      <td>ACO</td>
      <td>2022</td>
      <td>12</td>
      <td>473.75</td>
      <td>28.41</td>
      <td>628.99</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>PPCR</td>
      <td>PUESTO POZO CERCADO ORIENTAL</td>
      <td>PCE</td>
      <td>PUESTO POZO CERCADO</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2022-12-31</td>
    </tr>
    <tr>
      <th>556093</th>
      <td>ACO</td>
      <td>2022</td>
      <td>12</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>LGU</td>
      <td>LOMA GUADALOSA</td>
      <td>LGU</td>
      <td>LOMA GUADALOSA</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>NEUQUINA</td>
      <td>Rio Negro</td>
      <td>2022-12-31</td>
    </tr>
    <tr>
      <th>556094</th>
      <td>ACO</td>
      <td>2022</td>
      <td>12</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>PPCR</td>
      <td>PUESTO POZO CERCADO ORIENTAL</td>
      <td>PCE</td>
      <td>PUESTO POZO CERCADO</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2022-12-31</td>
    </tr>
    <tr>
      <th>556095</th>
      <td>ACO</td>
      <td>2022</td>
      <td>12</td>
      <td>493.97</td>
      <td>29.63</td>
      <td>802.92</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>PPCR</td>
      <td>PUESTO POZO CERCADO ORIENTAL</td>
      <td>PCE</td>
      <td>PUESTO POZO CERCADO</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2022-12-31</td>
    </tr>
  </tbody>
</table>
<p>60447 rows × 25 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-d97fb7b3-fd89-4870-b172-206bcb4ccca6')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-d97fb7b3-fd89-4870-b172-206bcb4ccca6 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-d97fb7b3-fd89-4870-b172-206bcb4ccca6');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




# Exploración general del conjunto de datos
El primer paso en el EDA es familiarizarse con el conjunto de datos. Para hacerlo, podemos utilizar algunas funciones simples de pandas:



# Shape y Types
Utilizar el método `shape` nos dá un preview del tamaño del dataset mientras que el método `dtypes` nos permite entender con que tipo de datos estámos lidiando:


```python
df.shape
```




    (24729, 25)




```python
df.dtypes
```




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



## Head y Tail
Podemos utilizar las funciones `head` y `tail` de pandas para ver las primeras y últimas filas del conjunto de datos, respectivamente:


```python
df.head()
```





  <div id="df-6cf64fa6-4a6e-4cd9-ade7-93ebad9079cf">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idempresa</th>
      <th>anio</th>
      <th>mes</th>
      <th>prod_pet</th>
      <th>prod_gas</th>
      <th>prod_agua</th>
      <th>iny_agua</th>
      <th>iny_gas</th>
      <th>iny_co2</th>
      <th>iny_ptros</th>
      <th>...</th>
      <th>idareapermisoconcesion</th>
      <th>areapermisoconcesion</th>
      <th>idareayacimiento</th>
      <th>areayacimiento</th>
      <th>tipo_de_recurso</th>
      <th>proyecto</th>
      <th>sub_tipo_recurso</th>
      <th>cuenca</th>
      <th>provincia</th>
      <th>fecha_data</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>135797</th>
      <td>YPF</td>
      <td>2020</td>
      <td>1</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>3399.8</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>BAR</td>
      <td>BARRANCAS</td>
      <td>BRC</td>
      <td>BARRANCAS</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2020-01-31</td>
    </tr>
    <tr>
      <th>135798</th>
      <td>YPF</td>
      <td>2020</td>
      <td>1</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>BAR</td>
      <td>BARRANCAS</td>
      <td>ECP</td>
      <td>ESTRUCTURA CRUZ DE PIEDRA</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2020-01-31</td>
    </tr>
    <tr>
      <th>135799</th>
      <td>YPF</td>
      <td>2020</td>
      <td>1</td>
      <td>1646.94</td>
      <td>46.87</td>
      <td>1508.72</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>BAR</td>
      <td>BARRANCAS</td>
      <td>UGA</td>
      <td>UGARTECHE</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2020-01-31</td>
    </tr>
    <tr>
      <th>135800</th>
      <td>YPF</td>
      <td>2020</td>
      <td>1</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>CEF</td>
      <td>CEFERINO</td>
      <td>Z306</td>
      <td>PUESTO PRIETO</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2020-01-31</td>
    </tr>
    <tr>
      <th>135801</th>
      <td>YPF</td>
      <td>2020</td>
      <td>1</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>LAV</td>
      <td>LA VENTANA</td>
      <td>ATA</td>
      <td>ATAMISQUI</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2020-01-31</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 25 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-6cf64fa6-4a6e-4cd9-ade7-93ebad9079cf')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-6cf64fa6-4a6e-4cd9-ade7-93ebad9079cf button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-6cf64fa6-4a6e-4cd9-ade7-93ebad9079cf');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
df.tail()
```





  <div id="df-14b4c68e-7bcf-4c27-8cf4-f379761bde80">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idempresa</th>
      <th>anio</th>
      <th>mes</th>
      <th>prod_pet</th>
      <th>prod_gas</th>
      <th>prod_agua</th>
      <th>iny_agua</th>
      <th>iny_gas</th>
      <th>iny_co2</th>
      <th>iny_ptros</th>
      <th>...</th>
      <th>idareapermisoconcesion</th>
      <th>areapermisoconcesion</th>
      <th>idareayacimiento</th>
      <th>areayacimiento</th>
      <th>tipo_de_recurso</th>
      <th>proyecto</th>
      <th>sub_tipo_recurso</th>
      <th>cuenca</th>
      <th>provincia</th>
      <th>fecha_data</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>556090</th>
      <td>ACO</td>
      <td>2022</td>
      <td>12</td>
      <td>334.68</td>
      <td>13.39</td>
      <td>792.94</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>CHA</td>
      <td>CHAÑARES HERRADOS</td>
      <td>CHA</td>
      <td>CHAÑARES HERRADOS</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2022-12-31</td>
    </tr>
    <tr>
      <th>556091</th>
      <td>ACO</td>
      <td>2022</td>
      <td>12</td>
      <td>2264.02</td>
      <td>90.54</td>
      <td>8569.47</td>
      <td>17786.8</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>CHA</td>
      <td>CHAÑARES HERRADOS</td>
      <td>CHA</td>
      <td>CHAÑARES HERRADOS</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2022-12-31</td>
    </tr>
    <tr>
      <th>556092</th>
      <td>ACO</td>
      <td>2022</td>
      <td>12</td>
      <td>473.75</td>
      <td>28.41</td>
      <td>628.99</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>PPCR</td>
      <td>PUESTO POZO CERCADO ORIENTAL</td>
      <td>PCE</td>
      <td>PUESTO POZO CERCADO</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2022-12-31</td>
    </tr>
    <tr>
      <th>556094</th>
      <td>ACO</td>
      <td>2022</td>
      <td>12</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.00</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>PPCR</td>
      <td>PUESTO POZO CERCADO ORIENTAL</td>
      <td>PCE</td>
      <td>PUESTO POZO CERCADO</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2022-12-31</td>
    </tr>
    <tr>
      <th>556095</th>
      <td>ACO</td>
      <td>2022</td>
      <td>12</td>
      <td>493.97</td>
      <td>29.63</td>
      <td>802.92</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>...</td>
      <td>PPCR</td>
      <td>PUESTO POZO CERCADO ORIENTAL</td>
      <td>PCE</td>
      <td>PUESTO POZO CERCADO</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>NaN</td>
      <td>CUYANA</td>
      <td>Mendoza</td>
      <td>2022-12-31</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 25 columns</p>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-14b4c68e-7bcf-4c27-8cf4-f379761bde80')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-14b4c68e-7bcf-4c27-8cf4-f379761bde80 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-14b4c68e-7bcf-4c27-8cf4-f379761bde80');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




Esto nos dará una idea de cómo se ven los datos y qué tipo de información contienen.


## Descripción general del conjunto de datos
Podemos obtener una descripción general del conjunto de datos utilizando la función `describe` de pandas:


```python
df.describe()
```





  <div id="df-26384bd2-769e-4c2a-a608-feb98238b62c">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
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
      <th>count</th>
      <td>24729.000000</td>
      <td>24729.000000</td>
      <td>24729.000000</td>
      <td>24729.000000</td>
      <td>2.472900e+04</td>
      <td>2.472900e+04</td>
      <td>24729.000000</td>
      <td>24729.0</td>
      <td>24729.0</td>
      <td>24729.000000</td>
      <td>2657.0</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2021.010312</td>
      <td>6.506450</td>
      <td>1137.667719</td>
      <td>1204.421572</td>
      <td>1.964759e+04</td>
      <td>1.944776e+04</td>
      <td>0.183789</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>490.423870</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>std</th>
      <td>0.999967</td>
      <td>3.451677</td>
      <td>5013.688060</td>
      <td>9261.733895</td>
      <td>8.704532e+04</td>
      <td>9.192685e+04</td>
      <td>20.517356</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2299.239069</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>min</th>
      <td>2020.000000</td>
      <td>1.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2020.000000</td>
      <td>4.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2022.000000</td>
      <td>7.000000</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.000000e+00</td>
      <td>0.000000e+00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.000000</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2022.000000</td>
      <td>10.000000</td>
      <td>260.520000</td>
      <td>56.000000</td>
      <td>2.079710e+03</td>
      <td>0.000000e+00</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>119.791670</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2022.000000</td>
      <td>12.000000</td>
      <td>130070.960000</td>
      <td>181831.920000</td>
      <td>1.058743e+06</td>
      <td>1.364515e+06</td>
      <td>2475.180000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>47752.100000</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-26384bd2-769e-4c2a-a608-feb98238b62c')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-26384bd2-769e-4c2a-a608-feb98238b62c button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-26384bd2-769e-4c2a-a608-feb98238b62c');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
df.describe().T
```





  <div id="df-a780cc1e-afdb-468f-bf62-974d51114b03">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>count</th>
      <th>mean</th>
      <th>std</th>
      <th>min</th>
      <th>25%</th>
      <th>50%</th>
      <th>75%</th>
      <th>max</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>anio</th>
      <td>24729.0</td>
      <td>2021.010312</td>
      <td>0.999967</td>
      <td>2020.0</td>
      <td>2020.0</td>
      <td>2022.0</td>
      <td>2022.00000</td>
      <td>2.022000e+03</td>
    </tr>
    <tr>
      <th>mes</th>
      <td>24729.0</td>
      <td>6.506450</td>
      <td>3.451677</td>
      <td>1.0</td>
      <td>4.0</td>
      <td>7.0</td>
      <td>10.00000</td>
      <td>1.200000e+01</td>
    </tr>
    <tr>
      <th>prod_pet</th>
      <td>24729.0</td>
      <td>1137.667719</td>
      <td>5013.688060</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>260.52000</td>
      <td>1.300710e+05</td>
    </tr>
    <tr>
      <th>prod_gas</th>
      <td>24729.0</td>
      <td>1204.421572</td>
      <td>9261.733895</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>56.00000</td>
      <td>1.818319e+05</td>
    </tr>
    <tr>
      <th>prod_agua</th>
      <td>24729.0</td>
      <td>19647.594275</td>
      <td>87045.322902</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>2079.71000</td>
      <td>1.058743e+06</td>
    </tr>
    <tr>
      <th>iny_agua</th>
      <td>24729.0</td>
      <td>19447.760932</td>
      <td>91926.852001</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00000</td>
      <td>1.364515e+06</td>
    </tr>
    <tr>
      <th>iny_gas</th>
      <td>24729.0</td>
      <td>0.183789</td>
      <td>20.517356</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00000</td>
      <td>2.475180e+03</td>
    </tr>
    <tr>
      <th>iny_co2</th>
      <td>24729.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00000</td>
      <td>0.000000e+00</td>
    </tr>
    <tr>
      <th>iny_ptros</th>
      <td>24729.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00000</td>
      <td>0.000000e+00</td>
    </tr>
    <tr>
      <th>tef</th>
      <td>24729.0</td>
      <td>490.423870</td>
      <td>2299.239069</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>119.79167</td>
      <td>4.775210e+04</td>
    </tr>
    <tr>
      <th>vida_util</th>
      <td>2657.0</td>
      <td>0.000000</td>
      <td>0.000000</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>0.00000</td>
      <td>0.000000e+00</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-a780cc1e-afdb-468f-bf62-974d51114b03')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-a780cc1e-afdb-468f-bf62-974d51114b03 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-a780cc1e-afdb-468f-bf62-974d51114b03');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>





```python
df.describe(include=['object'])
```





  <div id="df-ffc73c8c-59c3-4f2a-90bc-5fcf2af0c851">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>idempresa</th>
      <th>empresa</th>
      <th>formprod</th>
      <th>formacion</th>
      <th>idareapermisoconcesion</th>
      <th>areapermisoconcesion</th>
      <th>idareayacimiento</th>
      <th>areayacimiento</th>
      <th>tipo_de_recurso</th>
      <th>proyecto</th>
      <th>sub_tipo_recurso</th>
      <th>cuenca</th>
      <th>provincia</th>
      <th>fecha_data</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>24729</td>
      <td>24729</td>
      <td>24537</td>
      <td>24273</td>
      <td>24681</td>
      <td>24681</td>
      <td>24729</td>
      <td>24729</td>
      <td>24729</td>
      <td>24729</td>
      <td>255</td>
      <td>24729</td>
      <td>24729</td>
      <td>24729</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>28</td>
      <td>28</td>
      <td>37</td>
      <td>36</td>
      <td>144</td>
      <td>144</td>
      <td>479</td>
      <td>426</td>
      <td>3</td>
      <td>2</td>
      <td>2</td>
      <td>3</td>
      <td>5</td>
      <td>24</td>
    </tr>
    <tr>
      <th>top</th>
      <td>CGC</td>
      <td>COMPAÑÍA GENERAL DE COMBUSTIBLES S.A.</td>
      <td>SPRI</td>
      <td>springhill</td>
      <td>ANG</td>
      <td>ANTICLINAL GRANDE - CERRO DRAGON</td>
      <td>DIA</td>
      <td>POZOS SIN YACIMIENTO</td>
      <td>CONVENCIONAL</td>
      <td>Sin Proyecto</td>
      <td>TIGHT</td>
      <td>GOLFO SAN JORGE</td>
      <td>Santa Cruz</td>
      <td>2022-04-30</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>5504</td>
      <td>5504</td>
      <td>5632</td>
      <td>5632</td>
      <td>3783</td>
      <td>3783</td>
      <td>384</td>
      <td>684</td>
      <td>24082</td>
      <td>24225</td>
      <td>205</td>
      <td>11722</td>
      <td>11096</td>
      <td>1044</td>
    </tr>
  </tbody>
</table>
</div>
      <button class="colab-df-convert" onclick="convertToInteractive('df-ffc73c8c-59c3-4f2a-90bc-5fcf2af0c851')"
              title="Convert this dataframe to an interactive table."
              style="display:none;">

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-ffc73c8c-59c3-4f2a-90bc-5fcf2af0c851 button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-ffc73c8c-59c3-4f2a-90bc-5fcf2af0c851');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




Esto nos dará algunas estadísticas básicas sobre las variables numéricas en el conjunto de datos, como el número de observaciones, la media, la desviación estándar, los valores mínimo y máximo y los percentiles.


## Información de las columnas
Podemos obtener información sobre las columnas en el conjunto de datos utilizando la función `info` de pandas:


```python
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 24729 entries, 135797 to 556095
    Data columns (total 25 columns):
     #   Column                  Non-Null Count  Dtype  
    ---  ------                  --------------  -----  
     0   idempresa               24729 non-null  object 
     1   anio                    24729 non-null  int64  
     2   mes                     24729 non-null  int64  
     3   prod_pet                24729 non-null  float64
     4   prod_gas                24729 non-null  float64
     5   prod_agua               24729 non-null  float64
     6   iny_agua                24729 non-null  float64
     7   iny_gas                 24729 non-null  float64
     8   iny_co2                 24729 non-null  float64
     9   iny_ptros               24729 non-null  float64
     10  tef                     24729 non-null  float64
     11  vida_util               2657 non-null   float64
     12  empresa                 24729 non-null  object 
     13  formprod                24537 non-null  object 
     14  formacion               24273 non-null  object 
     15  idareapermisoconcesion  24681 non-null  object 
     16  areapermisoconcesion    24681 non-null  object 
     17  idareayacimiento        24729 non-null  object 
     18  areayacimiento          24729 non-null  object 
     19  tipo_de_recurso         24729 non-null  object 
     20  proyecto                24729 non-null  object 
     21  sub_tipo_recurso        255 non-null    object 
     22  cuenca                  24729 non-null  object 
     23  provincia               24729 non-null  object 
     24  fecha_data              24729 non-null  object 
    dtypes: float64(9), int64(2), object(14)
    memory usage: 4.9+ MB
    

Esto nos dará información sobre el número de valores no nulos en cada columna y el tipo de datos de cada columna.


```python
df.isnull().sum()
```




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
    vida_util                 22072
    empresa                       0
    formprod                    192
    formacion                   456
    idareapermisoconcesion       48
    areapermisoconcesion         48
    idareayacimiento              0
    areayacimiento                0
    tipo_de_recurso               0
    proyecto                      0
    sub_tipo_recurso          24474
    cuenca                        0
    provincia                     0
    fecha_data                    0
    dtype: int64



Se observa que las columnas emporesa, formprod, formacion, idareapermisoconcesion,  areapermisoconcesion y sub_tipo_recurso presentan nulos.






# Visualización de datos
La visualización de datos es una parte importante del EDA, ya que nos permite ver patrones y relaciones que podrían no ser evidentes en una tabla de datos. seaborn ofrece una amplia gama de herramientas para la visualización de datos.

## Diagrama de dispersión (scatter plot)
Una forma común de visualizar la relación entre dos variables numéricas es mediante un diagrama de dispersión. seaborn hace que sea fácil crear un diagrama de dispersión utilizando la función scatterplot:


```python
import matplotlib.pyplot as plt
sns.scatterplot(x="iny_agua", y="prod_pet", data=df, hue='cuenca',style='tipo_de_recurso')
plt.legend(bbox_to_anchor=(1, 1), loc=2, borderaxespad=0)

```




    <matplotlib.legend.Legend at 0x7ff74bdde710>




    
![png](README_files/README_26_1.png)
    


A partir de este gráfico podemos ver que hay una diferencia entre los reservorios convencionales de los no convencionales (NC). Estos ultimos se distinguen de los convencionales principalmente porque para que se produzcan hidrocarburos no es necesaria la inyección de agua, si no que resultan otros los metodos para su extracción.
Los reservorios convencionales en cambio, muestran una correlación lineal entre la inyeccion de agua y la producción de petroleo. Esto es debido a que mientras se va extrayendo el hidrocarburo, la presión de extracción es cada vez menor. Pero existe justamente este metodo de recuperación mediante la inyección de agua en el reservorio, para que "empuje" en petroleo y facilite su extracción.
Respecto a las tres cuencas visibles, se ve que la unica que posee reservorios NC es la Neuquina. El comportamiento de los registros de San Jorge son similares a los de la Neuquina, pero la cuenca Cuyana necesita mayores niveles de agua para poder extraer sus recursos.


```python
import matplotlib.pyplot as plt
sns.scatterplot(x="iny_agua", y="prod_pet", data=df_neuquina, hue='formacion', style='tipo_de_recurso')
plt.legend(bbox_to_anchor=(1, 1), loc=2, borderaxespad=0)

```




    <matplotlib.legend.Legend at 0x7ff750d40160>




    
![png](README_files/README_28_1.png)
    


Pareceria que la unica formacion no convencional que se tiene registro en el dataset es Vaca Muerta. Las demas formaciones convencionales suelen seguir el patron lineal.


```python
import matplotlib.pyplot as plt
sns.scatterplot(x="prod_gas", y="prod_pet", data=df_neuquina, hue='formacion', style='tipo_de_recurso')
plt.legend(bbox_to_anchor=(1, 1), loc=2, borderaxespad=0)
```




    <matplotlib.legend.Legend at 0x7ff74acb2a70>




    
![png](README_files/README_30_1.png)
    


Aqui podemos observar que la producción de petroleo esta en ocaciones vinculada a la producción de gas. Los mayores productores de gas son los NC. Se pueden distinguir por lo menos dos tendencias lineales. 

# Diagrama de barras (bar plot)
Otra forma común de visualizar los datos es mediante un diagrama de barras, que se utiliza para mostrar la distribución de una variable categórica. seaborn hace que sea fácil crear un diagrama de barras utilizando la función `countplot`:


```python
##sns.countplot(x="tipo_de_recurso", data=df)
ax=sns.countplot(x="tipo_de_recurso", data=df)
ax.set_xticklabels(ax.get_xticklabels(),rotation=40)
plt.show()
```


    
![png](README_files/README_33_0.png)
    


Esto nos dará un diagrama de barras de la distribución de la variable "tipo_de_recurso" en el conjunto de datos. Podemos ver que el número de observaciones es mayor del tipo Convencional.

# Histograma (histogram)
Un histograma es una forma común de visualizar la distribución de una variable numérica. seaborn hace que sea fácil crear un histograma utilizando la función `histplot`:


```python
sns.histplot(x="iny_agua", bins =5, data=df)
```




    <Axes: xlabel='iny_agua', ylabel='Count'>




    
![png](README_files/README_36_1.png)
    


La distribución de inyección de agua está mayoritariamente entre 0 y 0.25 aproximadamente.

# Análisis de correlación
El análisis de correlación es una parte importante del EDA, ya que nos permite ver la relación entre las variables numéricas en el conjunto de datos. Una forma común de analizar la correlación es mediante el cálculo de la matriz de correlación y la visualización de la misma mediante un mapa de calor.

## Matriz de correlación (correlation matrix)
Podemos calcular la matriz de correlación utilizando la función `corr` de pandas:


```python
df.corr()
```

    <ipython-input-79-2f6f6606aa2c>:1: FutureWarning: The default value of numeric_only in DataFrame.corr is deprecated. In a future version, it will default to False. Select only valid columns or specify the value of numeric_only to silence this warning.
      df.corr()
    





  <div id="df-2c590446-58d0-42b6-a976-2be2b54e829a">
    <div class="colab-df-container">
      <div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
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

  <svg xmlns="http://www.w3.org/2000/svg" height="24px"viewBox="0 0 24 24"
       width="24px">
    <path d="M0 0h24v24H0V0z" fill="none"/>
    <path d="M18.56 5.44l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94zm-11 1L8.5 8.5l.94-2.06 2.06-.94-2.06-.94L8.5 2.5l-.94 2.06-2.06.94zm10 10l.94 2.06.94-2.06 2.06-.94-2.06-.94-.94-2.06-.94 2.06-2.06.94z"/><path d="M17.41 7.96l-1.37-1.37c-.4-.4-.92-.59-1.43-.59-.52 0-1.04.2-1.43.59L10.3 9.45l-7.72 7.72c-.78.78-.78 2.05 0 2.83L4 21.41c.39.39.9.59 1.41.59.51 0 1.02-.2 1.41-.59l7.78-7.78 2.81-2.81c.8-.78.8-2.07 0-2.86zM5.41 20L4 18.59l7.72-7.72 1.47 1.35L5.41 20z"/>
  </svg>
      </button>

  <style>
    .colab-df-container {
      display:flex;
      flex-wrap:wrap;
      gap: 12px;
    }

    .colab-df-convert {
      background-color: #E8F0FE;
      border: none;
      border-radius: 50%;
      cursor: pointer;
      display: none;
      fill: #1967D2;
      height: 32px;
      padding: 0 0 0 0;
      width: 32px;
    }

    .colab-df-convert:hover {
      background-color: #E2EBFA;
      box-shadow: 0px 1px 2px rgba(60, 64, 67, 0.3), 0px 1px 3px 1px rgba(60, 64, 67, 0.15);
      fill: #174EA6;
    }

    [theme=dark] .colab-df-convert {
      background-color: #3B4455;
      fill: #D2E3FC;
    }

    [theme=dark] .colab-df-convert:hover {
      background-color: #434B5C;
      box-shadow: 0px 1px 3px 1px rgba(0, 0, 0, 0.15);
      filter: drop-shadow(0px 1px 2px rgba(0, 0, 0, 0.3));
      fill: #FFFFFF;
    }
  </style>

      <script>
        const buttonEl =
          document.querySelector('#df-2c590446-58d0-42b6-a976-2be2b54e829a button.colab-df-convert');
        buttonEl.style.display =
          google.colab.kernel.accessAllowed ? 'block' : 'none';

        async function convertToInteractive(key) {
          const element = document.querySelector('#df-2c590446-58d0-42b6-a976-2be2b54e829a');
          const dataTable =
            await google.colab.kernel.invokeFunction('convertToInteractive',
                                                     [key], {});
          if (!dataTable) return;

          const docLinkHtml = 'Like what you see? Visit the ' +
            '<a target="_blank" href=https://colab.research.google.com/notebooks/data_table.ipynb>data table notebook</a>'
            + ' to learn more about interactive tables.';
          element.innerHTML = '';
          dataTable['output_type'] = 'display_data';
          await google.colab.output.renderOutput(dataTable, element);
          const docLink = document.createElement('div');
          docLink.innerHTML = docLinkHtml;
          element.appendChild(docLink);
        }
      </script>
    </div>
  </div>




Esto nos dará una matriz de correlación que muestra la correlación entre todas las variables numéricas en el conjunto de datos.

# Mapa de calor (heatmap)
Podemos visualizar la matriz de correlación utilizando un mapa de calor. seaborn hace que sea fácil crear un mapa de calor utilizando la función `heatmap`:


```python
sns.heatmap(df.corr())
```

    <ipython-input-68-aa4f4450a243>:1: FutureWarning: The default value of numeric_only in DataFrame.corr is deprecated. In a future version, it will default to False. Select only valid columns or specify the value of numeric_only to silence this warning.
      sns.heatmap(df.corr())
    




    <Axes: >




    
![png](README_files/README_43_2.png)
    


Esto nos dará un mapa de calor que muestra la correlación entre todas las variables numéricas en el conjunto de datos. Los valores más oscuros indican una correlación más fuerte, mientras que los valores más claros indican una correlación más débil.

# Ejemplo de Análisis Exploratorio de Datos
A continuación, utilizaremos el conjunto de datos iris incluido en scikit-learn para realizar un ejemplo de Análisis Exploratorio de Datos.

## Importando librerías y cargando el conjunto de datos
Comenzamos importando las librerías necesarias y cargando el conjunto de datos:


```python

```

En este ejemplo, utilizamos `load_iris` de scikit-learn para cargar el conjunto de datos `iris`. Luego, creamos un objeto `DataFrame` de pandas con los datos y agregamos una columna para el objetivo (target) del conjunto de datos.

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
    

Esto nos dará una idea general del conjunto de datos. Podemos ver que el conjunto de datos tiene 150 observaciones y 5 variables. No hay valores nulos en el conjunto de datos.

## Visualizando los datos
A continuación, podemos utilizar algunas de las visualizaciones discutidas anteriormente para explorar los datos:


```python
# Visualizando los datos
sns.pairplot(df_neuquina, hue='anio',palette='viridis')
```




    <seaborn.axisgrid.PairGrid at 0x7ff7490ff490>




    
![png](README_files/README_52_1.png)
    



```python
a1=sns.displot(df, x='provincia',kde=True)
labels = a1.ax.get_xticklabels()
a1.set_xticklabels(labels,rotation=45)
plt.show()
```


    
![png](README_files/README_53_0.png)
    


La provincia dentro de las tres cuencas en tener más registros es Neuquén.


```python
order = df_neuquina['formacion'].sort_values().unique()
ax=sns.countplot(x='formacion', data=df_neuquina, palette='viridis', order=order)
ax.set_xticklabels(ax.get_xticklabels(),rotation=90)
plt.show()
```


    
![png](README_files/README_55_0.png)
    


El mayor conteo de registros es cuando una formación no es productiva (no se extrajo petroleo). Entre las formaciones más destacadas se encuentran: Vaca Muerta, Agrio, Quintuco, Centenario, teniendo en cuenta solo a datos de la cuenca neuquina.

## Análisis de correlación
Finalmente, podemos utilizar `corr` de pandas y `heatmap` de seaborn para analizar la correlación entre las variables numéricas en el conjunto de datos:


```python
# Análisis de correlación
corr = df.corr()
sns.heatmap(corr, annot=True, cmap='coolwarm')
```

    <ipython-input-78-d9e97c3d970a>:2: FutureWarning: The default value of numeric_only in DataFrame.corr is deprecated. In a future version, it will default to False. Select only valid columns or specify the value of numeric_only to silence this warning.
      corr = df.corr()
    




    <Axes: >




    
![png](README_files/README_58_2.png)
    


Se observa una buena correlacion entre la inyección de agua y la producción de agua, probablemente porque parte de lo que se inyecta de agua termina siendo extraida con el tiempo. 
La tasa efectiva (tef) tambien esta muy correlacionada a la producción e inyección de agua, esto puede ser debido a que al inyectar agua, se incrementa la producción de hidrocarburos y por eso, las cantidades medidas producidas se acercan más a las hipoteticamente calculadas (previstas a producir).
