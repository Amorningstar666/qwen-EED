# HISTORIA DE USUARIO HU-15-01: CONSULTAR Y VALIDAR TÉRMINO DE INDAGACIÓN PREVIA

| **Fecha** | **ID Historia** | **Creado por** | **Validado por** | **Estado** | **Versión** |
|-----------|-----------------|----------------|------------------|------------|-------------|
| 13/05/2026 | HU-15-01 | Analista de Negocio - Equipo PGN | Líder Técnico - Arquitectura EED | Pendiente | 1.0 |

---

## INFORMACIÓN GENERAL DEL PROCESO

| **Macroproceso** | **Proceso** | **Actividad** | **Subactividad** | **Clasificación** |
|------------------|-------------|---------------|------------------|-------------------|
| M4 - Gestión Jurídica Disciplinaria | P17 - Instrucción y Evaluación Descargos | A32 - Control de Términos Procesales | SA01 - Consulta y Validación de Término Indagación Previa | Funcionalidad Crítica - Cumplimiento Normativo |

| **Valor de Negocio** | **Prioridad** | **Complejidad** | **Puntos Story** | **Sprint Objetivo** |
|----------------------|---------------|-----------------|------------------|---------------------|
| Garantizar el cumplimiento del término perentorio de 6 meses establecido en el Art. 208 CGD, evitando nulidades por vencimiento de términos y asegurando la debida diligencia en la investigación disciplinaria | Alta | Media | 8 | Sprint 15 |

---

## DESCRIPCIÓN DETALLADA DE LA HISTORIA DE USUARIO

### ¿QUIÉN? (Rol del Usuario)

El **Funcionario de Instrucción** (rol sistémico: `instructor`), quien es el servidor público designado mediante auto de apertura de indagación previa para llevar a cabo las actuaciones investigativas preliminares establecidas en el Artículo 208 de la Ley 734 de 2002 (Código General Disciplinario). Este rol corresponde a un abogado o profesional del derecho con facultades delegadas por la autoridad disciplinaria competente para practicar pruebas, decretar oficios, recibir declaraciones y determinar si existen méritos para abrir investigación disciplinaria formal o archivar las actuaciones.

**Perfil del Usuario:**
- Profesional universitario con título en Derecho o áreas afines
- Conocimiento avanzado en procedimiento disciplinario ordinario
- Capacitación certificada en uso del Sistema Expediente Electrónico Disciplinario (EED)
- Clave tokenizada o certificado digital vigente para firma electrónica de actos procesales
- Asignación formal mediante resolución o auto de designación registrado en el sistema

### ¿QUÉ? (Funcionalidad Requerida)

El usuario requiere **consultar, visualizar y validar el término vigente de la etapa de Indagación Previa** asociada a un expediente disciplinario específico, mediante un widget interactivo que calcule automáticamente los días hábiles transcurridos y faltantes para el vencimiento del término perentorio de seis (6) meses establecido en el Artículo 208 del Código General Disciplinario.

La funcionalidad debe incluir:
1. Visualización clara del estado actual del término mediante semáforo de alertas (verde, amarillo, rojo)
2. Cálculo automático de días hábiles descontando sábados, domingos, festivos oficiales de Colombia y días de receso judicial
3. Registro y cálculo de prórrogas excepcionales por causas relacionadas con Derechos Humanos (DDHH) o Derecho Internacional Humanitario (DIH) conforme al parágrafo del Art. 208 CGD
4. Historial cronológico de todas las actuaciones que han generado interrupción, suspensión o reanudación del término
5. Alertas proactivas cuando el término esté próximo a vencer (30 días, 15 días, 5 días, 24 horas)
6. Posibilidad de generar informes de estado del término para inclusión en autos y providencias
7. Integración con el calendario oficial colombiano y el calendario judicial interno de la Procuraduría General de la Nación

### ¿PARA QUÉ? (Objetivo y Justificación)

Esta funcionalidad permite **garantizar el debido proceso y el principio de celeridad procesal** establecidos en el Artículo 29 de la Constitución Política de Colombia y el Artículo 76 del Código General Disciplinario, asegurando que el funcionario de instrucción conozca en todo momento el tiempo disponible para culminar las actuaciones de indagación previa antes de que opere la caducidad de la facultad disciplinaria o se configuren causales de nulidad por actuación fuera de término.

**Beneficios Específicos:**
- **Prevención de Nulidades:** Evita que las actuaciones se realicen fuera del término legal, lo que acarrearía nulidad de pleno derecho conforme al Artículo 114 CGD
- **Optimización de la Gestión:** Permite al funcionario priorizar expedientes próximos a vencer y distribuir eficientemente su carga laboral
- **Transparencia Procesal:** Ofrece trazabilidad completa del cómputo del término para control de las partes y órganos de vigilancia
- **Cumplimiento de Metas Institucionales:** Contribuye al cumplimiento de los indicadores de gestión de la Procuraduría en materia de descongestión y eficiencia procesal
- **Seguridad Jurídica:** Brinda certeza a los sujetos procesales sobre el estado temporal de la investigación

**Impacto Normativo:**
El incumplimiento del término de indagación previa puede generar:
- Caducidad de la acción disciplinaria (Art. 154 CGD)
- Nulidad de las actuaciones practicadas fuera de término (Art. 114 CGD)
- Responsabilidad disciplinaria del funcionario por retardo injustificado (Art. 48 CGD)
- Acciones de tutela por vulneración al derecho al debido proceso

