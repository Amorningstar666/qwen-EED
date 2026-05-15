# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por |
|-------|-------|------------|--------------|
| 15/05/2026 | HU-19-01 | Analista de Negocio | Líder Técnico |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica | P17-Apoyo a la Investigación | A52-Calificación y Formulación de Pliego de Cargos | Funcionalidad Crítica | Permite la formulación del pliego de cargos cumpliendo los 9 elementos obligatorios del Art. 222 CGD, garantizando el debido proceso, el derecho de defensa y evitando nulidades por defectos de forma o fondo en la calificación provisional |

### Descripción

**¿Quién?** El Funcionario de Instrucción (rol: instructor) que ha completado la etapa de investigación disciplinaria y considera que existen méritos para formular pliego de cargos, o el Procurador Delegado que avoca el conocimiento para juzgamiento.

**¿Qué?** Realiza la calificación provisional de la conducta investigada mediante la elaboración del pliego de cargos que contiene los nueve (9) elementos obligatorios establecidos en el artículo 222 del Código General Disciplinario, utilizando un asistente guiado que valida checklist de completitud, genera vista previa del documento y registra trazabilidad completa de la actuación.

**¿Para qué?** Para formular pliego de cargos conforme al artículo 222 de la Ley 1952 de 2019 (modificado por Ley 2094 de 2021), garantizando que la calificación provisional cumpla con todos los requisitos legales que permiten al disciplinado ejercer su derecho de defensa, conocer con precisión los cargos en su contra y preparar sus alegatos de conclusión antes del traslado a juzgamiento.

**Referencias Normativas:**
- Ley 1952 de 2019 (Código General Disciplinario), Artículo 222: Contenido obligatorio del pliego de cargos.
- Ley 1952 de 2019, Artículo 223: Notificación y traslado del pliego de cargos.
- Ley 1952 de 2019, Artículo 224: Recurso de apelación contra el pliego de cargos.
- Ley 1952 de 2019, Artículo 225: Traslado a juzgamiento.
- Ley 2094 de 2021, Artículo 1: Principios rectores de la función disciplinaria.
- Ley 1952 de 2019, Artículo 47: Criterios de gravedad y levedad.
- Ley 1952 de 2019, Artículo 115: Reserva de las actuaciones disciplinarias.
- Ley 1437 de 2011 (CPACA), Artículo 3: Principios del procedimiento administrativo.
- Constitución Política de Colombia, Artículo 29: Debido proceso.

## Dependencias y Precondiciones

1. El usuario debe estar autenticado con credenciales válidas en el sistema EED y tener asignado el rol de "Funcionario de Instrucción" o "Procurador Delegado" con competencia para formular pliego de cargos en el expediente específico.
2. El expediente disciplinario debe encontrarse en etapa de "Investigación Disciplinaria" cerrada, con todas las pruebas practicadas y valoradas conforme al artículo 219 del CGD.
3. Debe existir auto de cierre de investigación disciplinaria firmado y notificado (Art. 220 CGD) que ordene el traslado a calificación provisional.
4. El sistema debe contar con toda la información procesal del expediente: sujetos procesales identificados, conductas investigadas, normas presuntamente violadas, pruebas allegadas y argumentos de defensa.
5. El módulo de shell corporativo (HU-02) debe estar activo con configuración de RBAC habilitado para validación de permisos por tipo de actuación.
6. Debe existir trazabilidad completa de todas las actuaciones procesales previas, incluyendo historial de pruebas, alegatos y decisiones intermedias.
7. El componente de procuradurIA debe estar disponible para brindar asistencia contextual durante la redacción del pliego, con registro auditado de todas las interacciones.
8. La base de datos debe mantener integridad referencial entre el expediente, los sujetos procesales, las conductas investigadas y las normas aplicables.
9. El sistema debe contar con plantillas documentales preconfiguradas para la generación del pliego de cargos en formato PDF/A conforme a estándares de archivo digital.
10. Debe existir conectividad con el módulo de notificaciones (HU-18) para generar automáticamente las comunicaciones de traslado una vez firmado el pliego.

