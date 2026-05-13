# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por | Estado |
|-------|-------|------------|--------------|--------|
| 13/05/2026 | HU-15-06 | Analista de Negocio | Líder Técnico / Oficina Jurídica | Pendiente |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de Negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica Disciplinaria | P17-Apoyo a la Investigación Disciplinaria | A36-Auditoría y Trazabilidad | Funcionalidad Crítica | Garantiza la transparencia, inmutabilidad y control de las actuaciones procesales conforme al Art. 76 y 208 CGD |

### Descripción

**¿Quién?** 
El Funcionario de Instrucción (rol: instructor), el Secretario Judicial, el Juez Disciplinario y los auditores autorizados por la Procuraduría General de la Nación.

**¿Qué?** 
Consulta el historial completo e inmutable de todas las actuaciones, movimientos, consultas y cambios de estado realizados durante la etapa de Indagación Previa, visualizados en una línea de tiempo (timeline) cronológica con filtros avanzados.

**¿Para qué?** 
Para garantizar el derecho de defensa, la trazabilidad del proceso disciplinario, el cumplimiento del principio de publicidad restringida (Art. 115 CGD) y permitir la auditoría forense digital de la actuación, asegurando que cada decisión tenga un registro verificable de sus antecedentes.

**Referencias Normativas:**
- **Ley 1952 de 2019 (CGD):** Art. 76 (Deberes de los servidores), Art. 115 (Reserva de la actuación), Art. 208 (Indagación Previa).
- **Ley 2094 de 2021:** Art. 13 (Separación de funciones instructor-juzgador), Art. 45 (Medios probatorios digitales).
- **Decreto 1083 de 2015:** Gestión documental y conservación de expedientes electrónicos.
- **Acuerdo 01 de 2023 PGN:** Política de seguridad de la información y auditoría.

## Dependencias y Precondiciones

1. El expediente debe encontrarse en estado "En Indagación Previa" o haber culminado dicha etapa (Archivado/Apertura).
2. El usuario debe estar autenticado con credenciales válidas y tener asignado el rol de "Instructor", "Secretario" o "Auditor".
3. Debe existir registro de auditoría (logs) generado por las HU-15-01 a HU-15-05 y HU-15-07.
4. El sistema de gestión documental debe tener habilitada la función de versionado de documentos.
5. La infraestructura de base de datos debe soportar consultas de grandes volúmenes de logs sin degradar el rendimiento.
6. Debe estar configurada la política de retención de logs según la tabla de retención documental de la PGN.

## Restricciones

1. **Inmutabilidad:** Los registros del historial no pueden ser modificados ni eliminados por ningún usuario, solo adicionados.
2. **Reserva Legal:** El historial solo es visible para usuarios con acceso autorizado al expediente; terceros solo verán lo permitido tras levantamiento de reserva.
3. **Performance:** La carga del historial completo no debe exceder los 3 segundos para expedientes con hasta 500 actuaciones.
4. **Integridad:** Cada entrada del historial debe incluir hash criptográfico para validación de integridad.
5. **Filtros:** Los filtros de búsqueda deben operar sobre metadata indexada (fecha, tipo actuación, usuario, palabra clave).
6. **Exportación:** La exportación del historial solo está permitida en formato PDF firmado digitalmente, no editable.
7. **Acceso Concurrente:** Soportar hasta 50 consultas simultáneas de historial sin bloqueo del sistema.

## Reglas de Negocio

1. **RN-01:** Toda acción del usuario (crear, leer, actualizar, eliminar, imprimir, exportar) debe quedar registrada con marca de tiempo (timestamp) precisa al milisegundo.
2. **RN-02:** El historial debe mostrar la evolución del estado del expediente (ej: "Abierto" -> "Pruebas" -> "Citación" -> "Archivo").
3. **RN-03:** Las actuaciones anuladas deben aparecer tachadas visualmente pero conservando su registro histórico con la causal de anulación.
4. **RN-04:** No se permite consultar el historial de otros expedientes sin autorización expresa de transferencia de competencia.
5. **RN-05:** El sistema debe destacar las actuaciones críticas (ej: Decreto de pruebas, Auto de apertura, Auto de archivo) con un ícono diferenciador.
6. **RN-06:** La consulta del historial por parte del investigado (una vez levantada la reserva) debe quedar registrada como "Entrega de copia".
7. **RN-07:** Los archivos adjuntos consultados desde el historial deben registrar quién, cuándo y qué documento vio.

## Supuestos

1. Se asume que la red de comunicación interna de la PGN garantiza la sincronización de relojes (NTP) para la consistencia de timestamps.
2. Se asume que los usuarios conocen la estructura básica de una actuación disciplinaria para interpretar el historial.
3. Se asume capacidad de almacenamiento suficiente para retener logs históricos por 30 años (término de conservación).
4. Se asume que el navegador del usuario soporta renderizado eficiente de listas largas (virtual scrolling).

## Criterios de Aceptación (Gherkin)

**Escenario 1: Visualización completa de la línea de tiempo**
Dado que soy un Funcionario de Instrucción autenticado
Cuando accedo a la pestaña "Historial" de un expediente en Indagación Previa
Entonces el sistema muestra una lista cronológica descendente de todas las actuaciones
Y cada ítem muestra: fecha, hora, tipo de actuación, usuario responsable y resumen.

**Escenario 2: Filtrado por tipo de actuación**
Dado que estoy consultando el historial de un expediente extenso
Cuando aplico el filtro "Tipo: Decreto de Pruebas"
Entonces el sistema oculta las actuaciones que no coinciden
Y muestra únicamente los decretos de pruebas librados en la etapa.