---

## DEPENDENCIAS Y PRECONDICIONES

### Dependencias Técnicas

| **ID** | **Dependencia** | **Descripción** | **Estado** | **HU Relacionada** |
|--------|-----------------|-----------------|------------|---------------------|
| D01 | Módulo de Autenticación Centralizada | El usuario debe estar autenticado mediante OAuth 2.0 + JWT con certificado digital vigente | Implementado | HU-02 (Shell y RBAC) |
| D02 | Servicio de Calendario Oficial Colombiano | API externa que proporciona los días festivos nacionales y locales de Colombia | Implementado | HU-05 (Configuración Calendario) |
| D03 | Motor de Cálculo de Días Hábiles | Algoritmo interno que descuenta sábados, domingos y festivos del cómputo del término | En Desarrollo | HU-15-01 |
| D04 | Repositorio Documental del Expediente | Base de datos que almacena todas las actuaciones procesales del expediente | Implementado | HU-08 (Gestión Expediente) |
| D05 | Sistema de Notificaciones Electrónicas | Módulo para envío de alertas por correo electrónico y notificaciones en plataforma | Implementado | HU-12 (Notificaciones) |
| D06 | Servicio de Auditoría y Trazabilidad | Registro inmutable de todas las consultas y acciones realizadas sobre el término | Implementado | HU-03 (Audit Log) |

### Precondiciones de Negocio

| **ID** | **Precondición** | **Validación Requerida** | **Fundamento Legal** |
|--------|------------------|--------------------------|----------------------|
| P01 | El expediente debe encontrarse en estado "En Indagación Previa" | Verificar campo `estado_etapa = 'INDAGACION_PREVIA'` en tabla `expedientes` | Art. 208 CGD |
| P02 | Debe existir auto de apertura de indagación previa debidamente notificado | Confirmar registro de auto con fecha de ejecutoria en tabla `autos_procesales` | Art. 208 CGD |
| P03 | El usuario consultante debe tener rol `instructor` asignado al expediente | Validar relación en tabla `asignaciones_exp_funcionario` donde `rol = 'instructor'` | Art. 76 CGD |
| P04 | Debe haber fecha de inicio válida registrada para el cómputo del término | Campo `fecha_inicio_indagacion` no nulo en tabla `terminos_procesales` | Art. 208 CGD |
| P05 | El sistema debe tener configurado el calendario oficial colombiano vigente | Tabla `calendario_festivos` actualizada con resolución de festivos del año en curso | Decreto 2247/2017 |
| P06 | No debe existir causal de terminación anticipada de la etapa | Verificar que no haya auto de archivo o apertura investigación con ejecutoria | Art. 208 Parágrafo CGD |

### Precondiciones Técnicas

1. El navegador del usuario debe soportar JavaScript ES6+ para la ejecución del widget de cálculo
2. La conexión a internet debe tener latencia menor a 200ms para garantizar respuesta en tiempo real
3. El certificado digital del usuario debe estar vigente y no revocado
4. El servicio de cálculo de días hábiles debe estar disponible con uptime mínimo del 99.5%

---

## RESTRICCIONES Y REGLAS DE NEGOCIO

### Restricciones Normativas

| **ID** | **Restricción** | **Fundamento Legal** | **Consecuencia por Incumplimiento** |
|--------|-----------------|----------------------|-------------------------------------|
| R01 | El término de indagación previa es perentorio e improrrogable, salvo excepción DDHH/DIH | Art. 208 Parágrafo CGD | Nulidad de actuaciones posteriores |
| R02 | El cómputo del término se realiza en días hábiles, excluyendo sábados, domingos y festivos | Art. 93 CGD | Cálculo erróneo del vencimiento |
| R03 | La prórroga por causas DDHH/DIH no puede exceder la mitad del término original (3 meses) | Art. 208 Parágrafo CGD | Improcedencia de la prórroga |
| R04 | Las decisiones tomadas en indagación previa (archivo o apertura) no son susceptibles de recurso | Art. 208 Parágrafo CGD | Inadmisión de recursos interpuestos |
| R05 | Toda actuación debe quedar registrada con fecha y hora exacta para efectos del cómputo | Art. 76 Numeral 10 CGD | Imposibilidad de verificar oportunidad |
| R06 | El instructor no puede ser el mismo funcionario que juzgue el caso (separación de funciones) | Art. 13 Ley 2094/2021 | Nulidad por violación al debido proceso |
| R07 | Las actuaciones de indagación previa están sujetas a reserva hasta tanto se decida la apertura | Art. 115 CGD | Vulneración de derechos del investigado |

### Reglas de Cálculo del Término

