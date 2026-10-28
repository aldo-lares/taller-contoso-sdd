# Taller: Spec Kit-driven Development con Power Platform Skills

Este repositorio es el punto de partida del taller práctico de Contoso. Está pensado
para personas que no son desarrolladoras: avanzaremos paso a paso, con instrucciones
claras y decisiones de negocio antes de construir.

## El caso

Contoso necesita una bitácora de incidencias de mantenimiento para las líneas de
producción de sus plantas. Los supervisores registran fallas de equipo y el equipo
de mantenimiento les da seguimiento.

## El flujo

Con Spec Kit iremos de la idea a una aplicación revisada:

**constitución → spec → clarify → plan → tareas → construir → verificar**

La persona participante aprueba el diseño y el plan antes de construir.

## Dónde vive cada cosa

- `.specify/memory/constitution.md`: principios y límites del proyecto.
- `.github/copilot-instructions.md`: instrucciones para el asistente.
- `docs/plantilla-spec.md`: guía para describir el problema y el comportamiento esperado.
- `docs/criterios-ejemplo.md`: ejemplos de criterios de aceptación comprobables.
- `specs/<carpeta-de-la-feature>/spec.md`: qué necesita el usuario y por qué.
- `specs/<carpeta-de-la-feature>/plan.md`: cómo se implementará la solución.
- `specs/<carpeta-de-la-feature>/tasks.md`: trabajo dividido en tareas.
- `docs/app-de-respaldo.md`: estado de la app de respaldo del taller.

La rama `main` contiene solo este punto de partida; no incluye una spec, un plan ni
tareas de la feature.

## Puntos de rescate

Si te quedas atrás, crea una sesión nueva en la rama que corresponda:

- `checkpoint-1-spec`: la spec ya está lista.
- `checkpoint-2-plan`: el plan y las tareas ya están listos.
- `checkpoint-3-app`: checkpoint final del taller.

Al crear una copia desde esta plantilla, debes marcar **Include all branches**
(«Incluir todas las ramas») para que también se copien los puntos de rescate.
