# Feature Specification: Bitácora de incidencias de mantenimiento

**Feature Branch**: `checkpoint-1-spec`

**Created**: 2026-10-27

**Status**: Draft

**Input**: User description: "Contoso necesita una bitácora de incidencias de mantenimiento para las líneas de producción de sus plantas. La usan los supervisores de turno para registrar fallas de equipo y el equipo de mantenimiento para darles seguimiento. Debe permitir registrar una incidencia (línea, equipo, severidad, descripción), ver la lista filtrando por estado y severidad, y cambiar el estado a En proceso o Cerrada. Las incidencias de severidad Alta deben verse primero. Solo mantenimiento puede cerrar incidencias. Fuera de alcance: notificaciones, reportes y fotos. Sabremos que funciona si un supervisor registra una incidencia en menos de 1 minuto y mantenimiento ve las abiertas de su línea en una sola vista."

## User Scenarios & Testing

### User Story 1 - Registrar una incidencia (Priority: P1)

Como supervisor de turno, quiero registrar una falla de equipo con su línea,
severidad y descripción para que mantenimiento pueda atenderla.

**Why this priority**: Sin un registro claro de la falla, mantenimiento no puede
darle seguimiento.

**Independent Test**: Un supervisor registra una incidencia con los datos
solicitados y confirma que aparece con un folio, fecha y estado inicial.

**Acceptance Scenarios**:

1. CUANDO un supervisor intente guardar una incidencia sin línea de producción,
   EL SISTEMA DEBE impedir el guardado.
2. CUANDO un supervisor registre una incidencia completa, EL SISTEMA DEBE asignar
   un folio automático, registrar la fecha de reporte y dejar el estado como
   Abierta.

### User Story 2 - Consultar incidencias (Priority: P2)

Como supervisor o integrante de mantenimiento, quiero consultar incidencias y
filtrarlas por estado y severidad para encontrar las que requieren atención.

**Why this priority**: Una consulta sencilla permite que cada equipo ubique el
trabajo pendiente sin revisar registros que no necesita.

**Independent Test**: Una persona consulta las incidencias abiertas de su línea,
filtra por estado y severidad, y localiza primero las de severidad Alta.

**Acceptance Scenarios**:

1. CUANDO la severidad sea Alta, EL SISTEMA DEBE mostrar la incidencia al inicio de
   la vista de incidencias abiertas.
2. CUANDO mantenimiento consulte incidencias, EL SISTEMA DEBE permitir ver las
   abiertas de su línea en una sola vista y filtrar por estado y severidad.

### User Story 3 - Dar seguimiento y cerrar una incidencia (Priority: P3)

Como integrante de mantenimiento, quiero cambiar una incidencia a En proceso o
Cerrada para mantener actualizado su seguimiento.

**Why this priority**: Un estado actualizado permite distinguir las fallas que
siguen pendientes de las que ya se atendieron.

**Independent Test**: Mantenimiento actualiza una incidencia y, al cerrarla,
confirma que se registra la fecha de cierre; un supervisor no puede cerrarla.

**Acceptance Scenarios**:

1. CUANDO un usuario con rol Supervisor intente cerrar una incidencia, EL SISTEMA
   DEBE impedirlo.
2. CUANDO alguien cambie el estado a Cerrada, EL SISTEMA DEBE registrar la fecha
   de cierre.
3. CUANDO mantenimiento actualice una incidencia, EL SISTEMA DEBE permitir cambiar
   su estado a En proceso o Cerrada.

### Edge Cases

- Si falta la línea de producción, no se puede guardar la incidencia.
- Si una persona con rol Supervisor intenta cerrar una incidencia, el cierre se
  impide y la incidencia conserva su estado.
- Al volver a consultar una incidencia cerrada, su fecha de cierre debe seguir
  visible y corresponder al momento en que se cerró.
- Si el catálogo no contiene la línea necesaria, debe poder editarse el catálogo
  para agregarla.

## Requirements

### Functional Requirements

- **FR-001**: El sistema DEBE permitir que un supervisor registre una incidencia
  con línea de producción, equipo, severidad y descripción.
- **FR-002**: El sistema DEBE ofrecer un catálogo editable de líneas de producción
  que incluya inicialmente Línea 1, Línea 2 y Línea 3.
- **FR-003**: El dato de equipo DEBE aceptar texto libre.
- **FR-004**: La severidad DEBE permitir los valores Alta, Media y Baja.
- **FR-005**: El sistema DEBE asignar automáticamente un folio y la fecha de
  reporte a cada incidencia.
- **FR-006**: El estado inicial DEBE ser Abierta; mantenimiento DEBE poder cambiar
  el estado a En proceso o Cerrada.
- **FR-007**: El sistema DEBE permitir filtrar incidencias por estado y severidad.
- **FR-008**: Las incidencias de severidad Alta DEBEN aparecer primero en la vista
  de incidencias abiertas.
- **FR-009**: El sistema DEBE permitir a mantenimiento consultar las incidencias
  abiertas de su línea en una sola vista.
- **FR-010**: El rol Supervisor DEBE poder crear y consultar incidencias, pero no
  cerrarlas. El rol Mantenimiento DEBE poder consultar, actualizar y cerrar
  incidencias.
- **FR-011**: Al cambiar el estado de una incidencia a Cerrada, el sistema DEBE
  registrar automáticamente la fecha de cierre.
- **FR-012**: Los formularios, vistas y textos para las personas usuarias DEBEN
  estar en español.

### Key Entities

- **Incidencia**: Una falla que requiere seguimiento. Incluye folio, línea de
  producción, equipo, severidad, descripción, estado, fecha de reporte y fecha de
  cierre.
- **Línea de producción**: Una opción del catálogo editable que identifica la línea
  donde ocurrió la falla. El catálogo inicia con Línea 1, Línea 2 y Línea 3.
- **Rol de usuario**: Define si una persona actúa como Supervisor o como
  Mantenimiento y qué acciones puede realizar.

### Fuera de alcance

- Notificaciones.
- Reportes.
- Fotografías.
- Integraciones externas.

## Success Criteria

### Measurable Outcomes

- **SC-001**: En una prueba con los datos de la incidencia disponibles, un
  supervisor puede completar y registrar una incidencia en menos de 1 minuto.
- **SC-002**: En una prueba, mantenimiento puede ver todas las incidencias abiertas
  de su línea en una sola vista y filtrarlas por estado y severidad.
- **SC-003**: Las cuatro reglas de aceptación de `docs/criterios-ejemplo.md` se
  cumplen al probar la aplicación.
- **SC-004**: Ningún usuario con rol Supervisor puede cerrar una incidencia; cada
  intento de cierre se impide.

## Assumptions

- Las líneas disponibles inicialmente son Línea 1, Línea 2 y Línea 3; una persona
  autorizada puede editar el catálogo.
- El equipo se captura como texto libre.
- Las severidades son Alta, Media y Baja.
- Los estados son Abierta (predeterminado), En proceso y Cerrada.
- El folio y la fecha de reporte se asignan automáticamente; la fecha de cierre se
  registra al cerrar.
- Supervisor puede crear y consultar; Mantenimiento puede consultar, actualizar y
  cerrar.
- El idioma para las personas usuarias es español.
