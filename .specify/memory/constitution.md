# Constitución del proyecto: Bitácora de incidencias de mantenimiento de Contoso

1. Plataforma: la solución es una app model-driven de Power Apps sobre Dataverse,
   construida con el plugin model-apps en el ambiente del laboratorio. No se crean
   servicios fuera de Power Platform.
2. Solución y nombres: todo se crea dentro de la solución de la pareja, con su
   prefijo. No se modifican tablas de otros.
3. Seguridad: identidad con Microsoft Entra ID; acceso por roles de seguridad
   (Supervisor: crea y consulta; Mantenimiento: consulta, actualiza y cierra);
   se respetan las políticas de DLP.
4. Simplicidad: una tabla principal más catálogos; formularios y vistas en español;
   textos claros para usuarios de planta.
5. Calidad: cada historia tiene criterios de aceptación verificables; el agente no
   se autoaprueba: una persona aprueba el diseño y el plan antes de construir.
6. Alcance: sin integraciones externas, notificaciones ni reportes en esta versión.