| **Regla ID** | **Descripción** | **Fórmula/Aplicación** | **Ejemplo** |
|--------------|-----------------|------------------------|-------------|
| RC01 | Fecha de inicio del término | `fecha_inicio = fecha_ejecutoria_auto_apertura_indagacion` | Auto notificado el 15/01/2026, ejecutoriado el 20/01/2026 → Inicio: 20/01/2026 |
| RC02 | Término ordinario | `termino_ordinario = 6 meses calendario convertidos a días hábiles` | 20/01/2026 + 6 meses ≈ 130 días hábiles (varía según festivos) |
| RC03 | Descuento de días inhábiles | `dias_habiles = dias_calendario - (sabados + domingos + festivos)` | Entre 20/01/2026 y 20/07/2026 hay 182 días calendario, 52 sábados, 52 domingos, 8 festivos → 70 días hábiles reales |
| RC04 | Prórroga DDHH/DIH | `prorroga_maxima = termino_ordinario / 2` | Si término ordinario = 130 días hábiles → Prórroga máxima = 65 días hábiles |
| RC05 | Suspensión del término | `fecha_reanudacion = fecha_suspension + duracion_causal` | Suspensión por fuerza mayor del 01/03/2026 al 15/03/2026 → Reanuda 16/03/2026 |
| RC06 | Interrupción del término | `nuevo_inicio = fecha_interrupcion` | Interrupción por recusación del instructor → Nuevo cómputo desde notificación auto que resuelve |
| RC07 | Vencimiento del término | `fecha_vencimiento = fecha_inicio + termino_ordinario + prorroga_aprobada` | Inicio 20/01/2026 + 130 días hábiles = Vencimiento 25/07/2026 |

### Restricciones Técnicas

| **ID** | **Restricción Técnica** | **Especificación** |
|--------|-------------------------|--------------------|
| RT01 | Tiempo de respuesta del widget | Máximo 2 segundos para cálculo y visualización del término |
| RT02 | Disponibilidad del servicio | 99.5% uptime en horario hábil (6:00 AM - 8:00 PM lunes a viernes) |
| RT03 | Precisión del cálculo | Exactitud del 100% en el cómputo de días hábiles según calendario oficial |
| RT04 | Compatibilidad de navegadores | Chrome 90+, Firefox 88+, Edge 90+, Safari 14+ |
| RT05 | Accesibilidad | Cumplimiento WCAG 2.1 Nivel AA para usuarios con discapacidad visual |
| RT06 | Seguridad de datos | Encriptación AES-256 en reposo y TLS 1.3 en tránsito |
| RT07 | Registro de auditoría | Todas las consultas deben quedar registradas con timestamp, usuario IP y acción |

---

## SUPUESTOS OPERATIVOS

| **ID** | **Supuesto** | **Justificación** | **Plan de Contingencia** |
|--------|--------------|-------------------|--------------------------|
| S01 | El calendario oficial colombiano es publicado anualmente antes del 1 de diciembre del año anterior | Decreto 2247/2017 obliga al Ministerio del Trabajo a publicar festivos | Si no hay calendario oficial, usar último calendario disponible y actualizar cuando sea publicado |
| S02 | El funcionario de instrucción tiene acceso estable a internet durante su jornada laboral | La Procuraduría provee conectividad institucional a todos sus funcionarios | Habilitar modo offline con sincronización diferida cuando se restablezca la conexión |
| S03 | Las fechas de ejecutoria de los autos son registradas oportunamente por el secretario del despacho | Es función del secretario llevar control de estados procesales (Art. 76 CGD) | Implementar alerta de recordatorio para registro de ejecutorias pendientes > 5 días |
| S04 | No habrá cambios legislativos que modifiquen el término de indagación previa durante la vigencia del sistema | El término de 6 meses está consolidado desde Ley 734/2002 sin modificaciones | Diseñar arquitectura configurable para permitir actualización de términos sin cambio de código |
| S05 | Los servidores del sistema estarán disponibles en horario extendido para consulta | La carga procesal requiere acceso fuera de horario tradicional | Implementar balanceo de carga y escalado automático para picos de demanda |

---

## CRITERIOS DE ACEPTACIÓN (FORMATO GHERKIN)

### Escenario 1: Consulta Exitosa del Término con Semáforo Verde

```gherkin
DADO que soy un Funcionario de Instrucción con rol "instructor" asignado al expediente DISC-2026-001234
Y el expediente se encuentra en estado "En Indagación Previa" iniciado hace 45 días hábiles
Y la fecha actual es 15 de marzo de 2026
CUANDO accedo al módulo "Gestión de Indagación Previa" y selecciono la pestaña "Término"
ENTONCES el sistema debe mostrar un widget con semáforo en color VERDE
Y debe indicar "Término Vigente: 85 días hábiles restantes de 130 días totales"
Y debe mostrar la fecha de vencimiento estimada: "Vencimiento: 25 de julio de 2026"
Y debe mostrar una línea de tiempo con hitos procesales registrados hasta la fecha
Y el tiempo de carga del widget no debe exceder 2 segundos
```

### Escenario 2: Alerta Amarilla por Vencimiento Próximo (30 días)

```gherkin
DADO que soy un Funcionario de Instrucción con rol "instructor" asignado al expediente DISC-2026-005678
Y el expediente se encuentra en estado "En Indagación Previa" iniciado hace 100 días hábiles
Y la fecha actual es 10 de junio de 2026
Y faltan exactamente 30 días hábiles para el vencimiento del término
CUANDO accedo al módulo "Gestión de Indagación Previa" y selecciono la pestaña "Término"
ENTONCES el sistema debe mostrar un widget con semáforo en color AMARILLO
Y debe indicar "ALERTA: Término próximo a vencer - 30 días hábiles restantes"
Y debe mostrar la fecha de vencimiento: "Vencimiento: 25 de julio de 2026"
Y debe desplegar un mensaje destacado: "Se recomienda priorizar las actuaciones pendientes"
Y debe enviar automáticamente una notificación por correo electrónico al instructor y su jefe inmediato
Y debe registrar en audit log la generación de la alerta amarilla
```

