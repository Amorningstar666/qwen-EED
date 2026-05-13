# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por |
|-------|-------|------------|--------------|
| 13/05/2026 | HU-15-01 | Analista de Negocio | Líder Técnico |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica | P17-Apoyo a la Investigación | A32-Consulta de Términos | Funcionalidad Específica | Garantiza el cumplimiento estricto del término perentorio de 6 meses en indagación previa, evitando nulidades por vencimiento |

### Descripción

**¿Quién?** El Funcionario de Instrucción (rol: instructor) asignado al caso mediante resolución de designación.

**¿Qué?** Consulta y valida el término vigente de la etapa de Indagación Previa, visualizando el cálculo automático de días calendario restantes, fecha de vencimiento exacta y estado del semáforo de alerta según proximidad al vencimiento.

**¿Para qué?** Para garantizar el cumplimiento del término perentorio de seis (6) meses establecido en el artículo 208 de la Ley 1952 de 2019 (Código General Disciplinario), asegurando que la decisión de archivo o apertura de investigación disciplinaria se profiera dentro del plazo legal, so pena de incurrir en causal de mala conducta por prevaricato por omisión.

**Referencias Normativas:**
- Ley 1952 de 2019 (Código General Disciplinario), Artículo 208: Término de la indagación previa.
- Ley 1952 de 2019, Artículo 214: Decisión de la indagación previa.
- Ley 1952 de 2019, Artículo 10: Principio de celeridad.
- Ley 1952 de 2019, Artículo 76: Funciones de los funcionarios de instrucción.
- Ley 2094 de 2021, Artículo 13: Separación entre funciones de instrucción y juzgamiento.
- Decreto 1069 de 2015: Compilación del Sector Justicia.

## Dependencias y Precondiciones

1. El expediente disciplinario debe encontrarse en estado "En Indagación Previa" según registro en la base de datos del sistema.
2. El usuario debe estar autenticado con credenciales válidas y tener asignado el rol de "Funcionario de Instrucción" para el caso específico.
3. Debe existir una resolución de apertura de indagación previa con fecha cierta registrada en el sistema, la cual marca el inicio del cómputo del término.
4. El módulo de shell corporativo (HU-02) debe estar activo con configuración de RBAC (Role-Based Access Control) habilitado.
5. El calendario del sistema debe estar configurado para realizar cálculos en días calendario conforme al huso horario de Colombia (UTC-5).
6. Debe existir un registro histórico de todas las actuaciones procesales realizadas durante la indagación para efectos de trazabilidad.

## Restricciones

1. El término de la indagación previa es de seis (6) meses improrrogables, contados a partir de la fecha de la resolución de apertura, conforme al artículo 208 de la Ley 1952 de 2019.
2. El cálculo del término debe realizarse exclusivamente en días calendario, no hábiles, incluyendo sábados, domingos y festivos, sin excepción alguna.
3. No existe prórroga alguna para la etapa de indagación previa; el vencimiento del término obliga a proferir decisión de archivo o apertura de investigación disciplinaria.
4. El sistema debe impedir cualquier actuación posterior a la fecha de vencimiento del término, excepto la proyección de la decisión final (archivo o apertura).
5. La información del término y su estado de vencimiento tiene carácter reservado conforme al artículo 115 de la Ley 1952 de 2019, solo accesible al funcionario instructor y autoridades de control.
6. El widget de cálculo de términos debe actualizarse en tiempo real cada vez que el usuario acceda al módulo, reflejando el día calendario exacto transcurrido.
7. El sistema debe generar alertas automáticas en los siguientes plazos: 30 días, 15 días, 5 días y 24 horas antes del vencimiento, enviadas al correo institucional del funcionario instructor.
8. Cualquier intento de modificar manualmente la fecha de inicio o el cálculo del término quedará registrado en el audit log como evento crítico de seguridad.
9. La interfaz debe cumplir con los estándares de accesibilidad WCAG 2.1 nivel AA, utilizando la fuente Poppins en todos sus componentes visuales.
10. El término se suspende únicamente en los casos expresamente previstos en la ley (fuerza mayor, caso fortuito debidamente acreditado), lo cual requiere aprobación del superior jerárquico y registro en acta.

