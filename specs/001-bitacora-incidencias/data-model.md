# Modelo de datos: Bitácora de incidencias de mantenimiento

Todos los componentes se crean en la solución de la pareja. El prefijo se acuerda
al construir; no se modifica ninguna tabla ajena.

## Tabla principal: Incidencia

| Campo | Tipo de dato | Requerido | Regla |
|---|---|---:|---|
| Folio | Número automático | Sí | Se genera al crear cada incidencia. |
| Línea de producción | Referencia al catálogo de líneas | Sí | No se guarda la incidencia si falta la línea. |
| Equipo | Texto | No definido | Texto libre. |
| Severidad | Opción: Alta, Media, Baja | No definido | Alta aparece primero en la vista de abiertas. |
| Descripción | Texto de varias líneas | No definido | Describe la falla de equipo. |
| Estado | Opción: Abierta, En proceso, Cerrada | Sí | Valor inicial: Abierta. Mantenimiento puede cambiarlo a En proceso o Cerrada. |
| Fecha de reporte | Fecha y hora | Sí | Se registra automáticamente al crear la incidencia. |
| Fecha de cierre | Fecha y hora | No | Se registra al cambiar el estado a Cerrada; no se sobrescribe. |

## Catálogo: Línea de producción

| Campo | Tipo de dato | Regla |
|---|---|---|
| Nombre de línea | Texto | Editable; inicia con Línea 1, Línea 2 y Línea 3. |

## Acceso por rol

| Rol | Crear | Consultar | Actualizar | Cerrar |
|---|---:|---:|---:|---:|
| Supervisor | Sí | Sí | No | No |
| Mantenimiento | No | Sí | Sí | Sí |

Las identidades se administran con Microsoft Entra ID y reciben estos permisos por
roles de seguridad. Las vistas de mantenimiento incluyen un filtro de línea para
mostrar las incidencias abiertas de la línea que atiende la persona.

## Automatización

Un flujo de nube de Power Automate, dentro de la solución y sin conectores
externos, se activa al crear o actualizar una incidencia. Si el estado es Cerrada
y la fecha de cierre está vacía, establece la fecha y hora actuales. Si el flujo
vuelve a activarse después, no cambia una fecha ya registrada.
