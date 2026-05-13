# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por |
|-------|-------|------------|--------------|
| 13/05/2026 | HU-15-04 | Analista de Negocio | Líder Técnico |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica Disciplinaria | P17-Apoyo a la Investigación Disciplinaria | A34-Gestión Documental en Indagación | Funcionalidad Específica | Garantiza la integridad, trazabilidad y reserva de los documentos que conforman el acervo probatorio durante la indagación previa |

### Descripción

**¿Quién?** El Funcionario de Instrucción (rol: instructor) y el Secretario de Actuaciones Procesales (rol: secretario) asignados al caso.

**¿Qué?** Gestiona el ciclo completo de documentos del expediente disciplinario en etapa de indagación previa, incluyendo carga, clasificación, consulta, descarga controlada y eliminación justificada de archivos digitales, manteniendo la reserva de la actuación y la cadena de custodia documental.

**¿Para qué?** Para asegurar que todo el material probatorio recopilado durante la indagación previa quede properly registrado, organizado y protegido, facilitando su consulta oportuna por parte del funcionario instructor mientras se garantiza la integridad del expediente y el cumplimiento del principio de reserva establecido en el Artículo 115 del CGD.

**Referencias Normativas:**
- Ley 1952 de 2019 (Código General Disciplinario), Artículo 115: Reserva de la Actuación.
- Ley 1952 de 2019, Artículo 208: Indagación Previa y término de seis meses.
- Ley 1952 de 2019, Artículo 121: Notificaciones y comunicaciones.
- Ley 594 de 2000 (Ley General de Archivos): Gestión documental en entidades públicas.
- Decreto 1080 de 2015: Reglamento único del Sector Cultura - Subsector Archivos.
- Resolución AGN 003 de 2020: Tablas de retención documental para procesos disciplinarios.
- Ley 527 de 1999: Mensajes de datos y firmas digitales.
- Decreto 1069 de 2015: Protección de datos personales en el sector justicia.
- Sentencia C-749 de 2015 (Corte Constitucional): Valor probatorio de documentos digitales.

## Dependencias y Precondiciones

1. El expediente disciplinario debe estar creado y en estado "En Indagación Previa" en el sistema.
2. El usuario debe estar autenticado con rol "Funcionario de Instrucción" o "Secretario de Actuaciones Procesales".
3. El sistema debe contar con almacenamiento seguro configurado para documentos judiciales.
4. Debe existir política de clasificación documental aprobada por el comité de archivo institucional.
5. El módulo de digitalización debe estar operativo con escáneres calibrados según normativa AGN.
6. La sesión del usuario debe tener permisos RBAC específicos para operaciones documentales.
7. Debe haberse completado la HU-15-01 para validación del término vigente antes de cargar documentos críticos.

## Restricciones

1. Todos los documentos cargados deben cumplir con formatos aceptados: PDF/A, TIFF, JPEG2000 según normativa AGN.
2. El tamaño máximo por documento individual no podrá exceder 50 MB sin autorización especial.
3. No se permitirá la eliminación de documentos una vez incorporados al expediente sin auto motivado.
4. La descarga masiva de documentos está restringida al funcionario instructor y requiere justificación.
5. Los documentos con información sensible deben cifrarse adicionalmente con clave de acceso.
6. El tiempo de carga de documentos no podrá exceder 10 segundos por archivo de hasta 10 MB.
7. La interfaz debe mantener estándares WCAG 2.1 AA para usuarios con discapacidad visual.
8. Cada operación documental debe quedar registrada en el audit log con hash criptográfico del archivo.

## Reglas de Negocio

1. **RN-15-04-01**: Todo documento cargado debe clasificarse obligatoriamente en: Probatorio, Trámite, Notificación, Decisión o Soporte.
2. **RN-15-04-02**: Los documentos probatorios requieren validación de cadena de custodia antes de ser incorporados al expediente.
3. **RN-15-04-03**: La eliminación de documentos solo procede mediante auto motivado del funcionario instructor con aprobación del jefe inmediato.
4. **RN-15-04-04**: Los documentos cargados fuera del término de indagación previa generan alerta automática de extemporaneidad.
5. **RN-15-04-05**: Cada documento debe asociarse metadata mínima: fecha creación, autor, tipo documental, palabra clave y descripción.
6. **RN-15-04-06**: La consulta de documentos reservados requiere registro explícito en audit log con finalidad de la consulta.
7. **RN-15-04-07**: Los documentos escaneados deben cumplir resolución mínima de 300 DPI según normativa AGN.
8. **RN-15-04-08**: El sistema debe generar automáticamente versión PDF/A de cualquier documento ofimático cargado.

## Supuestos

1. Se asume que los usuarios cuentan con equipos de digitalización calibrados según normativa técnica AGN.
2. Se presume que la conectividad de red permite transferencia de archivos de gran tamaño sin interrupciones.
3. Se considera que los funcionarios tienen capacitación básica en gestión documental electrónica.
4. Se espera que el almacenamiento central tenga capacidad suficiente para retención documental a 10 años.

## Criterios de Aceptación