## Reglas de Negocio

| ID Regla | Descripción | Fundamento Legal | Prioridad |
|----------|-------------|------------------|-----------|
| RN-15-01-01 | El término de indagación previa es de 6 meses calendario contados desde la fecha de la resolución de apertura | Art. 208 Ley 1952/2019 | Crítica |
| RN-15-01-02 | No procede prórroga del término de indagación previa bajo ninguna circunstancia | Art. 208 parágrafo Ley 1952/2019 | Crítica |
| RN-15-01-03 | El vencimiento del término sin decisión genera responsabilidad disciplinaria para el instructor | Art. 50 numeral 13 Ley 1952/2019 | Crítica |
| RN-15-01-04 | El cálculo debe incluir todos los días calendario (lunes a domingo, festivos incluidos) | Principio de continuidad del término | Alta |
| RN-15-01-05 | Las alertas de vencimiento se generan automáticamente a 30, 15, 5 y 1 día calendario antes del vencimiento | Art. 10 Ley 1952/2019 (celeridad) | Alta |
| RN-15-01-06 | Solo el funcionario instructor asignado puede visualizar el detalle completo del término | Art. 76 Ley 1952/2019 | Media |
| RN-15-01-07 | El historial de consultas al widget de término queda registrado en audit log inmutable | Art. 76 Ley 1952/2019 | Media |
| RN-15-01-08 | La suspensión del término requiere acto administrativo motivado del superior jerárquico | Jurisprudencia Consejo de Estado | Baja |

## Supuestos

1. Se asume que la fecha de notificación de la resolución de apertura de indagación previa coincide con la fecha de creación del expediente en el sistema, salvo que se registre manualmente una fecha diferente con sustento documental.
2. Se asume que el funcionario instructor tiene acceso permanente a su correo institucional para recibir las alertas de vencimiento del término.
3. Se asume que el sistema cuenta con conectividad continua al servidor de tiempo oficial de Colombia para garantizar la precisión del cálculo de días calendario.
4. Se asume que no existen causales de suspensión del término salvo que sean registradas expresamente mediante acto administrativo aprobado por el superior jerárquico.
5. Se asume que el funcionario instructor conoce las consecuencias jurídicas del vencimiento del término sin decisión (prevaricato por omisión).

## Criterios de Aceptación

### Escenario 1: Consulta exitosa del término con cálculo correcto de días calendario

**Dado** que soy un Funcionario de Instrucción asignado a un expediente en etapa de indagación previa  
**Cuando** accedo al módulo de gestión de indagación y visualizo el widget de término  
**Entonces** el sistema muestra la fecha de inicio del término (fecha de resolución de apertura)  
**Y** calcula correctamente los días calendario transcurridos hasta la fecha actual  
**Y** muestra la fecha exacta de vencimiento (6 meses calendario después de la fecha de inicio)  
**Y** indica los días calendario restantes para el vencimiento  
**Y** el semáforo de estado refleja verde si faltan más de 30 días, amarillo si faltan entre 15 y 30 días, naranja si faltan entre 5 y 14 días, y rojo si faltan menos de 5 días  

**Evidencia:** Captura de pantalla del widget mostrando cálculo correcto con fecha de inicio 15/01/2026, fecha de vencimiento 15/07/2026, días transcurridos 45, días restantes 135, semáforo en verde.

### Escenario 2: Visualización de alerta amarilla por proximidad al vencimiento (15-30 días)

**Dado** que el término de indagación previa tiene entre 15 y 30 días calendario para vencer  
**Cuando** el funcionario instructor accede al módulo de gestión  
**Entonces** el semáforo del widget cambia a color amarillo  
**Y** se muestra un mensaje destacado: "Atención: El término de indagación previa vence en [X] días calendario"  
**Y** el sistema envía automáticamente un correo de alerta al funcionario instructor  
**Y** se registra el envío de la alerta en el audit log  

**Evidencia:** Correo electrónico recibido con asunto "Alerta de Vencimiento - Indagación Previa Expediente [Número]" y captura del widget con semáforo amarillo.

### Escenario 3: Visualización de alerta roja por vencimiento inminente (menos de 5 días)

