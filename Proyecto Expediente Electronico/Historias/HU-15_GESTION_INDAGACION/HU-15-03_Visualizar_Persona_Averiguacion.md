# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por |
|-------|-------|------------|--------------|
| 13/05/2026 | HU-15-03 | Analista de Negocio | Líder Técnico |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica Disciplinaria | P17-Apoyo a la Investigación Disciplinaria | A33-Visualización de Persona en Averiguación | Funcionalidad Específica | Garantiza el derecho al debido proceso mediante la correcta identificación del sujeto pasivo sin vinculación formal prematura |

### Descripción

**¿Quién?** El Funcionario de Instrucción (rol: instructor) asignado al caso mediante auto de reparto.

**¿Qué?** Visualiza la información consolidada de la persona que se encuentra en etapa de averiguación dentro del módulo de indagación previa, accediendo a sus datos de identificación, antecedentes registrales relevantes y estado actual del procedimiento.

**¿Para qué?** Para contar con información veraz y actualizada que permita orientar las actuaciones investigativas iniciales, verificar la identidad del posible sujeto pasivo y garantizar que las comunicaciones y notificaciones se dirijan correctamente, respetando la presunción de inocencia y la naturaleza no vinculante de esta etapa.

**Referencias Normativas:**
- Ley 1952 de 2019 (Código General Disciplinario), Artículo 208: Indagación Previa.
- Ley 1952 de 2019, Artículo 7: Presunción de Inocencia.
- Ley 1952 de 2019, Artículo 115: Reserva de la Actuación.
- Ley 1952 de 2019, Artículo 121: Notificaciones Personales.
- Ley 1564 de 2012 (Código General del Proceso), Artículo 169: Medios de Prueba Documental.
- Decreto 1069 de 2015: Regulación de Datos Personales en el Sector Justicia.
- Sentencia T-760 de 2004 (Corte Constitucional): Protección de datos personales en procesos disciplinarios.

## Dependencias y Precondiciones

1. El expediente disciplinario debe encontrarse en estado "En Indagación Previa" según registro en el sistema.
2. El usuario debe estar autenticado con rol "Funcionario de Instrucción" asignado al caso específico.
3. Debe existir al menos un registro de identificación preliminar de la persona en averiguación cargado en el sistema.
4. El sistema debe tener conexión activa con las bases de datos registrales autorizadas (RUNT, SISBEN, Antecedentes Disciplinarios, etc.).
5. La sesión del usuario debe estar activa dentro del shell institucional con permisos RBAC configurados.
6. Debe haberse completado la HU-15-01 para validación del término vigente de la indagación.

## Restricciones

1. La información mostrada debe limitarse estrictamente a datos necesarios para la identificación, sin revelar conclusiones anticipadas.
2. No se permitirá la descarga masiva de datos personales de la persona en averiguación sin autorización expresa.
3. El acceso a antecedentes registrales está sujeto a los niveles de clasificación definidos por la ley de protección de datos.
4. La visualización debe mantener la reserva de la actuación conforme al Artículo 115 del CGD.
5. No se mostrarán datos sensibles (origen racial, opiniones políticas, convicciones religiosas) salvo excepción legal expresa.
6. El tiempo de carga de la información no podrá exceder los 3 segundos.
7. La interfaz debe ser accesible bajo estándares WCAG 2.1 nivel AA.
8. Cualquier consulta a bases de datos externas debe quedar registrada en el audit log.

## Reglas de Negocio

1. **RN-15-03-01**: Solo el funcionario instructor asignado puede visualizar datos completos; otros roles ven información anonimizada.
2. **RN-15-03-02**: Los datos de identificación deben provenir exclusivamente de fuentes oficiales validadas por el Estado colombiano.
3. **RN-15-03-03**: Si existen múltiples personas con nombres similares, el sistema debe mostrar alertas de posible homonimia.
4. **RN-15-03-04**: La actualización de datos desde registros externos se realiza cada 24 horas automáticamente.
5. **RN-15-03-05**: Cualquier modificación manual a los datos de identificación requiere justificación escrita y aprobación del jefe inmediato.
6. **RN-15-03-06**: El sistema debe impedir la visualización si el término de indagación previa ha vencido.
7. **RN-15-03-07**: Los datos de contacto deben verificarse antes de cada intento de notificación personal.

## Supuestos

1. Se asume que la persona en averiguación cuenta con documentos de identificación vigentes emitidos por autoridad colombiana.
2. Se presume que las bases de datos registrales están actualizadas y disponibles durante el horario hábil.
3. Se considera que el funcionario instructor tiene capacitación básica en manejo de herramientas digitales del sistema.
4. Se espera que la conectividad a internet sea estable durante la consulta de información registral.

