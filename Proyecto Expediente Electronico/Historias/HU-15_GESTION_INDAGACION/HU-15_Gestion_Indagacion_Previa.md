# 📄 HISTORIA DE USUARIO — EED PROCURADURÍA
**ID HU:** HU-15 | **Fecha:** 12-05-2026 | **Creado por:** Consultora EED | **Validado por:** [Pendiente]
**Macroproceso:** Proceso Disciplinario | **Proceso:** Instrucción - Indagación Previa | **Actividad:** Gestión de actuaciones y seguimiento de términos
**Clasificación:** Funcional | **Valor de negocio:** Permitir al Funcionario de Instrucción gestionar eficazmente la etapa de Indagación Previa con trazabilidad auditada, cálculo automático de términos y cumplimiento del Art. 208 CGD

## 👥 DESCRIPCIÓN DE LA HISTORIA DE USUARIO
**¿Quién?** Funcionario de Instrucción (rol: instructor)
**¿Qué?** Gestionar las actuaciones procesales de la etapa de Indagación Previa, incluyendo consulta de estado del expediente, visualización de términos perentorios, decreto y seguimiento de pruebas, y proyección de decisiones finales (archivo o apertura de investigación)
**¿Para qué?** Garantizar el cumplimiento del término de 6 meses establecido en el Art. 208 CGD para la indagación previa, asegurando la identificación del posible autor de la conducta disciplinable con trazabilidad completa, cálculo automático de días hábiles colombianos y reserva de la actuación según Art. 115 CGD

## 🔗 DEPENDENCIA(S) Y/O PRECONDICIÓN(ES)
1. Expediente disciplinario creado y en estado "En Indagación Previa" (Art. 208 CGD)
2. Usuario autenticado con rol "Funcionario de Instrucción" asignado al expediente mediante reparto (Art. 76 CGD)
3. Módulo de Shell de Navegación activo (HU-02) con controles RBAC que separan funciones de instructor y juzgador
4. Calendario oficial colombiano configurado para cálculo de días hábiles (DDHH)
5. Notificación electrónica habilitada conforme Art. 122 CGD para comunicaciones a sujetos procesales

## 🚫 RESTRICCIONES
1. **Separación funcional estricta:** El rol instructor NO puede acceder a funciones de juzgamiento (Art. 13 Ley 2094/2021)
2. **Reserva de la actuación:** Durante indagación previa aplica reserva total conforme Art. 115 CGD - solo visible para funcionario asignado, superior jerárquico y secretario jurídico
3. **Término perentorio:** 6 meses improrrogables salvo violación de DDHH/DIH (6 meses adicionales) - el sistema debe alertar vencimiento inminente
4. **Decisiones sin recurso:** Las decisiones en indagación previa no proceden recursos (Art. 208 CGD parágrafo)
5. **Audit trail inmutable:** Toda acción debe registrarse con usuario, timestamp certificado, contexto y IP
6. **Accesibilidad WCAG 2.1 AA:** Contrastes, navegación por teclado, etiquetas ARIA en todos los componentes
7. **Datos ficticios de prueba:** Usar siempre datos anonimizados en ambiente de desarrollo

## 📌 SUPUESTOS
1. El expediente proviene de evaluación de noticia disciplinaria que determinó apertura de indagación previa (HU-05)
2. El sistema integra calendario oficial colombiano para exclusión de domingos y festivos
3. Existe módulo de notificaciones electrónicas integrado con DOKUS o sistema equivalente
4. El funcionario cuenta con firma digital calificada para proyectar actos administrativos
5. La sesión expira después de 15 minutos de inactividad por seguridad de datos sensibles

## ✅ CRITERIO(S) DE ACEPTACIÓN (GHERKIN)

### Escenario 1: Acceso exitoso a gestión de indagación previa con validación de rol
**Dado que:** Un Funcionario de Instrucción autenticado tiene asignado un expediente en estado "En Indagación Previa"
**Cuando:** Accede al módulo "Gestión de Indagación Previa" desde el dashboard o menú de navegación
**Entonces:** El sistema valida que el rol corresponde al perfil instructor (RBAC), carga la pantalla 15_gestion_indagacion_v1.html mostrando:
   - Datos generales del expediente (número radicado, fecha inicio, estado actual)
   - Widget de términos con semáforo visual calculando días hábiles restantes según Art. 208 CGD
   - Panel de actuaciones procesales con historial auditado
   - Botones de acción habilitados según estado del expediente
   - Mensaje de reserva de la actuación conforme Art. 115 CGD