## Restricciones

1. El botón de firmar el pliego de cargos permanece deshabilitado hasta que los nueve (9) elementos obligatorios del artículo 222 CGD estén completos y validados.
2. Una vez firmado el pliego de cargos, la actuación es irreversible salvo mediante recurso de apelación interpuesto por los sujetos procesales dentro de los cinco (5) días siguientes a la notificación.
3. El funcionario que formula el pliego de cargos debe ser el mismo que tuvo competencia para la investigación, salvo que se haya configurado avocamiento por parte del superior jerárquico.
4. El sistema debe validar que no existan causales de impedimento o conflicto de interés del funcionario que formula el pliego respecto del disciplinado o la conducta investigada.
5. La descripción de la conducta debe incluir necesariamente las circunstancias de tiempo, modo y lugar, so pena de nulidad por indefensión del disciplinado.
6. El análisis de ilicitud sustancial y culpabilidad debe estar fundamentado en pruebas practicadas con observancia de las reglas de valoración legal.
7. Los criterios de gravedad o levedad deben exponerse de manera fundada conforme al artículo 47 CGD, considerando los subcriterios de antijuridicidad, culpabilidad y necesidad de sanción.
8. El sistema debe generar acta automática de formulación de pliego que incluya: fecha y hora de firma, identificación del funcionario, sujetos procesales notificados y términos de traslado.
9. La interfaz debe cumplir con los estándares de accesibilidad WCAG 2.1 nivel AA, utilizando la fuente Poppins en todos sus componentes visuales y los tokens de diseño institucional PGN.
10. Cualquier intento de formular pliego de cargos sin cumplir los nueve elementos obligatorios quedará registrado en el audit log como evento de seguridad potencial.
11. El pliego de cargos no puede formularse si el expediente está en estado de indagación previa; requiere necesariamente cierre de investigación disciplinaria.
12. La reserva de las actuaciones (Art. 115 CGD) cesa parcialmente con la formulación del pliego, pero solo los sujetos procesales y sus defensores pueden acceder al contenido completo.

## Reglas de Negocio

| ID Regla | Descripción | Fundamento Legal | Prioridad |
|----------|-------------|------------------|-----------|
| RN-19-01-01 | Solo se permite formular pliego de cargos si existe auto de cierre de investigación firmado y notificado | Art. 220 Ley 1952/2019 | Crítica |
| RN-19-01-02 | El sistema debe validar que los 9 elementos del Art. 222 CGD estén completos antes de habilitar la firma | Art. 222 Ley 1952/2019 | Crítica |
| RN-19-01-03 | La descripción de la conducta debe incluir tiempo, modo y lugar de comisión | Art. 222 numeral 3 Ley 1952/2019 | Crítica |
| RN-19-01-04 | El análisis de ilicitud sustancial debe demostrar la afectación al deber funcional | Art. 222 numeral 5 Ley 1952/2019 | Alta |
| RN-19-01-05 | El análisis de culpabilidad debe verificar dolo o culpa en la conducta | Art. 222 numeral 6 Ley 1952/2019 | Alta |
| RN-19-01-06 | Las pruebas analizadas deben haber sido practicadas con observancia de las reglas de valoración | Art. 219 Ley 1952/2019 | Alta |
| RN-19-01-07 | Los criterios de gravedad deben exponerse conforme al Art. 47 CGD | Art. 47 y 222 numeral 8 Ley 1952/2019 | Alta |
| RN-19-01-08 | El sistema debe impedir la formulación si hay causal de impedimento vigente | Art. 77 Ley 1952/2019 | Media |
| RN-19-01-09 | Todos los eventos de formulación quedan registrados en audit log inmutable | Art. 76 Ley 1952/2019 | Media |
| RN-19-01-10 | El pliego generado debe ser en formato PDF/A con firma digital cualificada | Decreto 1069/2015 | Media |
| RN-19-01-11 | El sistema debe generar automáticamente las comunicaciones de traslado a juzgamiento | Art. 223 Ley 1952/2019 | Baja |
| RN-19-01-12 | No procede recurso contra el auto que ordena traslado a juzgamiento | Art. 225 Ley 1952/2019 | Baja |

