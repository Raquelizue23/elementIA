# Product Backlog — Remarketing Tool

## A. Resumen del producto

| Aspecto | Descripción |
|--------|-------------|
| **Problema que se desea resolver** | Falta de una herramienta centralizada que permita gestionar el ciclo de vida completo de las solicitudes de remarketing de unidades, desde su creación, validación, asignación de patios y pickups, gestión documental, órdenes de trabajo, seguimiento, hasta el cierre y depuración histórica. |
| **Objetivo del producto** | Construir el módulo **Remarketing Tool** que integre y automatice la operación regular e histórica de solicitudes de remarketing, reutilizando los mecanismos de seguridad, catálogos y bitácora de la plataforma existente, e integrándose con servicios externos (Collateral, DMS, APIs ELEMENT). |
| **Usuarios principales** | Usuarios operativos del área de remarketing (creación y modificación), administradores / supervisores (tracking, validación, cierre), sistema (procesos batch de validación y depuración). |
| **Alcance conocido** | Gestión de solicitudes de remarketing, unidades, patios, pickups, documentos/placas/bajas, órdenes de trabajo, pantalla única de administración y tracking, exportación XLSX/PDF, cierre de solicitudes y depuración histórica. |
| **Exclusiones** | Mecanismos de gestión de usuarios, perfiles, menús, control de acceso, catálogos generales, bitácora de eventos y reglas de configuración/patios (se reutilizan sin cambios de la plataforma base). |
| **Indicadores de éxito** | Reducción de tiempos de gestión de solicitudes, trazabilidad completa del ciclo de vida, disminución de errores manuales, visibilidad centralizada vía pantalla única de tracking. |

---

## B. Product Backlog

