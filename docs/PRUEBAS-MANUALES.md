# Lista de verificación de RutaEstudiante

Esta lista sirve para una comprobación manual antes de publicar cambios. No representa pruebas ya ejecutadas.

## Móvil y escritorio
- [ ] Abrir en un navegador móvil con HTTPS y en escritorio.
- [ ] Comprobar que el mapa se puede mover y acercar sin quedar tapado por la navegación.
- [ ] Comprobar que el panel de búsqueda y la barra inferior permiten acceder a los controles principales.
- [ ] Verificar navegación con teclado y que el foco visible se distingue.

## Búsqueda y GPS
- [ ] Buscar un destino válido y seleccionar un resultado.
- [ ] Buscar un texto sin resultados y confirmar que aparece un mensaje útil.
- [ ] Permitir GPS, comprobar marcador y recentrado.
- [ ] Rechazar GPS y comprobar que la búsqueda manual continúa disponible.
- [ ] Comprobar que los permisos no se solicitan repetidamente.

## Rutas y capas
- [ ] Calcular el trazado de referencia de ida, vuelta y ambos sentidos.
- [ ] Confirmar que se etiqueta como referencia vial, no como recorrido de autobús confirmado.
- [ ] Importar KML, GPX y GeoJSON válidos.
- [ ] Probar archivo vacío, extensión no admitida, coordenadas inválidas y archivo superior al límite anunciado.
- [ ] Quitar solo la ruta importada y verificar que las otras capas siguen visibles.
- [ ] Confirmar que Q'ruta abre en una pestaña independiente si el iframe no carga.

## Paraderos y fuentes
- [ ] Consultar paraderos de OpenStreetMap y gestionar error de conexión.
- [ ] Consultar el catálogo público de paraderos y comprobar que se advierte su antigüedad.
- [ ] Consultar GTFS y confirmar que el calendario histórico se etiqueta claramente.
- [ ] Verificar que ninguna pantalla afirma disponer de GPS de autobuses en vivo sin feed autorizado.

## Preferencias
- [ ] Guardar y volver a abrir un favorito.
- [ ] Confirmar que el historial reciente persiste al recargar.
- [ ] Cambiar a modo oscuro, recargar y comprobar que se conserva.
- [ ] Probar almacenamiento local bloqueado o lleno y verificar que el fallo no rompe el mapa.

## Registro de ejecución
- Fecha:
- Navegador / versión:
- Dispositivo:
- Resultado:
- Errores o capturas:

**Estado actual:** esta lista se añadió como guía. No se ejecutaron pruebas reales en un dispositivo ni una suite automatizada en este cambio. Los servicios externos dependen de red y de sus propias políticas y disponibilidad.
