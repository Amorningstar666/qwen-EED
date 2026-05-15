# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por |
|-------|-------|------------|--------------|
| 15/05/2026 | HU-11-04 | Analista de Negocio | Líder Técnico |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica | P17-Apoyo a la Investigación | A41-Incorporación Manual de Expedientes | Funcionalidad Específica | Garantiza que el acto de incorporación de expedientes sea consciente, informado e irreversible mediante una confirmación explícita del funcionario con advertencias claras de las consecuencias jurídicas y registro auditado inmutable |

### Descripción

**¿Quién?** El Funcionario de Instrucción (rol: instructor) o el Procurador Delegado (rol: juez) que ha completado los tres pasos anteriores del asistente de incorporación (selección de expedientes, definición del principal y registro de causales) y está listo para ejecutar la incorporación.

**¿Qué?** Visualiza un resumen completo y detallado de todas las decisiones tomadas en los pasos anteriores (expedientes seleccionados, expediente principal, causales invocadas y justificación), recibe advertencias explícitas sobre el carácter irreversible de la incorporación, y ejecuta la confirmación final mediante un botón de acción crítica con doble factor de validación.

**¿Para qué?** Para asegurar que el funcionario tenga plena conciencia de las consecuencias jurídicas de la incorporación de expedientes antes de ejecutarla, cumpliendo con los principios de seguridad jurídica, buena fe y transparencia administrativa, y generando un registro auditado inmutable que sirva como constancia del acto administrativo de acumulación procesal.

**Referencias Normativas:**
- Ley 1952 de 2019 (Código General Disciplinario), Artículo 188: Acumulación de procesos (efectos de la incorporación).
- Ley 1952 de 2019, Artículo 14: Principios del procedimiento disciplinario (seguridad jurídica, buena fe).
- Ley 1437 de 2011 (Código de Procedimiento Administrativo), Artículo 3: Principio de publicidad y transparencia.
- Ley 2094 de 2021, Artículo 1: Principios rectores de la función disciplinaria.
- Decreto 1069 de 2015: Compilación del Sector Justicia (gestión documental).
- Resolución 000191 de 2021 de la PGN: Lineamientos para la gestión de expedientes disciplinarios.
- Jurisprudencia del Consejo de Estado sobre irreversibilidad de actos procesales de acumulación.

## Dependencias y Precondiciones

1. El usuario debe haber completado exitosamente los Pasos 1, 2 y 3 del asistente de incorporación con: mínimo dos expedientes seleccionados, un expediente principal definido, al menos una causal seleccionada y justificación redactada (mínimo 50 caracteres).
2. Todos los datos de los pasos anteriores deben estar almacenados temporalmente en la sesión del asistente y disponibles para mostrar en el resumen de confirmación.
3. El sistema debe tener acceso a información adicional de cada expediente para mostrar en el resumen: número de folios, cantidad de pruebas allegadas, último movimiento procesal, valor estimado del daño.
4. El módulo de shell corporativo (HU-02) debe mantener la sesión activa del usuario con validación continua de permisos RBAC.
5. Debe existir un componente de generación de acta de incorporación en formato PDF que se crea automáticamente al confirmar la incorporación.
6. El sistema de audit log debe estar operativo y configurado para registrar eventos críticos de incorporación con marca de tiempo, identificación del usuario y huella digital del acto.
7. La interfaz debe mostrar claramente el Paso 4 como activo y los Pasos 1, 2 y 3 como completados en el indicador de pasos.
8. Debe existir un mecanismo de rollback automático en caso de fallo técnico durante el proceso de confirmación para evitar incorporaciones parciales o inconsistentes.

## Restricciones

