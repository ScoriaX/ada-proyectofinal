# ADA Proyecto Final


## Análisis-Algoritmos y Visualización del Grafo de la Red ‘X’
[Enlace Documento Principal](ada_proyectofinal.ipynb)

---


**Autores:**
- Piero Fabricio Poblete Andía


---


## 1. Introducción


- **Motivación.**


La motivación principal de este proyecto es comprender en profundidad los datos y las relaciones internas contenidas en el conjunto de datos proporcionado, así como analizar la estructura del grafo derivado y sus diversas propiedades. El estudio de esta red social de gran escala permite explorar fenómenos complejos como la formación de comunidades y la distribución geográfica de los nodos, brindando así una visión integral del comportamiento estructural de la red.


- **Objetivos.**
 
El objetivo principal de este proyecto es analizar y visualizar la estructura de un gran grafo
de red social para descubrir patrones interesantes y obtener información sobre la
conectividad social, las estructuras de la comunidad y las propiedades de la red.


---


## 2. Requerimientos


### Archivos Necesarios


- `10_million_user.txt`: Archivo de texto con las relaciones de amistad entre usuarios.
- `10_million_location.txt`: Archivo con latitudes y longitudes de cada usuario.
- `ada_proyectofinal.ipynb` o `ada_proyectofinal.py`: Código principal del proyecto.


### Bibliotecas Utilizadas


- `pandas`  
- `networkx`, `igraph`  
- `matplotlib`, `seaborn`  
- `cartopy`
- `geopy`
- `google.colab`
- `collections.Counter`  
- `warnings`


###  Instrucciones de Uso


1. **Subir los archivos** a tu Google Drive en la ruta: `/content/drive/MyDrive/ada_proyectofinal_data/`.


