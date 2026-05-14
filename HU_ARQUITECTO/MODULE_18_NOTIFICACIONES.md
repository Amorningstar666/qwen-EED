# Módulo 18: Notificaciones y Comunicaciones

## Índice de Historias de Usuario

| ID | Historia de Usuario | Prioridad | Estado |
|----|---------------------|-----------|--------|
| HU-18-01 | Crear nuevas notificaciones manuales y automáticas a sujetos procesales | Alta | ✅ Completada |
| HU-18-02 | Gestionar comunicaciones a quejosos, terceros, tutelas y solicitudes de juzgados | Alta | 📝 En desarrollo |
| HU-18-03 | Consultar bandeja de notificaciones pendientes y enviadas del expediente | Media | ⏳ Pendiente |
| HU-18-04 | Registrar fecha de entendida y gestionar acuses de recibo | Alta | ⏳ Pendiente |
| HU-18-05 | Reenviar notificaciones fallidas y gestionar incidencias de entrega | Media | ⏳ Pendiente |
| HU-18-06 | Generar reportes de trazabilidad y auditoría de notificaciones | Baja | ⏳ Pendiente |

---

## HU-18-02: Gestionar comunicaciones a quejosos, terceros, tutelas y solicitudes de juzgados

### Descripción
Como **Funcionario de la entidad**,  
quiero **gestionar comunicaciones oficiales dirigidas a quejosos (Art. 129 CGD), terceros involucrados, procesos de tutela y solicitudes de otros juzgados**,  
para **garantizar el debido proceso, la participación de las partes y el cumplimiento de los requerimientos interinstitucionales**.

### Criterios de Aceptación

| ID | Criterio | Tipo |
|----|----------|------|
| CA-02-01 | El sistema debe permitir seleccionar el tipo de destinatario: Quejoso, Tercero, Ente Judicial (Tutela), Otro Juzgado | Funcional |
| CA-02-02 | Debe validar automáticamente los datos de contacto del destinatario según el rol seleccionado | Funcional |
| CA-02-03 | Para quejosos, debe aplicar lo dispuesto en el Art. 129 del CGD (notificación personal) | Normativo |
| CA-02-04 | Debe permitir adjuntar documentos soporte de la comunicación (oficios, autos, providencias) | Funcional |
| CA-02-05 | Debe generar un número único de radicado para cada comunicación externa | Funcional |
| CA-02-06 | El sistema debe clasificar las comunicaciones por urgencia: Normal, Urgente, Prioritaria | Funcional |
| CA-02-07 | Debe permitir redactar el cuerpo del mensaje utilizando plantillas predefinidas según el tipo | Funcional |
| CA-02-08 | Las comunicaciones a otros juzgados deben incluir los metadatos requeridos para interoperabilidad (Radicado origen, asunto, clase de proceso) | Funcional |
| CA-02-09 | Debe registrar la fecha y hora exacta de generación y envío de la comunicación | Técnico |
| CA-02-10 | El sistema debe impedir el envío si faltan datos obligatorios del destinatario o del documento | Validación |

### Escenarios de Prueba (Gherkin)

#### Escenario 1: Envío de comunicación a Quejoso (Art. 129 CGD)
```gherkin
DADO que el funcionario está en el módulo de notificaciones
Y selecciona "Nueva Comunicación"
Y elige el tipo de destinatario "Quejoso"
CUANDO ingresa los datos del quejoso y adjunta el acto administrativo
Y valida que cumple con el Art. 129 del CGD
ENTONCES el sistema habilita el botón "Enviar"
Y genera el radicado de la comunicación
Y registra la salida en la bitácora del expediente.
```

#### Escenario 2: Solicitud de información a otro Juzgado
```gherkin
DADO que se requiere solicitar información a un juzgado de otra entidad
Y el funcionario selecciona "Comunicación a Ente Judicial"
CUANDO diligencia el formulario con el radicado de origen y el asunto
Y adjunta la solicitud formal
ENTONCES el sistema valida la estructura del oficio
Y envía la comunicación por el canal de interoperabilidad habilitado
Y notifica al funcionario el éxito del envío.
```

