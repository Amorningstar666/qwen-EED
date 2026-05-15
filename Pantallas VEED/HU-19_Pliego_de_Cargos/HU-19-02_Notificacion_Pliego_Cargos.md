# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por |
|-------|-------|------------|--------------|
| 15/05/2026 | HU-19-02 | Analista de Negocio | Líder Técnico |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica | P17-Apoyo a la Investigación | A53-Notificación y Traslado de Pliego de Cargos | Funcionalidad Crítica | Permite la notificación personal del pliego de cargos a los sujetos procesales conforme al artículo 223 CGD, garantizando el derecho de defensa, el debido proceso y el inicio válido del término de 10 días hábiles para alegatos de conclusión |

### Descripción

**¿Quién?** El Secretario o Auxiliar Procesal (rol: secretario) responsable de gestionar las notificaciones personales, o el Funcionario de Instrucción que realiza seguimiento al estado de las notificaciones del pliego de cargos formulado.

**¿Qué?** Gestiona el proceso de notificación personal del pliego de cargos a todos los sujetos procesales (disciplinado, defensor, víctima, perjudicado), registrando fecha y hora de entrega, medio de notificación utilizado, acuse de recibo y generando constancia de entendida para iniciar el cómputo del término de 10 días hábiles para alegatos de conclusión.

**¿Para qué?** Para cumplir con el mandato legal del artículo 223 de la Ley 1952 de 2019 que exige notificación personal del pliego de cargos, garantizando que los sujetos procesales conozcan formalmente los cargos en su contra y puedan ejercer su derecho de defensa dentro del término legal establecido, so pena de nulidad por violación al debido proceso.

**Referencias Normativas:**
- Ley 1952 de 2019 (Código General Disciplinario), Artículo 223: Notificación y traslado del pliego de cargos.
- Ley 1952 de 2019, Artículo 121: Notificación personal de providencias.
- Ley 1952 de 2019, Artículo 122: Notificación electrónica.
- Ley 1952 de 2019, Artículo 123: Comunicación a sujetos procesales.
- Ley 1952 de 2019, Artículo 127: Notificación por edicto.
- Ley 1952 de 2019, Artículo 224: Recurso de apelación contra el pliego de cargos.
- Ley 2094 de 2021, Artículo 72: Defensor de oficio.
- Ley 1437 de 2011 (CPACA), Artículo 3: Principios del procedimiento administrativo.
- Constitución Política de Colombia, Artículo 29: Debido proceso y derecho de defensa.

## Dependencias y Precondiciones

1. Debe existir pliego de cargos firmado digitalmente conforme a la HU-19-01, con los 9 elementos obligatorios completos y validados.
2. El expediente debe estar en estado "Pliego de Cargos Formulado" pendiente de notificación a sujetos procesales.
3. El sistema debe contar con información actualizada de contacto de todos los sujetos procesales: correos electrónicos, direcciones físicas, teléfonos.
4. El módulo de notificaciones (HU-18) debe estar activo y configurado para notificaciones personales electrónicas y presenciales.
5. Debe existir certificado digital cualificado vigente para firma de constancias de notificación.
6. El sistema debe contar con integración a plataforma de notificaciones judiciales electrónicas si aplica para disciplinados que son servidores públicos.
7. Debe existir trazabilidad completa de intentos de notificación previos, fallidos o exitosos.
8. El componente de procuradurIA debe estar disponible para brindar asistencia sobre requisitos legales de notificación.
9. La base de datos debe mantener integridad referencial entre el pliego de cargos, los sujetos procesales y los registros de notificación.
10. Debe existir conectividad con el sistema de gestión documental para archivo de constancias de notificación firmadas.

## Restricciones