## Supuestos

1. Se asume que el funcionario instructor conoce los nueve elementos obligatorios del artículo 222 del CGD y sabe redactar cada sección conforme a la técnica jurídica requerida.
2. Se asume que todas las pruebas practicadas en la investigación están debidamente registradas en el sistema con su respectiva valoración jurídica.
3. Se asume que el sistema cuenta con conectividad continua a la base de datos central de expedientes para consultar información actualizada de sujetos procesales y normas.
4. Se asume que el funcionario tiene acceso a su correo institucional y al sistema de notificaciones electrónicas para verificar la entrega del pliego.
5. Se asume que不存在 causales de impedimento o conflicto de interés del funcionario que formula el pliego respecto de los sujetos procesales.
6. Se asume que la formulación del pliego de cargos no modifica los términos procesales individuales; el término de traslado de 10 días comienza a correr desde la notificación personal.
7. Se asume que el disciplinado cuenta con defensor constituido o, en su defecto, el sistema permitirá la designación de defensor de oficio dentro de los 5 días siguientes.

## Criterios de Aceptación

### Escenario 1: Acceso exitoso al módulo de formulación de pliego de cargos

**Dado** que soy un Funcionario de Instrucción autenticado en el sistema EED  
**Cuando** accedo a un expediente en estado "Investigación Cerrada" con auto de cierre notificado  
**Y** presiono el botón "Formular Pliego de Cargos"  
**Entonces** el sistema valida que existe auto de cierre de investigación firmado  
**Y** muestra el asistente de formulación de pliego con los 9 elementos obligatorios  
**Y** cada elemento aparece con indicador de estado "Pendiente" o "Completado"  
**Y** el botón "Firmar Pliego" permanece deshabilitado  

**Evidencia:** Captura de pantalla del asistente mostrando los 9 elementos con checkboxes vacíos y botón "Firmar" en estado disabled.

### Escenario 2: Diligenciamiento del elemento 1 - Identificación del autor

**Dado** que estoy en el asistente de formulación de pliego de cargos  
**Cuando** selecciono el elemento 1 "Identificación del autor o autores"  
**Y** el sistema carga automáticamente los datos del disciplinado desde el expediente  
**Y** verifico que incluye: nombre completo, documento de identidad, cargo público, entidad, dependencia  
**Y** confirmo que los datos son correctos  
**Entonces** el sistema marca el elemento 1 como "Completado"  
**Y** actualiza el contador de progreso (1 de 9 elementos completados)  
**Y** habilita la navegación al elemento 2  

**Evidencia:** Captura de pantalla del elemento 1 diligenciado con datos del disciplinado y checkbox marcado como completado.

### Escenario 3: Redacción del elemento 3 - Descripción de la conducta

**Dado** que estoy redactando el elemento 3 "Descripción de la conducta"  
**Cuando** ingreso la descripción detallada de la conducta investigada  
**Y** el sistema valida que incluye circunstancias de tiempo (fecha específica o rango)  
**Y** valida que incluye circunstancias de modo (forma de ejecución)  
**Y** valida que incluye circunstancias de lugar (sitio donde ocurrieron los hechos)  
**Y** la longitud mínima es de 200 caracteres  
**Entonces** el sistema marca el elemento 3 como "Completado"  
**Y** si falta alguna circunstancia, muestra mensaje de advertencia: "Debe especificar tiempo, modo y lugar de la conducta"  
**Y** el botón "Guardar Parcial" permite almacenar avances sin completar todos los elementos  

**Evidencia:** Captura de pantalla con descripción de conducta que incluye "El día 15 de marzo de 2025, en la oficina de Atención al Ciudadano de la Secretaría de Hacienda, el disciplinado omitió el trámite de radicación de solicitud...".

