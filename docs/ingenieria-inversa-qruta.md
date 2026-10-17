# Ingeniería inversa funcional de Q'ruta para RutaEstudiante

Fecha de revisión: 2026-10-17.

## Alcance y límites

Esta documentación recoge el comportamiento visible y los datos expuestos públicamente. No reconstruye código propietario ni presupone acceso a APIs privadas. No se ha confirmado una API pública completa para descargar la base de datos de Q'ruta.

Fuentes públicas consultadas:
- https://www.queruta.com/ — presenta la plataforma y enumera 13 ciudades.
- https://near.queruta.com/ — generador público de rutas cercanas.
- https://near.queruta.com/?city=OWcpsp0ID3&hideMap=false&latitude=11.0193206&longitude=-74.8504426&title=Auditorio+Marvel+Moreno — listado público de rutas cercanas de Barranquilla.
- https://blog.queruta.com/index.php/2024/01/18/como-ayudarnos-con-informacion-de-rutas/ — explica el envío de recorridos KML, información de horarios y frecuencias.

## Observaciones de la interfaz pública

1. El catálogo público identifica Armenia, Barranquilla, Bogotá, Bucaramanga, Cali, Cartagena, Ibagué, Medellín, Neiva, Pasto, Santa Marta, Tunja y Valledupar.
2. La herramienta de rutas cercanas recibe un identificador de ciudad y coordenadas geográficas, y presenta filtros de transporte urbano y masivo.
3. Los listados públicos pueden mostrar código, operador y nombre de ruta; la página no demuestra por sí sola que cada servicio esté funcionando en este momento.
4. La documentación de Q'ruta propone archivos KML para describir recorridos y recomienda documentar horarios por tipo de día y frecuencias.
5. La integración mediante iframe no permite leer su contenido interno desde RutaEstudiante debido a las restricciones de mismo origen del navegador. La importación de un archivo de recorrido es una alternativa legítima.

## Datos de referencia

El archivo `data/qruta-cities.json` contiene:
- El catálogo de las 13 ciudades que la web pública enumera, con centros aproximados de mapa para inicializar una vista.
- El identificador público de Barranquilla que aparece en un enlace de rutas cercanas.
- Una pequeña muestra de rutas nombradas en listados públicos de Barranquilla.

La muestra de rutas no es exhaustiva y no debe interpretarse como una fuente de operación en tiempo real. Los centros de mapa son aproximados; no son datos de transporte.

## Arquitectura recomendada para RutaEstudiante

- Mantener GPS como función opcional.
- Permitir origen y destino escritos manualmente o seleccionados en el mapa.
- Mantener separado el trazado vial de referencia y el trazado de una ruta de autobús validada.
- Importar geometrías propias en KML, GPX o GeoJSON al mapa principal.
- Guardar procedencia y fecha de consulta para cada ruta, parada y horario.
- No mostrar frecuencias, vehículos en vivo ni transbordos como confirmados sin una fuente actual que los respalde.
- Mantener el mapa principal existente y añadir nuevas funciones de forma incremental.

## Esquema de datos propuesto

Una ruta debería contener como mínimo: ciudad, operador, código, nombre, sentido, geometría, paradas, calendario, frecuencia, URL de origen y fecha de verificación. Cada parada debería tener identificador, nombre, latitud, longitud, rutas relacionadas y procedencia.

## Validación antes de producción

- Verificar que las coordenadas estén dentro de los límites geográficos.
- Revisar el sentido de ida y vuelta por separado.
- Validar que la geometría coincida con las paradas.
- Registrar la fecha de última actualización.
- Indicar explícitamente cuándo la información es histórica, incompleta o no verificada.
- No extraer ni copiar endpoints privados ni intentar saltarse controles de acceso.