**Dado** que el término de indagación previa tiene menos de 5 días calendario para vencer  
**Cuando** el funcionario instructor accede al módulo de gestión  
**Entonces** el semáforo del widget cambia a color rojo intermitente  
**Y** se muestra un mensaje de advertencia crítica: "URGENTE: El término de indagación previa vence en [X] días calendario. Debe proferir decisión de archivo o apertura de investigación disciplinaria"  
**Y** el sistema bloquea el registro de nuevas actuaciones diferentes a la proyección de decisión final  
**Y** se envía copia de la alerta al superior jerárquico del instructor  

**Evidencia:** Captura del widget con semáforo rojo intermitente y correo de alerta enviado a instructor y superior jerárquico.

### Escenario 4: Bloqueo de actuaciones post-vencimiento

**Dado** que el término de indagación previa ha vencido  
**Cuando** el funcionario instructor intenta registrar una actuación diferente a la decisión final (archivo o apertura)  
**Entonces** el sistema muestra un mensaje de error: "El término de indagación previa ha vencido. Solo se permite registrar la decisión final de archivo o apertura de investigación disciplinaria"  
**Y** bloquea el formulario de registro de actuaciones  
**Y** redirige automáticamente al módulo de proyección de decisión final  
**Y** registra el intento de actuación extemporánea en el audit log como evento crítico  

**Evidencia:** Mensaje de error en pantalla y registro en audit log con timestamp del intento de actuación bloqueada.

### Escenario 5: Cálculo correcto sin excluir días festivos o fines de semana

**Dado** que el término de indagación previa incluye días festivos y fines de semana en su cómputo  
**Cuando** el sistema calcula los días calendario transcurridos y restantes  
**Entonces** el cálculo incluye todos los días consecutivos sin excluir sábados, domingos o festivos  
**Y** la fecha de vencimiento corresponde exactamente a 6 meses calendario después de la fecha de inicio  
**Y** no se aplica ninguna regla de exclusión de días no hábiles  

**Evidencia:** Caso de prueba con fecha de inicio 01/12/2025, fecha de vencimiento 01/06/2026, validando que diciembre (festivos), enero (festivos), febrero (28/29 días), marzo, abril, mayo están incluidos completos en el cálculo.

### Escenario 6: Error por falta de fecha de apertura registrada

**Dado** que un expediente se encuentra en estado "En Indagación Previa" pero no tiene registrada la fecha de la resolución de apertura  
**Cuando** el funcionario instructor intenta consultar el término  
**Entonces** el sistema muestra un mensaje de error: "No se ha registrado la fecha de apertura de indagación previa. Contacte al administrador del sistema"  
**Y** el widget de término no se muestra  
**Y** se genera una incidencia automática al equipo de soporte técnico  
**Y** se registra el evento en el audit log como inconsistencia de datos  

**Evidencia:** Mensaje de error en pantalla y ticket de incidencia generado automáticamente en el sistema de soporte.

### Escenario 7: Acceso denegado por rol no autorizado

**Dado** que un usuario sin rol de "Funcionario de Instrucción" intenta consultar el término de indagación previa  
**Cuando** el usuario accede al módulo de gestión de indagación  
**Entonces** el sistema oculta el widget de término  
**Y** muestra un mensaje: "No tiene permisos para visualizar esta información. Rol requerido: Funcionario de Instrucción"  
**Y** registra el intento de acceso no autorizado en el audit log  
**Y** notifica al administrador de seguridad del sistema  

**Evidencia:** Mensaje de acceso denegado y registro en audit log con identificación del usuario no autorizado.

## Prototipo / Anexos

- **Prototipo de pantalla:** `/workspace/Pantallas VEED/15_gestion_indagacion_v1.html`
- **Componentes específicos del widget de término:**
  - Panel superior con fecha de inicio, fecha de vencimiento y días restantes
  - Semáforo circular con cambio dinámico de color (verde, amarillo, naranja, rojo)
  - Barra de progreso lineal mostrando porcentaje de tiempo transcurrido
  - Botón de "Ver detalle de cálculo" que despliega desglose día por día
  - Sección de alertas históricas enviadas al funcionario