### Escenario 4: Análisis de ilicitud sustancial con soporte probatorio

**Dado** que estoy redactando el elemento 5 "Análisis de la ilicitud sustancial"  
**Cuando** describo cómo la conducta afecta el deber funcional  
**Y** selecciono las pruebas que demuestran la ilicitud desde el repositorio del expediente  
**Y** el sistema muestra lista de pruebas disponibles: testimoniales, documentales, periciales, inspección judicial  
**Y** vinculo cada prueba al argumento de ilicitud correspondiente  
**Entonces** el sistema marca el elemento 5 como "Completado"  
**Y** genera referencia cruzada entre el análisis y las pruebas seleccionadas  
**Y** en la vista previa del pliego, las pruebas aparecen citadas con su número de folio  

**Evidencia:** Captura de pantalla del análisis de ilicitud con 5 pruebas seleccionadas y referenciadas (Testimonio Juan Pérez, Folio 45; Documento contrato, Folio 12).

### Escenario 5: Validación de completitud de los 9 elementos

**Dado** que he diligenciado 8 de los 9 elementos obligatorios  
**Cuando** intento avanzar a la sección de firma  
**Entonces** el sistema muestra mensaje de advertencia: "Falta completar 1 elemento obligatorio"  
**Y** resalta en amarillo el elemento pendiente en el índice del asistente  
**Y** el botón "Firmar Pliego" permanece deshabilitado  
**Y** el sistema sugiere: "Complete el elemento 7 'Análisis de las pruebas' para continuar"  

**Evidencia:** Captura de pantalla con mensaje de validación y elemento 7 resaltado en amarillo como pendiente.

### Escenario 6: Vista previa del documento pliego de cargos

**Dado** que he completado los 9 elementos obligatorios  
**Cuando** presiono el botón "Vista Previa"  
**Entonces** el sistema genera un documento PDF en pantalla con estructura formal de pliego de cargos  
**Y** muestra encabezado institucional PGN con logo y datos del expediente  
**Y** incluye los 9 elementos en orden secuencial con numeración oficial  
**Y** muestra pie de página con número de radicado y fecha de generación  
**Y** habilita botones "Descargar Borrador", "Editar Elemento", "Firmar Pliego"  

**Evidencia:** Captura de pantalla de vista previa PDF mostrando pliego completo de 15 páginas con membrete PGN.

### Escenario 7: Firma digital del pliego de cargos

**Dado** que he completado los 9 elementos y revisado la vista previa  
**Cuando** presiono el botón "Firmar Pliego"  
**Entonces** el sistema solicita autenticación con certificado digital cualificado  
**Y** muestra modal de confirmación: "Esta acción genera pliego de cargos irreversible. ¿Confirmar?"  
**Y** al confirmar, aplica firma digital con sello de tiempo  
**Y** genera PDF final con código de verificación QR  
**Y** registra el evento en audit log con huella digital del documento  
**Y** cambia el estado del expediente a "Pliego de Cargos Formulado"  

**Evidencia:** Captura de pantalla de modal de confirmación y posterior mensaje de éxito con código de verificación: PLC-2026-001234-FIRMADO.

### Escenario 8: Generación automática de comunicaciones de traslado

**Dado** que el pliego de cargos ha sido firmado exitosamente  
**Cuando** el sistema completa el proceso de firma digital  
**Entonces** genera automáticamente las comunicaciones de notificación personal a los sujetos procesales  
**Y** calcula el término de 10 días hábiles para alegatos de conclusión (Art. 223 CGD)  
**Y** programa recordatorio de vencimiento de término para el día 8  
**Y** envía notificación al correo institucional del funcionario instructor  
**Y** registra las comunicaciones en el módulo de notificaciones (HU-18)  
**Y** muestra mensaje: "Pliego formulado. Se han generado 3 comunicaciones de traslado. Término de alegatos vence el [fecha]"  

**Evidencia:** Captura de pantalla de mensaje de éxito con detalle de comunicaciones generadas y fecha de vencimiento de término.

