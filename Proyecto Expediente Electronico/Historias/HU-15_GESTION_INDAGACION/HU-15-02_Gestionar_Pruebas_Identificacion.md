# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por | Estado |
|-------|-------|------------|--------------|--------|
| 13/05/2026 | HU-15-02 | Analista de Negocio | Líder Técnico / Oficina Jurídica | Borrador |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de Negocio |
|--------------|---------|-----------|---------------|------------------|
| M4 - Gestión Jurídica Disciplinaria | P17 - Apoyo a la Investigación Disciplinaria | A34 - Práctica y Valoración Probatoria en Indagación Previa | Funcionalidad Crítica | Alta |

**Descripción del Valor de Negocio:**
Permitir al Funcionario de Instrucción gestionar el acervo probatorio mínimo necesario para determinar si existen causales de apertura de investigación disciplinaria o de archivo de la actuación, garantizando la celeridad procesal exigida en la etapa de indagación previa y asegurando que las pruebas recaudadas sean pertinentes, conducentes y útiles para la toma de decisión final dentro del término legal perentorio.

---

## Descripción de la Historia de Usuario

### ¿Quién? (Rol)
**Funcionario de Instrucción** (Rol sistema: `INSTRUCTOR`), actuando bajo las facultades conferidas en el artículo 208 de la Ley 1952 de 2019 (Código General Disciplinario). Este rol tiene la competencia exclusiva para practicar pruebas durante la indagación previa, con la limitante estricta de que solo pueden ser aquellas necesarias para identificar al presunto autor o partícipe y determinar la existencia de la conducta.

### ¿Qué? (Funcionalidad)
El sistema permitirá **gestionar las pruebas de identificación** dentro del módulo de Indagación Previa. Esta funcionalidad abarca:
1.  **Solicitud y Libramiento:** Generación automática de oficios para pruebas documentales (certificados, registros), testimoniales (declaraciones de terceros que conozcan los hechos) y periciales básicas (solo si son indispensables para la identificación).
2.  **Seguimiento:** Control del estado de cada prueba solicitada (Pendiente, En Trámite, Recepcionada, Practicada).
3.  **Recepción y Incorporación:** Carga digital de los resultados de las pruebas al expediente electrónico, asegurando la cadena de custodia digital y la reserva de la actuación.
4.  **Validación de Pertinencia:** El sistema alertará si una prueba solicitada excede el objeto de la indagación previa (ej. pruebas de fondo sobre la responsabilidad que corresponden a la investigación).

### ¿Para qué? (Objetivo)
Para cumplir con la carga probatoria establecida en el **Artículo 208 de la Ley 1952 de 2019**, permitiendo al funcionario contar con los elementos materiales necesarios para proferir el Auto de Archivo o el Auto de Apertura de Investigación Disciplinaria dentro del término de seis (6) meses, evitando la nulidad por práctica de pruebas impertinentes en esta etapa y garantizando el derecho de defensa del servidor público en averiguación.

### Referencias Normativas Directas
*   **Ley 1952 de 2019 (CGD), Artículo 208:** Define el objeto de la indagación previa y el término para su realización. Establece que solo se practicarán las pruebas necesarias para identificar al autor y determinar la existencia de la conducta.
*   **Ley 1952 de 2019 (CGD), Artículo 214:** Causales de apertura de investigación disciplinaria, las cuales dependen directamente del mérito de las pruebas recaudadas en esta etapa.
*   **Ley 1952 de 2019 (CGD), Artículo 115:** Principio de reserva de la actuación durante la indagación previa.
*   **Ley 1952 de 2019 (CGD), Artículo 121 y siguientes:** Régimen de notificaciones y comunicaciones electrónicas para el traslado de pruebas.
*   **Ley 2094 de 2021, Artículo 13:** Principio de separación de funciones entre quien indaga/instruye y quien juzga.
*   **Decreto 1083 de 2015 (Decreto Único Reglamentario del Sector Justicia):** Normas sobre gestión documental y archivo electrónico aplicables a la incorporación de pruebas.

