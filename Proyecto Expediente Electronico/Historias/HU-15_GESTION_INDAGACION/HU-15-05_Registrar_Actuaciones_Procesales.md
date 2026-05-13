# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por |
|-------|-------|------------|--------------|
| 13/05/2026 | HU-15-05 | Analista de Negocio | Líder Técnico |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica Disciplinaria | P17-Apoyo a la Investigación Disciplinaria | A35-Registro de Actuaciones Procesales | Funcionalidad Específica | Garantiza la trazabilidad completa de todas las actuaciones procesales realizadas durante la indagación previa, asegurando cumplimiento de términos y reserva de la actuación |

### Descripción

**¿Quién?** El Funcionario de Instrucción (rol: instructor) y el Secretario de Actuaciones Procesales (rol: secretario) asignados al caso mediante auto de reparto.

**¿Qué?** Registra nuevas actuaciones procesales en el expediente disciplinario durante la etapa de indagación previa, incluyendo decretos de pruebas, oficios, citaciones, actas de audiencia y demás actos procesales requeridos para el avance de la investigación, manteniendo secuencia cronológica y numeración consecutiva.

**¿Para qué?** Para dejar constancia formal de cada actuación procesal realizada dentro del término de seis meses de la indagación previa, garantizando el debido proceso, la defensa técnica del posible sujeto pasivo, y generando los documentos necesarios para soportar la decisión final de archivo o apertura de investigación disciplinaria conforme al Artículo 208 del CGD.

**Referencias Normativas:**
- Ley 1952 de 2019 (Código General Disciplinario), Artículo 208: Indagación Previa y actuaciones permitidas.
- Ley 1952 de 2019, Artículo 7: Debido Proceso y Derecho de Defensa.
- Ley 1952 de 2019, Artículo 115: Reserva de la Actuación.
- Ley 1952 de 2019, Artículo 121-123: Notificaciones y Comunicaciones.
- Ley 1952 de 2019, Artículo 214: Ruptura de la Unidad Procesal.
- Ley 1437 de 2011 (Código de Procedimiento Administrativo y de lo Contencioso Administrativo), Artículo 13: Principios del procedimiento administrativo.
- Decreto 1069 de 2015: Protección de datos personales en el sector justicia.
- Sentencia C-497 de 2016 (Corte Constitucional): Derechos fundamentales en procesos disciplinarios.

## Dependencias y Precondiciones

1. El expediente disciplinario debe estar creado y en estado "En Indagación Previa" según registro en el sistema.
2. El usuario debe estar autenticado con rol "Funcionario de Instrucción" o "Secretario de Actuaciones Procesales".
3. Debe existir al menos una persona identificada en averiguación registrada en el sistema.
4. El término de indagación previa debe estar vigente (no superados los seis meses calendario).
5. El sistema debe tener plantillas documentales preconfiguradas para cada tipo de actuación.
6. La sesión del usuario debe tener permisos RBAC específicos para creación de actuaciones procesales.
7. Debe haberse completado la HU-15-01 para validación del término restante antes de registrar actuaciones críticas.

## Restricciones

1. Todas las actuaciones deben registrarse con fecha y hora exacta de realización sin posibilidad de modificación posterior.
2. La numeración de actuaciones debe ser consecutiva y automática, sin saltos ni duplicaciones.
3. No se permitirá registrar actuaciones con fecha anterior a la apertura de la indagación previa.
4. Las actuaciones que generen notificación personal deben incluir campos obligatorios de datos de contacto.
5. El tiempo de guardado de una actuación no podrá exceder los 3 segundos.
6. No se permitirá eliminar actuaciones registradas; solo podrán dejarse sin efecto mediante actuación posterior motivada.
7. La interfaz debe mantener estándares WCAG 2.1 AA para usuarios con discapacidad.
8. Cada actuación debe quedar asociada al usuario que la registró con firma electrónica avanzada.

## Reglas de Negocio