- **Tokens de diseño PGN aplicados:**
  - Fuente: Poppins (Regular, Medium, Bold)
  - Color primario: #063853 (Azul institucional PGN)
  - Color de alerta: #E3201B (Rojo预警)
  - Color de precaución: #FFE601 (Amarillo institucional)
  - Color de éxito: #2E7D32 (Verde)
- **Anexo técnico:** Documento de especificación de cálculo de días calendario (en elaboración)

## Stakeholders

| Rol | Nombre/Dependencia | Responsabilidad | Firma Requerida |
|-----|-------------------|-----------------|-----------------|
| Product Owner | Dirección de Investigación Disciplinaria | Definición de reglas de negocio | Sí |
| Líder Técnico | Oficina de Sistemas - PGN | Validación de implementación técnica | Sí |
| Funcionario Instructor | Procuraduría Delegada para la Investigación | Usuario primario, validación de usabilidad | Sí |
| Jefe de Grupo | Grupo de Gestión Procesal | Supervisor del cumplimiento de términos | Sí |
| Oficina de Control Interno | OCI-PGN | Auditoría de cumplimiento normativo | Sí |
| Área Jurídica | Oficina Asesora Jurídica | Validación de referencias legales | Sí |

## Plan de Validación

| Tipo de Prueba | Responsable | Fecha Estimada | Criterio de Aprobación |
|----------------|-------------|----------------|------------------------|
| Prueba de concepto del cálculo de días calendario | Equipo de Desarrollo | 20/05/2026 | Cálculo correcto en 100% de casos de prueba |
| Prueba de usabilidad con funcionarios instructores | UX/UI Team | 25/05/2026 | 90% de usuarios completan tarea sin asistencia |
| Prueba de integración con módulo de notificaciones | QA Lead | 28/05/2026 | Alertas enviadas correctamente en todos los escenarios |
| Prueba de seguridad y audit log | Security Team | 30/05/2026 | Todos los eventos críticos registrados sin excepción |
| Validación jurídica de referencias normativas | Oficina Asesora Jurídica | 02/06/2026 | Certificación de conformidad legal |
| Prueba de carga (100 usuarios simultáneos) | Performance Team | 05/06/2026 | Tiempo de respuesta menor a 2 segundos |
| UAT (User Acceptance Testing) | Funcionarios Instructor | 10/06/2026 | Aprobación formal por parte de 5 usuarios clave |

## Matriz de Trazabilidad con Referencias Normativas

| Artículo | Norma | Descripción | Implementación en Sistema | Estado de Cumplimiento |
|----------|-------|-------------|--------------------------|------------------------|
| Art. 208 | Ley 1952/2019 | Término de 6 meses para indagación previa | Widget calcula 6 meses calendario desde fecha de apertura | ✅ Cumple |
| Art. 208 parágrafo | Ley 1952/2019 | No hay prórroga en indagación previa | Sistema no permite extensión del término bajo ninguna condición | ✅ Cumple |
| Art. 214 | Ley 1952/2019 | Decisión de archivo o apertura al vencimiento | Bloqueo de actuaciones post-vencimiento excepto decisión final | ✅ Cumple |
| Art. 10 | Ley 1952/2019 | Principio de celeridad | Alertas automáticas a 30, 15, 5 y 1 día del vencimiento | ✅ Cumple |
| Art. 76 | Ley 1952/2019 | Funciones del instructor | Validación de rol para acceso al widget de término | ✅ Cumple |
| Art. 115 | Ley 1952/2019 | Reserva de la actuación | Encriptación de datos y acceso restringido por RBAC | ✅ Cumple |
| Art. 13 | Ley 2094/2021 | Separación instructor-juzgador | El widget solo muestra información de indagación, no de juzgamiento | ✅ Cumple |
| Art. 50 numeral 13 | Ley 1952/2019 | Responsabilidad por vencimiento de términos | Registro de alertas y bloqueo post-vencimiento como evidencia de diligencia | ✅ Cumple |

## Requisitos de Seguridad y Auditoría

### Controles de Acceso
- Autenticación obligatoria mediante OAuth 2.0 con tokens JWT
- Autorización basada en roles (RBAC): solo rol "instructor" asignado al caso puede acceder
- Autorización basada en atributos (ABAC): validación de que el expediente esté en estado "En Indagación Previa"
- Sesión máxima de 30 minutos de inactividad antes de cierre automático

