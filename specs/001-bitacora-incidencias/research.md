# Investigación y decisiones

## Plataforma y almacenamiento

- **Decisión**: App model-driven de Power Apps sobre Dataverse, creada con el
  plugin model-apps (`/app-builder`) en el ambiente del laboratorio y dentro de la
  solución de la pareja.
- **Motivo**: Es la plataforma y el método indicados para el taller y cumplen
  la constitución del proyecto.
- **Alternativas consideradas**: Servicios o almacenamiento externos; se descartan
  porque la constitución los prohíbe.

## Modelo de datos

- **Decisión**: Una tabla principal `Incidencia` y un catálogo editable
  `Línea de producción`, con nombres lógicos generados usando el prefijo de la
  pareja.
- **Motivo**: Mantiene el diseño simple y permite cambiar las líneas sin
  modificar la tabla principal.
- **Alternativas consideradas**: Guardar la línea como texto libre; se descarta
  porque la línea debe seleccionarse de un catálogo editable.

## Roles y vistas por línea

- **Decisión**: Asignar roles de seguridad Supervisor y Mantenimiento. Una vista
  de incidencias abiertas permite seleccionar la línea correspondiente y filtrar
  los registros en la misma vista.
- **Motivo**: Conserva los permisos descritos y permite consultar las abiertas
  por línea sin agregar una tabla de asignaciones no solicitada.
- **Alternativas consideradas**: Crear una tabla adicional para asignar personas a
  líneas; se descarta para mantener el modelo acotado a la tabla principal y los
  catálogos.

## Fecha de cierre

- **Decisión**: Un flujo de nube de Power Automate dentro de la solución se activa
  al crear o actualizar una incidencia. Si el estado es Cerrada y la fecha está
  vacía, registra la fecha y hora actuales.
- **Motivo**: Conserva el momento del cierre aunque después cambien otros datos.
- **Alternativas consideradas**: Usar la fecha de última modificación; se descarta
  porque puede cambiar después del cierre. Usar un servicio o conector externo se
  descarta por la constitución y las políticas de DLP.

## Límites

- **Decisión**: No agregar conectores externos, notificaciones ni reportes.
- **Motivo**: Están fuera del alcance de la primera versión.
- **Alternativas consideradas**: Integraciones externas o automatizaciones para
  enviar avisos; se descartan por alcance.