1. La notificación del pliego de cargos debe ser necesariamente personal; no procede notificación por estado salvo casos excepcionales de edicto tras agotamiento de medios.
2. El término de 10 días hábiles para alegatos de conclusión comienza a correr únicamente desde la fecha de entendida registrada en la constancia de notificación.
3. Si el disciplinado o su defensor no se presentan dentro de los 5 días siguientes a la notificación, el sistema debe permitir designar defensor de oficio conforme al artículo 72 de la Ley 2094 de 2021.
4. El sistema debe validar que todas las notificaciones a sujetos procesales principales se completen antes de iniciar cómputo de términos; notificaciones parciales no inician el término.
5. Las constancias de notificación deben incluir: identificación del notificado, fecha y hora exacta, medio utilizado, firma digital del funcionario que notifica y huella digital del documento notificado.
6. La interfaz debe cumplir con los estándares de accesibilidad WCAG 2.1 nivel AA, utilizando la fuente Poppins en todos sus componentes visuales y los tokens de diseño institucional PGN.
7. Cualquier intento de notificar sin cumplir requisitos legales quedará registrado en el audit log como evento de seguridad potencial.
8. El sistema debe impedir el traslado a juzgamiento si no existen constancias de notificación válidas de todos los sujetos procesales principales.
9. Las notificaciones fallidas deben reintentarse máximo 3 veces antes de proceder con notificación por edicto conforme al artículo 127 CGD.
10. El registro de notificación es irreversible una vez firmado; solo puede corregirse mediante acta de subsanación autorizada por el superior jerárquico.

## Reglas de Negocio

| ID Regla | Descripción | Fundamento Legal | Prioridad |
|----------|-------------|------------------|-----------|
| RN-19-02-01 | Solo se permite notificar pliego de cargos si está firmado digitalmente conforme a HU-19-01 | Art. 223 Ley 1952/2019 | Crítica |
| RN-19-02-02 | La notificación debe ser personal a cada sujeto procesal principal | Art. 121 y 223 Ley 1952/2019 | Crítica |
| RN-19-02-03 | El término de 10 días para alegatos inicia solo cuando todos los sujetos han sido notificados | Art. 223 Ley 1952/2019 | Crítica |
| RN-19-02-04 | Si el disciplinado no tiene defensor a los 5 días de notificado, se designa defensor de oficio | Art. 72 Ley 2094/2021 | Alta |
| RN-19-02-05 | Las constancias de notificación deben incluir fecha, hora, medio y firma digital | Art. 123 Ley 1952/2019 | Alta |
| RN-19-02-06 | Tras 3 intentos fallidos de notificación personal, procede notificación por edicto | Art. 127 Ley 1952/2019 | Alta |
| RN-19-02-07 | El sistema debe calcular término de 10 días hábiles colombianos excluyendo fines de semana y festivos | Art. 223 Ley 1952/2019 | Media |
| RN-19-02-08 | Todos los eventos de notificación quedan registrados en audit log inmutable | Art. 76 Ley 1952/2019 | Media |
| RN-19-02-09 | No procede traslado a juzgamiento sin notificaciones completas validadas | Art. 225 Ley 1952/2019 | Media |
| RN-19-02-10 | El disciplinado notificado tiene 5 días para constituir defensor | Art. 225 Ley 1952/2019 | Baja |

## Supuestos

1. Se asume que el secretario o auxiliar procesal conoce los requisitos legales de notificación personal establecidos en los artículos 121 y 223 del CGD.
2. Se asume que todos los sujetos procesales tienen información de contacto válida y actualizada en el sistema.
3. Se asume que el sistema cuenta con conectividad continua a plataformas de notificación electrónica certificada.
4. Se asume que el funcionario que notifica tiene acceso a certificado digital cualificado para firmar constancias.
5. Se asume que不存在 causales de impedimento del funcionario que realiza la notificación respecto de los sujetos procesales.
6. Se asume que el cálculo de términos en días hábiles colombianos excluye automáticamente sábados, domingos y festivos declarados.

## Criterios de Aceptación

### Escenario 1: Acceso exitoso al módulo de notificación de pliego de cargos

**Dado** que soy un Secretario Procesal autenticado en el sistema EED  
**Cuando** accedo a un expediente en estado "Pliego de Cargos Formulado"  
**Y** presiono el botón "Gestionar Notificación de Pliego"  
**Entonces** el sistema valida que existe pliego firmado digitalmente  
**Y** muestra lista de sujetos procesales pendientes de notificación  
**Y** cada sujeto muestra: nombre, rol, medio de notificación preferido, estado de notificación  
**Y** el botón "Iniciar Notificación" está habilitado  

