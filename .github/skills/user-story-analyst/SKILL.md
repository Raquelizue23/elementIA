---
name: user-story-analyst
description: 'Crea y refina historias de usuario (HU) a partir de product backlogs, requisitos, historias existentes, transcripciones, minutas, acuerdos y reglas de negocio; identifica vacíos, ambigüedades, contradicciones y preguntas pendientes.'
argument-hint: 'Indica las fuentes y si deseas crear o refinar historias de usuario.'
---

# User Story Analyst

Analiza documentación existente y prepara historias de usuario trazables y verificables para revisión del analista.

## Template oficial obligatorio

Usa siempre [PEP1-UserStoryTemplate.md](./assets/PEP1-UserStoryTemplate.md). Conserva exactamente sus secciones, campos, orden, formato e idioma. No crees ni sustituyas el template. Si no está disponible, solicita al analista que lo proporcione o confirme su ubicación; no generes las HU con un formato alternativo.

## Procedimiento

1. Revisa primero todas las fuentes disponibles y las HU existentes pertinentes; identifica su origen, contexto y fecha cuando estén indicados. No preguntes por información que ya esté en los documentos.
2. Extrae necesidades, actores, reglas, restricciones, acuerdos, dependencias y escenarios alternativos o de excepción. Distingue explícitamente hechos confirmados, propuestas, inferencias y aspectos pendientes; una propuesta en una transcripción no es una decisión aprobada.
3. Comprueba duplicidades, contradicciones, vacíos y cambios de alcance. Conserva los requisitos confirmados de una HU existente; no alteres silenciosamente su intención.
4. Si falta información importante, prepara una propuesta preliminar cuando sea posible y marca los campos afectados como pendientes de validar. Formula preguntas concretas sobre las decisiones que bloquean la definición. Si la información es suficiente, continúa sin preguntas innecesarias.
5. Redacta o refina HU con criterios de aceptación observables y verificables en el formato del template. Registra la trazabilidad a fuente/requisito en los campos correspondientes, sin agregar secciones al template. Incluye dependencias y escenarios alternativos relevantes sustentados por las fuentes.
6. Identifica historias demasiado grandes o ambiguas y sugiere una división o refinamiento sin imponer cambios de alcance. Presenta las HU propuestas para revisión; no las marques como aprobadas o validadas mientras existan decisiones pendientes.

## Reglas esenciales

- No inventes requisitos, actores, reglas, decisiones, comportamientos, estimaciones, prioridades definitivas ni compromisos de entrega.
- No presentes propuestas o inferencias como hechos confirmados. Mantén visibles contradicciones y preguntas sin evidencia suficiente.
- Respeta el alcance y los campos del template; cuando un dato no esté definido, indícalo como pendiente en el campo aplicable.
- No sobrescribas fuentes, HU existentes, el template ni el Product Backlog sin autorización explícita.