### Escenario 3: Alerta Roja Crítica por Vencimiento Inminente (5 días o menos)

```gherkin
DADO que soy un Funcionario de Instrucción con rol "instructor" asignado al expediente DISC-2026-009012
Y el expediente se encuentra en estado "En Indagación Previa" iniciado hace 125 días hábiles
Y la fecha actual es 18 de julio de 2026
Y faltan exactamente 5 días hábiles para el vencimiento del término
CUANDO accedo al módulo "Gestión de Indagación Previa" y selecciono la pestaña "Término"
ENTONCES el sistema debe mostrar un widget con semáforo en color ROJO parpadeante
Y debe indicar "CRÍTICO: Vencimiento inminente - 5 días hábiles restantes"
Y debe mostrar la fecha de vencimiento en rojo destacado: "Vencimiento: 25 de julio de 2026"
Y debe desplegar una alerta modal bloqueante que requiera confirmación de lectura
Y debe enviar automáticamente notificación urgente por correo electrónico, SMS y notificación push
Y debe copiar la notificación al Secretario General y al Procurador Delegado
Y debe generar un informe automático de estado para inclusión en auto de prórroga si aplica
Y debe registrar en audit log la generación de la alerta roja con timestamp exacto
```

### Escenario 4: Cálculo con Prórroga por Causas DDHH/DIH

```gherkin
DADO que soy un Funcionario de Instrucción con rol "instructor" asignado al expediente DISC-2026-003456
Y el expediente involucra presuntas violaciones a Derechos Humanos cometidas en contexto de conflicto armado
Y fue solicitada y aprobada prórroga excepcional por 60 días hábiles por causa DDHH/DIH
Y el término ordinario de 130 días hábiles ya fue consumido en su totalidad
CUANDO accedo al módulo "Gestión de Indagación Previa" y selecciono la pestaña "Término"
ENTONCES el sistema debe mostrar un widget indicando "Término en Prórroga Excepcional DDHH/DIH"
Y debe indicar "Días restantes de prórroga: 60 días hábiles de 60 días autorizados"
Y debe mostrar la nueva fecha de vencimiento: "Vencimiento con prórroga: 15 de octubre de 2026"
Y debe mostrar el auto que aprobó la prórroga con enlace al documento PDF firmado
Y debe indicar claramente que la prórroga no puede superar el 50% del término original
Y debe advertir que vencida la prórroga opera caducidad de la acción disciplinaria
```

### Escenario 5: Visualización de Historial de Interrupciones y Suspensiones

```gherkin
DADO que soy un Funcionario de Instrucción consultando el expediente DISC-2026-007890
Y el término de indagación previa ha tenido 2 suspensiones y 1 interrupción registradas
Y la primera suspensión fue por fuerza mayor (desastre natural) del 10/02/2026 al 20/02/2026
Y la segunda suspensión fue por espera de prueba pericial del 15/04/2026 al 30/04/2026
Y la interrupción fue por recusación del instructor original del 05/05/2026 al 12/05/2026
CUANDO accedo a la pestaña "Historial del Término" dentro del widget de consulta
ENTONCES el sistema debe mostrar una línea de tiempo cronológica con todos los eventos
Y debe indicar claramente los períodos de suspensión con icono de pausa
Y debe indicar claramente los períodos de interrupción con icono de reinicio
Y debe calcular y mostrar "Días hábiles suspendidos: 25 días"
Y debe calcular y mostrar "Días hábiles interrumpidos: 7 días (reinicio de cómputo)"
Y debe mostrar la fecha de vencimiento recalculada considerando todos los eventos
Y debe permitir descargar el historial en formato PDF con validez probatoria
```

### Escenario 6: Error por Falta de Rol Autorizado

```gherkin
DADO que soy un usuario con rol "auxiliar_archivo" sin asignación como instructor
Y intento acceder al módulo "Gestión de Indagación Previa" para el expediente DISC-2026-001111
CUANDO selecciono la pestaña "Término" desde el menú principal
ENTONCES el sistema debe denegar el acceso al widget de consulta
Y debe mostrar un mensaje: "ACCESO DENEGADO: Usted no tiene rol de Funcionario de Instrucción asignado a este expediente"
Y debe sugerir: "Si considera que debería tener acceso, contacte al Secretario de su Despacho"
Y debe registrar en audit log el intento de acceso no autorizado con IP, timestamp y usuario
Y debe enviar alerta de seguridad al administrador del sistema si hay más de 3 intentos fallidos
```

### Escenario 7: Cálculo Incorrecto por Festivo No Registrado

```gherkin
DADO que el sistema tiene desactualizado el calendario de festivos y no registra el festivo del 20 de julio de 2026
Y soy un Funcionario de Instrucción consultando el término del expediente DISC-2026-002222
Y la fecha actual es 15 de julio de 2026
Y el sistema calcula incorrectamente incluyendo el 20 de julio como día hábil
CUANDO detecto que el cálculo incluye un día festivo nacional no registrado
ENTONCES debo poder reportar el error mediante botón "Reportar Error en Cálculo"
Y el sistema debe crear un ticket automático para el equipo de soporte técnico
Y debe marcar el cálculo como "Sujeto a Verificación" con bandera amarilla
Y debe permitir al usuario ingresar manualmente la corrección con justificación
Y debe requerir aprobación del Secretario General para aplicar la corrección
Y una vez corregido, debe recalcular automáticamente la fecha de vencimiento
Y debe notificar a todas las partes del expediente sobre la corrección aplicada
```