| ID | Épica | Título | Tipo | Historia o descripción | Valor de negocio | Criterios de aceptación | Prioridad sugerida | Dependencias | Estado de análisis | Preguntas abiertas |
|----|-------|--------|------|------------------------|------------------|-------------------------|-------------------|--------------|--------------------|--------------------|
| PB-001 | Operación Regular del Sistema | Gestionar solicitudes de remarketing | Funcionalidad | Agrupa las funciones de búsqueda, alta, modificación y cancelación de solicitudes de remarketing conforme a reglas de configuración y control por perfil. | Habilita el proceso base del negocio; sin esto no existen las solicitudes. | Dado un usuario autenticado, cuando accede a la opción de menú, entonces puede buscar, crear y modificar solicitudes aplicando filtros y validaciones. La cancelación actualiza el estatus y bloquea modificaciones futuras. | Alta | Reutilización de autenticación, perfiles y catálogos de la plataforma base. | Confirmado | ¿Cuáles son los estados válidos de una solicitud y sus transiciones? |
| PB-002 | Operación Regular del Sistema | Buscar solicitudes de remarketing | Historia | Como usuario de remarketing, quiero buscar solicitudes previamente registradas con filtros y según mi perfil, para localizar rápidamente la información que necesito gestionar. | Reduce el tiempo de localización de casos y respeta el control de acceso por perfil. | Dado que existen solicitudes registradas, cuando el usuario aplica filtros y confirma, entonces el sistema muestra solo las solicitudes permitidas para su perfil. | Media | PB-001 | Confirmado | ¿Cuáles son los filtros obligatorios y cuáles opcionales? |
| PB-003 | Operación Regular del Sistema | Dar de alta una nueva solicitud de remarketing | Historia | Como usuario de remarketing, quiero registrar una nueva solicitud de remarketing capturando cliente, flota y datos de cabecera, para iniciar el proceso de remarketing. | Inicia el ciclo de vida del negocio; alimenta todas las demás funcionalidades. | Dado un usuario con permisos, cuando completa los datos obligatorios y guarda, entonces el sistema valida, persiste la solicitud y la muestra en la lista. | Alta | PB-001, API.ELEMENT.Buscar Clientes, API.ELEMENT.Buscar Flotas. | Confirmado | ¿Qué datos de cabecera son obligatorios? ¿Existe numeración automática? |
| PB-004 | Operación Regular del Sistema | Modificar / cancelar una solicitud de remarketing | Historia | Como usuario de remarketing, quiero modificar o cancelar una solicitud existente, para corregir información o detener el proceso. | Mantiene la integridad de la información y permite la corrección de errores. | Dado una solicitud en estatus editable, cuando el usuario modifica o cancela, entonces el sistema valida, actualiza y, en caso de cancelación, bloquea futuras modificaciones. | Alta | PB-003 | Confirmado | ¿Quién puede cancelar? ¿Se requiere motivo de cancelación? |
| PB-005 | Operación Regular del Sistema | Gestionar unidades de una solicitud | Funcionalidad | Agrupa el alta/modificación manual y la carga masiva de unidades (VINs) asociadas a una solicitud de remarketing. | Permite asociar el inventario de unidades a procesar. | Dado una solicitud existente, cuando el usuario agrega, edita o carga unidades, entonces el sistema valida duplicados, formato y límites, y actualiza la lista de unidades. | Alta | PB-003, API.ELEMENT.Buscar VINs. | Confirmado | ¿Cuál es el layout exacto del archivo de carga masiva? |
| PB-006 | Operación Regular del Sistema | Dar de alta / modificar unidades en lista | Historia | Como usuario de remarketing, quiero mantener la lista de unidades de una solicitud, para agregar o corregir VINs individuales. | Flexibilidad en la administración del inventario de unidades. | Dado una solicitud con unidades, cuando el usuario agrega o edita un VIN, entonces el sistema valida su existencia y actualiza la lista. | Media | PB-005 | Confirmado | ¿Se valida que el VIN no esté en otra solicitud activa? |
| PB-007 | Operación Regular del Sistema | Cargar masivamente unidades | Historia | Como usuario de remarketing, quiero cargar un archivo con hasta 1000 unidades, para poblar rápidamente la lista de una solicitud. | Acelera la captura de volumen y reduce errores manuales. | Dado una solicitud sin unidades, cuando se selecciona un archivo válido y se confirma, entonces el sistema valida layout y contenido, carga las unidades y reporta errores si los hay. Rechaza archivos con errores o solicitudes que ya tengan unidades. | Media | PB-005 | Confirmado | ¿Dónde se define el layout y las reglas de validación del archivo? |
| PB-008 | Operación Regular del Sistema | Validar solicitudes de remarketing | Historia | Como sistema, quiero ejecutar un proceso batch que valide todas las solicitudes activas contra reglas de negocio y genere notificaciones, para asegurar la calidad de los datos y detectar observaciones. | Garantiza calidad de datos y automatiza alertas tempranas. | Dado que existen solicitudes activas, cuando el batch se ejecuta, entonces verifica catálogos, reglas de configuración, reglas de patios, genera notificaciones de observaciones y actualiza estatus. | Alta | PB-005, PB-009 (asignación de patios), reglas de configuración y patios. | Confirmado | ¿Con qué frecuencia se ejecuta el batch? ¿Quién configura las reglas? |
| PB-009 | Operación Regular del Sistema | Asignar / desasignar patio a unidad | Historia | Como usuario de remarketing, quiero asignar o desasignar un patio a cada unidad de una solicitud, manualmente o conforme a reglas, para definir dónde se procesará la unidad. | Define la ubicación operativa de cada unidad. | Dado una solicitud con unidades, cuando el usuario asigna/desasigna un patio, entonces el sistema valida contra reglas de asignación y actualiza el patio de la unidad. | Media | PB-005, API.ELEMENT.Buscar Proveedores, reglas de asignación de patios. | Confirmado | ¿Una misma unidad puede cambiar de patio múltiples veces? |
| PB-010 | Operación Regular del Sistema | Programar / reprogramar pick up de unidad | Historia | Como usuario de remarketing, quiero programar o reprogramar la fecha de pick up de una unidad, para coordinar la recolección con el patio. | Coordina la logística física del proceso. | Dado una unidad con patio asignado, cuando el usuario programa/reprograma el pick up, entonces el sistema valida, actualiza la fecha y notifica por correo. | Media | PB-009, API.ELEMENT.Enviar correo. | Confirmado | ¿Se envía notificación al patio, al cliente o a ambos? |
| PB-011 | Operación Regular del Sistema | Gestionar documentos, placas y bajas de unidad | Historia | Como usuario de remarketing, quiero registrar y modificar documentos, placas y bajas de una unidad, para mantener la documentación requerida actualizada. | Cumple con requisitos documentales y legales del proceso. | Dado una unidad de una solicitud, cuando el usuario registra/modifica documentos, placas o bajas, entonces el sistema interactúa con DMS y actualiza los registros. | Media | PB-005, API.ELEMENT.DMS.Buscar Documentos, API.ELEMENT.DMS.Registrar Documento. | Confirmado | ¿Qué tipos de documentos son obligatorios? |
| PB-012 | Operación Regular del Sistema | Relacionar orden de trabajo (OT) a solicitud | Historia | Como usuario de remarketing, quiero solicitar la generación de una OT en Collateral para una solicitud, para dar seguimiento a los trabajos requeridos. | Integra el proceso con el sistema de taller/servicio. | Dado una solicitud lista para OT, cuando el usuario solicita la creación, entonces el sistema invoca a Collateral, almacena la OT relacionada y notifica por correo. | Alta | PB-003, API.ELEMENT.Solicitar creación de una OT, API.ELEMENT.Enviar correo. | Confirmado | ¿Cuándo y quién decide que una solicitud requiere OT? |
| PB-013 | Operación Regular del Sistema | Pantalla única de administración y tracking | Historia | Como usuario de remarketing, quiero visualizar en una pantalla tabular el estado de las solicitudes y sus unidades con filtros y columnas clave, para tener visibilidad completa del proceso. | Visibilidad operativa y toma de decisiones. | Dado un usuario con permisos, cuando accede a la pantalla única, entonces ve columnas de VIN, unidad, cliente, estatus, proveedor, patio, fechas, documentos, OT, bajas/placas, sold date, usuario y última actualización, aplicando filtros y control por perfil. | Alta | PB-002, PB-008, PB-012. | Confirmado | ¿Se permite ordenar y paginar? ¿Cuál es el límite de registros mostrados? |
| PB-014 | Operación Regular del Sistema | Exportar vista de tracking a XLSX | Historia | Como usuario de remarketing, quiero descargar la vista actual de la pantalla única en un archivo Excel, para analizarla fuera del sistema. | Facilita análisis externo y reportes. | Dado una vista filtrada en la pantalla única, cuando el usuario selecciona exportar a XLSX, entonces se genera y descarga el archivo con los datos visibles. | Baja | PB-013 | Confirmado | ¿Se exportan todos los registros filtrados o solo la página actual? |
| PB-015 | Operación Regular del Sistema | Exportar vista de tracking a PDF | Historia | Como usuario de remarketing, quiero descargar la vista actual de la pantalla única en un archivo PDF, para compartir o archivar un reporte. | Facilita reportes formales y compartir información. | Dado una vista filtrada en la pantalla única, cuando el usuario selecciona exportar a PDF, entonces se genera y descarga el archivo con los datos visibles. | Baja | PB-013 | Confirmado | ¿Se aplica formato de reporte (logo, encabezados)? |
| PB-016 | Operación Regular del Sistema | Dar de alta registro de cierre | Historia | Como usuario de remarketing, quiero registrar el cierre de una solicitud y/o de sus unidades, para finalizar el proceso de remarketing. | Cierra el ciclo de vida y libera recursos. | Dado una solicitud en estatus cerrable, cuando el usuario captura los datos de cierre, entonces el sistema valida y actualiza los registros de cierre de la solicitud/unidades. | Media | PB-003, PB-005. | Confirmado | ¿Qué condiciones deben cumplirse para permitir el cierre? |
| PB-017 | Operación Histórica del Sistema | Depurar solicitudes históricas de remarketing | Historia | Como sistema, quiero ejecutar un proceso batch que inactiva solicitudes antiguas según reglas de depuración, para mantener limpio el histórico y mejorar el rendimiento. | Limpieza de datos históricos y mantenimiento de rendimiento. | Dado solicitudes activas, cuando el batch de depuración se ejecuta, entonces aplica las reglas definidas, inactiva las solicitudes que correspondan y actualiza la base de datos. | Baja | PB-001, PB-008 (reglas de depuración por definir). | Propuesto | ¿Cuáles son las reglas exactas de depuración? ¿Con qué frecuencia se ejecuta? |

