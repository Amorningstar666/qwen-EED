# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por |
|-------|-------|------------|--------------|
| 15/05/2026 | HU-11-05 | Analista de Negocio | Líder Técnico |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica | P17-Apoyo a la Investigación | A41-Incorporación Manual de Expedientes | Funcionalidad Transversal | Proporciona asistencia contextual inteligente mediante procuradurIA durante todo el proceso de incorporación, garantizando trazabilidad ética de las sugerencias de IA y manteniendo al funcionario como único responsable de las decisiones procesales |

### Descripción

**¿Quién?** El Funcionario de Instrucción (rol: instructor) o el Procurador Delegado (rol: juez) que está utilizando el asistente de incorporación de expedientes y requiere asistencia contextual en cualquiera de los cuatro pasos del flujo.

**¿Qué?** Interactúa con el botón flotante de procuradurIA ubicado en la esquina inferior derecha de la pantalla para solicitar sugerencias, validaciones, redacción asistida o aclaraciones conceptuales relacionadas con la incorporación de expedientes, recibiendo respuestas contextualizadas que quedan registradas en un audit log especializado de interacciones con IA.

**¿Para qué?** Para brindar apoyo inteligente al funcionario durante el proceso de incorporación, mejorando la calidad de las decisiones mediante sugerencias basadas en normativa vigente, patrones históricos de incorporaciones aprobadas y validaciones de coherencia jurídica, siempre manteniendo el principio ético fundamental de que la IA nunca decide actos procesales, solo asiste con trazabilidad completa.

**Referencias Normativas:**
- Ley 1952 de 2019 (Código General Disciplinario), Artículo 76: Funciones de los funcionarios de instrucción (responsabilidad indelegable).
- Ley 1952 de 2019, Artículo 14: Principios del procedimiento disciplinario (responsabilidad del decisor).
- Ley 1581 de 2012: Protección de datos personales (tratamiento de datos en interacciones con IA).
- Decreto 1069 de 2015: Compilación del Sector Justicia.
- Lineamientos de Gobierno Digital: Uso ético de inteligencia artificial en entidades públicas.
- Documento CONPES 3975: Estrategia de Inteligencia Artificial para Colombia.
- Circular 003 de 2024 de la PGN: Lineamientos para el uso de herramientas de IA en procesos disciplinarios.

## Dependencias y Precondiciones

1. El módulo de procuradurIA debe estar operativo y configurado con el modelo de lenguaje especializado en derecho disciplinario colombiano.
2. El usuario debe estar autenticado en el sistema EED con rol válido ("Funcionario de Instrucción" o "Procurador Delegado").
3. El sistema de audit log debe estar configurado con una tabla especializada para registrar interacciones con IA, incluyendo: timestamp, identificación del usuario, contexto de la solicitud, sugerencia proporcionada, decisión final del usuario.
4. El botón flotante de procuradurIA debe estar visible y accesible en todas las pantallas del asistente de incorporación (líneas 147-192 del prototipo HTML).
5. Debe existir un mecanismo de rate limiting para prevenir abuso del servicio de IA (máximo 20 consultas por sesión de incorporación).
6. El sistema debe mantener contexto de la conversación durante toda la sesión de incorporación, permitiendo referencias a mensajes anteriores.
7. La interfaz del chat de procuradurIA debe cumplir con los estándares de accesibilidad WCAG 2.1 nivel AA.
8. Debe existir un descargo de responsabilidad visible que indique claramente: "procuradurIA es un asistente. Usted es el único responsable de las decisiones procesales".

## Restricciones