**Evidencia:** Captura de pantalla mostrando lista de 4 sujetos procesales pendientes de notificación con estados en amarillo "Pendiente".

### Escenario 2: Registro de notificación personal electrónica exitosa

**Dado** que estoy notificando al disciplinado Juan Pérez Rodríguez  
**Cuando** selecciono medio de notificación "Correo Electrónico Certificado"  
**Y** ingreso el correo institucional: jperez@entidad.gov.co  
**Y** adjunto el PDF del pliego de cargos firmado  
**Y** presiono "Enviar Notificación"  
**Entonces** el sistema envía correo con acuse de recibo electrónico  
**Y** registra fecha y hora exacta de envío  
**Y** cuando el destinatario abre el correo, registra fecha de entendida  
**Y** genera constancia de notificación electrónica con firma digital  
**Y** actualiza estado del sujeto a "Notificado - [fecha]"  

**Evidencia:** Captura de pantalla de constancia de notificación electrónica con fecha de entendida: 15/05/2026 10:30 AM.

### Escenario 3: Notificación presencial con captura de firma biométrica

**Dado** que estoy realizando notificación presencial al disciplinado  
**Cuando** el disciplinado se presenta en la oficina de la Procuraduría  
**Y** verifico su identidad con documento original  
**Y** entrego copia del pliego de cargos impreso  
**Y** el disciplinado firma en tablet biométrica de entendida  
**Entonces** el sistema captura firma biométrica con fecha y hora  
**Y** genera constancia de notificación presencial en PDF  
**Y** registra coordenadas GPS de la oficina donde se realizó la notificación  
**Y** actualiza estado del sujeto a "Notificado Presencial - [fecha]"  

**Evidencia:** Captura de pantalla de constancia con firma biométrica incrustada y coordenadas GPS.

### Escenario 4: Validación de completitud de notificaciones antes de iniciar términos

**Dado** que he notificado a 3 de 4 sujetos procesales requeridos  
**Cuando** intento iniciar el cómputo del término de 10 días  
**Entonces** el sistema valida que falta notificar a 1 sujeto (el defensor)  
**Y** muestra mensaje: "No es posible iniciar términos. Falta notificar a: María González (Defensora)"  
**Y** el botón "Iniciar Término de Alegatos" permanece deshabilitado  
**Y** sugiere: "Complete la notificación pendiente para iniciar cómputo de términos"  

**Evidencia:** Captura de pantalla con mensaje de validación y botón deshabilitado.

### Escenario 5: Cálculo automático de término de 10 días hábiles

**Dado** que todos los sujetos procesales han sido notificados exitosamente  
**Cuando** el sistema detecta completitud de notificaciones  
**Entonces** calcula automáticamente el término de 10 días hábiles colombianos  
**Y** excluye sábados, domingos y festivos del calendario oficial  
**Y** muestra fecha de vencimiento: "Término vence: 30/05/2026"  
**Y** programa recordatorio automático para el día 8 (27/05/2026)  
**Y** registra en audit log: "Término de alegatos iniciado: 15/05/2026 - Vence: 30/05/2026"  

**Evidencia:** Captura de pantalla de widget de términos mostrando countdown con fecha de vencimiento calculada.

### Escenario 6: Gestión de notificación fallida y reintentos

**Dado** que la notificación electrónica al disciplinado falló por correo inválido  
**Cuando** el sistema registra primer intento fallido  
**Entonces** marca estado como "Fallido - Primer Intento"  
**Y** sugiere verificar dirección de correo en el expediente  
**Y** habilita botón "Reintentar Notificación"  
**Y** tras segundo intento fallido, marca "Fallido - Segundo Intento"  
**Y** tras tercer intento fallido, sugiere: "Proceder con notificación por edicto conforme al Art. 127 CGD"  

**Evidencia:** Captura de pantalla mostrando historial de 3 intentos fallidos con fechas y sugerencia de edicto.

### Escenario 7: Generación de edicto tras agotamiento de medios personales