---

## Dependencias y Precondiciones

1.  **Estado del Expediente:** El expediente electrónico debe encontrarse necesariamente en estado **"En Indagación Previa"**. No es posible gestionar pruebas de identificación si el expediente está en "Investigación Disciplinaria" (requiere otras pruebas) o "Archivo".
2.  **Asignación de Rol:** El usuario autenticado debe tener asignado el rol de **Funcionario de Instrucción** mediante acto administrativo de designación cargado en el sistema (HU-02 Shell y RBAC).
3.  **Existencia de Hechos:** Debe existir un registro previo de los "Hechos Conocidos" o la "Noticia Verbal/Escrita" que dio origen a la indagación, pues las pruebas deben versar exclusivamente sobre estos hechos para fines de identificación.
4.  **Configuración de Plantillas:** El sistema debe contar con las plantillas documentales preconfiguradas para los diferentes tipos de oficios (solicitud de certificados bancarios, laborales, declaraciones, etc.) aprobadas por la Oficina Jurídica.
5.  **Módulo de Notificaciones Activo:** Debe estar operativo el servicio de notificaciones electrónicas (HU-Módulo Notificaciones) para enviar los oficios a las entidades externas o citar a los testigos.
6.  **Almacenamiento Disponible:** El repositorio documental debe tener espacio disponible y política de retención configurada para los archivos digitales de las pruebas (PDF, Audio, Video).

---

## Restricciones y Reglas de Negocio

1.  **Limitación Objetiva (Regla de Oro):** El sistema **bloqueará** la solicitud de pruebas que tengan como objetivo exclusivo demostrar la responsabilidad disciplinaria o el dolo/culpa del servidor. En esta etapa solo se permiten pruebas para **identificar al autor** y confirmar la **existencia material de la conducta**. Cualquier prueba que busque establecer el juicio de imputación deberá reservarse para la etapa de Investigación Disciplinaria.
2.  **Término Perentorio:** Todas las pruebas gestionadas deben poder practicarse y incorporarse dentro del remanente del término de **seis (6) meses calendario**. El sistema no permitirá librar oficios cuya fecha probable de respuesta exceda el vencimiento del término de indagación, salvo justificación expresa autorizada por el Juez Disciplinario (excepcional).
3.  **Reserva Estricta:** Por mandato del Art. 115 CGD, todas las pruebas incorporadas en esta etapa tendrán automáticamente la etiqueta de **"RESERVADO"**. Solo serán visibles para el Funcionario de Instrucción y el Procurador Delegado. Ni siquiera el servidor público en averiguación tendrá acceso a ellas hasta que se decida la apertura de la investigación o se archive (momento en que se levanta la reserva según corresponda).
4.  **Prohibición de Interrogatorio al Investigado:** En indagación previa **no existe la figura del "indagatorio"** al servidor público. El sistema no habilitará formularios para tomar declaración al presunto autor en esta etapa, ya que aún no ha sido formalmente vinculado como investigado.
5.  **Cadena de Custodia Digital:** Toda prueba documental cargada debe generar automáticamente un hash de verificación (SHA-256) y registrar en el audit log quién, cuándo y desde qué IP se incorporó el documento.
6.  **Formatos Permitidos:**
    *   Documental: PDF/A (obligatorio para archivo), TIFF.
    *   Audio: MP3, WAV (máximo 1 hora por archivo).
    *   Video: MP4, AVI (máximo 500MB).
    *   Se prohíbe la carga de formatos ejecutables o editables (.docx, .xlsx) como prueba definitiva; deben ser convertidos a PDF.