### Escenario 8: Generación de Informe de Estado del Término

```gherkin
DADO que soy un Funcionario de Instrucción necesitando incluir en un auto información detallada del término
Y he consultado exitosamente el término del expediente DISC-2026-003333
CUANDO hago clic en el botón "Generar Informe de Estado del Término"
ENTONCES el sistema debe generar un documento PDF con membrete institucional
Y debe incluir: número de expediente, nombre del instructor, fecha de inicio del término
Y debe incluir: término total en días hábiles, días transcurridos, días restantes
Y debe incluir: fecha de vencimiento ordinaria y con prórrogas si aplican
Y debe incluir: listado cronológico de todas las actuaciones registradas
Y debe incluir: estado actual del semáforo (verde/amarillo/rojo)
Y debe incluir: firma electrónica del funcionario y sello de tiempo certificado
Y el documento debe ser descargable y tener validez probatoria como anexo del auto
```

---

## PROTOTIPO DE PANTALLA Y REFERENCIAS UX

### Prototipo Asociado

**Archivo de Referencia:** `/workspace/Pantallas VEED/15_gestion_indagacion_v1.html`

**Pestaña Específica:** Pestaña 1 - "Término Indagación"

### Componentes de Interfaz Requeridos

| **Componente** | **ID en Prototipo** | **Descripción** | **Comportamiento Esperado** |
|----------------|---------------------|-----------------|----------------------------|
| Widget Semáforo | `widget-semaforo-term` | Círculo LED con colores verde/amarillo/rojo | Cambia de color según días restantes (>30 verde, 30-5 amarillo, <5 rojo) |
| Label Días Restantes | `lbl-dias-restantes` | Texto grande mostrando "X días hábiles restantes" | Actualización en tiempo real al cargar la página |
| Label Fecha Vencimiento | `lbl-fecha-vencimiento` | Texto con fecha proyectada de vencimiento | Formato DD/MM/YYYY, color rojo si < 15 días |
| Barra de Progreso | `progress-term-indag` | Barra horizontal 0-100% con fill animado | Porcentaje = (días_transcurridos / días_totales) * 100 |
| Timeline Hitos | `timeline-hitosterm` | Línea vertical con nodos de actuaciones | Scrollable, cada nodo muestra fecha, tipo actuación y descripción corta |
| Botón Generar Informe | `btn-generar-informe-term` | Botón primario con ícono de descarga | Abre modal de confirmación y genera PDF al aceptar |
| Botón Reportar Error | `btn-reportar-error-calc` | Botón secundario con ícono de alerta | Abre formulario de reporte de inconsistencias en cálculo |
| Modal Alerta Crítica | `modal-alerta-critica` | Ventana emergente bloqueante | Se activa automáticamente cuando días_rest <= 5, requiere click en "Entendido" |
| Tabla Prórrogas | `tabla-prorrogas-ddhh` | Grid con prórrogas DDHH/DIH aprobadas | Columnas: Auto, Fecha, Días Autorizados, Días Consumidos, Estado |
| Tooltip Informativo | `tooltip-info-term` | Ícono de información con hover | Muestra resumen del Art. 208 CGD al pasar el mouse |

### Tokens de Diseño PGN Aplicados

| **Token** | **Valor** | **Aplicación** |
|-----------|-----------|----------------|
| `--pgn-color-primary` | #063853 | Encabezados, botones primarios, bordes activos |
| `--pgn-color-secondary` | #FFE601 | Alertas amarillas, destacados, iconos informativos |
| `--pgn-color-danger` | #E3201B | Alertas rojas, errores, vencimientos críticos |
| `--pgn-color-success` | #28A745 | Semáforo verde, confirmaciones, estados favorables |
| `--pgn-font-family` | 'Segoe UI', Roboto, sans-serif | Tipografía general de toda la interfaz |
| `--pgn-border-radius` | 4px | Bordes de botones, tarjetas, inputs |
| `--pgn-shadow-card` | 0 2px 8px rgba(6, 56, 83, 0.15) | Sombras de tarjetas y widgets |

### Wireframe Detallado de la Pestaña Término