#### Escenario 3: Comunicación a Tercero en proceso de Tutela
```gherkin
DADO que existe un proceso de tutela vinculado al expediente
Y se requiere notificar o comunicar algo a un tercero
CUANDO el funcionario selecciona "Tercero - Tutela"
Y asocia la comunicación al expediente de tutela correspondiente
ENTONCES el sistema vincula automáticamente la comunicación al trámite de tutela
Y notifica al tercero según el medio registrado.
```

### Datos de Prueba

| Campo | Valor Ejemplo 1 | Valor Ejemplo 2 |
|-------|-----------------|-----------------|
| Tipo Destinatario | Quejoso | Otro Juzgado |
| Nombre Destinatario | Juan Pérez Rodríguez | Juzgado 45 Civil Municipal Bogotá |
| Medio Notificación | Correo Electrónico | Plataforma Tyba/Notificaciones Judiciales |
| Asunto | Notificación Auto No. 123 | Solicitud de Copias Expediente |
| Prioridad | Urgente | Normal |
| Documento Adjunto | Auto_123.pdf | Solicitud_Info.pdf |
| Radicado Generado | COM-2024-00158 | COM-2024-00159 |

### Trazabilidad

| Requisito Legal / Técnico | Huella en el Sistema |
|---------------------------|----------------------|
| Art. 129 CGD (Notificación Personal) | Registro de entrega personal o electrónica certificada |
| Art. 133 CGD (Notificación Electrónica) | Uso de correo electrónico válido y acuse de recibo |
| Interoperabilidad Judicial | Envío vía red judicial o plataforma habilitada |
| Auditoría | Log inmutable de creación, envío y recepción |

### Definición de Terminado (DoD)
- [ ] Código implementado y probado en ambiente de desarrollo.
- [ ] Pruebas unitarias y de integración aprobadas (Cobertura > 85%).
- [ ] Validación de normas CGD aplicables.
- [ ] Documentación de API actualizada.
- [ ] Aprobación por parte del área jurídica.

---

## HU-18-03: Consultar bandeja de notificaciones pendientes y enviadas del expediente

### Descripción
Como **Funcionario o Administrador del Expediente**,  
quiero **visualizar en una bandeja unificada las notificaciones pendientes por enviar y las ya realizadas asociadas al expediente**,  
para **tener control total del estado de las comunicaciones y asegurar que ninguna notificación quede sin gestionar**.

### Criterios de Aceptación

| ID | Criterio | Tipo |
|----|----------|------|
| CA-03-01 | El sistema debe mostrar dos pestañas principales: "Pendientes" y "Enviadas/Realizadas" | Funcional |
| CA-03-02 | La lista de pendientes debe ordenarse por fecha de generación (más antiguas primero) | Funcional |
| CA-03-03 | Cada registro debe mostrar: Destinatario, Tipo Notificación, Estado, Fecha Límite, Acciones | Funcional |
| CA-03-04 | Debe permitir filtrar por tipo de notificación, destinatario, estado y rango de fechas | Funcional |
| CA-03-05 | Las notificaciones vencidas o próximas a vencer deben tener indicadores visuales de alerta | UI/UX |
| CA-03-06 | Al hacer clic en un registro, se debe mostrar el detalle completo de la notificación | Funcional |
| CA-03-07 | Desde la bandeja de pendientes, se debe poder ejecutar la acción de "Enviar" directamente | Funcional |
| CA-03-08 | La bandeja de enviadas debe permitir descargar el comprobante de entrega o acuse | Funcional |
| CA-03-09 | El sistema debe actualizar el estado en tiempo real si cambia (ej. de "Enviado" a "Entregado") | Técnico |
| CA-03-10 | Debe mostrar el conteo total de notificaciones por estado en un resumen superior | UI/UX |

### Escenarios de Prueba (Gherkin)