1. **RN-15-05-01**: Toda actuación procesal debe clasificarse en categorías: Decreto, Oficio, Citación, Acta, Auto, Providencia o Diligencia.
2. **RN-15-05-02**: Las actuaciones que decreten pruebas deben especificar término de ejecución y medio de notificación.
3. **RN-15-05-03**: Los autos que requieran notificación personal generan automáticamente agenda de notificación para el secretario.
4. **RN-15-05-04**: Las actuaciones registradas fuera del término de indagación generan alerta roja de extemporaneidad.
5. **RN-15-05-05**: Cada actuación debe tener descripción clara del objeto y fundamento jurídico de la decisión.
6. **RN-15-05-06**: Las citaciones a audiencias deben validar disponibilidad de salas y participantes antes de confirmarse.
7. **RN-15-05-07**: Los oficios enviados a entidades externas requieren número de radicado de salida registrado en correspondencia.
8. **RN-15-05-08**: El sistema debe impedir registro de actuaciones si el usuario no tiene caso asignado activamente.

## Supuestos

1. Se asume que los funcionarios conocen los tipos de actuaciones procesales permitidas en indagación previa.
2. Se presume que las plantillas documentales están actualizadas conforme a normativa vigente.
3. Se considera que existe conectividad estable para registro en tiempo real de actuaciones.
4. Se espera que los usuarios cuenten con certificados digitales vigentes para firma electrónica.

## Criterios de Aceptación

**Escenario 1: Registro exitoso de decreto de pruebas**
Dado que soy un Funcionario de Instrucción con caso activo en indagación previa
Cuando registro un nuevo decreto de pruebas documentales
Entonces el sistema genera número consecutivo de actuación
Y valida campos obligatorios (objeto, término, medio de notificación)
Y genera documento PDF con plantilla institucional
Y registra la actuación en audit log con timestamp y firma electrónica
Y muestra confirmación con opción de notificar inmediatamente

**Escenario 2: Creación de oficio con radicación externa**
Dado que soy un Secretario de Actuaciones Procesales
Cuando registro un oficio dirigido a entidad externa para solicitud de información
Entonces el sistema requiere diligenciamiento de destinatario completo (entidad, dirección, correo)
Y genera número de radicado de salida sincronizado con sistema de correspondencia
Y adjunta documento PDF listo para envío
Y programa recordatorio de seguimiento a 10 días hábiles
Y registra la actuación con clasificación "Oficio"

**Escenario 3: Citación a audiencia con validación de disponibilidad**
Dado que soy un Funcionario de Instrucción necesitando citar a audiencia
Cuando registro citación para audiencia de práctica de pruebas
Entonces el sistema consulta disponibilidad de salas físicas o virtuales
Y valida agenda de participantes (funcionario, citado, testigos, secretario)
Y genera citación con fecha, hora, lugar y enlace de conexión si es virtual
Y envía notificación automática a todos los convocados
Y registra la actuación como "Citación Confirmada"

**Escenario 4: Alerta de actuación extemporánea**
Dado que soy un Funcionario de Instrucción intentando registrar actuación
Cuando la fecha actual supera el término de seis meses de indagación previa
Entonces el sistema bloquea el registro y muestra alerta roja "TÉRMINO VENCIDO"
Y sugiere proyección de decisión final (archivo o apertura investigación)
Y notifica al jefe de dependencia sobre la situación crítica
Y registra el intento fallido en sistema de seguridad

**Escenario 5: Intento de modificación de actuación registrada**
Dado que soy un usuario intentando modificar actuación ya registrada
Cuando intento editar contenido de actuación con fecha anterior
Entonces el sistema bloquea la modificación y muestra mensaje "Actuación inmutable - Use actuación de dejando sin efecto si corresponde"
Y sugiere crear nueva actuación que deje sin efecto la anterior si hay error
Y registra el intento de modificación en audit log de seguridad