```
+----------------------------------------------------------------------------------+
|  EXPEDIENTE: DISC-2026-001234  |  ETAPA: Indagación Previa  |  INSTRUCTOR: Dr. Pérez  |
+----------------------------------------------------------------------------------+
|  [TÉRMINO]  [PRUEBAS]  [PERSONA]  [DOCUMENTOS]  [ACTUACIONES]  [HISTORIAL]  [DECISIÓN]  |
+----------------------------------------------------------------------------------+
|                                                                                  |
|  +----------------------------------------------------------------------------+  |
|  |                    ESTADO DEL TÉRMINO DE INDAGACIÓN PREVIA                 |  |
|  +----------------------------------------------------------------------------+  |
|  |                                                                              |  |
|  |   (●) SEMÁFORO                                                               |  |
|  |    VERDE                                                                     |  |
|  |                                                                              |  |
|  |   Término Vigente                                                            |  |
|  |   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━            |  |
|  |   [████████████████████████░░░░░░░░░░░░░░░░░░░░░░░░░░] 65% completado        |  |
|  |                                                                              |  |
|  |   Días Transcurridos: 85 de 130 días hábiles                                 |  |
|  |   Días Restantes: 45 días hábiles                                            |  |
|  |   Fecha de Vencimiento: 25 de julio de 2026                                  |  |
|  |                                                                              |  |
|  |   ℹ️ El término de indagación previa es de 6 meses perentorios (Art. 208 CGD)|  |
|  |                                                                              |  |
|  +----------------------------------------------------------------------------+  |
|                                                                                  |
|  +----------------------------------------------------------------------------+  |
|  |                         HITOS PROCESALES REGISTRADOS                       |  |
|  +----------------------------------------------------------------------------+  |
|  |                                                                              |  |
|  |   ● 20/01/2026 - Auto de Apertura de Indagación Previa (Fecha Inicio)       |  |
|  |   ● 25/01/2026 - Notificación al Quejado                                     |  |
|  |   ● 10/02/2026 - Decreto de Pruebas Testimoniales                            |  |
|  |   ● 15/03/2026 - Recepción de Declaración del Denunciante                    |  |
|  |   ● 30/04/2026 - Solicitud de Concepto Técnico                               |  |
|  |                                                                              |  |
|  |   [Ver todos los hitos →]                                                    |  |
|  |                                                                              |  |
|  +----------------------------------------------------------------------------+  |
|                                                                                  |
|  +----------------------------------------------------------------------------+  |
|  |                              PRÓRROGAS EXCEPCIONALES                       |  |
|  +----------------------------------------------------------------------------+  |
|  |                                                                              |  |
|  |   No se han registrado prórrogas por causas DDHH/DIH para este expediente.   |  |
|  |                                                                              |  |
|  |   [Solicitar Prórroga DDHH/DIH] (Solo habilitado si hay justificación)      |  |
|  |                                                                              |  |
|  +----------------------------------------------------------------------------+  |
|                                                                                  |
|  [📄 Generar Informe de Estado]    [⚠️ Reportar Error en Cálculo]                |
|                                                                                  |
+----------------------------------------------------------------------------------+
```

---

## STAKEHOLDERS Y VALIDACIÓN REQUERIDA

### Matriz de Stakeholders

| **Stakeholder** | **Rol** | **Interés en la HU** | **Responsabilidad** | **Nivel de Influencia** |
|-----------------|---------|----------------------|---------------------|-------------------------|
| Funcionario de Instrucción | Usuario Primario | Consultar término para cumplir plazos | Realizar consultas diarias, actuar según alertas | Alto |
| Secretario del Despacho | Usuario Secundario | Verificar registros de actuaciones | Registrar fechas de ejecutoria y notificaciones | Medio |
| Sujeto Procesal (Quejado) | Beneficiario Indirecto | Conocer estado temporal de la investigación | Recibir notificaciones de vencimiento si aplica | Bajo |
| Procurador Delegado | Supervisor | Monitorear cumplimiento de metas de descongestión | Revisar informes de expedientes próximos a vencer | Alto |
| Oficina de Gestión Procesal | Área de Apoyo | Consolidar estadísticas de términos procesales | Generar reportes institucionales de cumplimiento | Medio |
| Equipo de Desarrollo EED | Implementador | Codificar widget de cálculo y semáforo | Desarrollar, probar y desplegar funcionalidad | Alto |
| Área de Seguridad TI | Control | Garantizar integridad y confidencialidad del cálculo | Auditar logs de consultas y accesos | Medio |
| Oficina Jurídica Institucional | Validador Normativo | Verificar conformidad con Art. 208 CGD | Revisar y aprobar reglas de cálculo implementadas | Alto |
| Auditoría Interna | Control | Verificar trazabilidad de las consultas | Revisar audit logs periódicamente | Medio |

### Plan de Validación

| **Actividad** | **Responsable** | **Fecha Estimada** | **Criterio de Aprobación** | **Entregable** |
|---------------|-----------------|--------------------|----------------------------|----------------|
| Revisión de Reglas de Cálculo | Oficina Jurídica PGN | 15/05/2026 | Todas las reglas alineadas con Art. 208 y 93 CGD | Acta de Validación Normativa firmada |
| Prueba de Usabilidad con Instructores | UX Lead + 5 instructores reales | 20/05/2026 | 80% de tareas completadas sin asistencia | Reporte de Usabilidad con hallazgos |
| Validación de Cálculo con Casos Prueba | QA Lead + Secretario experto | 22/05/2026 | 100% de coincidencia en 50 casos de prueba | Matriz de Pruebas ejecutada y aprobada |
| Auditoría de Seguridad | CISO PGN | 25/05/2026 | Sin vulnerabilidades críticas o altas | Informe de Pentest aprobado |
| Aprobación Final para Producción | Product Owner PGN | 28/05/2026 | Todos los criterios anteriores cumplidos | Acta de Aceptación de HU firmada |

---

## MATRIZ DE TRAZABILIDAD NORMATIVA