#### Escenario 1: Visualización de bandeja de pendientes
```gherkin
DADO que el usuario ingresa al módulo de notificaciones
Y existen 5 notificaciones pendientes para el expediente actual
CUANDO el sistema carga la pestaña "Pendientes"
ENTONCES muestra las 5 notificaciones ordenadas por fecha de creación
Y resalta en rojo aquellas que han superado su fecha límite de envío.
```

#### Escenario 2: Filtrado de notificaciones enviadas
```gherkin
DADO que el usuario está en la pestaña "Enviadas"
Y desea ver solo las notificaciones electrónicas de la última semana
CUANDO aplica el filtro por Tipo "Electrónica" y Rango de fechas "Últimos 7 días"
ENTONCES el sistema muestra únicamente los registros que coinciden
Y actualiza el contador total de resultados.
```

#### Escenario 3: Acceso a detalle y comprobante
```gherkin
DADO que el usuario selecciona una notificación enviada exitosamente
CUANDO hace clic en el botón "Ver Detalle"
ENTONCES el sistema muestra el modal con toda la información
Y habilita el botón "Descargar Acuse" si está disponible.
```

### Datos de Prueba

| Campo | Valor Ejemplo |
|-------|---------------|
| Estado Pendiente | Por Enviar, Vencida, Próxima a Vencer |
| Estado Enviada | Entregada, Leída, Fallida, En Proceso |
| Tipo Notificación | Electrónica, Personal, Edicto, Correo Postal |
| Fecha Límite | 2024-10-25 |
| Destinatario | Abogado Demandante, Ministerio Público |

### Trazabilidad

| Elemento | Detalle |
|----------|---------|
| Fuente de Datos | Tabla `NOTIFICACIONES_EXPEDIENTE` |
| Actualización | Evento en tiempo real vía WebSocket o Polling |
| Seguridad | Solo usuarios con permiso de lectura del expediente |

### Definición de Terminado (DoD)
- [ ] Interfaz de bandeja implementada con paginación y filtros.
- [ ] Conexión exitosa con el servicio de notificaciones.
- [ ] Pruebas de carga para listados grandes (>1000 registros).
- [ ] Indicadores visuales de estado implementados correctamente.

---

## HU-18-04: Registrar fecha de entendida y gestionar acuses de recibo

### Descripción
Como **Funcionario de Notificaciones**,  
quiero **registrar la fecha y hora en que el destinatario recibió y entendió la notificación, así como gestionar los acuses de recibo digitales o físicos**,  
para **cumplir con los requisitos legales de notificación válida y contar con prueba fehaciente de la comunicación**.

### Criterios de Aceptación

| ID | Criterio | Tipo |
|----|----------|------|
| CA-04-01 | El sistema debe capturar automáticamente la fecha/hora de apertura del correo electrónico (si es posible) | Técnico |
| CA-04-02 | Debe permitir el registro manual de la "Fecha de Entendida" cuando la notificación es personal | Funcional |
| CA-04-03 | Debe exigir la firma digital o huella del destinatario para notificaciones personales presenciales | Funcional |
| CA-04-04 | El acuse de recibo electrónico debe generarse automáticamente al abrir la notificación (píxel de tracking o link de confirmación) | Técnico |
| CA-04-05 | Debe almacenar el PDF del acuse de recibo firmado en el expediente digital | Funcional |
| CA-04-06 | El sistema debe notificar al funcionario cuando se confirme la "Entendida" | Funcional |
| CA-04-07 | En caso de negativa a firmar, debe permitir registrar la constancia de negativa con testigos | Funcional |
| CA-04-08 | La fecha de entendida no puede ser anterior a la fecha de envío | Validación |
| CA-04-09 | Debe quedar registro de la IP y dispositivo desde donde se confirmó la recepción (electrónica) | Técnico/Seguridad |
| CA-04-10 | El estado de la notificación debe cambiar automáticamente a "Entendida" al registrar este dato | Funcional |