---

## C. Reglas de negocio

| ID | Descripción | Origen | Elementos afectados | Estado de validación |
|----|-------------|--------|---------------------|----------------------|
| RN-001 | Una solicitud enviada a Remarketing Tool no puede modificarse en Xcelerate. | Documento de alcance | Solicitudes de Remarketing | Confirmado |
| RN-002 | El archivo de carga masiva de unidades está limitado a 1000 unidades. | RF-002, carga masiva | Carga masiva de unidades | Confirmado |
| RN-003 | El archivo de carga masiva debe estar 100% correcto para ser aceptado; de lo contrario se rechaza completo. | RF-002, carga masiva | Carga masiva de unidades | Confirmado |
| RN-004 | No se permite carga masiva de unidades en solicitudes que ya tengan unidades asignadas. | RF-002, carga masiva | Carga masiva de unidades | Confirmado |
| RN-005 | La pantalla única de tracking filtra y muestra información según el perfil del usuario. | RF-008 | Pantalla única de administración y tracking | Confirmado |
| RN-006 | El proceso batch de validación genera una notificación por cada solicitud con observaciones detectadas. | RF-003 | Validación de solicitudes, notificaciones | Confirmado |

---

## D. Requisitos no funcionales

| ID | Necesidad | Justificación | Criterio medible | Estado de validación |
|----|-----------|---------------|------------------|----------------------|
| RNF-001 | Seguridad y control de acceso | Reutilizar mecanismos existentes de autenticación, perfiles y control de acceso a datos. | Solo usuarios autorizados con el perfil adecuado pueden ejecutar funciones y ver datos. | Confirmado |
| RNF-002 | Integridad de datos | La bitácora de eventos debe ser inalterable y confiable. | Toda acción relevante queda registrada en bitácora sin posibilidad de modificación. | Confirmado |
| RNF-003 | Disponibilidad de procesos batch | Los batch de validación y depuración deben ejecutarse sin intervención manual. | Configuración de frecuencia y ejecución automática documentada. | Pendiente de validar |
| RNF-004 | Rendimiento de carga masiva | Cargar hasta 1000 unidades de manera eficiente. | Tiempo de carga y validación menor a 5 minutos para 1000 registros (umbral propuesto). | Propuesto |
| RNF-005 | Escalabilidad de pantalla única | La pantalla de tracking puede crecer en volumen de datos. | Paginación, filtros indexados y límite de registros configurable. | Propuesto |

