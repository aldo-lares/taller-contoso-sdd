# Guía de validación: Bitácora de incidencias

Esta guía se ejecuta en el ambiente del laboratorio después de que una persona
apruebe el App Spec y el dry-run. No crees recursos en otro ambiente.

## Prerrequisitos

- Acceso al ambiente de Power Platform autorizado para el laboratorio.
- La solución de la pareja y su prefijo acordado.
- Una cuenta con rol Supervisor y otra con rol Mantenimiento.
- Las líneas Línea 1, Línea 2 y Línea 3 en el catálogo.

## Escenarios

1. **Registro**: con la cuenta Supervisor, crea una incidencia con línea, equipo,
   severidad y descripción. Comprueba que se asignen folio, fecha de reporte y
   estado Abierta, y que el registro pueda completarse en menos de 1 minuto.
2. **Línea obligatoria**: intenta guardar una incidencia sin línea. Comprueba que
   no se guarde.
3. **Consulta y prioridad**: con la cuenta Mantenimiento, abre la vista de
   incidencias abiertas, filtra la línea que atiende y comprueba que las de
   severidad Alta aparezcan primero. Usa filtros de estado y severidad.
4. **Permisos**: con Supervisor, intenta cerrar una incidencia. Comprueba que no
   sea posible. Con Mantenimiento, cambia una incidencia a En proceso y luego a
   Cerrada.
5. **Fecha de cierre**: comprueba que al cerrar se registre la fecha de cierre y
   que permanezca igual al modificar posteriormente otro dato.
6. **Idioma**: confirma que los formularios, vistas y mensajes estén en español.

## Resultado esperado

Los cuatro criterios de `docs/criterios-ejemplo.md` pasan y mantenimiento puede
consultar las incidencias abiertas de su línea en una sola vista.