### Escenario 9: Error por intento de formulación sin auto de cierre

**Dado** que soy Funcionario de Instrucción en un expediente en investigación abierta  
**Cuando** intento acceder al módulo de formulación de pliego de cargos  
**Entonces** el sistema valida que no existe auto de cierre de investigación notificado  
**Y** muestra mensaje de error: "No es posible formular pliego de cargos. El expediente debe contar con auto de cierre de investigación notificado conforme al Art. 220 CGD"  
**Y** sugiere: "Primero genere y notifique el auto de cierre de investigación"  
**Y** el botón de formulación permanece deshabilitado  

**Evidencia:** Captura de pantalla con mensaje de error bloqueante y sugerencia de acción alternativa.

### Escenario 10: Asistencia de procuradurIA en redacción de elementos

**Dado** que estoy redactando el elemento 6 "Análisis de culpabilidad"  
**Cuando** presiono el botón de asistencia de procuradurIA  
**Y** solicito: "Generar esquema de análisis de culpabilidad para conducta dolosa"  
**Entonces** procuradurIA responde con estructura sugerida: verificación de conocimiento, voluntad, ausencia de causales de exclusión  
**Y** cita jurisprudencia relevante del Consejo de Estado sobre dolo en faltas disciplinarias  
**Y** aclara: "Esta sugerencia no constituye decisión procesal. El funcionario debe valorar pruebas y redactar su propio análisis"  
**Y** registra la interacción en audit log con timestamp y contenido de la consulta  

**Evidencia:** Captura de pantalla de chat con procuradurIA mostrando sugerencia de esquema y disclaimer de trazabilidad.

## Prototipo / Anexos

- **Prototipo de pantalla:** `/workspace/Pantallas VEED/19_pliego_de_cargos.html` (por desarrollar)
- **Componentes específicos del asistente de pliego de cargos:**
  - Índice lateral con los 9 elementos y estado de completitud (checkbox + color)
  - Área de redacción principal con editor de texto enriquecido (negrita, cursiva, subrayado, citas)
  - Selector de pruebas del repositorio del expediente con búsqueda full-text
  - Contador de progreso: "X de 9 elementos completados"
  - Botones de acción: "Guardar Parcial", "Vista Previa", "Firmar Pliego"
  - Modal de confirmación de firma con advertencia de irreversibilidad
  - Chat flotante de procuradurIA con registro auditado
- **Tokens de diseño PGN aplicados:**
  - Fuente: Montserrat (títulos, badges), Poppins (cuerpo, inputs)
  - Color primario: #063853 (Azul institucional PGN)
  - Color de acción: #FFE601 (Amarillo institucional para botones principales)
  - Color de error: #E3201B (Rojo institucional)
  - Color de éxito: #33FFCC (Verde azulado para estados positivos)
  - Color de advertencia: #FFA500 (Naranja para validaciones pendientes)
- **Referencias a líneas del prototipo HTML:** (pendiente de desarrollo)
  - Estructura del asistente de 9 elementos
  - Editor de texto enriquecido con toolbar
  - Modal de firma digital con certificado
  - Vista previa en iframe o ventana emergente
- **Anexo técnico:** Documento de especificación de API de generación de PDF/A con firma digital (en elaboración)

## Stakeholders

| Rol | Nombre/Dependencia | Responsabilidad | Firma Requerida |
|-----|-------------------|-----------------|-----------------|
| Product Owner | Dirección de Investigación Disciplinaria | Definición de reglas de negocio | Sí |
| Líder Técnico | Oficina de Sistemas - PGN | Validación de implementación técnica | Sí |
| Funcionario Instructor | Procuraduría Delegada para la Investigación | Usuario primario, validación de usabilidad | Sí |
| Procurador Delegado | Despachos de Juzgamiento | Usuario secundario, validación de flujo | Sí |
| Jefe de Grupo | Grupo de Gestión Procesal | Supervisor de formulación de pliegos | Sí |
| Oficina de Control Interno | OCI-PGN | Auditoría de trazabilidad de pliegos | Sí |
| Oficina Asesora Jurídica | OA-Jurídica - PGN | Validación de conformidad con Art. 222 CGD | Sí |
| Secretario General | Secretaría General - PGN | Custodia de pliegos firmados | Sí |