**Escenario 6: Registro de actuación sin campos obligatorios**
Dado que soy un Funcionario de Instrucción diligenciando formulario de actuación
Cuando intento guardar sin completar campos obligatorios (descripción, fundamento jurídico)
Entonces el sistema resalta campos faltantes en rojo
Y muestra mensaje "Complete los campos obligatorios para continuar"
Y impide el guardado hasta cumplir validación
Y mantiene datos diligenciados para evitar pérdida de información

**Escenario 7: Generación de auto con notificación personal**
Dado que soy un Secretario registrando auto que requiere notificación personal
Cuando guardo auto de decreto de pruebas
Entonces el sistema genera automáticamente tarea en agenda de notificaciones
Y valida que existan datos de contacto completos del notificado
Y programa plazo de notificación conforme al Art. 121 CGD (3 días hábiles)
Y registra la actuación con estado "Pendiente de Notificación"

**Escenario 8: Error de concurrencia en numeración**
Dado que son dos secretarios registrando actuaciones simultáneamente
Cuando ambos intentan guardar actuaciones al mismo tiempo
Entonces el sistema maneja transacción atómica para numeración consecutiva
Y asigna números diferentes sin duplicación ni saltos
Y notifica a ambos usuarios con confirmación exitosa
Y registra ambas actuaciones con timestamps diferenciados por milisegundos

## Prototipo / Anexos

- Pantalla de referencia: `/workspace/Pantallas VEED/15_gestion_indagacion_v1.html`
- Sección específica: Pestaña "Registrar Actuaciones"
- Componentes UX identificados:
  - Formulario dinámico según tipo de actuación seleccionada
  - Selector de tipo de actuación con iconografía diferenciada
  - Editor de texto enriquecido para descripción y fundamentos jurídicos
  - Visor previo de documento generado antes de guardar
  - Timeline vertical de actuaciones registradas con filtros
  - Botones de acción: "Nueva Actuación", "Guardar", "Vista Previa", "Notificar"