7.  **Integridad del Documento:** Una vez incorporada una prueba al expediente, **no podrá ser eliminada ni modificada**. Solo se podrá adicionar un "Otrosí" o aclaración si hay error material, lo cual quedará registrado como una nueva versión vinculada, manteniendo la original inalterable.
8.  **Validación de Destinatarios:** Al librar un oficio a una entidad externa, el sistema validará que la entidad exista en el directorio oficial de entidades del Estado (DIRIP) y que el correo electrónico sea institucional (.gov.co).

---

## Supuestos Operativos

1.  **Conectividad con Entidades Externas:** Se asume que las entidades bancarias, registrales y otras dependencias estatales cuentan con canales de recepción de notificaciones electrónicas operativos para responder los oficios dentro de los términos legales.
2.  **Digitalización de Pruebas Físicas:** Si una prueba llega en formato físico (ej. un CD o un papel impreso), se asume que la Secretaría del despacho cuenta con los equipos de escaneo y digitalización para incorporarla al sistema inmediatamente después de recibida.
3.  **Capacitación del Usuario:** Se asume que el Funcionario de Instrucción conoce la diferencia técnica y jurídica entre una prueba de "identificación" (etapa actual) y una prueba de "responsabilidad" (etapa siguiente), para evitar solicitar pruebas que el sistema rechazará por improcedentes.
4.  **Disponibilidad de Firmantes:** Se asume que los testigos o peritos citados disponen de medios electrónicos para recibir las citaciones y, en lo posible, para rendir sus declaraciones de manera remota si el sistema lo habilita.

---

## Criterios de Aceptación (Gherkin)

### Escenario 1: Solicitud exitosa de prueba documental pertinente
**Dado** que el Funcionario de Instrucción se encuentra en un expediente en estado "Indagación Previa"
**Y** el término de vigencia de la indagación tiene más de 30 días calendario de vigencia restante
**Cuando** selecciona la opción "Solicitar Prueba Documental" y elige "Certificado Laboral" para identificar al servidor
**Y** completa los datos de la entidad solicitante y el objeto de la prueba (identificación)
**Entonces** el sistema genera el oficio con la plantilla oficial firmada digitalmente
**Y** envía la notificación electrónica a la entidad requerida
**Y** cambia el estado de la prueba a "En Trámite"
**Y** registra la acción en el historial de auditoría sin revelar detalles a otros roles.

### Escenario 2: Rechazo de prueba impertinente (Juicio de Responsabilidad)
**Dado** que el Funcionario de Instrucción intenta solicitar una prueba testimonial
**Cuando** en la descripción del objeto de la prueba escribe frases como "para demostrar que el servidor actuó con dolo" o "para establecer la responsabilidad disciplinaria"
**Entonces** el sistema muestra una alerta de validación normativa: *"Atención: En etapa de Indagación Previa (Art. 208 CGD) solo se permiten pruebas para identificación del autor y existencia de la conducta. Las pruebas sobre responsabilidad corresponden a la etapa de Investigación."*
**Y** bloquea el envío de la solicitud hasta que se corrija el objeto de la prueba.

### Escenario 3: Intento de tomar declaración al presunto autor (Prohibido)
**Dado** que el Funcionario de Instrucción desea interrogar a la persona que aparece en la noticia criminal
**Cuando** intenta crear una nueva actuación tipo "Indagatorio" o "Declaración del Investigado"
**Entonces** el sistema deshabilita la opción o muestra el mensaje: *"Acción no permitida: En la etapa de Indagación Previa no se ha formalizado la vinculación como investigado. No procede el interrogatorio directo."*
**Y** sugiere realizar una "Entrevista informal" solo si es estrictamente necesaria para identificación, marcándola como tal.

### Escenario 4: Incorporación de prueba con cadena de custodia
**Dado** que ha llegado la respuesta a un oficio librado (ej. certificado bancario)
**Cuando** el funcionario carga el archivo PDF al expediente
**Entonces** el sistema calcula automáticamente el hash SHA-256 del archivo
**Y** guarda el metadata de fecha, hora, usuario y IP de carga
**Y** marca el documento con la clasificación de seguridad "RESERVADO - ART. 115 CGD"
**Y** notifica al funcionario que la prueba ha sido incorporada exitosamente.

