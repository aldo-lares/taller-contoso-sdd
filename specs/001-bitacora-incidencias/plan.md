# Plan de implementación: Bitácora de incidencias de mantenimiento

**Rama**: `checkpoint-2-plan` | **Fecha**: 2026-10-27 | **Especificación**: [spec.md](spec.md)

**Entrada**: "La solución es una app basada en modelos (model-driven) de Power Apps sobre Dataverse,
construida con el plugin model-apps (/app-builder) en el ambiente del laboratorio,
dentro de la solución de la pareja con su prefijo. Define tablas, columnas,
formularios, vistas, roles de seguridad y mapa del sitio. Respeta la constitución."

## Summary

Crear una app model-driven de Power Apps en Dataverse para registrar y dar
seguimiento a incidencias de mantenimiento. El plugin model-apps (`/app-builder`)
construirá los componentes dentro de la solución de la pareja y su prefijo. El
diseño usa una tabla principal de incidencias y un catálogo editable de líneas,
formularios y vistas en español, dos roles de seguridad y navegación simple. No se
construirá hasta que una persona apruebe el diseño y el plan.

## Contexto técnico

**Idioma/versión**: Textos, formularios y vistas en español; no se agrega código de aplicación en este plan.

**Dependencias principales**: Power Apps model-driven, Dataverse y plugin model-apps (`/app-builder`).

**Almacenamiento**: Tablas de Dataverse dentro de la solución de la pareja en el ambiente del laboratorio.

**Pruebas**: Criterios de aceptación de `spec.md`, vista previa/dry-run del plugin y comprobaciones de la app después de la construcción.

**Plataforma destino**: Power Platform, en el ambiente del laboratorio indicado por la persona participante.

**Tipo de proyecto**: App model-driven de negocio.

**Metas de desempeño**: Un supervisor registra una incidencia en menos de 1 minuto; mantenimiento consulta las incidencias abiertas de su línea en una sola vista.

**Restricciones**: Usar el prefijo de la pareja; no modificar tablas ajenas ni crear servicios fuera de Power Platform; cumplir las políticas de DLP; no incluir integraciones externas, notificaciones ni reportes; aprobación humana antes de construir.

**Escala/alcance**: Una tabla principal, un catálogo editable de líneas con tres valores iniciales, dos roles, formularios y vistas en español.

## Revisión de la constitución

| Principio | Resultado | Aplicación al diseño |
|---|---|---|
| Plataforma Power Platform | Cumple | App model-driven en Dataverse mediante `/app-builder`; no se agregan servicios externos. |
| Solución y nombres | Cumple | Los componentes se crearán en la solución de la pareja y con su prefijo; no se modifican tablas de otras soluciones. |
| Seguridad | Cumple | Supervisor crea y consulta; Mantenimiento consulta, actualiza y cierra; se valida DLP. |
| Simplicidad | Cumple | Una tabla principal más el catálogo de líneas; formularios y vistas en español. |
| Calidad y aprobación | Cumple | Cada historia tiene escenarios verificables; una persona aprueba el diseño y el plan antes de construir. |
| Alcance | Cumple | Sin integraciones externas, notificaciones ni reportes. |

**Resultado de la puerta**: Cumple. No se detectan conflictos con la constitución.

## Diseño de la solución

### Tablas y columnas

El modelo completo, incluidos tipos, obligatoriedad y estados, está en
[data-model.md](data-model.md). Incluye `Incidencia` como tabla principal y `Línea
de producción` como catálogo editable; los nombres lógicos se generarán con el
prefijo de la pareja al construir.

- `Incidencia`: folio automático, línea, equipo de texto libre, severidad,
  descripción, estado, fecha de reporte y fecha de cierre.
- `Línea de producción`: nombre de línea; valores iniciales Línea 1, Línea 2 y
  Línea 3.
- Un flujo de nube de Power Automate dentro de la solución se activa al crear o
  actualizar una incidencia; si el estado es Cerrada y la fecha está vacía, registra
  la fecha y hora actuales. No utiliza conectores externos.

### Formularios

- Formulario principal de incidencia, con folio y fechas de solo lectura y los
  datos del caso agrupados en español.
- Formulario de creación rápida con línea, equipo, severidad y descripción.
- Formulario del catálogo para agregar o editar líneas.

### Vistas

- **Incidencias abiertas**: muestra Abierta y En proceso; prioriza Alta, luego
  Media y Baja, y permite filtrar por línea, estado y severidad.
- **Incidencias abiertas por línea**: permite seleccionar la línea que atiende la
  persona de mantenimiento y consultar sus abiertas en esa misma vista.
- **Todas las incidencias**: permite filtrar por estado y severidad.

### Roles de seguridad

- **Supervisor**: crear y leer incidencias; sin permiso para actualizarlas ni
  cerrarlas.
- **Mantenimiento**: leer y actualizar incidencias, incluso cambiar su estado a
  En proceso o Cerrada.
- El acceso se asigna a identidades de Microsoft Entra ID mediante roles de
  seguridad; no se concede acceso a tablas ajenas.

### Mapa del sitio

- **Incidencias**: Incidencias abiertas, Incidencias abiertas por línea, Todas las
  incidencias.
- **Catálogos**: Líneas de producción.

## Fases de trabajo

### Fase 0: decisiones de diseño

Las decisiones de plataforma, almacenamiento, límites y captura de la fecha de
cierre se documentan en [research.md](research.md). No se necesitan integraciones
externas ni contratos de API.

### Fase 1: diseño y validación

1. Revisar el modelo de datos en [data-model.md](data-model.md).
2. Construir formularios, vistas, roles y mapa del sitio en la solución de la
   pareja, usando el prefijo acordado.
3. Configurar la captura automática de fecha de cierre dentro de la solución.
4. Seguir los escenarios de [quickstart.md](quickstart.md) y verificar los cuatro
   criterios de `docs/criterios-ejemplo.md`.

### Puerta antes de construir

Una persona revisa y aprueba el App Spec y el dry-run del plugin. La construcción
solo puede ocurrir en el ambiente indicado, tras comprobar DLP y que la solución
pertenezca a la pareja. Sin URL de ambiente no se crean recursos.

## Estructura del proyecto

### Documentación de esta funcionalidad

```text
specs/001-bitacora-incidencias/
├── spec.md
├── plan.md
├── research.md
├── data-model.md
├── quickstart.md
├── checklists/requirements.md
└── tasks.md
```

### Componentes de Power Platform

```text
Solución de la pareja (prefijo acordado)
├── App model-driven: Bitácora de incidencias de mantenimiento
├── Tabla: Incidencia
├── Catálogo: Línea de producción
├── Formularios: incidencia, creación rápida y líneas
├── Vistas: abiertas, abiertas por línea y todas
├── Roles: Supervisor y Mantenimiento
├── Flujo: registrar fecha de cierre en Dataverse
└── Mapa del sitio: Incidencias y Catálogos
```

**Decisión de estructura**: La aplicación y sus componentes viven en una única
solución de Dataverse; el repositorio conserva la spec, el diseño, las tareas y la
guía de validación. No se crea una estructura de código fuente ni contratos
externos.

## Complexity Tracking

No hay violaciones de la constitución que requieran justificación.
