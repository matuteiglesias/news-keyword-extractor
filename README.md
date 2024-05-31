# News Keyword Extractor

Este proyecto contiene un módulo en Python que busca y extrae noticias de varios feeds RSS utilizando una lista de keywords proporcionada y almacena los resultados en Google BigQuery. Este software está diseñado para ser integrado fácilmente en otros proyectos de Python y proporciona una manera eficiente de mantenerse actualizado con las noticias relevantes basadas en keywords específicas.

## Requisitos
- Python 3.x
- Librerías `feedparser`, `pandas`, `beautifulsoup4`, `requests`, `google-cloud-bigquery`, `google-auth`, `google-auth-oauthlib`, `google-auth-httplib2`

## Instalación
1. Clona este repositorio:
   ```bash
   git clone https://github.com/tu_usuario/news-keyword-extractor.git
   cd news-keyword-extractor
   ```

2. Instala las dependencias necesarias:
   ```bash
   pip install -r requirements.txt
   ```

3. Configura las credenciales de Google Cloud:
   - Descarga el archivo de credenciales de tu proyecto en Google Cloud Platform.
   - Guarda el archivo de credenciales en la raíz del proyecto y actualiza la ruta en el script de ejemplo si es necesario.

## Uso
### Ejemplo Básico
Puedes integrar este módulo en tu proyecto importando las funciones necesarias. Aquí hay un ejemplo básico:

```python
from src.news_extractor import NewsExtractor
from src.config import RSS_FEEDS, DEFAULT_KEYWORDS

# Configuración
rss_feeds = RSS_FEEDS
keywords = DEFAULT_KEYWORDS

# Creación del extractor de noticias
extractor = NewsExtractor(rss_feeds, keywords, credentials_path='./../media-monitor-tool-465a31b84648.json', project_id='media-monitor-tool')

# Ejecución de la búsqueda
news = extractor.extract_news()

# Mostrar las noticias extraídas
print(news)

# Exportación de resultados a CSV
extractor.export_to_csv('output.csv')

# Inserción de resultados en BigQuery
extractor.insert_news_bigquery('tu-dataset-id.noticias')
```

### Ejecutar el Script de Ejemplo
1. Ejecuta el script de ejemplo para ver cómo funciona:
   ```bash
   python examples/example_usage.py
   ```

2. Las noticias extraídas se mostrarán en la consola, se guardarán en un archivo CSV y se insertarán en Google BigQuery.

## Funciones Principales
### `extract_news()`
Busca y extrae noticias de las fuentes RSS configuradas que contengan las keywords proporcionadas.

### `export_to_csv(file_name)`
Exporta las noticias extraídas a un archivo CSV.

### `insert_news_bigquery(table_id)`
Inserta las noticias extraídas en una tabla de Google BigQuery.

## Automatización y Actualización
Para automatizar la ejecución del script periódicamente, puedes usar un cron job en sistemas Unix. Aquí tienes un ejemplo de cómo configurar un cron job para ejecutar el script cada hora:

1. Abre el crontab para editar:
   ```bash
   crontab -e
   ```

2. Añade la siguiente línea para ejecutar el script cada hora:
   ```plaintext
   0 * * * * /usr/bin/python3 /ruta/al/proyecto/news-keyword-extractor/examples/example_usage.py
   ```

## Contribuciones
Las contribuciones son bienvenidas. Por favor, abre un issue o un pull request para sugerencias o mejoras.

## Licencia
Este proyecto está licenciado bajo la Licencia MIT. Consulta el archivo [LICENSE](LICENSE) para más detalles.