**Escenario 3: Búsqueda por palabra clave**
Dado que necesito encontrar una actuación específica
Cuando ingreso la palabra clave "testigo" en el buscador del historial
Entonces el sistema resalta las actuaciones que contienen esa palabra en su descripción o metadatos
Y me permite navegar directamente a esos registros.

**Escenario 4: Auditoría de integridad (Hash)**
Dado que soy un auditor de control interno
Cuando selecciono una actuación crítica del historial
Entonces el sistema permite visualizar el hash criptográfico del registro
Y valida que no ha sido alterado desde su creación.

**Escenario 5: Exportación segura del historial**
Dado que requiero entregar copia del historial al investigado
Cuando solicito la exportación en PDF
Entonces el sistema genera un documento con sello de tiempo y código de verificación
Y registra esta acción como "Entrega de Copia - Historial".

**Escenario 6: Visualización de actuaciones anuladas**
Dado que existe una actuación que fue corregida por error material
Cuando consulto el historial
Entonces veo la actuación original tachada con la etiqueta "ANULADA"
Y veo inmediatamente después la actuación correcta con referencia a la anterior.

**Escenario 7: Error por falta de permisos**
Dado que soy un usuario de otra dependencia sin acceso al expediente
Cuando intento consultar el historial mediante URL directa
Entonces el sistema deniega el acceso con mensaje "No autorizado"
Y registra el intento de acceso indebido en el log de seguridad.

## Prototipo / Anexos

- **Pantalla Referencia:** `Pantallas VEED/15_gestion_indagacion_v1.html` (Sección: Pestaña "Historial / Audit Log")
- **Componentes UX:**
  - Timeline vertical con conectores visuales.
  - Barra lateral de filtros (Fecha inicio/fin, Tipo actuación, Usuario).
  - Buscador full-text con resaltado.
  - Modal de detalle de actuación con metadata técnica (IP, User-Agent, Hash).
  - Botón "Exportar PDF" con confirmación.
- **Estilos:** Fuente Poppins, colores institucionales PGN (#063853, #E3201B para alertas).

## Stakeholders

- **Funcionario de Instrucción:** Usuario principal para seguimiento del caso.
- **Secretario Judicial:** Responsable de la certificación de copias.
- **Oficina de Control Interno Disciplinario:** Auditoría de procesos.
- **Investigado y Defensor:** Acceso limitado post-reserva.
- **Área de Tecnología (TI):** Administración de logs y almacenamiento.

## Plan de Validación

1. **Prueba de Carga:** Simular 10.000 registros en el historial y medir tiempos de respuesta (<3s).
2. **Prueba de Integridad:** Intentar modificar un registro en base de datos y verificar que la aplicación detecta la inconsistencia de hash.
3. **Validación Legal:** Revisión por la Oficina Jurídica de que el contenido mostrado cumple con la reserva del Art. 115 CGD.
4. **UX Testing:** Verificar usabilidad de filtros y navegación en timeline con usuarios reales.

## Matriz de Trazabilidad Normativa

| Artículo | Norma | Requisito Implementado | Cumplimiento |
|----------|-------|------------------------|--------------|
| Art. 76 | Ley 1952/2019 | Deber de registrar actuaciones | ✅ Log inmutable |
| Art. 115 | Ley 1952/2019 | Reserva de la actuación | ✅ Control de acceso |
| Art. 208 | Ley 1952/2019 | Término indagación | ✅ Registro de fechas |
| Art. 45 | Ley 2094/2021 | Medios probatorios digitales | ✅ Integridad hash |
| Art. 13 | Ley 2094/2021 | Separación funciones | ✅ Logs diferenciados por rol |
| Dec. 1083/2015 | Gestión Documental | Conservación expediente | ✅ Retención 30 años |

## Requisitos de Seguridad y Auditoría

- **Cifrado:** Logs almacenados cifrados en reposo (AES-256).
- **Acceso:** Autenticación multifactor para funciones de auditoría avanzada.
- **Trazabilidad:** El propio log de consulta del historial debe ser auditable (log de logs).
- **Prevención:** Detección de patrones anómalos (ej: consulta masiva de historiales en corto tiempo).
- **Backup:** Copias de seguridad diarias incrementales de la tabla de auditoría.

## Protocolo de Incidentes

1. **Detección:** Alerta automática por intento de borrado o modificación de logs.
2. **Contención:** Bloqueo inmediato del usuario sospechoso y congelamiento del expediente.
3. **Investigación:** Revisión de IPs y sesiones activas por el equipo de seguridad.
4. **Reporte:** Notificación obligatoria a la Oficina de Control Interno en menos de 24 horas.
5. **Recuperación:** Restauración desde backup seguro y validación de integridad.

## Glosario

- **Audit Trail:** Pista de auditoría o rastro digital de las acciones.
- **Hash Criptográfico:** Algoritmo que garantiza la integridad del dato (SHA-256).
- **Timeline:** Línea de tiempo visual de eventos.
- **Reserva de Actuación:** Secreto sumarial durante la indagación previa.
- **Inmutabilidad:** Propiedad de no poder ser cambiado.

## Definition of Done (DoD)

- [ ] Historia documentada y aprobada por líder técnico.
- [ ] Desarrollo del componente Timeline completado.
- [ ] Implementación de filtros y buscador funcional.
- [ ] Generación de hash por cada registro.
- [ ] Pruebas de carga superadas (>10k registros).
- [ ] Validación de seguridad (pentesting de logs).
- [ ] Documentación de API de auditoría.
- [ ] Capacitación a funcionarios sobre uso de historial.
- [ ] Aprobación final de la Oficina Jurídica.
