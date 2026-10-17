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