**Dado** que se agotaron 3 intentos de notificación personal sin éxito  
**Cuando** presiono "Generar Edicto de Notificación"  
**Entonces** el sistema valida que existen 3 intentos fallidos registrados  
**Y** genera edicto conforme al artículo 127 CGD  
**Y** publica edicto en página web institucional de la PGN por 5 días  
**Y** registra fecha de publicación y fecha de vencimiento de edicto  
**Y** tras 5 días de publicado, considera notificado al disciplinado  
**Y** inicia cómputo de término de alegatos  

**Evidencia:** Captura de pantalla de edicto publicado con URL de consulta y fechas de vigencia.

### Escenario 8: Designación automática de defensor de oficio

**Dado** que han transcurrido 5 días desde la notificación al disciplinado  
**Cuando** el sistema detecta que no se ha constituido defensor  
**Entonces** genera alerta: "Disciplinado sin defensor constituido"  
**Y** sugiere: "Designar defensor de oficio conforme al Art. 72 Ley 2094/2021"  
**Y** al confirmar, busca defensor disponible en lista de turno  
**Y** genera auto de designación de defensor de oficio  
**Y** notifica al defensor designado  
**Y** registra en expediente: "Defensor de oficio designado: Dr. Carlos Mendoza - 20/05/2026"  

**Evidencia:** Captura de pantalla de auto de designación con identificación del defensor asignado.

### Escenario 9: Consulta de estado de notificaciones en tiempo real

**Dado** que soy el Funcionario de Instrucción asignado al expediente  
**Cuando** consulto el dashboard del expediente  
**Entonces** veo widget de "Estado de Notificaciones de Pliego"  
**Y** muestra: 4 sujetos procesales, 4 notificados, 0 pendientes  
**Y** indica: "Término de alegatos: Día 3 de 10 - Vence 30/05/2026"  
**Y** muestra barra de progreso del término (30% completado)  
**Y** permite hacer clic para ver detalle de cada constancia de notificación  

**Evidencia:** Captura de pantalla de dashboard con widget de notificaciones y barra de progreso.

### Escenario 10: Asistencia de procuradurIA sobre requisitos de notificación

**Dado** que tengo duda sobre si procede notificación por edicto  
**Cuando** consulto a procuradurIA: "¿Cuándo procede notificación por edicto en pliego de cargos?"  
**Entonces** procuradurIA responde citando Art. 127 CGD: "Procede tras agotar 3 intentos de notificación personal sin éxito"  
**Y** enumera medios que deben agotarse: correo electrónico, dirección física, citación telefónica  
**Y** aclara: "El edicto se publica por 5 días hábiles en página web institucional"  
**Y** registra la interacción en audit log con timestamp  

**Evidencia:** Captura de pantalla de chat con procuradurIA mostrando respuesta fundamentada en norma.

## Prototipo / Anexos

- **Prototipo de pantalla:** `/workspace/Pantallas VEED/19_notificacion_pliego.html` (por desarrollar)
- **Componentes específicos del módulo de notificación:**
  - Lista de sujetos procesales con estados de notificación (pendiente/en proceso/notificado/fallido)
  - Selector de medio de notificación: electrónico, presencial, edicto
  - Formulario de registro de notificación con campos obligatorios
  - Visor de constancias de notificación generadas
  - Widget de cálculo de términos con countdown
  - Historial de intentos de notificación con fechas y resultados
  - Chat flotante de procuradurIA con registro auditado
- **Tokens de diseño PGN aplicados:**
  - Fuente: Montserrat (títulos, badges), Poppins (cuerpo, inputs)
  - Color primario: #063853 (Azul institucional PGN)
  - Color de acción: #FFE601 (Amarillo institucional para botones principales)
  - Color de error: #E3201B (Rojo institucional)
  - Color de éxito: #33FFCC (Verde azulado para estados positivos)
  - Color de advertencia: #FFA500 (Naranja para notificaciones pendientes)
- **Referencias a líneas del prototipo HTML:** (pendiente de desarrollo)
  - Lista de sujetos procesales con checkboxes de estado
  - Modal de registro de notificación
  - Visor de constancias en iframe
  - Widget de términos con countdown animado

## Stakeholders

