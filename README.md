# Tarea 1 Análisis y Limpieza de Datos



# Ejercicio I: GitHub: fork, clone, push, pull request, merge, fetch

1. Cada grupo debe designarle un número de identificación único a cada uno de sus integrantes, partiendo desde el 1 hasta el n.
2. El integrante número 1 debe hacer un fork del siguiente [repositorio](https://github.com/vmlandae/tarea1-add). Debe hacerlo desde la misma interfaz de la web de github, ya que ni por GitHub Desktop ni por el terminal puedes hacer directamente un fork. Luego, a través de GitHub Desktop o de la línea de comandos con git, debe clonar el repositorio a su máquina local.

3. Cada integrante, del número 2 hasta el n, debe hacen un **fork al repositorio del integrante 1**, desde la interfaz web. Luego, a través de GitHub Desktop o de la línea de comandos con git, debe clonar el repositorio a su máquina local. y luego en este repositorio, crear un branch que se llame `in_***-t1` donde `n` es su número y `***` es su usuario de github.  

4. Luego, el integrante 1 en el branch `main` debe crear un archivo nuevo (puedes hacerlo en la interfaz web usando `add file` -> `create new file`, o en la carpeta de tu máquina local), que se encuentre en el *root* del repositorio, y que se llame `Integrantes-***.md`,  donde `***` es su usuario de github. El archivo debe tener la siguiente estructura:

#### Integrantes

  * 1. i1 [Nombre Apellido](https://github.com/***) DD/MM
  * 2. i2 [Nombre Apellido](https://github.com/***) DD/MM
  * 3. 
  * ...
  * n. 

donde `DD/MM` es el día y mes de cumpleaños del integrante en formato `04/09` para el 4 de Septiembre y donde el integrante 1 debe ingresar sus datos. Una vez creado el archivo, el integrante 1 debe hacer un *commit* con el título `create Integrantes.md`, y luego debe hacer un `push` a github.

5. Cada integrante debe entrar a su repositorio, en el branch recién creado, y hacer un fetch, para poder ver el nuevo archivo creado por el integrante 1. Luego, debe abrir `Integrantes-***.md`, donde debe ingresar sus datos en la línea del `n.` que le corresponda, sin modificar ninguna otra y guardar los cambios. Una vez guardado, debe hacer un *commit*, con el título `update datos n. ***` a su branch `in_***-t1`, y luego un `push` a su github. Finalmente, cada integrante debe hacer un pull request desde su branch hacia el main del repositorio del integrante 1. 

6. El integrante 1 debe aceptar todos los pull request, cuidando que si hubieran merge conflicts, tiene que revisarlos con algún editor y dejar el archivo en el orden esperado (del 1. al n. según corresponda). Todos los integrantes del grupo tienen que hacer un fetch y quedar con el archivo actualizado. 

# Ejercicio II: Excel y tidy data:

Todos los archivos de datos se encuentran en la carpeta `data/raw`. **NO LOS MODIFIQUE**, solo lealos y guarde nuevos archivos cuando lo crea conveniente en la carpeta `data/interim` o si ya están totalmente procesados, o cuando se le indique, en la carpeta `data/processed`.

0. Cree un notebook de jupyter, guárdelo en la carpeta notebooks con el nombre `2_nb_***.ipynb` donde `***` es el github del integrante 1. Una vez que tenga todo el ejercicio listo, limpie los outputs, reinicie el kernel y corra todo el notebook. Luego, exporta el notebook como html y guárdalo en la carpeta `output`.

1. Cargue el archivo `dolar_2019_sii.csv` a un dataframe que se llame `dolar_2019` usando `pandas`. ¿Que argumento necesita `pd.read_csv()` para leer las columnas correctamente?
2. Explore el archivo `dolar_2020_sii.txt`. ¿Qué estructura tiene, en que se diferencia y en qué es igual al dataframe anterior?  ¿Qué método y argumento hay que usar para leer las columnas correctamente?. Carguelo en un dataframe llamado `dolar_2020_txt`.
3. Explore el archivo `dolar_2020_sii_AA.txt`.  ¿Qué estructura tiene? ¿Será buena idea ocupar expresiones regulares para indicar el separador? (*hint: sí*). Carguelo en un dataframe llamado `dolar_2020_regex` y compárelo con el dataframe `dolar_2020_txt`. ¿Son exactamente iguales en la información que traen?
4. Haga las siguientes operaciones de wrangling y limpieza:
    * Filtre sacando la última fila, arreglando y homogeneizando los encabezados para los tres dataframes 
    * Revise que los nombres de las columnas sean los mismos en cada dataframe.
    * Cree una columna en cada uno de los tres dataframes que se llame `year` y que tenga el año correspondiente, y que su type sea `int64`.
    * Convierta las comas a puntos en cada uno de los tres dataframes.
    * Fuerce que todas las variables sean de tipo `int` o de tipo `float`.
5. Exporte estos tres dataframes en la carpeta `data/interim` de la siguiente forma:
    * `dolar_2019` en formato csv, separado por comas, con nombre `d2019.csv`
    * `dolar_2020_txt` en formato txt, separado por un espacio simple, con nombre `d2020.txt`.
    * `dolar_2020_regex` en formato CSV, separado por ";", de nombre `dolar_2020_excel.csv`  
6. Concatene con `pd.concat` de dos formas:
    * `dolar_2019` y `dolar_2020_txt` solo con el argumento `axis=1` guardandolo en el dataframe `df_concat_1`
    * `dolar_2019` y `dolar_2020_txt` solo con el argumento  `axis=0`  guardandolo en el dataframe `df_concat_0`
¿Qué problema podríamos tener con las columnas en `df_concat_1` y en los índices en `df_concat_0`?

# Ejercicio III: 

0. Crea un nuevo notebook de jupyter, guárdelo en la carpeta notebooks con el nombre `3_nb_***.ipynb` donde `***` es el github del integrante 1. Una vez que tenga todo el ejercicio listo, limpie los outputs, reinicie el kernel y corra todo el notebook. Luego, exporta el notebook como html y guárdalo en la carpeta `output`.
1. En el notebook `3_nb_***.ipynb`, cargue los dos archivos `d2019.csv` y `d2020.txt` en dos dataframes llamados `df2019` y `df2020` respectivamente. Luego, usando el método `melt`, genera un dataframe llamado `df_sii` donde estén incluidos los datos del 2019 y del 2020, que tenga las columnas `year`,`mes`, `dia`, `valor`, y guardalo como csv en la carpeta `data/interim` con el nombre `df_sii.csv`.     
2. Usando el método `groupby` en `df_sii`:
    * Agrupa por `mes`, con el argumento `as_index = True` y usando el método `aggregation` con el método `mean`, imprime el resultado.
    * Agrupa por `[year, mes]`, con el argumento `as_index = False` y usando el método `agg` con el método `mean`, imprime el resultado
    * Compara ambos resultados. ¿Qué cambia al usar `as_index = False`? ¿Al agrupar por `mes`, con respecto a `[year,mes]`?
3. ¿Qué podrías inferir de los *missing values* y los días hábiles? Úsalos para crear una nueva variable llamada `dia_de_la_semana` en `df_sii` con valores "Lunes", "Martes", "Miércoles", "Jueves", "Viernes", "Sábado", "Domingo".
4. Explora el archivo `dolar_observado_bc.xlsx` y su estructura. 
    * Lee cada hoja por separado con `read_excel`, usando los argumentos `skiprows=2, dtype={'Periodo':str }`. 
    * Ocupa el método `str.split` para crear las columnas `dia`,`mes` y `year` en cada dataframe.
    * Crea un dataframe que una todos los dataframes en uno solo con las mismas columnas, y nombralo `df_bc_all`.
    * Crea una carpeta dentro de la carpeta `data/processed` llamada `dolar_bc_year`, agrupa por `year` usando `groupby` y guarda un CSV para cada año desde 1982 hasta 2022, con los nombres `dolar_bc_YYYY.csv` donde `YYYY` es el año. Busca una manera de hacerlo iterando y no uno a uno.
    * Crea un dataframe que tenga los años 2019 y 2020 que se llame `df_bc_2019_2020`
    * Compara los valores de `df_bc_2019_2020` y `df_sii`. ¿Son iguales o diferentes? 
 
5. Haz un `merge` de la columna `dia_de_la_semana` del `df_sii` al dataframe `df_bc_all`. Luego, extiende la variable `dia_de_la_semana` para todos los valores. Finalmente, crea una variable con las combinaciones `[dia,mes]` que tienen al menos un `NaN` que sea en día de semana (es decir, excluyendo Sábado y Domingo). Luego, cuenta cuantos `NaN`(incluyendo Sábados y Domingos) hay para cada combinación`[dia/mes]`. ¿Qué puedes inferir de los días con mayor cantidad de `NaN`?  
6. Calcula el promedio del precio del dolar en los días de cumpleaños del grupo para cada año entre 1983 y 2021 y el promedio del precio del dolar para cada año completo entre 1983 y 2021, y muestra una tabla donde se vean ambos resultados. ¿Qué diferencias hay en ambos indicadores en cada año?