## Plan de Validación

| Tipo de Prueba | Responsable | Fecha Estimada | Criterio de Aprobación |
|----------------|-------------|----------------|------------------------|
| Prueba de concepto de validación de 9 elementos | Equipo de Desarrollo | 22/05/2026 | Sistema impide firma si falta 1 elemento |
| Prueba de usabilidad con funcionarios instructores | UX/UI Team | 27/05/2026 | 90% de usuarios completan pliego sin asistencia |
| Prueba de generación de PDF/A con firma digital | Security Team | 30/05/2026 | PDF cumple estándar ISO 19005-1 y firma válida |
| Prueba de integración con módulo de notificaciones | QA Lead | 03/06/2026 | Comunicaciones generadas automáticamente sin error |
| Validación jurídica de elementos del Art. 222 | Oficina Asesora Jurídica | 05/06/2026 | Certificación de conformidad con Art. 222 CGD |
| Prueba de carga (generación simultánea de pliegos) | Performance Team | 08/06/2026 | Tiempo de respuesta menor a 3 segundos con 50 usuarios |
| UAT (User Acceptance Testing) | Funcionarios Instructor | 12/06/2026 | Aprobación formal por parte de 5 usuarios clave |

## Matriz de Trazabilidad con Referencias Normativas

| Artículo | Norma | Descripción | Implementación en Sistema | Estado de Cumplimiento |
|----------|-------|-------------|--------------------------|------------------------|
| Art. 222 | Ley 1952/2019 | Contenido obligatorio del pliego de cargos | 9 elementos validados con checklist | ✅ Cumple |
| Art. 223 | Ley 1952/2019 | Notificación y traslado del pliego | Generación automática de comunicaciones | ✅ Cumple |
| Art. 224 | Ley 1952/2019 | Recurso de apelación | Registro de término de 5 días para apelar | ✅ Cumple |
| Art. 225 | Ley 1952/2019 | Traslado a juzgamiento | Remisión automática a juzgador tras firmeza | ✅ Cumple |
| Art. 47 | Ley 1952/2019 | Criterios de gravedad y levedad | Elemento 8 incluye subcriterios de valoración | ✅ Cumple |
| Art. 219 | Ley 1952/2019 | Valoración de pruebas | Elemento 7 vincula pruebas con argumentos | ✅ Cumple |
| Art. 115 | Ley 1952/2019 | Reserva de actuaciones | Acceso restringido hasta notificación de pliego | ✅ Cumple |
| Art. 29 | Constitución Política | Debido proceso | Derecho de defensa garantizado con pliego completo | ✅ Cumple |
| Art. 3 | Ley 1437/2011 | Principios procedimentales | Publicidad, contradicción y motivación | ✅ Cumple |

## Notas Adicionales

- Esta HU-19-01 cubre exclusivamente la **formulación del pliego de cargos** conforme al artículo 222 CGD. Las HU siguientes cubrirán la notificación, los recursos de apelación y el traslado a juzgamiento.
- El término "calificación provisional" es equivalente a "formulación de pliego de cargos" en la terminología jurídica del CGD.
- La irreversibilidad de la firma del pliego busca garantizar seguridad jurídica, pero no impide que mediante recurso de apelación el superior modifique o revoque la calificación.
- El sistema debe prevenir la formulación de pliegos incompletos mediante validación estricta de los 9 elementos; cualquier excepción debe ser autorizada por el superior jerárquico con justificación escrita.
- La asistencia de procuradurIA es meramente sugerente; el funcionario instructor mantiene responsabilidad exclusiva sobre el contenido jurídico del pliego formulado.
- El PDF generado debe cumplir con estándar PDF/A (ISO 19005-1) para garantía de preservación a largo plazo conforme a políticas de archivo digital de la PGN.