- Tokens de diseño: Fuente Poppins, colores institucionales (#063853 primario, #FFE601 para acciones principales)
- Mockup de interfaz responsive aprobado por área UX
- Catálogo de plantillas documentales por tipo de actuación

## Stakeholders

- Funcionarios de Instrucción (Usuarios primarios)
- Secretarios de Actuaciones Procesales (Usuarios operativos)
- Procuraduría General de la Nación (Supervisión procesal)
- Oficina de Tecnologías de la Información (Soporte técnico)
- Área Jurídica Institucional (Validación de plantillas)
- Grupo de Gestión Documental (Control de numeración y archivo)
- Defensoría del Pueblo (Supervisión derechos fundamentales)

## Plan de Validación

| Fase | Actividad | Responsable | Entregable | Criterio de éxito |
|------|-----------|-------------|------------|-------------------|
| 1 | Revisión de plantillas documentales | Área Jurídica | Acta de aprobación de plantillas | 100% de plantillas validadas |
| 2 | Pruebas de numeración consecutiva | Equipo QA | Reporte de pruebas de concurrencia | 0 duplicados en 1000 registros simultáneos |
| 3 | Validación de flujos de notificación | Secretaría General | Certificado de integración | Notificaciones entregadas en < 1 minuto |
| 4 | Auditoría de inmutabilidad de registros | Auditor Interno | Informe de auditoría | 0 modificaciones detectadas en histórico |
| 5 | Capacitación en tipos de actuaciones | Equipo de Formación | Constancias de asistencia | 95% de aprobados en evaluación práctica |
| 6 | Prueba piloto con casos reales | Funcionarios Piloto | Acta de aceptación | 0 errores críticos en 30 días de operación |

## Matriz de Trazabilidad con Referencias Normativas

| Artículo | Norma | Descripción | Implementación Técnica | Estado |
|----------|-------|-------------|------------------------|--------|
| Art. 208 | Ley 1952/2019 | Indagación previa y actuaciones | Formulario específico para etapa de indagación | ✅ |
| Art. 7 | Ley 1952/2019 | Debido proceso y defensa | Campos de fundamentación jurídica obligatorios | ✅ |
| Art. 115 | Ley 1952/2019 | Reserva de actuación | Control de acceso por roles y registro de consultas | ✅ |
| Art. 121-123 | Ley 1952/2019 | Notificaciones | Agenda integrada de notificaciones personales | ✅ |
| Art. 214 | Ley 1952/2019 | Ruptura unidad procesal | Vinculación de actuaciones a personas específicas | ✅ |
| Art. 13 | Ley 1437/2011 | Principios procedimiento | Trazabilidad completa de cada actuación | ✅ |
| Decreto 1069/2015 | Protección de Datos | Tratamiento de datos personales | Minimización de datos en notificaciones | ✅ |
| Sentencia C-497/16 | Corte Constitucional | Derechos fundamentales | Validación de derechos en citaciones y notificaciones | ✅ |

## Requisitos de Seguridad y Auditoría

1. **Autenticación**: OAuth 2.0 con doble factor para registro de actuaciones críticas.
2. **Autorización**: Modelo RBAC + ABAC basado en rol, caso asignado y tipo de actuación.
3. **Firma Electrónica**: Integración con certificado digital para firma de todas las actuaciones.
4. **Inmutabilidad**: Una vez registrada, ninguna actuación puede ser modificada o eliminada.
5. **Audit Log**: Registro inmutable de todas las operaciones con metadata completa (usuario, IP, timestamp, actuación).
6. **Prevención de fraudes**: Detección de patrones anómalos en registro de actuaciones (ej: múltiples actuaciones en segundos).
7. **Retención**: Conservación de registros por 10 años según normativa de archivo judicial.
8. **Backup**: Copias de seguridad diarias con retención de 30 días en sitio alterno.

## Protocolo de Respuesta a Incidentes de Actuaciones

| Tipo de Incidente | Acción Inmediata | Notificación | Plazo | Responsable |
|-------------------|------------------|--------------|-------|-------------|
| Error en numeración consecutiva | Auditoría y corrección manual | Jefe de Dependencia | 4 horas | Admin BD |
| Firma electrónica inválida | Rechazo de actuación y notificación | Usuario y CISO | Inmediato | Security Ops |
| Pérdida de integridad de actuación | Restauración desde backup | Comité de Ética | 24 horas | Auditor Interno |
| Acceso no autorizado a registro | Bloqueo de sesión y forense | CISO | 2 horas | Security Ops |
| Saturación del sistema | Escalamiento automático | DevOps | Inmediato | Infraestructura |

## Glosario de Términos

- **Actuación Procesal**: Cada acto formal realizado dentro del proceso disciplinario que queda registrado en el expediente.
- **Decreto de Pruebas**: Actuación mediante la cual el funcionario ordena la práctica de medios probatorios.
- **Auto**: Decisión interlocutoria del funcionario de instrucción que requiere fundamentación jurídica.
- **Notificación Personal**: Forma de comunicación que requiere entrega directa al interesado o su apoderado.
- **Radicado de Salida**: Número único asignado a documentos enviados a entidades externas.
- **Inmutabilidad**: Principio que garantiza que los registros no pueden ser modificados una vez creados.

## Definition of Done (DoD)

- [ ] Historia de usuario documentada según estándar PGN
- [ ] Plantillas documentales validadas por Área Jurídica Institucional
- [ ] Prototipo de interfaz aprobado por comité UX
- [ ] Casos de prueba unitaria implementados (cobertura ≥ 90%)
- [ ] Pruebas de concurrencia exitosas (1000 registros simultáneos sin duplicados)
- [ ] Auditoría de inmutabilidad de registros aprobada
- [ ] Integración con sistema de notificaciones verificada
- [ ] Manual de procedimientos de registro de actuaciones elaborado
- [ ] Sesión de capacitación realizada con funcionarios y secretarios
- [ ] Aprobación formal del Product Owner y Comité de Gobierno

---

*Documento generado bajo estándares de calidad del Sistema de Gestión de Calidad ISO 9001:2015*
*Versión: 1.0 | Última actualización: 13/05/2026 | Clasificación: Reservado*
