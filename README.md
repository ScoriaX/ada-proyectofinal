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

1. **Subir los archivos** a tu Google Drive en la ruta:

2. **Abrir** el archivo `ada_proyectofinal.ipynb` o `ada_proyectofinal.py` en [Google Colab](https://colab.research.google.com/).

3. **Ejecutar todo el código** usando la opción `Entorno de ejecución > Ejecutar todo` (o `Ctrl+F9`).

4. **Conceder permisos** para acceder a Google Drive.

5. Esperar la ejecución (≈10 minutos, dependiendo de tu entorno), principalmente debido a la carga masiva y visualización de datos.

---

## 📈 Hallazgos del Análisis Exploratorio de Datos (EDA)

- La red presenta una **distribución de grado altamente sesgada**, donde unos pocos usuarios tienen muchos amigos o seguidores, mientras que la mayoría tiene pocos (estructura típica tipo “power-law”).
- Se detectaron **outliers en las ubicaciones geográficas**, principalmente coordenadas fuera de los rangos válidos, que fueron filtradas.
- A través del geolocalizador `geopy`, se identificaron los países de los usuarios más conectados, mostrando una **presencia global significativa** con concentración en regiones como América del Norte, Europa y Asia.
- El número promedio de conexiones (grado promedio) es bajo comparado con la cantidad total de usuarios, indicando una red **poco densa** pero con hubs importantes.
- Las visualizaciones muestran **patrones geoespaciales** con hotspots evidentes en ciudades y regiones densamente pobladas.
- Los histogramas de latitud y longitud revelan la **distribución desigual** de los usuarios a nivel mundial, alineada con patrones reales de población.

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
