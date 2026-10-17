# Fuentes de datos y estado de integración

Fecha de revisión: 2026-10-17.

## Resumen verificable

| Fuente | Cobertura y contenido | Frescura observada | Licencia / uso | Estado en RutaEstudiante |
|---|---|---|---|---|
| [Datos Abiertos Colombia: Paraderos del Sistema](https://www.datos.gov.co/en/Transporte/Paraderos-del-Sistema/hxy3-94yh) | Transmetro, Barranquilla; metadatos del conjunto indican 928 filas y campos para nombre de ruta, parada, secuencia y coordenadas. | La ficha muestra actualización de datos del 28-09-2020 y metadatos actualizados el 23-09-2026. No deben confundirse. | Revisar los términos y la licencia mostrados en la ficha antes de redistribuir o importar. | Fuente candidata; no conectada automáticamente. |
| [TUMI Datahub: GTFS Barranquilla](https://hub.tumidata.org/dataset/gtfs_barranquilla) | Feed GTFS estático para Transmetro/Barranquilla. | La página informa última actualización 31-10-2025 y advierte que puede quedar desactualizado. | La página advierte que la información de licencia puede estar desactualizada; confirmar con la fuente original. | Candidato para validar en un importador GTFS; no se presenta como vigente ni como fuente oficial en tiempo real. |
| [ColombiaInfo/ColombiaGTFS: Transmetro](https://github.com/ColombiaInfo/ColombiaGTFS/tree/master/Barranquilla%20-%20Transmetro) | Repositorio comunitario con archivos GTFS como rutas y posiblemente otros archivos del feed. | El repositorio puede cambiar; comprobar el commit y las fechas de cada archivo al descargar. | Verificar licencia del repositorio y procedencia del feed antes de redistribuir. | Referencia comunitaria, no una conexión oficial en vivo. |
| [Transmetro oficial](https://transmetro.gov.co/) | Información institucional y de operación; no se confirmó en esta revisión un endpoint público de GTFS Realtime para posiciones de buses. | Las páginas pueden actualizarse, pero eso no prueba que exista una API GPS pública. | Aplican las condiciones del operador y las de cada recurso publicado. | Enlace de referencia; no se conecta seguimiento de buses. |
| [OpenStreetMap](https://www.openstreetmap.org/) / [política de Nominatim](https://operations.osmfoundation.org/policies/nominatim/) / [Overpass API](https://overpass-api.de/) | Datos cartográficos, geocodificación y objetos de paraderos etiquetados por la comunidad. La app ya consulta Overpass y Nominatim. | Variable según ediciones de la comunidad; las etiquetas pueden estar incompletas. | OpenStreetMap requiere atribución y está bajo ODbL; Nominatim y Overpass tienen políticas de uso específicas. | Ya usados por la app para mapa, búsqueda y paraderos cercanos. No proporcionan por sí solos GPS de buses. |
| [Especificación GTFS](https://gtfs.org/) y [GTFS Realtime](https://developers.google.com/transit/gtfs-realtime?hl=es-419) | Estándares para horarios/rutas estáticas y actualizaciones de viajes, alertas y posiciones de vehículos. | Depende del operador que publique los feeds. | Respetar las condiciones de cada operador y feed. | Referencia técnica; no se ha verificado un feed Realtime público de Transmetro. |

## Conclusiones

- En esta revisión no se verificó un feed GTFS Realtime público y autorizado de Transmetro con posiciones de buses. Por eso RutaEstudiante no muestra vehículos simulados ni promete llegadas en tiempo real.
- El dataset de paraderos de Datos Abiertos es útil como fuente candidata, pero la ficha indica que los datos subyacentes son de 2020. No debe describirse como información recién actualizada solo porque los metadatos se modificaron en 2026.
- Los feeds estáticos encontrados son candidatos para una fase posterior. Antes de importarlos hay que validar archivos GTFS, fechas de servicio, cobertura, licencia, atribución y correspondencia con la operación vigente.
- La consulta de paraderos de OpenStreetMap no es una lista oficial completa de rutas ni garantiza cobertura en Soledad o todos los barrios.
- No se añadió una dependencia de backend ni se expusieron claves. La sincronización automática de GTFS y el planificador de transporte público quedan pendientes de una fuente verificable y una canalización de importación probada.

## Recomendación para la siguiente fase

Implementar un importador de GTFS con validación, staging y sustitución transaccional de la última versión válida. Registrar URL de origen, fecha de descarga, hash, licencia, fecha de servicio y errores de validación. Activar el planificador solo cuando exista un feed validado y suficientemente vigente. Para GPS de buses, solicitar al operador un endpoint o feed GTFS Realtime oficial y documentar su frecuencia de actualización y autorización.