---

## E. Riesgos, supuestos y preguntas abiertas

### Riesgos
- **R-001:** Las APIs ELEMENT / Collateral no están disponibles o cambian de contrato, bloqueando las integraciones.
- **R-002:** Las reglas de configuración de solicitudes y patios no están definidas, lo que retrasa la implementación de validaciones y asignaciones automáticas.
- **R-003:** El volumen de datos históricos puede afectar el rendimiento de la pantalla única si no se aplican filtros y paginación desde el inicio.

### Supuestos por confirmar
- **S-001:** Los mecanismos de seguridad, catálogos, perfiles y bitácora de la plataforma base están operativos y no requieren cambios.
- **S-002:** Las entidades del modelo de dominio listadas en el documento ya existen o serán creadas sin cambios en sus definiciones base.
- **S-003:** Los servicios externos (Collateral, DMS, APIs ELEMENT) responden con los datos y formatos esperados.

### Decisiones pendientes
- **D-001:** Definir estados y transiciones de una solicitud de remarketing.
- **D-002:** Definir reglas exactas de depuración histórica y frecuencia de ejecución.
- **D-003:** Definir layout y reglas de validación del archivo de carga masiva de unidades.
- **D-004:** Definir política de notificaciones (destinatarios, plantillas, eventos que las disparan).

### Información faltante
- Catálogo de estados de solicitud.
- Reglas de configuración de solicitudes y de asignación de patios.
- Layout del archivo de carga masiva.
- Reglas de depuración histórica.
- Definición de perfiles y permisos específicos para este módulo.

---

## F. Recomendaciones

1. **Aclarar primero:** los estados del ciclo de vida de una solicitud y sus transiciones, ya que impactan en alta, modificación, cancelación, validación, cierre y depuración.
2. **Refinar:** las reglas de configuración de solicitudes y de asignación de patios, porque son insumos críticos para las historias PB-008, PB-009 y PB-017.
3. **Dependencia potencialmente bloqueante:** la disponibilidad y contrato de las APIs ELEMENT y Collateral; conviene validarlas con los equipos propietarios antes de comenzar las historias de integración (PB-007, PB-010, PB-011, PB-012).
4. **Decisión del Product Owner:** priorizar entre la pantalla única de tracking (visibilidad) y las integraciones con Collateral / DMS (operación), según el objetivo de entrega más valioso.
5. **Validación técnica:** revisar si el modelo de datos propuesto ya existe o requiere ajustes, especialmente para entidades como patios, pickups, órdenes de trabajo y registros de cierre.