### Escenarios de Prueba (Gherkin)

#### Escenario 1: Confirmación automática de entendida (Electrónica)
```gherkin
DADO que una notificación electrónica fue enviada al abogado
Y el abogado hace clic en el enlace de "Confirmar Recepción"
CUANDO el sistema detecta la apertura y confirmación
ENTONCES registra automáticamente la "Fecha de Entendida"
Y adjunta el log de conexión como acuse de recibo
Y cambia el estado a "Entendida".
```

#### Escenario 2: Registro manual de entendida (Personal)
```gherkin
DADO que el notificador realiza una visita presencial
Y el destinatario recibe y entiende la notificación
CUANDO el notificador ingresa al sistema desde su dispositivo móvil
Y registra la hora exacta y toma la firma digital del destinatario
ENTONCES el sistema guarda el acta de notificación personal
Y actualiza el expediente con la fecha de entendida.
```

#### Escenario 3: Constancia de negativa
```gherkin
DADO que el destinatario se niega a recibir la notificación
CUANDO el notificador selecciona la opción "Negativa a Recibir"
Y registra los datos de los dos testigos presentes
ENTONCES el sistema genera el acta de negativa
Y se tiene por surtida la notificación según la ley (Art. 135 CGD o equivalente).
```

### Datos de Prueba

| Campo | Valor Ejemplo |
|-------|---------------|
| Método Confirmación | Click Link, Firma Digital, Manual |
| Fecha Entendida | 2024-10-26 14:30:00 |
| IP Origen | 190.15.20.10 |
| Dispositivo | Chrome / Windows 10 |
| Testigo 1 | María Gómez, CC 123456 |
| Testigo 2 | Carlos Ruiz, CC 654321 |

### Trazabilidad

| Norma | Aplicación |
|-------|------------|
| Art. 135 CGD (Se tiene por surtida) | Registro de negativa con testigos |
| Ley 527 de 1999 (Mensaje de datos) | Validez del acuse electrónico |
| Decreto 1083 de 2015 | Firma digital y validez jurídica |

### Definición de Terminado (DoD)
- [ ] Mecanismo de tracking electrónico implementado.
- [ ] Formulario de registro manual con firma digital funcional.
- [ ] Generación de PDF de acuses integrada.
- [ ] Pruebas de seguridad de los logs de IP y dispositivos.

---

## HU-18-05: Reenviar notificaciones fallidas y gestionar incidencias de entrega

### Descripción
Como **Administrador del Sistema de Notificaciones**,  
quiero **identificar, reintentar y gestionar las notificaciones que fallaron en su primer intento de entrega**,  
para **asegurar que todos los sujetos procesales sean notificados correctamente y subsanar errores técnicos o de datos**.

### Criterios de Aceptación

| ID | Criterio | Tipo |
|----|----------|------|
| CA-05-01 | El sistema debe detectar automáticamente los rebotes de correos electrónicos (Hard Bounce / Soft Bounce) | Técnico |
| CA-05-02 | Debe clasificar el motivo del fallo: Dirección inválida, Buzón lleno, Servidor caído, Error de formato | Funcional |
| CA-05-03 | Debe permitir al funcionario corregir el dato de contacto y reenviar la notificación | Funcional |
| CA-05-04 | Para fallos recurrentes, el sistema debe sugerir cambiar el medio de notificación (ej. de Electrónica a Personal) | Inteligente |
| CA-05-05 | Debe llevar un conteo de intentos de reenvío por notificación (Máximo 3 intentos automáticos) | Funcional |
| CA-05-06 | Debe generar una alerta task para el funcionario cuando una notificación falla más de 2 veces | Funcional |
| CA-05-07 | El historial de intentos fallidos debe quedar registrado en la bitácora de la notificación | Auditoría |
| CA-05-08 | Debe permitir adjuntar justificación del fallo técnico si es reportado por el proveedor de correo | Funcional |
| CA-05-09 | El reenvío debe mantener el mismo contenido original salvo que se indique lo contrario | Funcional |
| CA-05-10 | Si el fallo es por indisponibilidad del sistema externo, debe programar reintentos automáticos escalonados | Técnico |