### Escenario 2: Visualización correcta del widget de términos con cálculo de días hábiles
**Dado que:** El expediente se encuentra en etapa de Indagación Previa con fecha de inicio registrada
**Cuando:** El sistema calcula el término restante usando el calendario oficial colombiano
**Entonces:** El widget muestra:
   - Días hábiles restantes en formato numérico grande (ej: "84 DDHH")
   - Barra de progreso visual con código de colores: verde (>50% tiempo), amarillo (25-50%), naranja (10-25%), rojo (<10%)
   - Fechas exactas de inicio y vencimiento del término
   - Botón "Solicitar Prórroga" habilitado solo si aplica (violación DDHH/DIH - Art. 208 CGD)
   - Alerta automática cuando faltan menos de 10 días hábiles para vencimiento

### Escenario 3: Registro de nueva actuación procesal con trazabilidad auditada
**Dado que:** El funcionario necesita registrar una actuación (ej: decreto de prueba, oficio librado, recepción de documento)
**Cuando:** Selecciona el tipo de actuación, completa los campos obligatorios y guarda
**Entonces:** El sistema:
   - Valida campos obligatorios según tipo de actuación
   - Registra la actuación con número consecutivo, fecha/hora certificada, usuario y IP
   - Actualiza el panel de actuaciones procesales inmediatamente
   - Genera entrada en audit_log inmutable con contexto completo
   - Muestra confirmación al usuario con número de registro
   - Notifica electrónicamente a sujetos procesales si aplica (Art. 123 CGD)

### Escenario 4: Proyección de decisión de archivo por no identificación del autor
**Dado que:** Ha transcurrido el término de indagación previa sin identificar al posible autor
**Cuando:** El funcionario proyecta auto de archivo conforme Art. 208 CGD
**Entonces:** El sistema:
   - Valida que el término haya vencido o esté próximo a vencer
   - Verifica que no se haya identificado al autor en las actuaciones
   - Permite proyectar auto de archivo con motivación fáctica y jurídica
   - Bloquea proyección si existen pruebas pendientes sin practicar
   - Genera borrador del auto con estructura normativa del Art. 208 CGD
   - Envía a flujo de aprobación del superior jerárquico
   - Registra trazabilidad completa de la proyección

### Escenario 5: Proyección de auto de apertura de investigación disciplinaria
**Dado que:** Se identificó al posible autor de la conducta durante la indagación previa
**Cuando:** El funcionario proyecta auto de apertura de investigación disciplinaria
**Entonces:** El sistema:
   - Valida que exista identificación plena del investigado (nombre, documento, cargo, entidad)
   - Verifica que los hechos estén descritos conforme Art. 215 CGD
   - Permite incluir pruebas decretadas y orden de incorporación de antecedentes
   - Genera borrador del auto con elementos obligatorios del Art. 215 CGD
   - Cambia estado del expediente a "En Investigación Disciplinaria" tras aprobación
   - Notifica personalmente al investigado conforme Art. 121 CGD
   - Activa nuevo término de investigación (6 meses - Art. 213 CGD)

### Escenario 6: Alerta crítica de vencimiento inminente del término
**Dado que:** Faltan menos de 10 días hábiles para vencer el término de indagación previa
**Cuando:** El funcionario ingresa al expediente o el sistema ejecuta job nocturno de verificación
**Entonces:** El sistema:
   - Muestra alerta visual roja en widget de términos y banner superior
   - Envía notificación electrónica al funcionario y su superior jerárquico
   - Registra la alerta en audit_log con timestamp
   - Sugiere acciones prioritarias para culminar la etapa
   - Bloquea creación de nuevas actuaciones no esenciales