**Escenario 1: Carga exitosa de documento probatorio**
Dado que soy un Funcionario de Instrucción con caso activo en indagación previa
Cuando cargo un documento PDF clasificado como "Probatorio" con metadata completa
Entonces el sistema valida formato, tamaño y genera hash criptográfico
Y almacena el documento en repositorio seguro con clasificación de reserva
Y registra la operación en audit log con timestamp y datos del usuario
Y muestra confirmación con número de radicación documental

**Escenario 2: Consulta de documento con reserva de actuación**
Dado que soy un Funcionario de Instrucción asignado al caso
Cuando consulto un documento clasificado como reservado según Art. 115 CGD
Entonces el sistema verifica mi rol y asignación al caso
Y permite visualización del documento en visor seguro sin opción de descarga directa
Y registra la consulta en audit log indicando finalidad investigativa
Y marca el documento como "Consultado" con fecha y hora

**Escenario 3: Descarga controlada de documento**
Dado que soy un Funcionario de Instrucción requiriendo documento para actuación externa
Cuando solicito descarga de un documento del expediente
Entonces el sistema requiere diligenciamiento de formulario de justificación
Y valida aprobación del jefe inmediato si supera 5 documentos
Y genera archivo descargable con marca de agua identificadora del usuario
Y registra la descarga en audit log con propósito y cantidad de archivos

**Escenario 4: Intento de eliminación sin autorización**
Dado que soy un usuario con rol de Secretario de Actuaciones
Cuando intento eliminar un documento ya incorporado al expediente
Entonces el sistema bloquea la operación y muestra mensaje "Eliminación requiere auto motivado"
Y sugiere trámite de solicitud de eliminación con aprobación jerárquica
Y registra el intento fallido en sistema de seguridad

**Escenario 5: Carga de documento con formato no válido**
Dado que soy un Funcionario de Instrucción cargando documentación
Cuando intento subir un archivo en formato no permitido (ej: .exe, .bat)
Entonces el sistema rechaza el archivo inmediatamente
Y muestra mensaje "Formato no permitido. Formatos aceptados: PDF/A, TIFF, JPEG2000, DOCX, XLSX"
Y sugiere conversión a formato válido mediante herramienta integrada

**Escenario 6: Alerta de documento extemporáneo**
Dado que soy un Funcionario de Instrucción cargando pruebas
Cuando la fecha actual supera el término de seis meses de indagación previa
Entonces el sistema muestra alerta amarilla "Documento cargado fuera de término"
Y requiere justificación escrita de la extemporaneidad
Y notifica automáticamente al jefe de la dependencia sobre la situación

**Escenario 7: Verificación de cadena de custodia**
Dado que soy un Secretario de Actuaciones recibiendo documento físico para digitalizar
Cuando cargo documento probatorio al sistema
Entonces el sistema requiere escaneo de código QR de cadena de custodia
Y valida que el documento físico coincida con registro en sistema de correspondencia
Y genera acta de incorporación digital firmada electrónicamente
Y actualiza estado del documento físico a "Digitalizado e Incorporado"

**Escenario 8: Error de almacenamiento lleno**
Dado que soy un usuario intentando cargar documentos
Cuando el repositorio alcanza capacidad máxima temporal
Entonces el sistema muestra mensaje "Almacenamiento temporalmente lleno. Intente en 15 minutos"
Y pone en cola la carga para procesamiento automático cuando haya espacio
Y notifica al administrador de infraestructura sobre la saturación

## Prototipo / Anexos

- Pantalla de referencia: `/workspace/Pantallas VEED/15_gestion_indagacion_v1.html`
- Sección específica: Pestaña "Documentos del Expediente"
- Componentes UX identificados:
  - Panel de carga drag-and-drop con barra de progreso
  - Árbol de carpetas por clasificación documental
  - Visor integrado de PDF con zoom y búsqueda textual
  - Formulario de metadata con campos obligatorios resaltados
  - Tabla de historial de operaciones con filtros por fecha y usuario
  - Botones de acción: "Cargar", "Consultar", "Descargar", "Solicitar Eliminación"