### Escenario 5: Alerta de vencimiento de término por práctica de pruebas
**Dado** que faltan 10 días calendario para el vencimiento del término de indagación previa
**Cuando** el funcionario intenta librar un nuevo oficio que requiere respuesta en 15 días hábiles
**Entonces** el sistema muestra una advertencia crítica: *"El término de respuesta estimado excede el tiempo restante de la Indagación Previa. Esta prueba podría quedar inconclusa y generar nulidad."*
**Y** solicita una justificación escrita obligatoria para proceder con el libramiento.

### Escenario 6: Visualización restringida por reserva de actuación
**Dado** que un abogado externo o el servidor público en averiguación intenta consultar el expediente
**Cuando** acceden al módulo de "Pruebas" o "Documentos"
**Entonces** el sistema oculta todos los documentos cargados en esta etapa
**Y** muestra el mensaje: *"Actuación en Reserva conforme al Art. 115 de la Ley 1952 de 2019. Solo visible para el Funcionario de Instrucción y autoridad competente."*

### Escenario 7: Modificación de prueba incorporada (Intento fallido)
**Dado** que una prueba ya fue incorporada al expediente con estado "Practicada"
**Cuando** el usuario intenta editar el archivo PDF o borrar el registro
**Entonces** el sistema deniega la operación con el mensaje: *"Inmutabilidad del Expediente: Las pruebas incorporadas no pueden ser modificadas ni eliminadas para garantizar la integridad probatoria."*
**Y** ofrece únicamente la opción de "Agregar Aclaración" como documento adjunto vinculado.

---

## Prototipo / Anexos

**Referencia al Prototipo de Pantalla:**
*   **Archivo Base:** `Pantallas VEED/15_gestion_indagacion_v1.html`
*   **Sección Específica:** Pestaña **"2. Pruebas"** y Modal de **"Nueva Solicitud de Prueba"**.

**Componentes UX/UI Detallados:**
1.  **Tabla de Gestión de Pruebas:**
    *   Columnas: Tipo (Icono), Descripción, Fecha Solicitud, Estado (Badge de color: Amarillo=Trámite, Verde=Practicada, Rojo=Vencida), Acciones (Ver, Descargar).
    *   Filtros: Por tipo de prueba, por estado, por fecha.
