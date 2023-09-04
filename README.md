![Logo](https://github.com/juanrave/Sistema-de-recomendacion-clientes-con-potencial-comercial/blob/main/doc/images/logo.png)
# Sistema-de-recomendacion-clientes-con-potencial-comercial
Sistema de Recomendación de Noticias sobre Clientes con Potencial Comercial

## Resumen
El Grupo Bancolombia busca desarrollar una herramienta analítica que utilice técnicas de Procesamiento del Lenguaje Natural (NLP) y Aprendizaje No Supervisado para ayudar a su fuerza comercial a comprender mejor a sus clientes a través de noticias relevantes. El objetivo es segmentar las noticias relacionadas con los clientes y determinar las características comunes entre ellas. Esto permitirá identificar noticias importantes para sectores específicos de clientes, lo que ayudará a la fuerza comercial a estar informada y ser más efectiva en su trabajo. 
La solución propuesta implica la extracción de información clave de los textos de las noticias y su representación matemática mediante técnicas de NLP. Estas representaciones se utilizan para agrupar las noticias que comparten características similares, lo que facilita la recomendación de noticias relevantes para sectores específicos. En resumen, el proyecto busca abordar el problema de la segmentación de noticias comerciales mediante técnicas de NLP y Aprendizaje No Supervisado para mejorar la comprensión de los clientes y la toma de decisiones comerciales.

## Introducción
Para el grupo Bancolombia es es necesario desarrollar una herramienta analitica que permita a su fuerza comercial conocer e informarse sobre sus clientes haciendo uso de noticias, para esto se presenta un problema el cual desde nuestro equipo planteamos solucionar mediante la aplicación de técnicas de NLP y Aprendizaje No Supervisado, que permitan segmentar el contenido de las noticias relacionadas con sus clientes y determinar qué características tienen en común. 
Es de interés poder determinar las noticias relevantes para un sector particular de clientes, que permitan a la fuerza comercial informarse mediante noticias si están atendiendo ese determinado sector y ser más efectivos en su labor. Para afrontar este problema, se plantea extraer información característica de los textos de las noticias que permitan su representación matemática, con técnicas de NLP, esto convertir cada texto de las noticias en una representación matricial con cierta dimensionalidad que depende de la técnica usada. Cuando se tiene esta representación se busca segmentar o agrupar las noticias  que tengan características similares y formen grupos representativos de sus características principales, que permiten determinar a qué grupo pertenece una noticia nueva que puede ser de interés de la fuerza comercial. 
Entonces, en este trabajo se propone una solución analitica al problema de segmentación de noticias con potencial comercial mediante técnicas de NLP y Aprendizaje No Supervisado para determinar las características que comparten por sector de interés y que permiten agrupar y recomendar una noticia para un sector específico.

## Descripción detallada de los datos
Los datos se encuentran conformados por tres bases de datos, contienen información sobre clientes, noticias y la relación entre ellos. Estas tres bases de datos están conectadas entre sí a través de relaciones entre las claves primarias y foráneas.

### Base de datos de clientes (clientes.csv)

La base de clientes contiene información sobre 1507 clientes, su actividad económica y el subsector al que pertenece, según ciiu  agrupado por división, grupo, clase y subsector.  Cada registro en esta base representa a un cliente único, identificado por su nit. No hay datos nulos ni duplicados. La mayoría de las variables son de tipo objeto, excepto el nit que es de tipo entero. 

Esta base se conecta con las otras dos bases a través de las columnas nit y new_id, que son claves foráneas que hacen referencia a las claves primarias de las bases de clientes y noticias, respectivamente.

Las columnas de la base de datos de clientes son:

nit: Identificador único del cliente.

nombre: Nombre corporativo del cliente.

desc_ciiu_división: Descripción general de la clasificación Industrial uniforme de todas las actividades económicas.

desc_ciiu_grupo: Descripción por grupo de la clasificación Industrial uniforme de todas las actividades económicas.

desc_ciiu_clase: Descripción por clase de la clasificación Industrial uniforme de todas las actividades económicas.

subsector: Clasificación de la actividad industrial.

Se observa que hay una gran variedad de subsectores, divisiones, grupos y clases en la clasificación industrial. En subsectores encontramos 83 categorías, 81 categorías en la descripción del ciiu por división, 156 por grupo y 244 por clase.

### Base de datos de noticias (Noticias.csv)

La base de datos de noticias contiene información sobre 23.377 noticias consultadas, en 23.116 urls, 2 fechas, 22.772 títulos y 21.621 contenidos. 

La dimensión de la base de datos es de 23.377 por 11 variables. No hay datos nulos ni duplicados. La mayoría de las variables son de tipo objeto, excepto las fechas que son de tipo datetime, la duración que es de tipo timedelta, y el intervalo de duración, el mes, el año y el día que son de tipo entero. La llave en la base de datos de noticias (noticias.csv) es new_id.

A continuación se observan las principales características de la base de datos.

En esta base de datos se observa que las noticias tienen dos fechas 2022-07-15 y 2022-07-29, el intervalo de tiempo para todos los registros es de 15 días. 

Las columnas de la base de datos de noticias son:

new_id: Identificador único de noticias.

news_url_absolute: Url de la noticia encontrada.

news_init_date: Fecha mínima del intervalo de tiempo al que pertenece la noticia.

news_final_date: Fecha máxima del intervalo de tiempo al que pertenece la noticia.

news_title: Título relacionado a la noticia.

news__text__content: Texto contenido de la noticia.

A partir de la distribución de noticias por cliente se puede observar que el número promedio de noticias por cliente es de aproximadamente 49.54, con una desviación estándar de 34.21. Esto indica que hay una variabilidad considerable en el número de noticias por cliente. 

El número mínimo de noticias por cliente es 4, mientras que el número máximo es 187. El primer cuartil (25%) es 27, lo que significa que el 25% de los clientes tienen 27 noticias o menos. La mediana (50%) es 36, lo que indica que el 50% de los clientes tienen 36 noticias o menos. El tercer cuartil (75%) es 60, lo que significa que el 75% de los clientes tienen 60 noticias o menos.

Esta tabla tiene dos llaves: nit y new_id. La columna nit es una llave foránea que hace referencia a la columna nit en la tabla de clientes, que es la clave primaria de esa tabla. La columna new_id es una llave foránea que hace referencia a la columna new_id en la tabla de noticias, que es la clave primaria de esa tabla. Estas dos columnas establecen una relación entre las tablas de clientes, noticias y clientes_noticias, permitiendo obtener información sobre los clientes y las noticias consultadas por ellos. 

Las columnas de la base de datos clientes_noticias son:

new_id: Identificador único del cliente.

news_url_absolute: url de la noticia encontrada.

news_init_date: Fecha mínima del intervalo de tiempo al que pertenece la noticia.

news_final_date: Fecha máxima del intervalo de tiempo al que pertenece la noticia.

![Histograma de numero de noticias por cliente](https://github.com/juanrave/Sistema-de-recomendacion-clientes-con-potencial-comercial/blob/main/doc/images/histograma_numero_noticias_por_cliente.png)https://github.com/juanrave/Sistema-de-recomendacion-clientes-con-potencial-comercial/blob/main/doc/images/histograma_numero_noticias_por_cliente.png)