### Escenario 7: Consulta de historial de actuaciones con filtro y búsqueda
**Dado que:** El funcionario necesita revisar actuaciones anteriores del expediente
**Cuando:** Utiliza los filtros por tipo de actuación, fecha o texto libre
**Entonces:** El sistema:
   - Filtra el panel de actuaciones procesales en tiempo real
   - Muestra resultados con resaltado de coincidencias
   - Permite exportar listado en PDF/A con validez documental
   - Mantiene trazabilidad de la consulta en audit_log

### Escenario 8: Error de acceso por rol no autorizado
**Dado que:** Un usuario con rol diferente a "Funcionario de Instrucción" intenta acceder
**Cuando:** Un funcionario de juzgamiento o ciudadano intenta ingresar al módulo
**Entonces:** El sistema:
   - Bloquea el acceso inmediatamente
   - Muestra mensaje genérico de "No tiene permisos para acceder a este módulo"
   - Registra intento de acceso no autorizado en audit_log con IP y timestamp
   - Redirecciona al dashboard correspondiente a su rol

## 🖼️ PROTOTIPO / ANEXOS
- **Pantalla de referencia:** `/workspace/Pantallas VEED/15_gestion_indagacion_v1.html`
- **Componentes UX identificados:**
  - Navbar institucional con breadcrumb de navegación
  - Panel izquierdo: Índice navegable de secciones del expediente
  - Panel central: Editor de actuaciones procesales con widget de términos
  - Panel derecho: Semáforo de términos, alertas críticas, botones de acción rápida
  - Botón flotante procuradurIA con asistencia IA trazada (no decisoria)
- **Tokens de marca PGN aplicados:**
  - Colores: #063853 (azul), #FFE601 (amarillo), #E3201B (rojo)
  - Tipografía: Montserrat (títulos, labels, botones), Poppins (cuerpo)
- **Stakeholders:** 
  - Funcionario de Instrucción | Firma: [Pendiente]
  - Oficina Control Interno Disciplinario Veeduría | Firma: [Pendiente]
  - Área Jurídica PGN | Validación normativa: [Pendiente]

---

## ⚖️ VALIDACIÓN NORMATIVA EXPLÍCITA

| Artículo CGD | Aplicación en HU-15 | Cumplimiento |
|---|---|---|
| Art. 208 CGD | Término de 6 meses para indagación previa, finalidad de identificar autor | ✅ Widget de términos calcula DDHH, decisiones de archivo/apertura |
| Art. 115 CGD | Reserva de la actuación por etapa procesal | ✅ Panel de reservas, control de acceso por roles, advertencias visuales |
| Art. 121 CGD | Notificación personal al investigado | ✅ Integración con módulo de notificaciones para auto de apertura |
| Art. 122 CGD | Notificación electrónica con autorización previa | ✅ Configuración de preferencias de notificación |
| Art. 123 CGD | Notificación de decisiones interlocutorias | ✅ Notificación automática de providencias en indagación |
| Art. 214 CGD | Ruptura de unidad procesal | ✅ Soporte para escisión de expediente si identifica algunos autores |
| Art. 224 CGD | Recurso de apelación contra archivo | ✅ Flujo de aprobación y recursos en proyección de archivo |
| Ley 2094/2021 Art. 13 | Separación instructor/juzgador | ✅ RBAC estricto, bloqueo de funciones cruzadas |

---

## 🔒 CONSIDERACIONES DE SEGURIDAD Y AUDITORÍA

1. **Autenticación:** OAuth 2.0 + JWT con refresh token
2. **Autorización:** RBAC + ABAC basado en asignación de expediente
3. **Cifrado:** AES-256 para datos en reposo, TLS 1.3 para datos en tránsito
4. **Audit Log:** Inmutable, con timestamp certificado y hash encadenado
5. **Session Management:** Timeout 15 min, máximo 3 intentos fallidos
6. **Data Privacy:** Anonimización en ambientes de desarrollo, Habeas Data (Ley 1581/2012)

---

❓ **Validación:** ¿Esta HU refleja correctamente el flujo de Indagación Previa, los roles del Funcionario de Instrucción y la normativa del Art. 208 CGD? ¿Requiere ajustes antes de proceder con HU descompuestas (ej: HU-15-01 para decreto de pruebas, HU-15-02 para proyección de auto de archivo)?