2. **Abrir** el archivo `ada_proyectofinal.ipynb` o `ada_proyectofinal.py` en [Google Colab](https://colab.research.google.com/).


3. **Ejecutar todo el código** usando la opción `Entorno de ejecución > Ejecutar todo` o `Ctrl+F9`.


4. **Conceder permisos** para acceder a Google Drive.


5. Esperar la ejecución (≈10 minutos, dependiendo de tu entorno), principalmente debido a la carga masiva y visualización de datos.


---


## 3. Preprocesamiento de Datos


### Metodología


El proceso de análisis se inició con la **carga de los datos en estructuras `DataFrame` utilizando la biblioteca `pandas`**, lo que permitió una manipulación eficiente y estructurada de la información. Se realizaron **validaciones de integridad y rango** para asegurar la coherencia de los datos, descartando valores fuera de los límites esperados.


Dado el tamaño del conjunto de datos y con el objetivo de **optimizar el uso de memoria**, se optó por **mantener las listas de conexiones en su forma original** (listas de adyacencia), en lugar de expandirlas en múltiples columnas.


A partir de los datos originales se generaron **atributos derivados**, como:


- El **número de seguidores y seguidos por usuario**, calculado a partir de las listas de adyacencia.
- El **país de origen de cada usuario**, estimado mediante técnicas de geocodificación inversa basadas en sus coordenadas geográficas (latitud y longitud).


---


## Construcción del Grafo


### Metodología


- Se utilizaron los `DataFrame` mencionados previamente, en particular las **listas de adyacencia**, sobre las cuales se aplicó un algoritmo para generar un archivo CSV que representara las relaciones en formato de **tuplas (origen, destino)**. Este formato fue elegido para facilitar la construcción eficiente del grafo utilizando las estructuras proporcionadas por la biblioteca `igraph`.


- En otras palabras, se generó un nuevo archivo CSV que contiene explícitamente las conexiones dirigidas entre usuarios, el cual sirvió como **fuente directa para la construcción del grafo** durante la fase de ejecución del programa.


- Además, para facilitar el proceso de visualización se aplicó el mismo procedimiento pero con los nodos o  usuarios agrupados por su país de origen.


---


## 4. Análisis Exploratorio de Datos (EDA)


### Hallazgos:


- La red presenta una **distribución de grado altamente sesgada**, donde unos pocos usuarios tienen muchos amigos o seguidores, mientras que la mayoría tiene pocos (estructura típica tipo “power-law”).
- No se encontraron **outliers en las ubicaciones geográficas**.
- No se encontraron **outliers en el número de amigos por usuario**.
- Utilizando `geopy`:
  - Se identificaron los países de los usuario con más seguidores, mostrando una **concentración significativa** en `Australia, South Africa, Indonesia y Malaysia`.
  - Se identificaron los países de los usuario con menos seguidores, mostrando una **concentración significativa** en `Estados Unidos`.
  - Se identificaron los países de los usuarios con más seguidos, mostrando una **concentración significativa** en `Desconocido y Australia`.
  - Se identificaron los países de los usuarios con menos seguidos, mostrando una **concentración significativa** en `Desconocido y Estados Unidos`.
   
- Estudio del `grafo`:
  - El número de nodos es: 10000000
  - El número de aristas es: 169488182
  - Su densidad es: 1.694881989488199e-06. El número de la densidad es bajo lo que indica que existe **poca conexión** dentro del grafo.
  - Su promedio de grado es: 16.9488182. El número promedio de conexiones es bajo comparado con la cantidad total de usuarios, indicando una red **poco densa** pero con nodos mas poblados.
   
- Las visualizaciones muestran **patrones geoespaciales** con hotspots evidentes en ciudades y regiones densamente pobladas.
- Los histogramas de latud y longitud revelan la **distribución desigual** de los usuarios a nivel mundial, alineada con patrones reales de población.


---


## 5. Propiedades y Métricas de la Red


### Detección de Comunidades:


Para la detección de comunidades dentro del grafo, se implementó el algoritmo de **propagación de etiquetas** (*Label Propagation*), una técnica no supervisada que se caracteriza por su simplicidad y eficiencia en grafos de gran escala.


La implementación sigue el siguiente enfoque:


- **Inicialización:** A cada nodo se le asigna una etiqueta única correspondiente a su propio identificador.
- **Iteración:** En cada iteración, se recorre aleatoriamente el conjunto de nodos. Cada nodo adopta la etiqueta más frecuente entre sus vecinos inmediatos. Este proceso simula la difusión de etiquetas a través del grafo.
- **Actualización:** Si un nodo cambia su etiqueta, se contabiliza como un cambio. El algoritmo continúa iterando hasta que no se produzcan más cambios o se alcance el número máximo de iteraciones.


Este método permite **identificar comunidades de forma eficiente sin requerir parámetros previos ni conocimiento de la estructura global del grafo**, lo cual lo hace especialmente adecuado para conjuntos de datos tan extensos como el utilizado en este proyecto.


---


## 6. Análisis Avanzado


### Análisis de Camino Más Corto:


Para determinar el **camino más corto entre dos nodos** dentro del grafo, se implementó el algoritmo de **Búsqueda en Anchura (BFS, por sus siglas en inglés)**, el cual es especialmente eficiente en grafos no ponderados.


El algoritmo funciona de la siguiente manera:


- Se inicializa una cola con el nodo de origen, y se marca como visitado.
- A medida que se recorren los nodos, se lleva un registro del **predecesor** de cada nodo visitado, lo que permite **reconstruir el camino** una vez que se alcanza el nodo de destino.
- El recorrido se realiza en amplitud, garantizando que el primer camino encontrado sea el más corto en número de aristas.
- Finalmente, si se encuentra el destino, se reconstruye el camino en orden inverso utilizando el arreglo de predecesores.


Este enfoque es adecuado para grafos dirigidos y no ponderados como el de este proyecto, donde el objetivo es encontrar el trayecto más corto en términos de conexiones directas entre dos usuarios.


En caso de que no exista un camino entre el nodo de origen y el destino, el algoritmo retorna `None`.


---


## 7. Visualización


### Visualizaciones Interactivas:


- Se presentan gráficas comparativas, representaciones en mapas y un grafo creado a partir de la agrupación de los diferentes usuarios en países.


### Visualización de Comunidades:


- Ninguna.


---


## 8. Conclusión


### Resumen de hallazgos:


A partir del análisis y procesamiento del grafo de la red social, se obtuvieron los siguientes resultados relevantes:


- El grafo presenta una estructura **dirigida y altamente conectada**, con múltiples componentes fuertemente conectados.
- Se identificaron múltiples **comunidades naturales** dentro de la red mediante el algoritmo de propagación de etiquetas (*Label Propagation*), lo que evidencia una organización modular típica de redes sociales reales.
- El número de **seguidores y seguidos** por usuario varía ampliamente, mostrando la existencia de usuarios altamente influyentes (hubs).
- A partir de la información geográfica, se observó una distribución de usuarios **ampliamente dispersa geográficamente**, con ciertos clusters de alta densidad en regiones específicas.
- El algoritmo de búsqueda en anchura (BFS) permitió encontrar **caminos mínimos entre pares de usuarios**, facilitando la evaluación de la eficiencia de la conectividad dentro del grafo.


Estos hallazgos confirman la presencia de patrones estructurales complejos, característicos de redes sociales reales, y resaltan la utilidad de los algoritmos aplicados para la exploración de grafos a gran escala.


### Trabajo Futuro:


- Implementar un verdadero análisis de el n promedio de nodos y tiempo que ocupa el algoritmo de camino más corto.


- Graficar las diferentes comunidades obtenidas con colores.


- Lograr una visualización completa del nodo total, utilizando programas online como Graphi…


- Lograr una visualización  más clara del grafo de países (Grafo Circular), utilizando software como Circos.


- Lograr una mejor presentación general utilizando Streamlit.


---


## Notas Técnicas


- El proceso de geolocalización puede ser lento debido a restricciones de `Nominatim`. Se empleó `RateLimiter` para evitar bloqueos.
- El código se puede optimizar usando procesamiento por lotes (`chunksize`) o ejecución paralela para mejorar la eficiencia.


---


## Estado del Proyecto


- Carga masiva eficiente  
- Análisis exploratorio detallado  
- Visualizaciones estadísticas y geográficas  
- Estudio de propiedades del grafo  
- Preparado para presentación y evaluación


---


## 9. Referencias


- https://cienciadedatos.net/documentos/pygml01-introduccion-grafos-redes-python
- https://netwulf.readthedocs.io/en/latest/
- https://cienciadedatos.net/documentos/pygml03-analisis-redes-python-networkx
- https://cienciadedatos.net/documentos/pygml02-detecion-comunidades-grafos-redes-python
- https://networkx.org/documentation/stable/reference/algorithms/generated/networkx.algorithms.community.centrality.girvan_newman.html
- https://algs4.cs.princeton.edu/43mst/








