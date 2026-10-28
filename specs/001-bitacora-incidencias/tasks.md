# Tareas: Bitácora de incidencias de mantenimiento

**Entrada**: Documentos de diseño de `/specs/001-bitacora-incidencias/`

**Prerequisitos**: `plan.md`, `spec.md`, `research.md`, `data-model.md` y `quickstart.md`

**Organización**: Las tareas se agrupan por historia de usuario para poder revisar
cada entrega por separado.

**Formato**: `- [ ] T### [P?] [US#?] Descripción con ruta de referencia`

- **[P]**: La tarea se puede realizar en paralelo con otra tarea marcada [P].
- **[US#]**: La historia de usuario a la que pertenece la tarea.
- Cada tarea apunta al documento que define los datos o el resultado esperado.

## Fase 1: Preparación

**Propósito**: Confirmar el ambiente y aprobar el diseño antes de construir.

- [ ] T001 Confirmar el URL del ambiente del laboratorio, la solución de la pareja, el prefijo acordado y el cumplimiento de DLP según `specs/001-bitacora-incidencias/quickstart.md`.
- [ ] T002 Revisar el App Spec y el dry-run de `/app-builder` y obtener aprobación humana antes de crear componentes, conforme a `specs/001-bitacora-incidencias/plan.md`.

---

## Fase 2: Base compartida

**Propósito**: Preparar los datos, los permisos y la navegación que necesitan las historias.

- [ ] T003 [P] Crear el catálogo editable Línea de producción con Línea 1, Línea 2 y Línea 3 según `specs/001-bitacora-incidencias/data-model.md`.
- [ ] T004 Crear la tabla Incidencia y sus campos, tipos y valores iniciales según `specs/001-bitacora-incidencias/data-model.md`.
- [ ] T005 [P] Crear los roles Supervisor y Mantenimiento con los permisos definidos en `specs/001-bitacora-incidencias/data-model.md`.
- [ ] T006 Crear la app model-driven y el mapa del sitio con las áreas Incidencias y Catálogos según `specs/001-bitacora-incidencias/plan.md`.

**Punto de revisión**: La tabla principal, el catálogo, los roles y la navegación están listos en la solución de la pareja.

---

## Fase 3: Historia 1 - Registrar una incidencia (Prioridad: P1)

**Objetivo**: Permitir que Supervisor registre una falla con sus datos principales.

**Prueba independiente**: Con Supervisor, guardar una incidencia completa en menos de 1 minuto; confirmar folio, fecha y estado Abierta; intentar guardar sin línea y confirmar que no se guarde.

- [ ] T007 [P] Crear el formulario principal de incidencia en español con los campos y el orden definidos en `specs/001-bitacora-incidencias/data-model.md`.
- [ ] T008 [P] Crear el formulario de creación rápida en español con línea, equipo, severidad y descripción según `specs/001-bitacora-incidencias/plan.md`.
- [ ] T009 Configurar la línea como obligatoria, el folio y la fecha de reporte automáticos, y el estado inicial Abierta según `specs/001-bitacora-incidencias/data-model.md`.

**Punto de revisión**: Supervisor puede registrar una incidencia y los datos automáticos aparecen sin captura manual.

---

## Fase 4: Historia 2 - Consultar incidencias (Prioridad: P2)

**Objetivo**: Ayudar a Supervisor y Mantenimiento a encontrar incidencias por estado, severidad y línea.

**Prueba independiente**: Con Mantenimiento, abrir una sola vista, filtrar las incidencias abiertas de su línea y comprobar que las de severidad Alta aparezcan primero.

- [ ] T010 [P] Crear la vista Incidencias abiertas con filtros por línea, estado y severidad, ordenando Alta antes que Media y Baja según `specs/001-bitacora-incidencias/plan.md`.
- [ ] T011 [P] Crear la vista Todas las incidencias con filtros por estado y severidad según `specs/001-bitacora-incidencias/spec.md`.

**Punto de revisión**: Mantenimiento encuentra las incidencias abiertas de su línea en una sola vista.

---

## Fase 5: Historia 3 - Dar seguimiento y cerrar una incidencia (Prioridad: P3)

**Objetivo**: Permitir a Mantenimiento actualizar el estado y registrar cuándo se cerró una incidencia.

**Prueba independiente**: Con Mantenimiento, cambiar una incidencia a En proceso y luego a Cerrada; confirmar la fecha de cierre. Con Supervisor, intentar cerrar una incidencia y confirmar que la acción se impide.

- [ ] T012 [P] Crear en la solución un flujo de nube de Power Automate que, al detectar una incidencia Cerrada sin fecha de cierre, guarde la fecha y hora actuales, siguiendo `specs/001-bitacora-incidencias/data-model.md`.
- [ ] T013 Configurar la actualización de estado para que Mantenimiento pueda seleccionar En proceso o Cerrada y Supervisor no pueda actualizar ni cerrar, según `specs/001-bitacora-incidencias/plan.md`.

**Punto de revisión**: Solo Mantenimiento puede cerrar y la fecha queda registrada una sola vez.

---

## Fase 6: Revisión final

**Propósito**: Verificar que la solución respeta los criterios, el idioma y los límites acordados.

- [ ] T014 Ejecutar los escenarios de `specs/001-bitacora-incidencias/quickstart.md` y verificar los cuatro criterios de `docs/criterios-ejemplo.md`.
- [ ] T015 Revisar que formularios, vistas y mapa del sitio estén en español y que la solución no use conectores externos, conforme a `specs/001-bitacora-incidencias/plan.md`.
- [ ] T016 Ejecutar las comprobaciones disponibles de la app y confirmar que los componentes están en la solución de la pareja y respetan DLP según `specs/001-bitacora-incidencias/quickstart.md`.

---

## Dependencias y orden de ejecución

### Dependencias entre fases

- **Preparación**: T001 precede a T002; no se crean componentes antes de la aprobación.
- **Base compartida**: depende de T002 y bloquea las historias.
- **Historias de usuario**: empiezan cuando la base compartida está lista. Pueden planearse por separado, pero se construyen en la misma solución y deben coordinarse.
- **Revisión final**: depende de las tres historias.

### Dependencias entre tareas

- T003 y T005 pueden avanzar en paralelo después de T002.
- T004 depende de T003 porque Incidencia referencia el catálogo de líneas.
- T006 depende de T004 y T005.
- T007, T008 y T009 dependen de T004 y T006.
- T010 y T011 dependen de T004 y T006.
- T012 depende de T004; T013 depende de T005 y T006.
- T014, T015 y T016 dependen de que las historias estén listas.

### Oportunidades para trabajar en paralelo

- Base compartida: crear el catálogo de líneas (T003) y los roles (T005) en paralelo.
- Historia 1: el formulario principal (T007) y el formulario de creación rápida (T008) son componentes distintos.
- Historia 2: las vistas de abiertas (T010) y todas (T011) son componentes distintos.
- Historia 3: el flujo de fecha de cierre (T012) es independiente de la configuración de permisos y estado (T013).

## Ejemplo de trabajo paralelo

Después de aprobar el diseño y antes de crear la tabla principal:

1. Preparar el catálogo `Línea de producción` según `specs/001-bitacora-incidencias/data-model.md`.
2. Preparar los roles Supervisor y Mantenimiento según `specs/001-bitacora-incidencias/data-model.md`.

## Estrategia de implementación

### MVP

La primera entrega es la Historia 1: registro de incidencias con línea obligatoria,
folio, fecha de reporte y estado inicial. Debe pasar su prueba independiente antes
de continuar.

### Entrega incremental

1. Completar preparación y base compartida.
2. Entregar registro de incidencias (Historia 1) y validarlo.
3. Agregar consultas y filtros (Historia 2) y validarlos.
4. Agregar seguimiento y cierre (Historia 3) y validarlos.
5. Ejecutar la revisión final de los criterios, DLP e idioma.

## Notas

- Las tareas describen componentes de Power Platform; las rutas de referencia
  apuntan a los documentos que especifican su diseño.
- No crear la app ni sus componentes hasta tener URL del ambiente y aprobación del
  App Spec y el dry-run.