| **Artículo/Norma** | **Tipo** | **Descripción** | **Requisito Asociado** | **Criterio Aceptación** | **Estado** |
|--------------------|----------|-----------------|------------------------|-------------------------|------------|
| Art. 208 CGD | Ley 734/2002 | Término de 6 meses para indagación previa | RC01, RC02 | Escenarios 1, 2, 3 | Implementado |
| Art. 208 Parágrafo CGD | Ley 734/2002 | Prórroga excepcional por DDHH/DIH | RC04 | Escenario 4 | Implementado |
| Art. 93 CGD | Ley 734/2002 | Cómputo de términos en días hábiles | RC02, RC03 | Escenarios 1, 5 | Implementado |
| Art. 76 Numeral 10 CGD | Ley 734/2002 | Deber de registrar fechas de actuaciones | R05 | Escenario 5 | Implementado |
| Art. 114 CGD | Ley 734/2002 | Nulidad por actuaciones fuera de término | R01 | Escenario 3 | Implementado |
| Art. 115 CGD | Ley 734/2002 | Reserva de las actuaciones | R07 | Escenario 6 | Implementado |
| Art. 29 Constitución | CP 1991 | Debido proceso y celeridad | Descripción "Para Qué" | Todos los escenarios | Implementado |
| Art. 13 Ley 2094/2021 | Ley 2094/2021 | Separación instructor-juzgador | R06 | Escenario 6 | Implementado |
| Decreto 2247/2017 | Decreto | Festivos oficiales Colombia | S01, RC03 | Escenario 7 | Implementado |
| Ley 1712/2014 | Ley | Transparencia y acceso a información | Generación de informes | Escenario 8 | Implementado |
| Ley 1581/2012 | Ley | Protección de datos personales | RT06, Seguridad | Escenario 6 | Implementado |
| Acuerdo PSAA16-10438 | CSJ | Calendario judicial | S01, RC03 | Escenario 7 | Implementado |

---

## CONSIDERACIONES DE SEGURIDAD Y AUDITORÍA

### Requisitos de Seguridad

| **ID** | **Requisito** | **Implementación Técnica** | **Normativa Aplicable** |
|--------|---------------|----------------------------|-------------------------|
| SEG01 | Autenticación fuerte obligatoria | OAuth 2.0 + JWT + Certificado Digital X.509 | Art. 76 CGD, Ley 1581/2012 |
| SEG02 | Autorización basada en roles (RBAC) | Middleware de validación de rol `instructor` por expediente | Art. 13 Ley 2094/2021 |
| SEG03 | Encriptación de datos en reposo | AES-256 para base de datos de términos y actuaciones | Ley 1581/2012 Art. 17 |
| SEG04 | Encriptación de datos en tránsito | TLS 1.3 para todas las comunicaciones cliente-servidor | Decreto 1008/2018 |
| SEG05 | Prevención de inyección SQL | Prepared statements y ORM con sanitización automática | OWASP Top 10 A03 |
| SEG06 | Control de sesiones concurrentes | Máximo 3 sesiones activas por usuario, invalidación por inactividad > 15 min | Política de Seguridad PGN |
| SEG07 | Mascaramiento de datos sensibles | Ocultar últimos dígitos de documentos de identidad en logs | Ley 1581/2012 Principio de Seguridad |

### Requisitos de Auditoría

| **ID** | **Evento a Auditar** | **Datos a Registrar** | **Retención** | **Acceso al Log** |
|--------|----------------------|-----------------------|---------------|-------------------|
| AUD01 | Consulta de término | Usuario, IP, timestamp, expediente, días_rest, estado_semaforo | 10 años | Auditoría Interna, Procurador Delegado |
| AUD02 | Generación de informe | Usuario, IP, timestamp, expediente, tipo_informe, hash_documento | 10 años | Auditoría Interna, Oficina Jurídica |
| AUD03 | Reporte de error | Usuario, IP, timestamp, expediente, descripción_error, ticket_id | 10 años | Soporte TI, Auditoría Interna |
| AUD04 | Intento de acceso no autorizado | Usuario, IP, timestamp, expediente, rol_usuario, motivo_denegacion | 10 años | Seguridad TI, Auditoría Interna |
| AUD05 | Modificación de cálculo manual | Usuario, IP, timestamp, expediente, valor_anterior, valor_nuevo, justificacion, aprobador | 10 años | Auditoría Interna, Procurador General |
| AUD06 | Alerta automática generada | Tipo_alerta, timestamp, expediente, dias_rest, destinatarios_notificados | 10 años | Oficina de Gestión Procesal |

### Protocolo de Respuesta a Incidentes

1. **Detección:** Monitoreo continuo de logs de auditoría mediante SIEM
2. **Clasificación:** Severidad basada en impacto (Crítico, Alto, Medio, Bajo)
3. **Contención:** Bloqueo preventivo de usuario o expediente si hay sospecha de manipulación
4. **Investigación:** Análisis forense de logs, entrevistas a involucrados, revisión de cámaras si aplica
5. **Remediación:** Corrección de vulnerabilidad, restablecimiento de datos, capacitación adicional
6. **Lecciones Aprendidas:** Documento post-incidente con mejoras preventivas

---

## DEFINICIÓN DE TERMINADO (DoD)

### Criterios Obligatorios para Cierre de HU