- Tokens de diseño: Fuente Poppins, colores institucionales (#063853 primario, #E3201B para alertas)
- Mockup de interfaz responsive aprobado por área UX
- Diagrama de flujo de proceso de carga y validación documental

## Stakeholders

- Funcionarios de Instrucción (Usuarios primarios)
- Secretarios de Actuaciones Procesales (Usuarios operativos)
- Comité Institucional de Archivos (Validación normativa)
- Oficina de Tecnologías de la Información (Soporte técnico)
- Grupo de Seguridad de la Información (Control de accesos)
- Procuraduría General de la Nación (Supervisión procesal)
- Archivo General de la Nación (Regulación archivística)

## Plan de Validación

| Fase | Actividad | Responsable | Entregable | Criterio de éxito |
|------|-----------|-------------|------------|-------------------|
| 1 | Revisión de requisitos archivísticos | Archivista Institucional | Acta de conformidad | Cumplimiento 100% normativa AGN |
| 2 | Pruebas de carga masiva | Equipo QA | Reporte de performance | 100 documentos en < 5 minutos |
| 3 | Validación de seguridad documental | CISO | Certificado de seguridad | 0 vulnerabilidades críticas |
| 4 | Auditoría de cadena de custodia | Auditor Interno | Informe de auditoría | Trazabilidad completa verificada |
| 5 | Capacitación en gestión documental | Equipo de Formación | Constancias de asistencia | 95% de aprobados en evaluación práctica |
| 6 | Prueba piloto con casos reales | Funcionarios Piloto | Acta de aceptación | 0 errores en producción tras 30 días |

## Matriz de Trazabilidad con Referencias Normativas

| Artículo | Norma | Descripción | Implementación Técnica | Estado |
|----------|-------|-------------|------------------------|--------|
| Art. 115 | Ley 1952/2019 | Reserva de la actuación | Control de acceso por roles y registro de consultas | ✅ |
| Art. 208 | Ley 1952/2019 | Término indagación previa | Alerta de documentos extemporáneos | ✅ |
| Art. 121 | Ley 1952/2019 | Notificaciones | Asociación de documentos de notificación a actuaciones | ✅ |
| Ley 594/2000 | Ley General de Archivos | Gestión documental | Clasificación, ordenación y conservación | ✅ |
| Decreto 1080/2015 | Reglamento Archivos | Formatos y resoluciones | Validación PDF/A, TIFF, 300 DPI mínimo | ✅ |
| Res. AGN 003/2020 | Tablas Retención | Tiempos de conservación | Política de retención configurable | ✅ |
| Ley 527/1999 | Firma Digital | Validez jurídica documentos electrónicos | Integración con firma digital certificada | ✅ |
| Sentencia C-749/15 | Corte Constitucional | Valor probatorio digital | Hash criptográfico y cadena de custodia | ✅ |

## Requisitos de Seguridad y Auditoría

1. **Autenticación**: OAuth 2.0 con doble factor para operaciones críticas (eliminación, descarga masiva).
2. **Autorización**: Modelo RBAC + ABAC basado en rol, caso asignado y tipo documental.
3. **Cifrado**: TLS 1.3 en transmisión, AES-256 en repositorio, cifrado adicional para documentos sensibles.
4. **Integridad**: Hash SHA-256 generado automáticamente para cada documento cargado.
5. **Audit Log**: Registro inmutable de todas las operaciones con metadata completa (usuario, IP, timestamp, operación, documento).
6. **Prevención de fugas**: DLP para detectar intentos de extracción masiva no autorizada.
7. **Marca de agua**: Inserción dinámica de marca de agua identificadora en descargas autorizadas.
8. **Retención**: Conservación de logs y documentos según tablas de retención documental (mínimo 10 años).

## Protocolo de Respuesta a Incidentes Documentales

| Tipo de Incidente | Acción Inmediata | Notificación | Plazo | Responsable |
|-------------------|------------------|--------------|-------|-------------|
| Pérdida de integridad de documento | Restauración desde backup | Jefe de Dependencia | 4 horas | Admin BD |
| Acceso no autorizado a documentos | Bloqueo de sesión y auditoría | CISO | 24 horas | Security Ops |
| Saturación de almacenamiento | Limpieza de temporales y expansión | DevOps | 2 horas | Infraestructura |
| Virus en documento cargado | Cuarentena automática | Usuario y CISO | Inmediato | Antivirus Corp |
| Eliminación no autorizada | Restauración y investigación | Comité de Ética | 24 horas | Auditor Interno |

## Glosario de Términos

- **Cadena de Custodia**: Procedimiento controlado que se aplica a los documentos probatorios desde su ubicación hasta su incorporación al expediente.
- **PDF/A**: Formato de archivo PDF especializado para la preservación a largo plazo de documentos electrónicos.
- **Hash Criptográfico**: Valor único generado algorítmicamente que garantiza la integridad del documento.
- **Reserva de Actuación**: Principio que limita el acceso a documentos del proceso durante etapas preliminares.
- **Metadata Documental**: Información descriptiva asociada al documento que facilita su gestión y recuperación.
- **Tabla de Retención**: Instrumento archivístico que determina los tiempos de conservación de los documentos.

## Definition of Done (DoD)

- [ ] Historia de usuario documentada según estándar PGN
- [ ] Requisitos archivísticos validados por Comité Institucional de Archivos
- [ ] Prototipo de interfaz aprobado por comité UX
- [ ] Casos de prueba unitaria implementados (cobertura ≥ 90%)
- [ ] Pruebas de carga y performance exitosas (100 documentos en < 5 min)
- [ ] Auditoría de seguridad informática aprobada
- [ ] Validación de cadena de custodia documental completada
- [ ] Manual de gestión documental electrónica elaborado
- [ ] Sesión de capacitación realizada con funcionarios y secretarios
- [ ] Aprobación formal del Product Owner y Comité de Gobierno

---

*Documento generado bajo estándares de calidad del Sistema de Gestión de Calidad ISO 9001:2015*
*Versión: 1.0 | Última actualización: 13/05/2026 | Clasificación: Reservado*