## Criterios de Aceptación

**Escenario 1: Visualización exitosa de datos básicos**
Dado que soy un Funcionario de Instrucción asignado al caso
Cuando accedo al módulo de visualización de persona en averiguación
Entonces el sistema muestra nombre completo, tipo y número de documento, fecha de expedición y lugar de expedición
Y muestra fotografía si está disponible en la base de datos oficial
Y el tiempo de carga es inferior a 3 segundos

**Escenario 2: Consulta de antecedentes registrales autorizados**
Dado que soy un Funcionario de Instrucción con caso activo en indagación previa
Cuando solicito consultar antecedentes disciplinares, fiscales y policivos
Entonces el sistema conecta con las bases de datos autorizadas (Procuraduría, Fiscalía, Policía)
Y muestra únicamente los antecedentes vigentes y relevantes para el caso
Y registra la consulta en el audit log con fecha, hora y usuario

**Escenario 3: Alerta de homonimia detectada**
Dado que soy un Funcionario de Instrucción consultando una persona en averiguación
Cuando existen múltiples registros con nombre y documento similares en las bases de datos
Entonces el sistema muestra una alerta visible indicando "Posible homonimia detectada"
Y presenta una lista diferenciada con datos adicionales para discriminación (fecha nacimiento, lugar expedición)
Y requiere confirmación explícita del usuario para continuar con el registro seleccionado

**Escenario 4: Acceso denegado por rol no autorizado**
Dado que soy un usuario con rol diferente a Funcionario de Instrucción
Cuando intento acceder a la visualización completa de datos de la persona en averiguación
Entonces el sistema bloquea el acceso y muestra mensaje "Acceso restringido: Rol no autorizado"
Y solo permite visualizar información pública genérica sin datos personales identificables
Y registra el intento de acceso no autorizado en el sistema de seguridad

**Escenario 5: Error de conexión a bases de datos externas**
Dado que soy un Funcionario de Instrucción intentando consultar antecedentes
Cuando las bases de datos registrales externas no están disponibles temporalmente
Entonces el sistema muestra mensaje "Servicio temporalmente no disponible. Intente más tarde"
Y permite continuar con los datos básicos almacenados localmente
Y programa un reintento automático de sincronización en 15 minutos

**Escenario 6: Visualización con término de indagación vencido**
Dado que soy un Funcionario de Instrucción consultando un caso
Cuando el término de indagación previa ha superado los seis meses calendario
Entonces el sistema muestra alerta roja "TÉRMINO VENCIDO - Requiere acción inmediata"
Y deshabilita opciones de ampliación de investigación sobre esta persona
Y sugiere proyección de decisión de archivo o apertura según corresponda

**Escenario 7: Actualización automática de datos de contacto**
Dado que soy un Funcionario de Instrucción preparando notificación personal
Cuando accedo a los datos de contacto de la persona en averiguación
Entonces el sistema verifica automáticamente la vigencia de direcciones y teléfonos
Y muestra indicador de última verificación (fecha y hora)
Y permite solicitar actualización mediante formulario especializado si los datos son antiguos

## Prototipo / Anexos

- Pantalla de referencia: `/workspace/Pantallas VEED/15_gestion_indagacion_v1.html`
- Sección específica: Pestaña "Persona en Averiguación"
- Componentes UX identificados:
  - Card informativa con fotografía y datos básicos
  - Panel de antecedentes registrales con semáforo de estados
  - Alerta de homonimia modal
  - Timeline de actualizaciones de datos
  - Botones de acción: "Solicitar actualización", "Reportar inconsistencia"