1. procuradurIA NUNCA puede tomar decisiones procesales; solo proporciona sugerencias que el funcionario puede aceptar, modificar o rechazar.
2. Todas las interacciones con procuradurIA quedan registradas en audit log inmutable con marca de tiempo, identificación del usuario y hash de integridad.
3. El sistema debe mostrar explícitamente que las sugerencias de IA son eso, sugerencias, y no constituyen actos administrativos ni vinculantes.
4. procuradurIA no tiene acceso a información reservada de otros expedientes no relacionados con la incorporación actual.
5. El tiempo máximo de respuesta de procuradurIA es de 5 segundos; superado este tiempo, debe mostrarse mensaje de timeout.
6. procuradurIA debe negarse cortésmente a responder preguntas fuera del contexto jurídico-disciplinario (política, religión, temas personales).
7. El sistema debe detectar y registrar intentos de ingeniería de prompts donde el usuario intente hacer que la IA tome decisiones en lugar de solo sugerir.
8. Las sugerencias de procuradurIA deben citar siempre las fuentes normativas en las que se basan (artículos específicos del CGD).
9. La interfaz debe cumplir con los estándares de accesibilidad WCAG 2.1 nivel AA, utilizando tokens de diseño PGN.
10. No se permite que procuradurIA genere texto completo de actos administrativos; solo puede generar borradores de justificaciones que requieren edición sustancial por el funcionario.

## Reglas de Negocio

| ID Regla | Descripción | Fundamento Legal | Prioridad |
|----------|-------------|------------------|-----------|
| RN-11-05-01 | procuradurIA nunca decide actos procesales, solo sugiere | Art. 76 Ley 1952/2019 (responsabilidad indelegable) | Crítica |
| RN-11-05-02 | Todas las interacciones con IA se registran en audit log especializado | Principio de trazabilidad | Crítica |
| RN-11-05-03 | Debe mostrarse descargo de responsabilidad en cada interacción | Principio de transparencia | Crítica |
| RN-11-05-04 | procuradurIA debe citar fuentes normativas específicas en sus sugerencias | Principio de motivación | Alta |
| RN-11-05-05 | El sistema debe detectar y registrar intentos de ingeniería de prompts | Política de seguridad de IA | Alta |
| RN-11-05-06 | Rate limiting: máximo 20 consultas por sesión de incorporación | Política de uso razonable | Media |
| RN-11-05-07 | Tiempo máximo de respuesta: 5 segundos | Política de usabilidad | Media |
| RN-11-05-08 | procuradurIA debe negarse a responder preguntas fuera de contexto jurídico-disciplinario | Política de especialización | Media |
| RN-11-05-09 | No se permite generación de actos administrativos completos, solo borradores editables | Circular 003/2024 PGN | Media |
| RN-11-05-10 | El funcionario puede calificar la utilidad de cada sugerencia (útil/no útil) | Mejora continua del modelo | Baja |

## Supuestos

1. Se asume que el funcionario comprende que procuradurIA es una herramienta de asistencia y que la responsabilidad jurídica de las decisiones recae exclusivamente en él.
2. Se asume que el modelo de IA ha sido entrenado con normativa disciplinaria colombiana vigente y jurisprudencia relevante del Consejo de Estado.
3. Se asume que不存在 sesgos discriminatorios en las sugerencias de procuradurIA respecto a tipos de faltas, disciplinados o contextos geográficos.
4. Se asume que el sistema cuenta con mecanismos de actualización periódica del conocimiento de procuradurIA cuando hay cambios normativos.
5. Se asume que el funcionario tiene conectividad adecuada para interactuar en tiempo real con el servicio de IA.

## Criterios de Aceptación

### Escenario 1: Acceso al asistente procuradurIA desde cualquier paso del asistente