1. La incorporación es IRREVERSIBLE una vez confirmada; no existe funcionalidad de "deshacer incorporación" salvo mediante acto administrativo motivado de separación de procesos aprobado por el superior jerárquico.
2. El sistema debe mostrar al menos TRES advertencias explícitas sobre la irreversibilidad antes de habilitar el botón de confirmación final.
3. El botón de confirmación debe tener un estado inicial deshabilitado; solo se habilita después de que el usuario marque manualmente un checkbox declarando "He leído y comprendo que esta incorporación es irreversible".
4. El sistema debe requerir autenticación reforzada (reingreso de contraseña o validación biométrica) para ejecutar la confirmación cuando el monto del daño potencial supere los 1000 SMLMV.
5. Una vez confirmada la incorporación, el sistema debe generar automáticamente un acta en PDF con todos los detalles del acto y enviarla por correo institucional al funcionario y a las partes involucradas.
6. El tiempo máximo para completar la confirmación desde que se carga el Paso 4 es de 10 minutos; superado este tiempo sin confirmar, la sesión expira y se pierden los datos.
7. Durante el proceso de confirmación, el sistema debe bloquear cualquier otra actuación sobre los expedientes involucrados para evitar condiciones de carrera.
8. El sistema debe validar en tiempo real que ninguno de los expedientes haya cambiado de estado entre el Paso 1 y el momento de la confirmación (por ejemplo, que no haya sido archivado por otro usuario simultáneamente).
9. La interfaz debe cumplir con los estándares de accesibilidad WCAG 2.1 nivel AA, utilizando tokens de diseño PGN.
10. El registro en audit log debe incluir hash criptográfico de todos los datos de la incorporación para garantizar integridad y no repudio.

## Reglas de Negocio

| ID Regla | Descripción | Fundamento Legal | Prioridad |
|----------|-------------|------------------|-----------|
| RN-11-04-01 | La incorporación es irreversible una vez confirmada | Principio de seguridad jurídica | Crítica |
| RN-11-04-02 | Debe mostrarse mínimo 3 advertencias de irreversibilidad antes de habilitar confirmación | Principio de transparencia | Crítica |
| RN-11-04-03 | El checkbox de "comprendo irreversibilidad" es obligatorio para habilitar botón de confirmar | Principio de consentimiento informado | Crítica |
| RN-11-04-04 | Se requiere autenticación reforzada si el daño potencial supera 1000 SMLMV | Principio de proporcionalidad | Alta |
| RN-11-04-05 | El sistema debe generar acta de incorporación en PDF automáticamente tras la confirmación | Art. 188 Ley 1952/2019 | Alta |
| RN-11-04-06 | El audit log debe registrar hash criptográfico de todos los datos de incorporación | Principio de integridad | Alta |
| RN-11-04-07 | Debe validarse que ningún expediente haya cambiado de estado entre el inicio y la confirmación | Principio de consistencia | Alta |
| RN-11-04-08 | El sistema debe notificar por correo a todas las partes la incorporación ejecutada | Principio de publicidad | Media |
| RN-11-04-09 | El tiempo máximo de permanencia en Paso 4 es 10 minutos | Política de seguridad | Media |
| RN-11-04-10 | Debe existir mecanismo de rollback en caso de fallo técnico durante confirmación | Principio de atomicidad | Media |

## Supuestos

1. Se asume que el funcionario ha revisado cuidadosamente toda la información mostrada en el resumen antes de proceder a la confirmación.
2. Se asume que el funcionario comprende plenamente las consecuencias jurídicas de la incorporación irreversible de expedientes.
3. Se asume que el sistema cuenta con mecanismos de almacenamiento seguro para el acta de incorporación generada en PDF.
4. Se asume que不存在 conflictos de concurrencia donde múltiples usuarios intenten incorporar los mismos expedientes simultáneamente.
5. Se asume que el servicio de correo institucional está operativo para enviar las notificaciones automáticas de incorporación.
6. Se asume que el funcionario tiene acceso a su dispositivo de autenticación reforzada (token, biometría) cuando sea requerido.

## Criterios de Aceptación

### Escenario 1: Visualización completa del resumen de incorporación

