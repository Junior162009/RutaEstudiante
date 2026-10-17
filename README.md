# RutaEstudiante 🚌

PWA inicial para consultar lugares y paraderos cartografiados en Barranquilla y Soledad.

## Funciones
- Mapa Leaflet con OpenStreetMap.
- Búsqueda de lugares mediante Nominatim.
- Ubicación GPS opcional con seguimiento mientras la app está visible, indicador de precisión aproximada y botón para detenerlo; búsqueda manual disponible.
- Consulta de paraderos registrados en OpenStreetMap a 1 km (Overpass).
- Widget integrado de Q’ruta para consultar rutas SOBUSA, con opción de abrirlo en otra pestaña.
- Favoritos, historial y tema oscuro guardados localmente.
- PWA instalable y caché básica de la interfaz.
- Sin anuncios integrados.

## Limitaciones importantes
- El widget SOBUSA depende de la disponibilidad y contenido del servicio externo Q’ruta; no es una API propia ni una fuente de GPS en vivo.
- No incluye una base oficial y validada de rutas de buses de Barranquilla y Soledad.
- No calcula itinerarios de transporte público ni transbordos.
- No muestra posición de buses en tiempo real ni predice llegadas.
- Los paraderos pueden estar incompletos o desactualizados.
- Mapas, geocodificación y consulta de paraderos requieren Internet.
- Los accesos rápidos solicitan el nombre de un destino; aún no hay perfiles separados por tipo.

## Publicación
Web estática. Se puede publicar con GitHub Pages desde la raíz de la rama principal. HTTPS es necesario para PWA y GPS (localhost sirve para desarrollo).

## Auditoría de fuentes de transporte

Consulta [`docs/FUENTES_TRANSPORTE.md`](./docs/FUENTES_TRANSPORTE.md) para ver fuentes públicas revisadas, fechas observadas, advertencias de licencia y estado de integración. El widget de rutas SOBUSA usa Q’ruta: https://routes.queruta.com/?city=OWcpsp0ID3&company=yZYZbPJGbq. No se confirmó un feed público autorizado de posiciones GPS de buses de Transmetro; por eso no se simulan vehículos ni llegadas.

## Fuentes y políticas
- OpenStreetMap: https://www.openstreetmap.org/copyright
- Política Nominatim: https://operations.osmfoundation.org/policies/nominatim/
- Overpass API: https://overpass-api.de/
- Leaflet: https://leafletjs.com/

Los servicios públicos pueden imponer límites o tener interrupciones; no se deben tratar como infraestructura ilimitada. Las búsquedas y las consultas de paraderos se envían a los proveedores externos; no hay backend propio que almacene ubicación.

## Próximas fases
1. Obtener datos autorizados y verificables de rutas/paraderos (GTFS o datos de operadores).
2. Normalizar rutas, fuentes y fechas de actualización.
3. Implementar planificación de transporte público solo cuando existan datos suficientes.
4. Añadir pruebas automatizadas y revisar límites de APIs antes de producción.

## Planificador de viaje — Fase 1

La rama `feat/planificador-rutas-fase1` añade selección de origen y destino, búsqueda de coordenadas, un trazado vial de referencia y controles para mostrar ida (verde), vuelta (azul) o ambos recorridos. El trazado utiliza un servicio público de rutas viales y **no representa una ruta de autobús confirmada**. La distancia y duración mostradas son referencias del trazado vial, no predicciones del transporte público.

Esta fase no calcula líneas de bus, paraderos de subida/bajada, horarios, transbordos ni ubicación GPS de vehículos. Para habilitar esas funciones hacen falta feeds GTFS vigentes y autorizados, validados para la zona, y un feed GTFS-Realtime oficial si se quieren mostrar vehículos en vivo. Los paraderos de OpenStreetMap no prueban que un servicio pase por ellos.

El servicio de geocodificación y el motor de rutas son servicios públicos externos sujetos a disponibilidad, límites y políticas propias. La aplicación no debe presentar sus resultados como transporte público en tiempo real.

## Planificador de transporte — Fase 2

Esta fase añade una consulta opcional al catálogo público de paraderos de Transmetro en Datos Abiertos Colombia (`hxy3-94yh`). Los registros se representan como puntos y se etiquetan como históricos/no verificados; el catálogo informa que los datos de paraderos se actualizaron por última vez en 2020. Por ello, estos datos no deben usarse como confirmación de una ruta activa, horario vigente o posición de un bus. La app muestra errores de la fuente en lugar de inventar datos.

Fuentes de referencia:
- Catálogo de paraderos: https://www.datos.gov.co/resource/hxy3-94yh.json
- Ficha del conjunto de datos: https://www.datos.gov.co/en/Transporte/Paraderos-del-Sistema/hxy3-94yh
- Rutas y operación oficial: https://transmetro.gov.co/
- Listado de rutas priorizadas del Área Metropolitana de Barranquilla: https://barranquilla.gov.co/transito/rutas-transporte-publico-barranquilla-soledad

Limitación: no se ha encontrado ni validado en esta fase un feed GTFS vigente y un feed GTFS-Realtime autorizado que permita afirmar rutas completas, tiempos de llegada o localización de vehículos. El cálculo de conexiones y transbordos requiere datos actuales de itinerarios, secuencias de paradas y horarios.