| **Categoría** | **Criterio** | **Verificación** | **Responsable** | **Estado** |
|---------------|--------------|------------------|-----------------|------------|
| **Documentación** | Historia de usuario completa y aprobada | Revisión en Jira/Confluence | Product Owner | ☐ Pendiente |
| **Documentación** | Diagrama de flujo del cálculo de términos | Adjunto en repositorio documental | Analista de Negocio | ☐ Pendiente |
| **Documentación** | Manual de usuario con capturas de pantalla | PDF disponible en portal de capacitación | Líder de Capacitación | ☐ Pendiente |
| **Desarrollo** | Widget de semáforo implementado según prototipo | Demo en ambiente de QA | Desarrollador Frontend | ☐ Pendiente |
| **Desarrollo** | Algoritmo de cálculo de días hábiles unit-tested | Cobertura > 90% en tests unitarios | Desarrollador Backend | ☐ Pendiente |
| **Desarrollo** | Integración con API de calendario oficial | Pruebas de integración exitosas | Arquitecto de Software | ☐ Pendiente |
| **Pruebas** | Todos los escenarios Gherkin automatizados | Ejecución 100% pass en pipeline CI/CD | QA Engineer | ☐ Pendiente |
| **Pruebas** | Pruebas de carga con 100 usuarios concurrentes | Tiempo respuesta < 2 segundos en p95 | Performance Engineer | ☐ Pendiente |
| **Pruebas** | Pruebas de accesibilidad WCAG 2.1 AA | Reporte de herramienta automatizada + validación manual | Especialista UX | ☐ Pendiente |
| **Seguridad** | Scan de vulnerabilidades sin hallazgos críticos/altos | Reporte de SonarQube + OWASP ZAP | Security Engineer | ☐ Pendiente |
| **Seguridad** | Audit logs verificados con datos completos | Muestreo de 50 eventos en Kibana | Auditor Interno | ☐ Pendiente |
| **Despliegue** | Deploy exitoso en ambiente de Staging | Smoke tests pass después de deploy | DevOps Engineer | ☐ Pendiente |
| **Despliegue** | Plan de rollback documentado y probado | Simulación de rollback ejecutada | DevOps Engineer | ☐ Pendiente |
| **Capacitación** | Sesión de entrenamiento con 10 instructores piloto | Lista de asistencia + evaluación > 80% | Líder de Cambio | ☐ Pendiente |
| **Aceptación** | Sign-off formal del Product Owner | Acta de aceptación firmada digitalmente | Product Owner | ☐ Pendiente |

### Criterios de Salida por Ambiente

| **Ambiente** | **Criterios de Promoción** | **Aprobador** |
|--------------|----------------------------|---------------|
| Desarrollo → QA | Todos los unit tests pass, código revisado en PR, sin bugs críticos | Tech Lead |
| QA → Staging | 100% escenarios Gherkin pass, performance OK, seguridad OK | QA Manager |
| Staging → Producción | UAT aprobado por 5 usuarios piloto, plan de rollback listo, comunicación enviada | Product Owner + CTO |

---

## ANEXOS Y REFERENCIAS ADICIONALES

### Documentos de Referencia

1. **Código General Disciplinario (Ley 734 de 2002)** - Arts. 208, 93, 76, 114, 115
2. **Ley 2094 de 2021** - Reforma al régimen disciplinario, Art. 13 (separación de funciones)
3. **Decreto 2247 de 2017** - Festivos oficiales en Colombia
4. **Manual de Procedimiento Disciplinario PGN** - Versión 3.2, Capítulo de Indagación Previa
5. **Política de Seguridad de la Información PGN** - Documento interno clasificado
6. **Guía de Usabilidad para Sistemas Judiciales** - Consejo Superior de la Judicatura, 2024

### Glosario de Términos

| **Término** | **Definición** |
|-------------|----------------|
| Indagación Previa | Etapa preliminar del procedimiento disciplinario destinada a determinar si hay mérito para abrir investigación formal (Art. 208 CGD) |
| Día Hábil | Día que no es sábado, domingo ni festivo oficial en Colombia (Art. 93 CGD) |
| Prórroga DDHH/DIH | Extensión excepcional del término cuando la investigación involucra violaciones a derechos humanos en contexto de conflicto armado |
| Semáforo de Alerta | Indicador visual que muestra el estado de urgencia del término (verde=vigente, amarillo=próximo, rojo=crítico) |
| Audit Log | Registro inmutable y cronológico de todas las acciones realizadas en el sistema |
| RBAC | Role-Based Access Control, modelo de autorización basado en roles de usuario |

### Historias de Usuario Relacionadas

| **ID HU** | **Nombre** | **Relación** |
|-----------|------------|--------------|
| HU-15-02 | Gestionar Pruebas de Identificación | Hermana - misma etapa de indagación |
| HU-15-03 | Visualizar Persona en Averiguación | Hermana - misma etapa de indagación |
| HU-15-07 | Proyectar Decisión Final | Hermana - culmina la etapa de indagación |
| HU-08-01 | Consultar Expediente Disciplinario | Padre - funcionalidad general de consulta |
| HU-02 | Shell y RBAC | Dependencia - autenticación y autorización |
| HU-05 | Configuración de Calendario | Dependencia - fuente de festivos oficiales |
| HU-12 | Notificaciones Electrónicas | Dependencia - envío de alertas de vencimiento |

---

## CONTROL DE CAMBIOS

| **Versión** | **Fecha** | **Autor** | **Descripción del Cambio** | **Aprobado por** |
|-------------|-----------|-----------|----------------------------|------------------|
| 1.0 | 13/05/2026 | Analista de Negocio EED | Creación inicial de la HU-15-01 | Líder Técnico |
| | | | | |

---

**FIN DE LA HISTORIA DE USUARIO HU-15-01**

*Documento generado bajo estándar PGN para el Proyecto Expediente Electrónico Disciplinario (EED)*
*Procuraduría General de la Nación - República de Colombia*
