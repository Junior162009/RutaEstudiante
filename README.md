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

## Fase 3: buscador experimental de conexiones GTFS

Se añadió un buscador de conexiones directas basado en el feed comunitario de ColombiaGTFS para Transmetro. La aplicación consulta paraderos, rutas, viajes y secuencias de paradas, encuentra paraderos cercanos al origen/destino, busca viajes GTFS que conecten ambos puntos y permite dibujar el tramo histórico en el mapa. El buscador no necesita un backend propio, pero depende de que GitHub Raw esté disponible y de que el navegador permita las solicitudes externas.

**Advertencia crítica sobre vigencia:** el archivo `calendar.txt` de ese feed declara vigencia del 2016-01-01 al 2017-12-31. Por esa razón los resultados se muestran explícitamente como históricos, no como instrucciones actuales para viajar; tampoco se deben interpretar como horarios actuales. No se encontró en esta implementación una fuente oficial vigente de GTFS/GTFS-Realtime ni se afirma disponer de GPS de buses. El buscador de esta fase solo busca conexiones directas, no transbordos.

Fuentes revisadas:
- Feed comunitario GTFS: https://github.com/ColombiaInfo/ColombiaGTFS/tree/master/Barranquilla%20-%20Transmetro
- Catálogo de paraderos: https://www.datos.gov.co/en/Transporte/Paraderos-del-Sistema/hxy3-94yh
- Operación oficial Transmetro: https://transmetro.gov.co/

Antes de usar resultados en producción, hay que sustituir el feed histórico por uno actualizado y verificar fechas, licencias, cobertura y funcionamiento. Las pruebas reales de red y navegador siguen pendientes.

## Mostrar un recorrido de Q'ruta en el mapa principal

Se añadió un importador de recorridos que permite cargar archivos `KML`, `GPX` o `GeoJSON` (máximo 10 MB) y dibujar sus líneas y extremos sobre el mapa Leaflet principal. La ruta importada se puede quitar sin borrar el planificador ni otros datos. Se validan las coordenadas y se informa cuando el archivo no contiene una geometría compatible.

**Límite del widget de Q'ruta:** el contenido de `routes.queruta.com` se carga dentro de un iframe de otro dominio. La política de mismo origen del navegador impide que RutaEstudiante lea automáticamente qué ruta se seleccionó dentro del iframe. Por eso esta función necesita un archivo con las coordenadas de la ruta; no copia por sí sola una selección interna del widget. Q'ruta ha descrito el uso de recorridos KML para comunicar trazados de rutas: https://blog.queruta.com/index.php/2024/01/18/como-ayudarnos-con-informacion-de-rutas/.

Pruebas reales con archivos de Q'ruta y validación en navegadores/dispositivos pendientes. No se afirma que exista una API oficial de Q'ruta disponible para esta integración.


## Mejora progresiva de interfaz y accesibilidad

La rama `feat/redisenio-ux-rutaestudiante` incorpora una capa de ajustes visuales sobre la interfaz existente: foco de teclado visible, controles táctiles con tamaño mínimo, estados deshabilitados, respuesta visual de botones, tarjetas más claras y ajustes responsive para que el mapa tenga mayor espacio en móvil y escritorio. No sustituye Leaflet, el planificador, las fuentes de datos, el importador ni el widget de Q'ruta.

Se añadió una lista de comprobación manual en [docs/PRUEBAS-MANUALES.md](./docs/PRUEBAS-MANUALES.md). Es una guía pendiente de ejecución; no debe interpretarse como evidencia de pruebas ya realizadas.

### Alcance de este cambio

- Se mantienen las funciones existentes y sus identificadores de interfaz.
- No se añadió una fuente de GPS de autobuses ni se presentan los datos GTFS históricos como vigentes.
- La verificación en dispositivos físicos, la disponibilidad de servicios externos y las pruebas automatizadas quedan pendientes.