### Escenarios de Prueba (Gherkin)

#### Escenario 1: Detección y reporte de fallo
```gherkin
DADO que se envía una notificación a un correo inexistente
Y el servidor de correo devuelve un error "550 User unknown"
CUANDO el sistema procesa el rebote
ENTONCES marca la notificación como "Fallida"
Y notifica al funcionario con el motivo "Dirección inválida".
```

#### Escenario 2: Corrección y reenvío
```gherkin
DADO que una notificación falló por error en el dominio del correo
Y el funcionario corrige el correo electrónico del destinatario
CUANDO ejecuta la acción "Reenviar Notificación"
ENTONCES el sistema envía nuevamente el acto administrativo
Y resetea el contador de intentos para seguimiento.
```

#### Escenario 3: Cambio de medio por fallos recurrentes
```gherkin
DADO que una notificación ha fallado 3 veces por medios electrónicos
CUANDO el sistema alcanza el límite de reintentos
ENTONCES sugiere al funcionario realizar "Notificación Personal"
Y genera la orden de notificación para el equipo de terreno.
```

### Datos de Prueba

| Campo | Valor Ejemplo |
|-------|---------------|
| Código Error | 550, 452, 552 |
| Motivo Fallo | Mailbox Full, Domain Not Found, Spam Filter |
| Intentos Realizados | 1, 2, 3 |
| Acción Tomada | Reenvío Manual, Cambio a Personal, Anulación |
| Nuevo Contacto | nuevo.correo@ejemplo.com |

### Trazabilidad

| Componente | Detalle |
|------------|---------|
| Proveedor SMTP | Configuración de webhooks de rebote |
| Bitácora | Registro de cada intento con timestamp y error |
| SLA | Tiempo máximo de respuesta ante fallos (24h) |

### Definición de Terminado (DoD)
- [ ] Integración con servicio de manejo de rebotes (Bounce Handling).
- [ ] Flujo de corrección y reenvío probado.
- [ ] Alertas configuradas en el panel del funcionario.
- [ ] Documentación de códigos de error y soluciones.

---

## HU-18-06: Generar reportes de trazabilidad y auditoría de notificaciones

### Descripción
Como **Auditor Interno o Jefe de Despacho**,  
quiero **generar reportes detallados sobre la trazabilidad completa de las notificaciones y comunicaciones del expediente**,  
para **verificar el cumplimiento de los tiempos legales, auditar el proceso y responder a requerimientos de control**.

### Criterios de Aceptación

| ID | Criterio | Tipo |
|----|----------|------|
| CA-06-01 | El sistema debe permitir generar reportes por rango de fechas, tipo de notificación y estado | Funcional |
| CA-06-02 | El reporte debe incluir: Fecha creación, Fecha envío, Fecha entendida, Destinatario, Medio, Usuario responsable | Funcional |
| CA-06-03 | Debe permitir exportar los reportes en formatos PDF y Excel (.xlsx) | Funcional |
| CA-06-04 | Debe incluir una columna de "Tiempo Transcurrido" entre envío y entendida | Calculado |
| CA-06-05 | El reporte de auditoría debe ser inmutable y estar firmado digitalmente por el sistema | Seguridad |
| CA-06-06 | Debe permitir filtrar por notificaciones fuera de término legal (Vencidas) | Funcional |
| CA-06-07 | Debe mostrar el detalle de reintentos y fallos si los hubo | Funcional |
| CA-06-08 | El acceso a estos reportes debe estar restringido a roles de Auditoría o Jefatura | Seguridad |
| CA-06-09 | Debe permitir consultar el historial completo de una notificación específica desde el reporte | Funcional |
| CA-06-10 | Los reportes deben cumplir con la normativa de conservación documental (10 años mínimo) | Normativo |