**Dado** que he completado los Pasos 1, 2 y 3 del asistente de incorporación  
**Cuando** avanzo al Paso 4 (Confirmación)  
**Entonces** el sistema muestra un resumen detallado con: lista de expedientes seleccionados con sus radicados y disciplinados, expediente principal resaltado visualmente, causales seleccionadas con descripciones completas, justificación redactada en texto íntegro  
**Y** muestra información adicional: número total de folios acumulados, cantidad de pruebas, último movimiento procesal de cada expediente  
**Y** el resumen se presenta en formato de tarjetas colapsables organizadas por secciones  
**Y** el título del paso indica: "Revise cuidadosamente y confirme la incorporación"  

**Evidencia:** Captura de pantalla mostrando resumen completo con 3 expedientes, principal resaltado, 2 causales y justificación de 150 caracteres.

### Escenario 2: Visualización de advertencias de irreversibilidad

**Dado** que estoy visualizando el resumen del Paso 4  
**Cuando** hago scroll hacia la parte inferior del modal  
**Entonces** el sistema muestra tres advertencias consecutivas con iconos de alerta rojos (#E3201B):  
1. "ADVERTENCIA: La incorporación de expedientes es un acto procesal IRREVERSIBLE"  
2. "Una vez confirmada, solo podrá separar los expedientes mediante acto administrativo motivado del superior jerárquico"  
3. "Al confirmar, usted acepta plena responsabilidad jurídica por esta decisión"  
**Y** cada advertencia tiene fondo rojo claro (#FEF2F2) y borde rojo sólido  
**Y** debajo de las advertencias se muestra el checkbox obligatorio: "He leído y comprendo que esta incorporación es irreversible"  

**Evidencia:** Captura de pantalla mostrando las 3 advertencias apiladas verticalmente con estilos visuales distintivos.

### Escenario 3: Intento de confirmación sin marcar checkbox de comprensión

**Dado** que estoy en el Paso 4 sin haber marcado el checkbox de "He leído y comprendo"  
**Cuando** intento hacer clic en el botón "Confirmar Incorporación"  
**Entonces** el botón permanece deshabilitado (color gris, cursor not-allowed)  
**Y** al pasar el cursor, se muestra tooltip: "Debe marcar la casilla de comprensión para continuar"  
**Y** el checkbox muestra borde rojo temporalmente durante 2 segundos  
**Y** se aplica animación de vibración al contenedor de advertencias  

**Evidencia:** Captura de pantalla con botón "Confirmar Incorporación" en estado disabled y checkbox sin marcar.

### Escenario 4: Habilitación del botón de confirmación tras marcar checkbox

**Dado** que estoy en el Paso 4 y marco el checkbox de "He leído y comprendo que esta incorporación es irreversible"  
**Cuando** el checkbox cambia a estado marcado  
**Entonces** el sistema habilita inmediatamente el botón "Confirmar Incorporación"  
**Y** el botón cambia de color gris a amarillo institucional (#FFE601) con texto en azul (#063853)  
**Y** se aplica animación de pulso suave al botón durante 3 segundos para llamar la atención  
**Y** el checkbox muestra ícono de check verde (#33FFCC)  

**Evidencia:** Captura de pantalla mostrando checkbox marcado y botón "Confirmar Incorporación" en estado enabled con colores institucionales.

### Escenario 5: Confirmación exitosa con generación de acta PDF

**Dado** que he marcado el checkbox de comprensión y el botón "Confirmar Incorporación" está habilitado  
**Cuando** hago clic en el botón "Confirmar Incorporación"  
**Entonces** el sistema muestra modal de procesamiento con spinner y mensaje: "Procesando incorporación. Por favor espere..."  
**Y** genera automáticamente un acta de incorporación en formato PDF con todos los detalles del acto  
**Y** registra en audit log: "Incorporación ejecutada por [usuario] el [timestamp] con hash [hash_criptográfico]"  
**Y** envía correo electrónico de notificación al funcionario y a las partes involucradas  
**Y** muestra mensaje de éxito: "Incorporación ejecutada exitosamente. Acta enviada a su correo institucional"  
**Y** cierra el asistente y redirige al dashboard del expediente principal  

**Evidencia:** Secuencia de capturas mostrando modal de procesamiento, mensaje de éxito y correo de notificación recibido.

### Escenario 6: Requerimiento de autenticación reforzada por alto valor del daño

**Dado** que el valor estimado del daño acumulado en los expedientes supera los 1000 SMLMV  
**Cuando** hago clic en el botón "Confirmar Incorporación" después de marcar el checkbox  
**Entonces** el sistema interrumpe el flujo y muestra modal de autenticación reforzada  
**Y** solicita: "Por seguridad, debe reingresar su contraseña institucional para confirmar esta incorporación de alto valor"  
**Y** ofrece opciones alternativas: token hardware, validación biométrica o código SMS  
**Y** si la autenticación es exitosa, continúa con el proceso de confirmación  
**Y** si falla la autenticación 3 veces consecutivas, bloquea la incorporación y registra evento de seguridad  

**Evidencia:** Captura de pantalla del modal de autenticación reforzada con campos de entrada.

### Escenario 7: Error por cambio de estado de expediente durante confirmación

**Dado** que inicié el asistente con el expediente "2025-009876" en estado "Activo"  
**Cuando** otro usuario archiva ese expediente mientras yo estoy en el Paso 4  
**Y** intento confirmar la incorporación  
**Entonces** el sistema detecta la inconsistencia mediante validación en tiempo real  
**Y** muestra mensaje de error: "Error: El expediente 2025-009876 ha cambiado de estado a 'Archivado'. No es posible continuar con la incorporación"  
**Y** resalta en rojo el expediente problemático dentro del resumen  
**Y** ofrece opciones: "Reiniciar asistente" o "Continuar sin este expediente"  
**Y** registra el evento en audit log como "Conflicto de concurrencia en incorporación"  

**Evidencia:** Captura de pantalla con mensaje de error y expediente resaltado en rojo.

### Escenario 8: Generación y descarga de acta de incorporación

**Dado** que he confirmado exitosamente la incorporación de tres expedientes  
**Cuando** el sistema genera el acta de incorporación en PDF  
**Entonces** el acta incluye: encabezado institucional PGN, número de acta único, fecha y hora exactas, identificación completa del funcionario, lista de expedientes incorporados con metadata completa, expediente principal designado, causales invocadas, justificación íntegra, hash criptográfico de integridad  
**Y** el PDF tiene marca de agua "DOCUMENTO OFICIAL - EXPEDIENTE ELECTRÓNICO DISCIPLINARIO"  
**Y** el archivo se nombra siguiendo patrón: "ACTA_INCORPORACION_[radicado_principal]_[fecha].pdf"  
**Y** se adjunta automáticamente al correo de notificación enviado a las partes  
**Y** queda almacenada en el repositorio documental del expediente principal  

**Evidencia:** Captura de pantalla del PDF generado mostrando todas las secciones requeridas.

### Escenario 9: Notificación por correo a partes involucradas

**Dado** que se ha confirmado exitosamente una incorporación de expedientes  
**Cuando** el sistema ejecuta el proceso de notificación  
**Entonces** envía correos electrónicos a: funcionario instructor, procurador delegado, disciplinados (si tienen correo registrado), apoderados (si están registrados), superior jerárquico del funcionario  
**Y** el asunto del correo es: "Notificación de Incorporación de Expedientes - Radicado [número]"  
**Y** el cuerpo del correo incluye: resumen de expedientes incorporados, expediente principal designado, causales invocadas, fecha de ejecución, enlace para descargar acta completa  
**Y** el correo tiene firma institucional automatizada de la PGN  
**Y** se registra en audit log el envío de cada correo con timestamp y estado de entrega  

**Evidencia:** Captura de pantalla de correo electrónico recibido con todos los elementos descritos.

### Escenario 10: Rollback automático por fallo técnico durante confirmación

**Dado** que estoy en el proceso de confirmación de incorporación  
**Cuando** ocurre un fallo técnico crítico (caída de base de datos, timeout de conexión, error de servidor)  
**Entonces** el sistema ejecuta automáticamente un rollback de todas las operaciones parciales realizadas  
**Y** muestra mensaje de error: "Ha ocurrido un error técnico durante la confirmación. La incorporación NO se ha ejecutado. Por favor intente nuevamente"  
**Y** ninguna modificación se ha persistido en la base de datos (atomicidad garantizada)  
**Y** se registra el fallo en audit log como "Rollback ejecutado por fallo técnico en incorporación"  
**Y** se notifica automáticamente al equipo de soporte técnico para investigación del incidente  

**Evidencia:** Captura de pantalla del mensaje de error con rollback confirmado y registro en audit log.

### Escenario 11: Timeout de sesión por exceder tiempo máximo en Paso 4

**Dado** que permanezco 10 minutos en el Paso 4 sin confirmar ni interactuar  
**Cuando** intento realizar cualquier acción (marcar checkbox o hacer clic en botones)  
**Entonces** el sistema muestra modal de "Sesión Expirada"  
**Y** indica: "Ha superado el tiempo máximo de 10 minutos en este paso. Por seguridad, debe reiniciar el proceso de incorporación"  
**Y** todas las selecciones previas se pierden  
**Y** soy redirigido al dashboard del expediente principal  
**Y** se registra el evento en audit log como "Timeout de sesión en Paso 4 de incorporación"  

**Evidencia:** Captura de pantalla del modal de sesión expirada y registro en audit log.

### Escenario 12: Imposibilidad de navegación directa a otros módulos durante confirmación

**Dado** que estoy en el Paso 4 del asistente de incorporación con el botón de confirmación habilitado  
**Cuando** intento navegar directamente a otro módulo del sistema mediante URL manipulation o clic en menú lateral  
**Entonces** el sistema bloquea la navegación y muestra modal de advertencia  
**Y** indica: "Tiene una incorporación pendiente de confirmación. Debe confirmar o cancelar antes de navegar a otro módulo"  
**Y** ofrece opciones: "Volver al asistente" o "Cancelar incorporación y salir"  
**Y** si selecciono "Cancelar incorporación", se pierden todas las selecciones previas  
**Y** se registra el intento de navegación bloqueada en audit log  

**Evidencia:** Captura de pantalla del modal de bloqueo de navegación.

## Prototipo / Anexos

- **Prototipo de pantalla:** `/workspace/Pantallas VEED/11_incorporacion_manual.html`
- **Componentes específicos del paso 4 (Resumen y Confirmación):**
  - Resumen en tarjetas colapsables (líneas 1035-1090)
  - Sección de advertencias de irreversibilidad (líneas 647-683)
  - Checkbox de comprensión obligatoria
  - Botón de confirmación con estados disabled/enabled
  - Modal de procesamiento con spinner
- **Tokens de diseño PGN aplicados:**
  - Fuente: Montserrat (títulos de advertencia), Poppins (texto de resumen)
  - Color de error: #E3201B (Rojo institucional para advertencias)
  - Color de acción: #FFE601 (Amarillo institucional para botón de confirmación)
  - Color de fondo advertencia: #FEF2F2 (Rojo muy claro)
  - Color de éxito: #33FFCC (Verde azulado para checkbox marcado)
- **Referencias a líneas del prototipo HTML:**
  - Paso 4: Resumen y confirmación (líneas 1035-1114)
  - Estilos de advertencia (líneas 647-683)
  - Botón de confirmación (estilos genéricos btn-success)
- **Anexo técnico:** Documento de especificación de generación de acta PDF y hash criptográfico (en elaboración)

## Stakeholders

| Rol | Nombre/Dependencia | Responsabilidad | Firma Requerida |
|-----|-------------------|-----------------|-----------------|
| Product Owner | Dirección de Investigación Disciplinaria | Definición de contenido de acta | Sí |
| Líder Técnico | Oficina de Sistemas - PGN | Validación de mecanismos de seguridad | Sí |
| Funcionario Instructor | Procuraduría Delegada para la Investigación | Usuario primario, responsable jurídico del acto | Sí |
| Jefe de Grupo | Grupo de Gestión Procesal | Supervisor de incorporaciones ejecutadas | Sí |
| Área Jurídica | Oficina Asesora Jurídica | Validación de advertencias legales | Sí |
| Oficina de Control Interno | OCI-PGN | Auditoría de registros de incorporación | Sí |
| Archivista Central | Grupo de Gestión Documental | Custodia de actas generadas | Sí |
| Equipo de Seguridad | Oficina de Seguridad TI | Validación de hash criptográfico y audit log | Sí |

## Plan de Validación

| Tipo de Prueba | Responsable | Fecha Estimada | Criterio de Aprobación |
|----------------|-------------|----------------|------------------------|
| Prueba de visualización completa de resumen | Equipo de Desarrollo | 25/05/2026 | Todos los datos de pasos anteriores visibles correctamente |
| Prueba de advertencias de irreversibilidad | QA Lead | 30/05/2026 | Mínimo 3 advertencias visibles antes de habilitar confirmación |
| Prueba de habilitación condicional de botón | QA Lead | 01/06/2026 | Botón solo se habilita tras marcar checkbox obligatorio |
| Prueba de generación de acta PDF | Equipo de Desarrollo | 03/06/2026 | PDF generado con todos los campos requeridos y hash válido |
| Prueba de autenticación reforzada | Security Team | 05/06/2026 | Requiere validación adicional cuando daño > 1000 SMLMV |
| Prueba de detección de cambios de estado concurrentes | QA Lead | 06/06/2026 | Detecta 100% de cambios de estado entre inicio y confirmación |
| Prueba de rollback automático por fallos | Equipo de Desarrollo | 08/06/2026 | Rollback ejecutado correctamente en 100% de fallos simulados |
| Prueba de notificaciones por correo | QA Lead | 09/06/2026 | Correos enviados a todas las partes con contenido correcto |
| Validación jurídica de advertencias | Oficina Asesora Jurídica | 10/06/2026 | Certificación de conformidad legal de advertencias |
| UAT (User Acceptance Testing) | Funcionarios Instructor | 15/06/2026 | Aprobación formal por parte de 5 usuarios clave |

## Matriz de Trazabilidad con Referencias Normativas

| Artículo | Norma | Descripción | Implementación en Sistema | Estado de Cumplimiento |
|----------|-------|-------------|--------------------------|------------------------|
| Art. 188 | Ley 1952/2019 | Efectos de la acumulación de procesos | Irreversibilidad de incorporación implementada | ✅ Cumple |
| Art. 14 | Ley 1952/2019 | Seguridad jurídica y buena fe | Advertencias explícitas garantizan consentimiento informado | ✅ Cumple |
| Art. 3 | Ley 1437/2011 | Publicidad y transparencia | Notificaciones a todas las partes y acta descargable | ✅ Cumple |
| Art. 1 | Ley 2094/2021 | Principios rectores | Interfaz clara con validaciones previas a confirmación | ✅ Cumple |
| Art. 76 | Ley 1952/2019 | Funciones del instructor | Registro auditado con hash criptográfico del acto | ✅ Cumple |
| Art. 115 | Ley 1952/2019 | Reserva de actuaciones | Acceso restringido al acta según RBAC | ✅ Cumple |

## Notas Adicionales

- Esta HU-11-04 cubre exclusivamente el **Paso 4: Resumen y Confirmación Irreversible**.
- El hash criptográfico debe generarse utilizando algoritmo SHA-256 sobre todos los datos de la incorporación concatenados en orden específico.
- El acta PDF debe ser firmada digitalmente con certificado electrónico de la PGN para garantizar autenticidad.
- En futuras iteraciones, se podría implementar integración con blockchain para registro inmutable descentralizado de incorporaciones.
- El sistema debe prevenir ataques de doble gasto (double-spend) donde un usuario intente confirmar la misma incorporación dos veces mediante manipulación de requests.