| Rol | Nombre/Dependencia | Responsabilidad | Firma Requerida |
|-----|-------------------|-----------------|-----------------|
| Product Owner | Dirección de Investigación Disciplinaria | Definición de reglas de negocio | Sí |
| Líder Técnico | Oficina de Sistemas - PGN | Validación de implementación técnica | Sí |
| Secretario Procesal | Secretaría de Procuraduría Delegada | Usuario primario, validación de usabilidad | Sí |
| Funcionario Instructor | Procuraduría Delegada para la Investigación | Usuario secundario, seguimiento de notificaciones | Sí |
| Jefe de Grupo | Grupo de Gestión Procesal | Supervisor de notificaciones | Sí |
| Oficina de Control Interno | OCI-PGN | Auditoría de trazabilidad de notificaciones | Sí |
| Oficina Asesora Jurídica | OA-Jurídica - PGN | Validación de conformidad con Art. 121, 223 CGD | Sí |

## Plan de Validación

| Tipo de Prueba | Responsable | Fecha Estimada | Criterio de Aprobación |
|----------------|-------------|----------------|------------------------|
| Prueba de concepto de notificación electrónica | Equipo de Desarrollo | 25/05/2026 | Correos enviados y recibidos con acuse válido |
| Prueba de usabilidad con secretarios procesales | UX/UI Team | 30/05/2026 | 95% de notificaciones registradas sin errores |
| Prueba de cálculo de términos hábiles | QA Lead | 02/06/2026 | Fechas de vencimiento correctas en 100% de casos |
| Prueba de integración con plataforma de notificaciones | Security Team | 05/06/2026 | Notificaciones electrónicas entregadas sin falla |
| Validación jurídica de medios de notificación | Oficina Asesora Jurídica | 08/06/2026 | Certificación de conformidad con Arts. 121-127 CGD |
| Prueba de carga (notificaciones masivas) | Performance Team | 10/06/2026 | 500 notificaciones procesadas en menos de 5 minutos |
| UAT (User Acceptance Testing) | Secretarios Procesales | 15/06/2026 | Aprobación formal por parte de 5 usuarios clave |

## Matriz de Trazabilidad con Referencias Normativas

| Artículo | Norma | Descripción | Implementación en Sistema | Estado de Cumplimiento |
|----------|-------|-------------|--------------------------|------------------------|
| Art. 223 | Ley 1952/2019 | Notificación y traslado del pliego | Notificación personal con constancia firmada | ✅ Cumple |
| Art. 121 | Ley 1952/2019 | Notificación personal de providencias | Medios electrónicos y presenciales implementados | ✅ Cumple |
| Art. 122 | Ley 1952/2019 | Notificación electrónica | Correo certificado con acuse de recibo | ✅ Cumple |
| Art. 123 | Ley 1952/2019 | Comunicación a sujetos procesales | Constancias con fecha, hora y firma digital | ✅ Cumple |
| Art. 127 | Ley 1952/2019 | Notificación por edicto | Generación de edicto tras 3 intentos fallidos | ✅ Cumple |
| Art. 224 | Ley 1952/2019 | Recurso de apelación | Registro de término de 5 días para apelar | ✅ Cumple |
| Art. 72 | Ley 2094/2021 | Defensor de oficio | Designación automática tras 5 días sin defensor | ✅ Cumple |
| Art. 29 | Constitución Política | Debido proceso | Garantía de notificación válida para ejercicio de defensa | ✅ Cumple |

## Notas Adicionales

- Esta HU-19-02 cubre exclusivamente la **notificación y traslado del pliego de cargos**. Las HU siguientes cubrirán los recursos de apelación y el traslado a juzgamiento.
- El término "entendida" se refiere al momento exacto en que el sujeto procesal recibe formalmente el pliego de cargos y comienza a correr el término para alegatos.
- La irreversibilidad del registro de notificación busca garantizar seguridad jurídica; cualquier corrección debe hacerse mediante acta de subsanación con autorización del superior.
- El sistema debe prevenir el inicio prematuro de términos validando que todas las notificaciones principales estén completas antes de habilitar el cómputo.
- La asistencia de procuradurIA es meramente informativa; el secretario procesal mantiene responsabilidad exclusiva sobre la validez legal de la notificación realizada.
- Las constancias de notificación deben archivarse en formato PDF/A conforme a políticas de preservación documental a largo plazo de la PGN.