### Escenarios de Prueba (Gherkin)

#### Escenario 1: Generación de reporte mensual
```gherkin
DADO que el auditor necesita revisar las notificaciones del mes anterior
Y selecciona el rango de fechas y el tipo "Todas"
CUANDO hace clic en "Generar Reporte"
ENTONCES el sistema compila la información de la base de datos
Y descarga un archivo Excel con el consolidado de notificaciones.
```

#### Escenario 2: Auditoría de notificaciones vencidas
```gherkin
DADO que existe preocupación por notificaciones fuera de término
Y el jefe de despacho filtra por Estado "Vencida"
CUANDO genera el reporte
ENTONCES el sistema lista solo las notificaciones que excedieron el plazo legal
Y resalta los responsables de cada retraso.
```

#### Escenario 3: Trazabilidad de un caso específico
```gherkin
DADO que se requiere auditar una notificación controversial
Y el auditor busca por el Radicado específico
CUANDO abre el detalle en el reporte
ENTONCES ve la línea de tiempo completa: Creación -> Envío -> Intentos -> Entendida
Y puede descargar los soportes asociados.
```

### Datos de Prueba

| Campo | Valor Ejemplo |
|-------|---------------|
| Formato Exportación | .PDF, .XLSX |
| Columnas Reporte | Radicado, Asunto, Destinatario, Fechas, Estado, Usuario |
| Filtros | Por Estado, Por Tipo, Por Responsable, Por Fecha |
| Nivel de Acceso | Auditor, Jefe de Área, Administrador |

### Trazabilidad

| Requisito | Implementación |
|-----------|----------------|
| Conservación Documental | Almacenamiento en repositorio seguro a 10 años |
| Integridad | Hash criptográfico del reporte generado |
| Normativa | Ley 594 de 2000 (Archivo General de la Nación) |

### Definición de Terminado (DoD)
- [ ] Motor de reportes implementado y optimizado.
- [ ] Exportación a PDF y Excel funcional y con formato correcto.
- [ ] Control de acceso basado en roles (RBAC) verificado.
- [ ] Pruebas de integridad de datos en los reportes.

---

## Resumen de Artefactos Técnicos Asociados

### Base de Datos (Tablas Sugeridas)

| Tabla | Descripción |
|-------|-------------|
| `NOTIFICACIONES` | Cabecera de la notificación (ID, Expediente, Tipo, Estado) |
| `DESTINATARIOS_NOTIF` | Detalles del destinatario (Nombre, Email, Rol, Dirección) |
| `INTENTOS_ENVIO` | Log de cada intento (Fecha, Resultado, Error, IP) |
| `ACUSES_RECIBO` | Registro de la entendida (Fecha, Firma, Metodo, Soporte) |
| `COMUNICACIONES_EXTERNAS` | Registro de oficios a terceros y juzgados |
| `PLANTILLAS_NOTIF` | Plantillas de texto y HTML para notificaciones |

### Servicios / API Endpoints

| Método | Endpoint | Descripción |
|--------|----------|-------------|
| POST | `/api/notificaciones/crear` | Crea nueva notificación |
| GET | `/api/notificaciones/bandeja` | Obtiene lista de notificaciones |
| PUT | `/api/notificaciones/{id}/entendida` | Registra fecha de entendida |
| POST | `/api/notificaciones/{id}/reenviar` | Solicita reenvío |
| GET | `/api/reportes/notificaciones` | Genera reporte de auditoría |
| POST | `/api/comunicaciones/enviar` | Envía comunicación externa |

### Consideraciones de Seguridad
- **Cifrado:** TLS 1.3 para todas las transmisiones.
- **Autenticación:** MFA obligatorio para funcionarios que envían notificaciones.
- **No Repudio:** Firma digital en todos los acuses y reportes.
- **Logs:** Auditoría centralizada de todas las acciones (SIEM).

---
*Documento generado para el Módulo 18 del Sistema de Gestión de Expedientes Electrónicos Disciplinarios.*