**Dado** que estoy en cualquiera de los 4 pasos del asistente de incorporación  
**Cuando** hago clic en el botón flotante amarillo (#FFE601) de procuradurIA en la esquina inferior derecha  
**Entonces** se abre un panel de chat deslizante desde la derecha  
**Y** muestra un mensaje de bienvenida contextualizado al paso actual  
**Y** muestra el descargo de responsabilidad: "Soy procuradurIA, tu asistente jurídico. Tus decisiones son tuyas, yo solo sugiero"  
**Y** el historial de la conversación actual se mantiene si ya había interagido antes  

**Evidencia:** Captura de pantalla del panel de chat abierto desde el Paso 1 mostrando mensaje de bienvenida específico de búsqueda de expedientes.

### Escenario 2: Solicitud de sugerencia de causales aplicables en Paso 3

**Dado** que estoy en el Paso 3 (Causales y Justificación) sin haber seleccionado causales  
**Cuando** escribo en el chat: "¿Qué causales me recomiendas para incorporar estos expedientes?"  
**Entonces** procuradurIA analiza los expedientes seleccionados en el Paso 1  
**Y** responde: "Basado en los expedientes seleccionados, le sugiero considerar: 1) Mismos hechos - si versan sobre idénticos acontecimientos (Art. 188 CGD), 2) Conexidad - si los hechos están relacionados (Art. 188 CGD)"  
**Y** cita explícitamente: "Fundamento: Artículo 188 de la Ley 1952 de 2019"  
**Y** añade descargo: "Recuerde que usted debe verificar que estas causales apliquen al caso concreto"  
**Y** registra en audit log: "Usuario solicitó sugerencia de causales. Sugeridas: Mismos hechos, Conexidad. Timestamp: [fecha]"  

**Evidencia:** Captura de pantalla del chat mostrando sugerencia con citas normativas y descargo.

### Escenario 3: Solicitud de redacción asistida de justificación en Paso 3

**Dado** que he seleccionado la causal "Conexidad" en el Paso 3  
**Cuando** escribo: "Ayúdame a redactar una justificación para conexidad"  
**Entonces** procuradurIA responde: "Claro. Aquí tienes un borrador que debes editar: 'Se incorporan los expedientes [radicados] porque los hechos investigados guardan relación de conexidad probatoria y fáctica, específicamente [DESCRIBIR RELACIÓN ESPECÍFICA]. Esta acumulación garantiza economía procesal y evita fallos contradictorios.' IMPORTANTE: Debes completar la relación específica entre los hechos"  
**Y** muestra advertencia: "Este es un borrador. Debes editarlo sustancialmente antes de confirmar"  
**Y** ofrece botón "Insertar en formulario" que copia el texto al textarea del Paso 3  
**Y** registra en audit log: "Usuario solicitó borrador de justificación. Borrador generado e insertado"  

**Evidencia:** Captura de pantalla mostrando borrador generado con advertencia y botón de inserción.

### Escenario 4: Intento de hacer que procuradurIA tome decisión procesal

**Dado** que estoy en el Paso 4 (Confirmación)  
**Cuando** escribo: "¿Debo confirmar esta incorporación o no?"  
**Entonces** procuradurIA responde: "No puedo tomar esa decisión por ti. La incorporación de expedientes es un acto procesal de tu exclusiva responsabilidad como funcionario. Te sugiero revisar: 1) Que las causales aplican realmente, 2) Que la justificación es suficiente, 3) Que has verificado todos los datos en el resumen"  
**Y** muestra recordatorio: "Artículo 76 CGD: El funcionario es responsable de sus decisiones"  
**Y** registra en audit log: "INTENTO DETECTADO: Usuario solicitó que IA tome decisión. Bloqueado y educado sobre responsabilidad"  
**Y** notifica al supervisor de ética de IA sobre el intento  

**Evidencia:** Captura de pantalla mostrando respuesta de negativa educativa y registro en audit log.

### Escenario 5: Consulta sobre fundamento normativo de una causal

**Dado** que estoy en el Paso 3  
**Cuando** escribo: "¿En qué artículo se basa la causal de mismos hechos?"  
**Entonces** procuradurIA responde: "La causal de 'Mismos hechos' se fundamenta en el Artículo 188 de la Ley 1952 de 2019 (Código General Disciplinario), que establece: 'Podrán acumularse los procesos que versen sobre los mismos hechos...' Además, la jurisprudencia del Consejo de Estado ha señalado que..."  
**Y** proporciona enlace a texto completo del artículo en biblioteca jurídica digital  
**Y** registra en audit log: "Usuario consultó fundamento normativo de causal 'Mismos hechos'"  

**Evidencia:** Captura de pantalla mostrando cita textual del artículo y enlace a biblioteca.

### Escenario 6: Timeout por superar tiempo máximo de respuesta de IA

**Dado** que el servicio de procuradurIA presenta latencia elevada  
**Cuando** envío una consulta y transcurren más de 5 segundos sin respuesta  
**Entonces** el sistema muestra mensaje: "procuradurIA está tomando más tiempo de lo esperado. Por favor espera o intenta nuevamente en unos momentos"  
**Y** muestra spinner de carga animado  
**Y** si supera 15 segundos, muestra: "Timeout: No pudimos obtener respuesta. Verifica tu conexión o intenta después"  
**Y** registra en audit log: "Timeout en respuesta de procuradurIA. Consulta: [texto truncado]"  

**Evidencia:** Captura de pantalla mostrando mensaje de timeout y spinner.

### Escenario 7: Rechazo de pregunta fuera de contexto jurídico-disciplinario

**Dado** que escribo en el chat: "¿Qué opinas de la situación política actual en Colombia?"  
**Cuando** procuradurIA detecta que la pregunta está fuera de su dominio especializado  
**Entonces** responde: "Solo puedo asistirte en temas relacionados con derecho disciplinario y procesos de la PGN. No puedo opinar sobre temas políticos. ¿Hay algo en lo que pueda ayudarte con tu incorporación de expedientes?"  
**Y** registra en audit log: "PREGUNTA FUERA DE CONTEXTO: Usuario preguntó sobre política. Redirigido a tema jurídico"  
**Y** si el usuario insiste 3 veces en temas fuera de contexto, bloquea temporalmente el chat por 5 minutos  

**Evidencia:** Captura de pantalla mostrando respuesta de rechazo cortés.

### Escenario 8: Calificación de utilidad de sugerencia proporcionada

**Dado** que procuradurIA me ha proporcionado una sugerencia de justificación  
**Cuando** hago clic en los botones de calificación (👍 útil / 👎 no útil) debajo de la respuesta  
**Entonces** el sistema registra mi calificación asociada a esa interacción específica  
**Y** si califico como "no útil", abre campo opcional: "¿Por qué no fue útil? (respuesta muy genérica, error jurídico, otro)"  
**Y** utiliza esta retroalimentación para mejorar futuras sugerencias del modelo  
**Y** registra en audit log: "Usuario calificó sugerencia como [útil/no útil]. Feedback: [texto opcional]"  

**Evidencia:** Captura de pantalla mostrando botones de calificación y campo de feedback.

### Escenario 9: Mantenimiento de contexto conversacional entre múltiples consultas

**Dado** que he hecho tres consultas previas a procuradurIA en esta sesión  
**Cuando** escribo: "¿Y qué pasa con eso que mencionaste antes sobre la conexidad?"  
**Entonces** procuradurIA mantiene contexto de la conversación previa  
**Y** responde haciendo referencia a lo discutido anteriormente: "Retomando lo que comentamos sobre la conexidad, te recordaba que..."  
**Y** el historial completo de la conversación permanece visible en el panel de chat  
**Y** puedo hacer scroll para revisar mensajes anteriores  
**Y** al cerrar el chat y volver a abrirlo, el historial se mantiene (mientras dure la sesión de incorporación)  

**Evidencia:** Captura de pantalla mostrando hilo conversacional de 5 intercambios con contexto mantenido.

### Escenario 10: Rate limiting al exceder máximo de consultas por sesión

**Dado** que he realizado 20 consultas a procuradurIA en esta sesión de incorporación  
**Cuando** intento hacer una consulta número 21  
**Entonces** el sistema muestra mensaje: "Has alcanzado el límite de 20 consultas para esta sesión de incorporación. Si necesitas asistencia adicional, contacta a la Oficina Asesora Jurídica"  
**Y** deshabilita el campo de entrada del chat  
**Y** ofrece botón "Cerrar chat"  
**Y** registra en audit log: "RATE LIMIT EXCEDIDO: Usuario realizó 20 consultas. Chat bloqueado"  

**Evidencia:** Captura de pantalla mostrando mensaje de límite alcanzado y campo deshabilitado.

### Escenario 11: Visualización de trazabilidad completa de interacciones con IA

**Dado** que soy auditor de Control Interno revisando una incorporación específica  
**Cuando** accedo al audit log de la incorporación  
**Entonces** puedo visualizar una sección especializada "Interacciones con procuradurIA"  
**Y** veo lista cronológica de todas las interacciones: timestamp, consulta del usuario, sugerencia de IA, decisión final del usuario (aceptada/modificada/rechazada)  
**Y** puedo exportar este registro en formato PDF para informe de auditoría  
**Y** cada registro incluye hash criptográfico para garantizar integridad  

**Evidencia:** Captura de pantalla del audit log mostrando sección de interacciones con IA.

### Escenario 12: Detección de sesgo potencial en sugerencia de procuradurIA

**Dado** que procuradurIA genera una sugerencia que podría interpretarse como sesgada  
**Cuando** el sistema de monitoreo ético detecta patrones de lenguaje potencialmente discriminatorios  
**Entonces** añade nota automática a la respuesta: "Nota: Esta sugerencia ha sido marcada para revisión ética. Verifica que se ajuste a principios de igualdad y no discriminación"  
**Y** registra en audit log: "ALERTA ÉTICA: Sugerencia marcada para revisión. Motivo: [patrón detectado]"  
**Y** notifica automáticamente al comité de ética de IA de la PGN  
**Y** permite al usuario reportar explícitamente sesgo percibido mediante botón "Reportar sesgo"  

**Evidencia:** Captura de pantalla mostrando nota de alerta ética y botón de reporte.

## Prototipo / Anexos

- **Prototipo de pantalla:** `/workspace/Pantallas VEED/11_incorporacion_manual.html`
- **Componentes específicos de procuradurIA:**
  - Botón flotante circular amarillo (líneas 147-192)
  - Tooltip "Sugerencia asistida por IA" (línea 1461)
  - Panel de chat deslizante (implementación JavaScript líneas 1449-1476)
- **Tokens de diseño PGN aplicados:**
  - Color del botón: #FFE601 (Amarillo institucional PGN)
  - Icono: Sparkles/IA (28x28px)
  - Animación hover: scale(1.08) con sombra elevada
- **Referencias a líneas del prototipo HTML:**
  - Botón flotante procuradurIA (líneas 1449-1476)
  - Estilos del trigger (líneas 147-192)
  - Tooltip (líneas 173-191)
- **Anexo técnico:** Documento de especificación de arquitectura de procuradurIA, políticas de ética de IA y formato de audit log especializado (en elaboración)

## Stakeholders

| Rol | Nombre/Dependencia | Responsabilidad | Firma Requerida |
|-----|-------------------|-----------------|-----------------|
| Product Owner | Dirección de Investigación Disciplinaria | Definición de políticas de uso de IA | Sí |
| Líder Técnico | Oficina de Sistemas - PGN | Implementación técnica de procuradurIA | Sí |
| Especialista en Ética de IA | Oficina Asesora Jurídica | Supervisión de cumplimiento de lineamientos éticos | Sí |
| Funcionario Instructor | Procuraduría Delegada para la Investigación | Usuario primario, responsable de decisiones | Sí |
| Oficina de Control Interno | OCI-PGN | Auditoría de trazabilidad de interacciones con IA | Sí |
| Delegado de Protección de Datos | PGN | Cumplimiento de Ley 1581 de 2012 en interacciones con IA | Sí |
| Equipo de Seguridad TI | Oficina de Seguridad | Prevención de ingeniería de prompts y abusos | Sí |

## Plan de Validación

| Tipo de Prueba | Responsable | Fecha Estimada | Criterio de Aprobación |
|----------------|-------------|----------------|------------------------|
| Prueba de acceso contextual desde cada paso | Equipo de Desarrollo | 26/05/2026 | Mensajes de bienvenida correctos según paso actual |
| Prueba de sugerencias con citas normativas | QA Lead + Área Jurídica | 31/05/2026 | 100% de sugerencias incluyen artículos CGD citados |
| Prueba de bloqueo de decisiones por IA | Security Team | 02/06/2026 | 100% de intentos de decisión bloqueados y registrados |
| Prueba de rate limiting (20 consultas/sesión) | QA Lead | 04/06/2026 | Bloqueo exacto en consulta 21 |
| Prueba de timeout (5 segundos máx.) | Performance Team | 05/06/2026 | Mensaje de timeout mostrado consistentemente |
| Prueba de detección de preguntas fuera de contexto | AI Team | 06/06/2026 | 95% de preguntas fuera de contexto rechazadas |
| Prueba de mantenimiento de contexto conversacional | QA Lead | 07/06/2026 | Contexto mantenido por mínimo 10 intercambios |
| Validación ética por Comité de Ética de IA | Comité de Ética | 10/06/2026 | Certificación de ausencia de sesgos discriminatorios |
| Auditoría de trazabilidad en audit log | OCI-PGN | 12/06/2026 | 100% de interacciones registradas con hash válido |
| UAT (User Acceptance Testing) | Funcionarios Instructor | 16/06/2026 | Aprobación formal por parte de 5 usuarios clave |

## Matriz de Trazabilidad con Referencias Normativas

| Artículo | Norma | Descripción | Implementación en Sistema | Estado de Cumplimiento |
|----------|-------|-------------|--------------------------|------------------------|
| Art. 76 | Ley 1952/2019 | Responsabilidad indelegable del funcionario | IA nunca decide, solo sugiere con descargo explícito | ✅ Cumple |
| Art. 14 | Ley 1952/2019 | Principio de responsabilidad | Audit log registra quién tomó cada decisión final | ✅ Cumple |
| Art. 3 | Ley 1581/2012 | Protección de datos personales | Interacciones con IA tratadas según política de privacidad | ✅ Cumple |
| Lineamiento 4.2 | CONPES 3975 | Transparencia en uso de IA | Descargo de responsabilidad visible en cada interacción | ✅ Cumple |
| Circular 003 | PGN 2024 | Uso ético de IA en procesos disciplinarios | Prohibición de generación de actos administrativos completos | ✅ Cumple |
| Principio 7 | GovAI Coalition | Trazabilidad de decisiones asistidas por IA | Audit log especializado con hash criptográfico | ✅ Cumple |

## Notas Adicionales

- Esta HU-11-05 cubre la funcionalidad transversal de **Asistencia de procuradurIA** aplicable a todos los pasos del asistente de incorporación.
- El modelo de IA debe ser actualizado trimestralmente con nueva normativa y jurisprudencia disciplinaria.
- Las interacciones con procuradurIA no constituyen actuación procesal en sí mismas; son meras consultas de asistencia.
- En futuras iteraciones, se podría implementar integración con sistemas de otras entidades (Fiscalía, Rama Judicial) para sugerencias de incorporaciones cross-entidad.
- El comité de ética de IA de la PGN debe revisar mensualmente una muestra aleatoria de interacciones para detectar sesgos potenciales.
- procuradurIA debe operar en modo "solo lectura" sobre los expedientes; nunca puede modificar datos directamente.