- Tokens de diseño: Fuente Poppins, colores institucionales (#063853 primario, #FFE601 secundario)
- Mockup de interfaz responsive aprobado por área UX

## Stakeholders

- Funcionarios de Instrucción (Usuarios primarios)
- Procuraduría General de la Nación (Entidad reguladora)
- Oficina de Tecnologías de la Información (Soporte técnico)
- Grupo de Protección de Datos Personales (Control y vigilancia)
- Defensoría del Pueblo (Supervisión derechos fundamentales)
- Área Jurídica Institucional (Validación normativa)

## Plan de Validación

| Fase | Actividad | Responsable | Entregable | Criterio de éxito |
|------|-----------|-------------|------------|-------------------|
| 1 | Revisión documental de requisitos | Líder de Proyecto | Acta de revisión | 100% de requisitos cubiertos |
| 2 | Pruebas de usabilidad con funcionarios | UX Lead | Informe de usabilidad | SUS Score ≥ 80 |
| 3 | Validación de integración con registros | Arquitecto de Software | Reporte de pruebas | 0 errores críticos |
| 4 | Auditoría de protección de datos | DPO | Certificado de cumplimiento | Conformidad total con Decreto 1069/2015 |
| 5 | Capacitación a usuarios finales | Equipo de Formación | Constancias de asistencia | 90% de aprobados en evaluación |
| 6 | Despliegue en ambiente productivo | DevOps | Acta de puesta en producción | 0 incidentes post-despliegue |

## Matriz de Trazabilidad con Referencias Normativas

| Artículo | Norma | Descripción | Implementación Técnica | Estado |
|----------|-------|-------------|------------------------|--------|
| Art. 208 | Ley 1952/2019 | Indagación previa sin vinculación formal | Card informativa sin lenguaje vinculante | ✅ |
| Art. 7 | Ley 1952/2019 | Presunción de inocencia | Mensajes informativos neutros | ✅ |
| Art. 115 | Ley 1952/2019 | Reserva de actuación | Control de acceso por roles | ✅ |
| Art. 121 | Ley 1952/2019 | Notificaciones personales | Verificación de datos de contacto | ✅ |
| Art. 169 | Ley 1564/2012 | Prueba documental | Integración con registros oficiales | ✅ |
| Art. 15 | Decreto 1069/2015 | Principios de tratamiento de datos | Minimización y finalidad en visualización | ✅ |
| Art. 29 | Constitución Política | Debido proceso | Trazabilidad de consultas realizadas | ✅ |
| Sentencia T-760/04 | Corte Constitucional | Habeas Data | Derecho de acceso y rectificación | ✅ |

## Requisitos de Seguridad y Auditoría

1. **Autenticación**: OAuth 2.0 con doble factor para acceso a datos sensibles.
2. **Autorización**: Modelo RBAC + ABAC basado en rol, caso asignado y nivel de clasificación.
3. **Cifrado**: TLS 1.3 para transmisión, AES-256 para almacenamiento de datos personales.
4. **Audit Log**: Registro inmutable de todas las consultas con timestamp, usuario, IP y datos accedidos.
5. **Prevención de fugas**: DLP (Data Loss Prevention) para bloquear descargas no autorizadas.
6. **Máscara de datos**: Ofuscación parcial de números de documento en pantallas compartidas.
7. **Retención**: Conservación de logs por 10 años según normativa de archivo judicial.
8. **Respuesta a incidentes**: Protocolo de actuación ante brechas de datos personales (< 72 horas).

## Protocolo de Respuesta a Incidentes de Datos Personales

| Tipo de Incidente | Acción Inmediata | Notificación | Plazo | Responsable |
|-------------------|------------------|--------------|-------|-------------|
| Acceso no autorizado | Bloqueo de sesión | Superintendencia de Industria y Comercio | 72 horas | CISO |
| Fuga de datos | Contención y forense | Titulares de datos afectados | 72 horas | DPO |
| Inconsistencia de datos | Corrección y validación | Funcionario instructor | 24 horas | Admin BD |
| Caída de servicio externo | Modo degradado | Usuarios afectados | Inmediato | DevOps |

## Glosario de Términos

- **Persona en Averiguación**: Individuo sobre quien recaen indicios preliminares de conducta disciplinariamente relevante, sin vinculación formal aún.
- **Homonimia**: Coincidencia de nombres entre diferentes personas que puede generar confusión en identificación.
- **Antecedentes Registrales**: Información oficial sobre historial disciplinario, fiscal o policial de un ciudadano.
- **Reserva de Actuación**: Principio que limita el acceso a información del proceso durante etapas preliminares.
- **Audit Log**: Registro cronológico inmutable de eventos del sistema para fines de trazabilidad.

## Definition of Done (DoD)

- [ ] Historia de usuario documentada según estándar PGN
- [ ] Requisitos normativos validados por área jurídica
- [ ] Prototipo de interfaz aprobado por comité UX
- [ ] Casos de prueba unitaria implementados (cobertura ≥ 90%)
- [ ] Pruebas de integración con bases de datos registrales exitosas
- [ ] Auditoría de seguridad informática aprobada
- [ ] Evaluación de impacto en protección de datos realizada
- [ ] Manual de usuario elaborado y traducido a lenguaje claro
- [ ] Sesión de capacitación realizada con funcionarios piloto
- [ ] Aprobación formal del Product Owner y Comité de Gobierno

---

*Documento generado bajo estándares de calidad del Sistema de Gestión de Calidad ISO 9001:2015*
*Versión: 1.0 | Última actualización: 13/05/2026 | Clasificación: Reservado*
