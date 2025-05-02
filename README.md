# 📊 ADA Proyecto Final – Análisis y Visualización de una Red Social Masiva

## 👥 Análisis y Visualización de un Gran Grafo de Red Social

**Autores:**
- Piero Fabricio Poblete Andía  
- Miguel Andres Flavio Ocharan Coaquira

Este proyecto tiene como objetivo analizar y visualizar la estructura de un **grafo de red social compuesto por 10 millones de usuarios**, con el fin de descubrir **patrones de conectividad**, **distribución geográfica** y otras propiedades clave del grafo.

---

## 📦 Archivos Necesarios

- `10_million_user.txt`: Archivo de texto con las relaciones de amistad entre usuarios.
- `10_million_location.txt`: Archivo con latitudes y longitudes de cada usuario.
- `ada_proyectofinal.ipynb` o `ada_proyectofinal.py`: Código principal del proyecto.

---

## 🧰 Bibliotecas Utilizadas

- `pandas`  
- `networkx`, `igraph`  
- `matplotlib`, `seaborn`  
- `cartopy` (`ccrs`, `feature`)  
- `geopy` (`Nominatim`, `RateLimiter`)  
- `google.colab` (para montar Drive)  
- `collections.Counter`  
- `warnings`

---

## ⚙️ Instrucciones de Uso

1. **Subir los archivos** a tu Google Drive en la ruta: `/content/drive/MyDrive/ada_proyectofinal_data/`.

2. **Abrir** el archivo `ada_proyectofinal.ipynb` o `ada_proyectofinal.py` en [Google Colab](https://colab.research.google.com/).

3. **Ejecutar todo el código** usando la opción `Entorno de ejecución > Ejecutar todo` o `Ctrl+F9`.

4. **Conceder permisos** para acceder a Google Drive.

5. Esperar la ejecución (≈10 minutos, dependiendo de tu entorno), principalmente debido a la carga masiva y visualización de datos.

---

## 📈 Hallazgos del Análisis Exploratorio de Datos (EDA)

- La red presenta una **distribución de grado altamente sesgada**, donde unos pocos usuarios tienen muchos amigos o seguidores, mientras que la mayoría tiene pocos (estructura típica tipo “power-law”).
- No se encontraron **outliers en las ubicaciones geográficas**.
- No se encontraron **outliers en el número de amigos por usuario**.
- Utilizando `geopy`:
  - Se identificaron los países de los usuario con másseguidores, mostrando una **concentración significativa** en `Australia, South Africa, Indonesia y Malaysia`.
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

## 📌 Notas Técnicas

- El proceso de geolocalización puede ser lento debido a restricciones de `Nominatim`. Se empleó `RateLimiter` para evitar bloqueos.
- El código se puede optimizar usando procesamiento por lotes (`chunksize`) o ejecución paralela para mejorar la eficiencia.

---

## ✅ Estado del Proyecto

✔️ Carga masiva eficiente  
✔️ Análisis exploratorio detallado  
✔️ Visualizaciones estadísticas y geográficas  
✔️ Estudio de propiedades del grafo  
✔️ Preparado para presentación y evaluación

---