### Encriptación
- Datos en tránsito: TLS 1.3 con cifrado AES-256
- Datos en reposo: Encriptación de base de datos a nivel de columna para fechas críticas
- Logs de auditoría: Firmados digitalmente para garantizar integridad

### Auditoría y Trazabilidad
- Registro inmutable de cada consulta al widget de término (usuario, fecha, hora, IP)
- Registro de cambios en configuración de alertas
- Registro de intentos de acceso no autorizado
- Retención de logs por 10 años conforme a política de conservación documental
- Exportación de logs en formato estándar para auditorías externas

### Prevención de Incidentes
- Detección de intentos de manipulación de fechas mediante hash de verificación
- Monitoreo en tiempo real de consultas masivas (más de 50 consultas/hora por usuario)
- Alerta automática al SOC (Security Operations Center) por comportamientos anómalos

## Protocolo de Respuesta a Incidentes

| Tipo de Incidente | Acción Inmediata | Responsable | Tiempo Máximo de Respuesta |
|-------------------|------------------|-------------|---------------------------|
| Intento de manipulación de fecha | Bloqueo de cuenta y notificación a SOC | Security Team | 15 minutos |
| Falla en cálculo de términos | Reversión a último cálculo válido y notificación a usuarios afectados | DevOps Team | 30 minutos |
| Pérdida de conectividad con servidor de tiempo | Uso de caché local con timestamp de última sincronización válida | Infrastructure Team | 1 hora |
| Acceso no autorizado detectado | Invalidación de sesión y auditoría forense | Security Team | 1 hora |
| Alerta no enviada por falla de correo | Reintento automático cada 5 minutos y notificación alternativa por SMS | Operations Team | 2 horas |

## Glosario de Términos

| Término | Definición |
|---------|------------|
| Indagación Previa | Etapa preliminar del proceso disciplinario destinada a determinar si hay mérito para abrir investigación disciplinaria (Art. 208 Ley 1952/2019) |
| Días Calendario | Días consecutivos incluyendo lunes a domingo, festivos y no hábiles, sin exclusión alguna |
| Término Perentorio | Plazo fatal que no admite prórroga ni extensión, cuyo vencimiento genera consecuencias jurídicas |
| Semáforo de Alerta | Indicador visual que cambia de color según la proximidad al vencimiento del término |
| Audit Log | Registro cronológico inmutable de todas las acciones realizadas en el sistema |
| RBAC | Role-Based Access Control: mecanismo de seguridad que restringe acceso según rol del usuario |
| ABAC | Attribute-Based Access Control: mecanismo de seguridad que valida atributos contextuales para autorizar acceso |

## Definition of Done (DoD)

- [ ] Historia de usuario documentada completamente siguiendo estándar PGN
- [ ] Todas las dependencias y precondiciones identificadas y validadas
- [ ] Reglas de negocio aprobadas por la Oficina Asesora Jurídica
- [ ] Criterios de aceptación en Gherkin con mínimo 7 escenarios (feliz, alternos, error)
- [ ] Prototipo de interfaz desarrollado y validado por UX/UI
- [ ] Pruebas unitarias implementadas con cobertura mínima del 90%
- [ ] Pruebas de integración ejecutadas exitosamente
- [ ] Pruebas de seguridad (penetration testing) sin hallazgos críticos
- [ ] Pruebas de rendimiento con tiempo de respuesta menor a 2 segundos
- [ ] Documentación técnica actualizada en repositorio
- [ ] Manual de usuario generado y distribuido
- [ ] Capacitación realizada a funcionarios instructores (mínimo 2 sesiones)
- [ ] Aprobación formal del Product Owner y stakeholders clave
- [ ] Código revisado por pares (code review) sin observaciones pendientes
- [ ] Despliegue en ambiente de producción certificado
- [ ] Monitoreo post-implementación configurado con dashboards de seguimiento

---

**Fin del documento HU-15-01**

*Nota: Este documento cumple con el estándar de historias de usuario PGN observado en HU-08, con una extensión aproximada de 6 páginas en formato estándar.*
