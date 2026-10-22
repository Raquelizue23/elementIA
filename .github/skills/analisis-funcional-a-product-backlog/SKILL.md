---
name: analisis-funcional-a-product-backlog
description: 'Analiza documentación funcional y genera o refina un product backlog en español usando una plantilla. Úsala para analizar alcances, requisitos, especificaciones, casos de uso o documentos funcionales; identificar épicas, historias, reglas de negocio, criterios de aceptación, dependencias, riesgos y preguntas abiertas.'
argument-hint: 'Indica los documentos fuente, la plantilla y el archivo de salida.'
---

# Análisis funcional a Product Backlog

Convierte documentación funcional en un backlog trazable, verificable y útil para refinamiento con negocio y desarrollo.

## Cuándo usarla

- Analizar uno o varios documentos de alcance o requisitos.
- Crear un product backlog a partir de una plantilla existente.
- Revisar un backlog y detectar omisiones, ambigüedades o trazabilidad débil.

## Procedimiento

1. Identifica los documentos fuente, la plantilla solicitada y el destino. Si el usuario no indica plantilla, usa [la plantilla incluida](./assets/plantilla-product-backlog.md). Si proporciona una plantilla propia, conserva sus secciones, columnas, idioma y convenciones; no la sustituyas por la incluida.
2. Inspecciona el contenido disponible de todas las fuentes. Si un formato no puede leerse con las herramientas disponibles, informa la limitación y solicita una versión legible; no completes el análisis suponiendo su contenido.
3. Extrae objetivos, usuarios/actores, alcance, exclusiones, requisitos, flujos, reglas de negocio, datos, integraciones, restricciones, requisitos no funcionales y decisiones pendientes. Registra para cada elemento su fuente y referencia (sección, identificador o página cuando esté disponible).
4. Consolida duplicados y contradicciones. Mantén las contradicciones visibles como preguntas o decisiones pendientes; no elijas una interpretación sin evidencia.
5. Organiza el trabajo en épicas y elementos de backlog con granularidad útil para estimación. Usa historias en formato «Como [actor], quiero [capacidad], para [beneficio]» cuando aplique. Conserva como funcionalidad, tarea técnica o requisito no funcional los elementos que no sean historias de usuario.
6. Escribe criterios de aceptación observables y comprobables, preferentemente en formato Dado/Cuando/Entonces. Incluye escenarios alternos y validaciones relevantes que estén respaldados por las fuentes.
7. Asigna identificadores estables y únicos dentro del documento. Expresa dependencias mediante esos identificadores y verifica que no existan referencias rotas ni ciclos evidentes.
8. Separa explícitamente la certeza de cada dato: «Confirmado» solo cuando la fuente lo afirma; «Propuesto» para recomendaciones del análisis; «Pendiente» para información no definida o que requiere validación. No inventes valores, reglas, prioridades ni contratos de integración.
9. Sugiere prioridad únicamente como propuesta y explica brevemente el fundamento (valor, urgencia, riesgo o dependencia). Cuando falte información para priorizar, marca «Pendiente de priorizar».
10. Completa las secciones de reglas, requisitos no funcionales, riesgos, supuestos, preguntas abiertas e información faltante. Evita duplicar una regla como requisito salvo que la relación aporte claridad.
11. Revisa cobertura y consistencia: cada elemento relevante de la fuente debe quedar representado o anotado como excluido/no accionable; cada requisito debe tener origen; los criterios deben ser comprobables; preguntas abiertas deben señalar qué decisión bloquean.
12. Entrega el resultado en el formato de la plantilla. No sobrescribas documentos fuente ni una plantilla existente: crea un archivo nuevo salvo que el usuario pida expresamente actualizar uno. Al final, resume archivos analizados, limitaciones, elementos propuestos y decisiones que requieren validación.

## Criterios de calidad

- Trazabilidad: cada requisito del backlog remite a una fuente identificable.
- Fidelidad: distingue texto explícito, interpretación y recomendación.
- Completitud: cubre actores, flujos principales y alternos, reglas, integraciones, datos y requisitos no funcionales presentes en las fuentes.
- Verificabilidad: criterios y resultados esperados se pueden comprobar sin interpretaciones subjetivas.
- Transparencia: ambigüedades, conflictos, dependencias externas e información ausente permanecen visibles.
- Usabilidad: usa términos del dominio, evita duplicados y mantiene una granularidad que permita discutir, estimar y priorizar.

## Convenciones de análisis

- No conviertas cada requisito textual en una historia independiente si varios forman una capacidad coherente; conserva la referencia a todos los requisitos que cubre.
- No inventes personas, reglas, campos obligatorios, estados, métricas, plazos, límites ni comportamiento de integraciones.
- No marques una propuesta como confirmada. Prioridad, valor de negocio y criterios inferidos deben quedar identificados como propuestas para validar.
- Mantén la plantilla y los términos del usuario, incluso si difieren de las convenciones de la plantilla incluida.
- Si la documentación no permite definir criterios de aceptación completos, registra lo que sí está sustentado y formula preguntas concretas para cerrar la brecha.