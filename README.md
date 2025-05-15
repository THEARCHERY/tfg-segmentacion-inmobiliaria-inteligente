# tfg-segmentacion-inmobiliaria-inteligente

Implementación de un sistema de segmentación inteligente de la oferta inmobiliaria mediante Fuzzy K-means y DBSCAN geográfico, con visualizaciones espaciales y automatización de recomendaciones vía Make.com y OpenAI.

---

## Índice

* [Descripción](#descripción)
* [Estructura del Proyecto](#estructura-del-proyecto)
* [Requisitos](#requisitos)
* [Instalación](#instalación)
* [Uso](#uso)
* [Metodología](#metodología)
* [Datos](#datos)
* [Automatización](#automatización)
* [Contribuciones](#contribuciones)
* [Licencia](#licencia)
* [Contacto](#contacto)

---

## Descripción

Este proyecto desarrolla un sistema de segmentación inteligente de anuncios inmobiliarios basado en técnicas de clustering difuso (Fuzzy K-means) y clustering espacial (DBSCAN). Se generan perfiles de demanda y se automatizan recomendaciones personalizadas usando Make.com y OpenAI.

## Estructura del Proyecto

```text
|-- data/                  # Conjunto de datos originales y preprocesados
|   |-- raw/               # Datos crudos (Idealista, INE, infraestructuras)
|   |-- processed/         # Datos limpios y escalados
|
|-- notebooks/             # Jupyter Notebooks de análisis
|   |-- preprocessing.ipynb # Preprocesamiento y limpieza
|   |-- clustering.ipynb    # Modelado Fuzzy K-means y DBSCAN
|   |-- visualization.ipynb # Mapas y PCA
|
|-- automation/            # Escenarios de Make.com y scripts de integración
|   |-- scenario.make      # Definición de flujos en Make.com
|   |-- scripts/           # Scripts auxiliares (OpenAI, Google Sheets)
|
|-- src/                   # Código fuente
|   |-- clustering.py      # Implementación de algoritmos
|   |-- utils.py           # Funciones auxiliares (preprocesamiento, métricas)
|
|-- README.md              # Documentación del proyecto
|-- requirements.txt       # Dependencias Python
|-- LICENSE                # Licencia del proyecto
```

## Requisitos

* Python 3.9+
* Paquetes:

  * `numpy`
  * `pandas`
  * `scikit-learn`
  * `folium`
  * `matplotlib`
  * `openai`
  * `gspread`

## Instalación

1. Clonar el repositorio:

   ```bash
   git clone https://github.com/tu-usuario/tfg-segmentacion-inmobiliaria-inteligente.git
   cd tfg-segmentacion-inmobiliaria-inteligente
   ```
2. Crear y activar entorno virtual:

   ```bash
   python -m venv venv
   source venv/bin/activate  # Linux/Mac
   .\venv\Scripts\activate   # Windows
   ```
3. Instalar dependencias:

   ```bash
   pip install -r requirements.txt
   ```

## Uso

1. Preprocesar datos:

   ```bash
   python src/utils.py --preprocess data/raw/ data/processed/
   ```
2. Ejecutar clustering:

   ```bash
   python src/clustering.py --input data/processed/ --output results/
   ```
3. Generar visualizaciones:

   ```bash
   jupyter notebook notebooks/visualization.ipynb
   ```
4. Desplegar automatización:

   * Importar `scenario.make` en Make.com
   * Configurar credenciales de OpenAI y Google Sheets

## Metodología

1. **Preprocesamiento:** eliminación de duplicados, imputación de outliers (IQR y desviación estándar), normalización y escalado.
2. **Clustering difuso:** Fuzzy K-means con `m=2.0`, `c=4`, validado con índices FPC y FPE.
3. **Clustering espacial:** DBSCAN global y subclustering para identificar barrios con `eps` y `min_samples` ajustados.
4. **Perfiles:** cuatro segmentos: `accesible joven`, `media funcional`, `familiar premium`, `alta gama`.
5. **Validación y visualización:** PCA y mapas de calor geográficos con Folium.

## Datos

* **Idealista:** \~100 000 registros de anuncios (precio, área, habitaciones, equipamientos, coordenadas).
* **INE:** Variables sociodemográficas adicionales.
* **Infraestructuras:** Datos de transporte y servicios de Comunidad y Ayuntamiento de Madrid.

## Automatización

Flujo en **Make.com**:

1. Watch Email -> 2. OpenAI (gpt-4o-mini) extrae campos -> 3. Google Sheets consulta -> 4. OpenAI (gpt-4o) genera texto -> 5. Send Email.

## Contribuciones

Las contribuciones son bienvenidas: crear issues o pull requests sobre mejoras en el preprocesamiento, algoritmos o integración.

## Licencia

Este proyecto está bajo la licencia MIT. Consulte el archivo [LICENSE] para más detalles.

## Contacto

* Autor: Gonzalo Romero Carrato
* Email: [gonzalo.rcarrato@gmail.com](mailto:gonzalo.rcarrato@gmail.com)