2.  **Botón Principal:** "Solicitar Nueva Prueba" (Color primario #063853).
3.  **Formulario Modal de Solicitud:**
    *   **Campo Desplegable "Tipo de Prueba":** Documental, Testimonial, Pericial. (No incluye "Interrogatorio").
    *   **Campo Texto "Objeto de la Prueba":** Con validación en tiempo real de palabras clave prohibidas ("responsabilidad", "dolo", "culpa", "sanción").
    *   **Campo "Entidad/Persona a Solicitar":** Autocompletado con validación de dominio institucional.
    *   **Check de Confirmación:** "Declaro que esta prueba es indispensable para la identificación del autor o la existencia de la conducta (Art. 208 CGD)".
4.  **Visualizador de Documentos:** Visor PDF integrado con marca de agua "RESERVADO" en diagonal.
5.  **Timeline de Trazabilidad:** Línea de tiempo vertical que muestra: Solicitud -> Envío Notificación -> Recepción -> Incorporación.

**Estilos Técnicos:**
*   **Fuente:** Poppins (Regular 400, Medium 500, Bold 600).
*   **Colores de Estado:**
    *   Pendiente: #FFA000 (Ámbar)
    *   En Trámite: #1976D2 (Azul)
    *   Practicada: #388E3C (Verde)
    *   Vencida/Rechazada: #D32F2F (Rojo)
*   **Iconografía:** Material Icons o FontAwesome (versión ligera).

---

## Stakeholders Involucrados

| Rol | Interés / Responsabilidad | Nivel de Influencia |
|-----|---------------------------|---------------------|
| **Funcionario de Instrucción** | Usuario principal. Requiere agilidad para librar oficios y certeza jurídica en la pertinencia de las pruebas. | Alto |
| **Secretario/a de Despacho** | Encargado de la recepción física/digital de respuestas y carga inicial al sistema. | Medio |
| **Oficina Jurídica / Control Interno** | Valida que las pruebas practicadas no vulneren el debido proceso ni la reserva. | Alto |
| **Procurador Delegado** | Supervisor de la actuación. Debe poder visualizar las pruebas reservadas para control de garantías. | Alto |
| **Equipo de TI / Seguridad** | Responsable de la integridad de los archivos, hashes de custodia y disponibilidad del módulo. | Medio |
| **Entidades Externas (Bancos, Registro, etc.)** | Receptores de los oficios. Requieren formatos estándar y canales seguros. | Bajo (Externo) |

---

## Plan de Validación y Pruebas

1.  **Prueba de Concepto Legal:** Revisión por parte de la Oficina Jurídica de 5 casos simulados donde el sistema deba diferenciar entre prueba de identificación (válida) y prueba de responsabilidad (inválida en esta etapa).
2.  **Prueba de Carga y Rendimiento:** Simulación de carga de 50 expedientes con 20 pruebas cada uno, verificando que el cálculo de hashes y la generación de oficios no exceda los 3 segundos por transacción.
3.  **Prueba de Seguridad (Penetration Testing):** Intento de acceso a las pruebas reservadas desde un usuario con rol de "Abogado Defensor" o "Ciudadano", verificando el bloqueo total (HTTP 403).
4.  **Prueba de Usabilidad:** Sesión con 3 funcionarios de instrucción reales para validar la claridad de los mensajes de error al intentar solicitar pruebas improcedentes.
5.  **Validación de Notificaciones:** Verificación end-to-end del envío de correos electrónicos a dominios externos (.gov.co, .com) con acuse de recibo digital.

---

## Matriz de Trazabilidad Normativa

| Requisito Funcional | Norma / Artículo | Justificación Legal | Cumplimiento |
|---------------------|------------------|---------------------|--------------|
| Bloqueo de pruebas de responsabilidad | Ley 1952/2019 Art. 208 | La indagación previa solo busca identificar al autor y la existencia de la conducta, no juzgar. | ✅ Implementado en validación de formulario |
| Reserva de las pruebas | Ley 1952/2019 Art. 115 | La actuación es reservada hasta que se decida la apertura o archivo. | ✅ Implementado en permisos de visualización (ACL) |
| Término perentorio de 6 meses | Ley 1952/2019 Art. 208 Parágrafo | El término es improrrogable. Las pruebas deben caber en este lapso. | ✅ Implementado en alerta de vencimiento |
| Prohibición de indagatorio | Ley 1952/2019 Art. 208 | No hay vinculación formal ni cargos en esta etapa. | ✅ Implementado en catálogo de tipos de prueba |
| Cadena de custodia digital | Ley 2094/2021 Art. 45 (Principios) | Garantía de integridad del material probatorio. | ✅ Implementado con Hash SHA-256 y Audit Log |
| Notificación electrónica | Ley 1952/2019 Art. 121 | Las comunicaciones a entidades se hacen por medios electrónicos. | ✅ Integrado con módulo de notificaciones |
| Separación de funciones | Ley 2094/2021 Art. 13 | Quien practica pruebas no es quien juzga. | ✅ Validado por rol de usuario (Instructor vs Juez) |

---

## Requisitos de Seguridad y Auditoría

1.  **Confidencialidad:**
    *   Cifrado de la base de datos en reposo (AES-256) para los metadatos de las pruebas.
    *   Cifrado de los archivos adjuntos en el almacenamiento (Object Storage Encryption).
    *   Máscara de datos sensibles en logs de aplicación (ej. no mostrar números de cuenta completos en el log, solo últimos 4 dígitos).

2.  **Integridad:**
    *   Firma digital de los oficios generados usando el certificado de la entidad (PKI).
    *   Hashing irreversible de cada documento cargado para detectar alteraciones posteriores.
    *   Bitácora de inmutabilidad: Cualquier intento de borrado queda registrado como "Intento fallido" con trazabilidad completa.

3.  **Disponibilidad:**
    *   Réplica síncrona de los archivos de pruebas en un sitio alterno (DRP).
    *   SLA del 99.5% para el módulo de consulta y carga de pruebas.

4.  **Auditoría (Audit Log):**
    *   Se debe registrar: `ID_Usuario`, `Rol`, `Timestamp`, `IP`, `Acción` (Crear, Ver, Descargar), `ID_Prueba`, `Resultado`.
    *   Los logs deben ser exportables en formato JSON inmutable para procesos de control fiscal o disciplinario contra el mismo funcionario.

---

## Protocolo de Respuesta a Incidentes

*   **Incidente:** Carga de prueba con virus o malware.
    *   **Acción:** El antivirus del gateway bloquea la subida. El sistema notifica al administrador de seguridad y registra el intento con la IP de origen.
*   **Incidente:** Fuga de información (una prueba reservada se hace pública).
    *   **Acción:** Revisión inmediata de los logs de acceso. Revocación de sesiones activas. Notificación a la Oficina de Seguridad de la Información. Informe a la Procuraduría por posible falla de seguridad.
*   **Incidente:** Caída del sistema durante la carga de una prueba crítica cerca del vencimiento.
    *   **Acción:** Habilitación de modo de contingencia (carga asíncrona con timestamp de aceptación válido jurídicamente). Extensión automática del plazo por fuerza mayor certificada por TI.

---

## Glosario de Términos

*   **Indagación Previa:** Etapa preliminar del proceso disciplinario destinada a verificar si hay mérito para abrir investigación.
*   **Prueba de Identificación:** Aquella dirigida exclusivamente a establecer quién es el servidor público involucrado y si el hecho ocurrió.
*   **Reserva de Actuación:** Principio que obliga a mantener en secreto el contenido del expediente frente a terceros y el propio investigado mientras dura la indagación.
*   **Oficio de Requerimiento:** Comunicación formal enviada por el funcionario a una entidad o particular para solicitar información o documentos.
*   **Cadena de Custodia:** Procedimiento controlado que se aplica a los rastros materiales, para asegurar que no fueron alterados.
*   **Hash SHA-256:** Algoritmo criptográfico que genera una huella digital única para cada archivo.

---

## Definition of Done (DoD) - Criterio de Terminado

La Historia de Usuario HU-15-02 se considerará **TERMINADA** cuando cumpla simultáneamente con:

- [ ] **Desarrollo:** Código implementado para el CRUD de pruebas, generación de oficios y validaciones de negocio.
- [ ] **Pruebas Unitarias:** Cobertura > 85% en lógica de validación de pertinencia de pruebas.
- [ ] **Pruebas de Integración:** Flujo completo probado desde la solicitud hasta la incorporación del documento.
- [ ] **Seguridad:** Validación exitosa de roles (Reserva Art. 115) y cifrado de archivos.
- [ ] **Documentación:** Manual de usuario actualizado con capturas de pantalla del flujo de solicitud de pruebas.
- [ ] **Validación Jurídica:** VoBo de la Oficina Jurídica confirmando que los textos de los oficios y las reglas de bloqueo cumplen la Ley 1952/2019.
- [ ] **Despliegue:** Funcionalidad desplegada en ambiente de QA y validada por el Product Owner.
- [ ] **Rendimiento:** Tiempo de respuesta en carga y consulta < 2 segundos.

---
*Fin del documento HU-15-02*
