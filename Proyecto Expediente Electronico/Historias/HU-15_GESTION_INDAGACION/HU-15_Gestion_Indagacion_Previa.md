# Historia de Usuario Principal - HU-15

| Fecha | ID HU | Creado por | Validado por | Versión |
|-------|-------|------------|--------------|---------|
| 13/05/2026 | HU-15 | Analista de Negocio | Líder Técnico / Oficina Jurídica | 1.0 |

## Información General del Macroproceso

| Macroproceso | Proceso | Actividad | Clasificación | Valor de Negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica Disciplinaria | P17-Instrucción y Juzgamiento | A30-Gestión de Indagación Previa | Funcionalidad Crítica | Garantizar el cumplimiento estricto del término perentorio de 6 meses para la indagación previa, evitando nulidades por vencimiento de términos y asegurando la debida diligencia en la investigación preliminar conforme al Art. 208 CGD. |

---

## 1. DESCRIPCIÓN DETALLADA DE LA HISTORIA DE USUARIO

### ¿Quién? (Rol del Usuario)
El **Funcionario de Instrucción** (rol: `instructor`), quien es un abogado o profesional universitario designado mediante acto administrativo como Instructor Disciplinario, encargado de adelantar la etapa de Indagación Previa conforme a los artículos 76, 208 y siguientes de la Ley 1952 de 2019 (Código General Disciplinario). Este rol tiene la facultad legal de practicar pruebas, citar personas, solicitar informes y proyectar la decisión de archivo o apertura de investigación disciplinaria, bajo la supervisión del Despacho que ordenó la apertura.

### ¿Qué? (Funcionalidad Central)
Gestionar integralmente la etapa de **Indagación Previa** dentro del Sistema de Expediente Electrónico Disciplinario (VEED), permitiendo al instructor consultar el estado del término perentorio, registrar actuaciones procesales, gestionar pruebas de identificación (documentales, testimoniales, periciales), visualizar la información de la persona en averiguación sin vinculación formal, cargar y consultar documentos con reserva de actuación, proyectar autos de archivo o de apertura de investigación disciplinaria, y consultar el historial auditado de todas las actuaciones realizadas. La funcionalidad integra un widget de control de términos que calcula automáticamente los días calendario restantes hasta el vencimiento del plazo de 6 meses establecido en el Art. 208 CGD, sin posibilidad de prórroga.

### ¿Para qué? (Objetivo de Negocio y Legal)
Para garantizar el cumplimiento estricto del término perentorio de seis (6) meses establecido en el **Artículo 208 de la Ley 1952 de 2019**, evitando la caducidad de la acción disciplinaria por extemporaneidad en la decisión de archivo o apertura de investigación. Esta gestión permite al instructor ejercer sus funciones con eficiencia, trazabilidad y seguridad jurídica, asegurando que todas las actuaciones queden registradas en el expediente electrónico con respeto a la reserva de la actuación (Art. 115 CGD), la debida notificación electrónica (Arts. 121-123 CGD) y la separación funcional entre instructor y juzgador (Ley 2094 de 2021, Art. 13). El sistema previene errores humanos en el cálculo de términos y facilita la toma de decisiones fundamentadas dentro del plazo legal.

### Referencias Normativas Vigentes
- **Ley 1952 de 2019 (Código General Disciplinario - CGD):** Arts. 76 (Funcionarios de instrucción), 115 (Reserva), 121-123 (Notificaciones), 208 (Indagación Previa y término perentorio), 214-216 (Decisión de indagación).
- **Ley 2094 de 2021:** Art. 13 (Separación de funciones entre instructor y juzgador).
- **Decreto 1083 de 2015:** Decreto Único Reglamentario del Sector Justicia (gestión documental electrónica).
- **Sentencia C-161 de 2022 (Corte Constitucional):** Exequibilidad de términos perentorios en materia disciplinaria.
- **Circular 003 de 2020 (Procuraduría General):** Lineamientos para la indagación previa.
- **Acuerdo 001 de 2021 (Comisión Nacional de Disciplina Judicial):** Reglamento interno de procedimientos.

---

## 2. DEPENDENCIAS Y PRECONDICIONES LEGALES

Para que la funcionalidad HU-15 esté disponible y operativa, se deben cumplir estrictamente las siguientes precondiciones técnicas y legales:

1. **Estado del Expediente:** El expediente disciplinario debe haber sido creado y encontrarse en estado **"En Indagación Previa"**, generado automáticamente tras el auto de apertura de indagación previa proferido por el juez o despacho competente conforme al Art. 208 CGD. No se puede acceder a esta gestión si el expediente está en etapa de juicio, apelación o cerrado.

2. **Usuario Autenticado con Rol Asignado:** El usuario debe estar autenticado en el sistema mediante OAuth 2.0 + JWT y tener asignado explícitamente el rol `instructor` en el módulo RBAC (Role-Based Access Control). La asignación del rol debe corresponder a un acto administrativo de designación vigente registrado en el sistema (Art. 76 CGD).

3. **Shell Activo con Configuración RBAC/ABAC:** Debe existir una sesión activa del shell del sistema (HU-02) con políticas de control de acceso basadas en roles (RBAC) y atributos (ABAC) que validen que el instructor pertenece a la misma unidad administrativa o competencia territorial del expediente asignado.

4. **Calendario Oficial Colombiano Configurado:** El sistema debe tener cargado y activo el calendario oficial colombiano para el año en curso y años futuros, identificando correctamente los días festivos declarados por el Ministerio del Interior, aunque para la indagación previa el cálculo sea en días calendario, se requiere para notificaciones y actos posteriores.

5. **Notificación Electrónica Habilitada:** El módulo de notificaciones electrónicas (Art. 122 CGD) debe estar configurado y operativo, con certificados digitales vigentes para la notificación personal electrónica de autos y providencias a los sujetos procesales y sus defensores.

6. **Repositorio Documental Activo:** El sistema de gestión documental electrónico (SGDE) debe estar disponible para permitir la carga, almacenamiento y consulta de documentos con metadatos de reserva de actuación (Art. 115 CGD).

7. **Motor de Reglas de Términos Configurado:** El motor de reglas de negocio debe tener parametrizada la regla "TÉRMINO_INDAGACION_6_MESES" que calcula automáticamente la fecha de vencimiento sumando 6 meses calendario a la fecha del auto de apertura de indagación previa, sin permitir prórrogas.

---

## 3. RESTRICCIONES Y REGLAS DE NEGOCIO

La funcionalidad HU-15 está sujeta a las siguientes restricciones técnicas, legales y operativas que no pueden ser modificadas sin autorización de la Oficina Jurídica:

1. **Separación Funcional Instructor/Juzgador (Ley 2094/2021 Art. 13):** El sistema no permitirá que el mismo usuario que actúa como instructor en la etapa de indagación previa pueda posteriormente actuar como juzgador en la etapa de juicio del mismo expediente. Esta restricción se valida mediante ABAC en cada intento de acceso.

2. **Reserva de Actuación (Art. 115 CGD):** Durante toda la etapa de indagación previa, el acceso a los documentos y actuaciones del expediente está restringido exclusivamente al instructor, al sujeto procesal (una vez sea notificado de la indagación) y a su defensor. El sistema aplicará cifrado AES-256 a nivel de documento y ocultará el contenido a usuarios sin el rol adecuado.

3. **Término Perentorio Sin Prórroga (Art. 208 Parágrafo CGD):** El término de 6 meses para la indagación previa es perentorio y no admite prórroga bajo ninguna circunstancia. El sistema mostrará alertas críticas cuando falten 30, 15, 7 y 1 día(s) calendario para el vencimiento, pero no permitirá extensión del plazo. Vencido el término sin decisión, se configura causal de caducidad.

4. **Decisión Sin Recurso (Art. 208 Parágrafo CGD):** Los autos proferidos en la etapa de indagación previa (archivo o apertura de investigación) no son susceptibles de recurso alguno. El sistema bloqueará cualquier intento de interponer recursos contra estas decisiones y mostrará el mensaje normativo correspondiente.

5. **Audit Trail Inmutable:** Todas las actuaciones registradas en la HU-15 generarán un registro de auditoría inmutable (blockchain o tabla hash encadenada) que no podrá ser modificado ni eliminado, garantizando la trazabilidad completa conforme al Art. 76 CGD y principios de transparencia.

6. **Accesibilidad WCAG 2.1 AA:** Toda la interfaz de usuario debe cumplir con los niveles A y AA de las Pautas de Accesibilidad al Contenido Web (WCAG) 2.1, incluyendo contraste de colores, navegación por teclado, lectores de pantalla y fuente Poppins con tamaños ajustables.

7. **No Identificación Formal en Indagación:** Durante la indagación previa, la persona investigada no tiene la calidad de "sancionado" ni de "investigado formalmente". El sistema evitará usar terminología que implique vinculación formal antes del auto de apertura de investigación disciplinaria (Art. 215 CGD).

8. **Integridad de Fechas:** Las fechas de las actuaciones no pueden ser anteriores a la fecha de apertura de indagación previa ni posteriores a la fecha de vencimiento del término. El sistema validará cronológicamente cada registro.

9. **Límite de Descargas:** Por seguridad y reserva, un usuario solo podrá descargar máximo 20 documentos por sesión en la etapa de indagación previa, salvo autorización expresa del jefe de la unidad.

10. **Bloqueo por Vencimiento:** Una vez vencido el término de 6 meses sin que se haya proferido auto de archivo o apertura, el sistema bloqueará automáticamente el expediente para nuevas actuaciones y generará un reporte automático a la Oficina de Control Interno Disciplinario.

---

## 4. SUPUESTOS OPERATIVOS

Se asumen los siguientes escenarios operativos para el diseño e implementación de la HU-15:

1. **Conectividad Estable:** Se asume que el funcionario de instrucción cuenta con conexión a internet estable durante el horario laboral (lunes a viernes, 8:00 a.m. a 6:00 p.m.) para acceder al sistema VEED.

2. **Capacitación Previa:** Se asume que el usuario ha recibido capacitación básica en el uso del sistema VEED y conoce los conceptos fundamentales del proceso disciplinario (indagación previa, investigación, juicio).

3. **Disponibilidad de Documentos Fuente:** Se asume que los documentos necesarios para la indagación (denuncias, quejas, informes preliminares) ya fueron cargados al sistema en la etapa anterior de admisión.

4. **Validez de Certificados Digitales:** Se asume que los certificados digitales para notificación electrónica están vigentes y configurados correctamente en el sistema.

5. **Soporte Técnico Disponible:** Se asume que existe un equipo de soporte técnico disponible en horario extendido para resolver incidentes críticos relacionados con vencimiento de términos.

---

## 5. CRITERIOS DE ACEPTACIÓN EN GHERKIN

### Escenario 1: Acceso exitoso al módulo de gestión de indagación previa
**Dado** que soy un usuario autenticado con el rol `instructor` asignado  
**Y** el expediente se encuentra en estado "En Indagación Previa"  
**Y** mi sesión está activa con políticas RBAC validadas  
**Cuando** navego al módulo "Gestión de Indagación Previa" desde el menú principal  
**Entonces** el sistema me muestra la pantalla principal con las 5 pestañas: "Término", "Pruebas", "Persona", "Documentos", "Actuaciones"  
**Y** el widget de término muestra los días calendario restantes calculados desde la fecha del auto de apertura  

### Escenario 2: Visualización correcta del widget de término sin prórroga
**Dado** que estoy consultando un expediente en indagación previa  
**Y** la fecha de apertura de indagación fue hace 4 meses calendario  
**Cuando** el sistema calcula el término restante  
**Entonces** muestra "2 meses calendario restantes" (aproximadamente 60 días)  
**Y** NO muestra ninguna opción o botón para solicitar prórroga  
**Y** el semáforo está en amarillo (falta menos de 3 meses)  

### Escenario 3: Registro de actuación procesal con trazabilidad
**Dado** que estoy en la pestaña "Actuaciones"  
**Y** selecciono "Registrar Nueva Actuación"  
**Cuando** completo el formulario con tipo de actuación, descripción y fecha  
**Y** adjunto documentos de soporte  
**Entonces** el sistema guarda la actuación con timestamp inmutable  
**Y** genera un número consecutivo de actuación  
**Y** actualiza el historial auditado inmediatamente  

### Escenario 4: Alerta crítica por vencimiento inminente (30 días)
**Dado** que faltan exactamente 30 días calendario para el vencimiento del término  
**Cuando** el instructor accede al expediente  
**Entonces** el sistema muestra una alerta modal roja con el mensaje: "ALERTA CRÍTICA: Faltan 30 días calendario para el vencimiento del término de indagación previa. Según Art. 208 CGD, este término es perentorio y sin prórroga."  
**Y** envía automáticamente un correo electrónico al instructor y a su jefe inmediato  
**Y** registra la alerta en el log de incidentes  

### Escenario 5: Proyección de auto de archivo sin identificación formal
**Dado** que he determinado que no hay mérito para abrir investigación disciplinaria  
**Y** estoy en la pestaña "Decisiones"  
**Cuando** proyecto un "Auto de Archivo"  
**Entonces** el sistema valida que no existan pruebas pendientes  
**Y** genera el documento con la estructura normativa del Art. 208 parágrafo CGD  
**Y** muestra el mensaje: "Esta decisión no es susceptible de recurso alguno conforme al Art. 208 parágrafo CGD"  
**Y** NOTIFICA automáticamente al denunciante y al sujeto en averiguación  

### Escenario 6: Proyección de auto de apertura de investigación disciplinaria
**Dado** que he determinado que existen elementos probatorios suficientes para iniciar investigación formal  
**Y** estoy en la pestaña "Decisiones"  
**Cuando** proyecto un "Auto de Apertura de Investigación Disciplinaria"  
**Entonces** el sistema valida que se hayan practicado las pruebas mínimas de identificación  
**Y** genera el documento conforme al Art. 215 CGD  
**Y** cambia automáticamente el estado del expediente a "En Investigación Disciplinaria"  
**Y** NOTIFICA personalmente por medios electrónicos al nuevo investigado y a su defensor  

### Escenario 7: Error de acceso por rol no autorizado
**Dado** que soy un usuario con rol `ciudadano` o `defensor` sin asignación como `instructor`  
**Cuando** intento acceder al módulo "Gestión de Indagación Previa"  
**Entonces** el sistema bloquea el acceso inmediatamente  
**Y** muestra el mensaje: "Acceso denegado. Solo los funcionarios con rol 'Instructor' asignado pueden gestionar esta etapa. Artículo 76 CGD."  
**Y** registra el intento fallido en el log de seguridad  

### Escenario 8: Bloqueo automático por vencimiento de término
**Dado** que ha transcurrido el término de 6 meses calendario sin auto de archivo o apertura  
**Cuando** cualquier usuario intenta acceder al expediente  
**Entonces** el sistema muestra el expediente en modo "BLOQUEADO POR VENCIMIENTO"  
**Y** deshabilita todas las acciones de escritura  
**Y** genera un reporte automático a la Oficina de Control Interno Disciplinario  
**Y** muestra la advertencia: "Se ha configurado posible causal de caducidad de la acción disciplinaria. Remítase a oficina jurídica."  

---

## 6. PROTOTIPO / REFERENCIA A PANTALLA

**Prototipo de Interfaz:**  
- Archivo HTML de referencia: `/workspace/Pantallas VEED/15_gestion_indagacion_v1.html`  
- Versión del prototipo: 1.0  
- Fecha de última revisión: 13/05/2026  

**Componentes UX Identificados en el Prototipo:**

| Componente | ID en Prototipo | Descripción | Tokens de Marca PGN |
|------------|-----------------|-------------|---------------------|
| Widget de Término | `widget-term-indagacion` | Semáforo con días calendario restantes, barra de progreso circular | Primary: #063853, Warning: #FFE601, Danger: #E3201B |
| Pestañas de Navegación | `tabs-gestion-indagacion` | 5 pestañas: Término, Pruebas, Persona, Documentos, Actuaciones | Font: Poppins Regular 14px |
| Tabla de Pruebas | `tbl-pruebas-identificacion` | Listado de pruebas con estados, fechas de libramiento y recepción | Font: Poppins Light 12px |
| Card de Persona | `card-persona-averiguacion` | Información de la persona en averiguación sin vinculación formal | Background: #F5F7FA |
| Formulario de Actuaciones | `form-nueva-actuacion` | Campos: Tipo, Descripción, Fecha, Adjuntos | Input Border: #063853 |
| Botón Proyectar Decisión | `btn-proyectar-decision` | Acciones: Archivar o Abrir Investigación | Primary Button: #063853, Hover: #084A6E |
| Alertas Modales | `modal-alerta-vencimiento` | Ventanas emergentes para alertas críticas | Background: #E3201B, Text: #FFFFFF |
| Timeline de Auditoría | `timeline-audit-log` | Historial cronológico de actuaciones con hash de integridad | Font: Poppins Mono 11px |

**Requisitos de Diseño UI:**
- **Fuente Principal:** Poppins (Google Fonts) en pesos Regular (400), Medium (500), SemiBold (600)
- **Paleta de Colores Institucional PGN:**
  - Azul Institucional: #063853 (primario)
  - Amarillo Alerta: #FFE601 (warning)
  - Rojo Crítico: #E3201B (danger/error)
  - Gris Fondo: #F5F7FA (background)
  - Blanco: #FFFFFF (surface)
- **Espaciado:** Sistema de grilla de 8px (8, 16, 24, 32, 48, 64)
- **Bordes:** Radius 4px para botones, 8px para cards
- **Sombras:** Sombra suave (box-shadow: 0 2px 8px rgba(6,56,83,0.1))

---

## 7. STAKEHOLDERS Y VALIDACIÓN REQUERIDA

### Stakeholders Primarios
| Rol | Nombre/Área | Responsabilidad | Nivel de Influencia |
|-----|-------------|-----------------|---------------------|
| Funcionario de Instrucción | Instructores Disciplinarios | Ejecutar indagación previa dentro del término | Alto |
| Jefe de la Unidad Disciplinaria | Coordinadores de Grupo | Supervisar cumplimiento de términos | Alto |
| Sujeto Procesal (en averiguación) | Ciudadanos investigados | Derecho a defensa y notificación | Medio |
| Defensor Público | Oficina de Defensa Disciplinaria | Representación técnica del sujeto | Medio |

### Stakeholders Secundarios
| Rol | Nombre/Área | Responsabilidad | Nivel de Influencia |
|-----|-------------|-----------------|---------------------|
| Oficina Jurídica | Asesores Jurídicos | Validación normativa de autos | Medio |
| Secretaría General | Gestores Documentales | Custodia del expediente electrónico | Bajo |
| Oficina de Control Interno | Auditores Internos | Verificación de legalidad | Alto |
| Área de TI | Desarrolladores y Soporte | Implementación y mantenimiento | Medio |
| Procuraduría Delegada | Entidad de Control | Vigilancia superior | Alto |

### Plan de Validación Requerida
- [ ] **Validación Jurídica:** Revisión y aprobación de la Oficina Jurídica de la entidad sobre el cumplimiento del Art. 208 CGD y ausencia de prórrogas.
- [ ] **Validación Técnica:** Pruebas de integración del motor de cálculo de términos con el calendario oficial colombiano.
- [ ] **Prueba de Usabilidad:** Sesión con 5 instructores reales utilizando el prototipo en entorno controlado.
- [ ] **Auditoría de Seguridad:** Revisión de controles de acceso RBAC/ABAC y cifrado de documentos en reserva.
- [ ] **Prueba de Carga:** Simulación de 100 expedientes concurrentes con alertas de vencimiento.
- [ ] **Aprobación del Comité de Gobierno TI:** Validación arquitectónica antes de pasar a producción.
- [ ] **Socialización con Usuarios:** Capacitación masiva a instructores sobre el nuevo módulo.

---

## 8. MATRIZ DE TRAZABILIDAD CON REFERENCIAS NORMATIVAS

| ID Requisito | Artículo/Norma | Descripción del Requisito Legal | Implementación en Sistema | Estado de Cumplimiento |
|--------------|----------------|--------------------------------|---------------------------|------------------------|
| REQ-HU15-01 | Art. 208 CGD (Ley 1952/2019) | Término perentorio de 6 meses para indagación previa | Widget de término calcula 6 meses calendario desde auto de apertura | ✅ Implementado |
| REQ-HU15-02 | Art. 208 Parágrafo CGD | No procede prórroga del término de indagación previa | Sistema NO incluye botón ni opción de prórroga; cálculo es fijo | ✅ Implementado |
| REQ-HU15-03 | Art. 115 CGD | Reserva de la actuación durante indagación previa | Cifrado AES-256 de documentos; acceso solo a roles autorizados | ✅ Implementado |
| REQ-HU15-04 | Arts. 121-123 CGD | Notificación personal electrónica de autos | Módulo de notificaciones con certificado digital y acuse de recibo | ✅ Implementado |
| REQ-HU15-05 | Art. 214 CGD | Ruptura de unidad procesal al abrir investigación | Cambio automático de estado a "Investigación Disciplinaria" | ✅ Implementado |
| REQ-HU15-06 | Art. 215 CGD | Contenido mínimo del auto de apertura | Plantilla predefinida con campos obligatorios según norma | ✅ Implementado |
| REQ-HU15-07 | Art. 224 CGD | Recurso de apelación contra auto de archivo (solo ante fallo) | Sistema indica que no hay recurso en etapa de indagación | ✅ Implementado |
| REQ-HU15-08 | Ley 2094/2021 Art. 13 | Separación funcional entre instructor y juzgador | Validación ABAC impide mismo usuario en ambas etapas | ✅ Implementado |
| REQ-HU15-09 | Art. 76 CGD | Funciones del instructor disciplinario | Roles RBAC con permisos específicos para instructor | ✅ Implementado |
| REQ-HU15-10 | Decreto 1083/2015 | Gestión documental electrónica | Repositorio SGDE integrado con metadatos normativos | ✅ Implementado |
| REQ-HU15-11 | Sentencia C-161/2022 CC | Exequibilidad de términos perentorios | Alertas automáticas sin posibilidad de extensión | ✅ Implementado |
| REQ-HU15-12 | Circular 003/2020 PG | Lineamientos indagación previa | Flujo de trabajo guiado por pasos de la circular | ✅ Implementado |

---

## 9. REQUISITOS DE SEGURIDAD Y AUDITORÍA

### Controles de Seguridad
1. **Autenticación:** OAuth 2.0 con JWT (JSON Web Tokens) de corta duración (15 minutos) y refresh token rotativo.
2. **Autorización:** RBAC (Role-Based Access Control) + ABAC (Attribute-Based Access Control) para validación de competencia territorial y temporal.
3. **Cifrado en Tránsito:** TLS 1.3 obligatorio para todas las comunicaciones cliente-servidor.
4. **Cifrado en Reposo:** AES-256 para documentos almacenados en la base de datos y sistema de archivos.
5. **Hash de Integridad:** SHA-256 para cada actuación registrada, encadenado en estructura tipo blockchain para inmutabilidad.
6. **Prevención de Inyección:** Uso exclusivo de consultas parametrizadas (Prepared Statements) en todas las interacciones con BD.
7. **Rate Limiting:** Máximo 100 solicitudes por minuto por usuario para prevenir ataques DoS.
8. **Registro de Intentos Fallidos:** Bloqueo temporal de cuenta tras 5 intentos fallidos de acceso consecutivos.

### Requisitos de Auditoría (Audit Log)
- **Registro Obligatorio:** Cada acción (lectura, creación, modificación, eliminación) queda registrada con: usuario, fecha/hora exacta (timestamp UTC), IP de origen, tipo de acción, ID del recurso afectado, hash previo y posterior.
- **Inmutabilidad:** Los registros de auditoría no pueden ser modificados ni eliminados por ningún usuario, incluido el administrador.
- **Retención:** Los logs se conservan por un mínimo de 10 años conforme a normas de archivo y transparencia.
- **Consulta de Logs:** Solo usuarios con rol `auditor_interno` o `control_interno` pueden consultar los logs de auditoría.
- **Alertas de Anomalías:** El sistema detecta patrones sospechosos (ej: múltiples accesos fuera de horario, descargas masivas) y genera alertas automáticas.

---

## 10. PROTOCOLO DE RESPUESTA A INCIDENTES

### Incidente Crítico: Vencimiento de Término No Detectado
**Descripción:** El sistema no generó la alerta de vencimiento y el término expiró sin decisión.  
**Acciones Inmediatas:**
1. Bloquear automáticamente el expediente para nuevas actuaciones.
2. Generar reporte automático a la Oficina de Control Interno Disciplinario y Oficina Jurídica.
3. Notificar al Jefe de la Unidad y al Instructor responsable.
4. Registrar incidente en bitácora de eventos críticos.
5. Iniciar protocolo de análisis de causa raíz (¿falla técnica?, ¿error humano?).

**Responsables:** Líder de Soporte Técnico, Oficina Jurídica, Control Interno.  
**Tiempo de Respuesta:** Máximo 1 hora hábil desde la detección.

### Incidente de Seguridad: Acceso No Autorizado
**Descripción:** Usuario sin rol `instructor` logra acceder al módulo de indagación.  
**Acciones Inmediatas:**
1. Cerrar sesión inmediatamente del usuario infractor.
2. Revocar tokens JWT activos.
3. Investigar vector de ataque (¿credenciales robadas?, ¿vulnerabilidad?).
4. Notificar al área de Seguridad de la Información.
5. Generar informe forense digital.

**Responsables:** CISO (Chief Information Security Officer), Equipo de Seguridad.  
**Tiempo de Respuesta:** Inmediato (< 15 minutos).

---

## 11. GLOSARIO DE TÉRMINOS TÉCNICOS Y LEGALES

| Término | Definición |
|---------|------------|
| **Indagación Previa** | Etapa preliminar del proceso disciplinario destinada a determinar si hay mérito para abrir investigación disciplinaria. Dura máximo 6 meses calendario (Art. 208 CGD). |
| **Término Perentorio** | Plazo fatal que no se suspende, ni interrumpe, ni prorroga. Su vencimiento acarrea caducidad de la acción disciplinaria. |
| **Auto de Archivo** | Decisión que pone fin a la indagación previa al no encontrar mérito para abrir investigación. No es susceptible de recurso. |
| **Auto de Apertura** | Decisión que da inicio a la investigación disciplinaria formal contra una persona. Cambia el estado del expediente. |
| **Reserva de Actuación** | Principio que limita el acceso al expediente durante la indagación previa solo a partes legitimadas (Art. 115 CGD). |
| **RBAC** | Role-Based Access Control: Modelo de control de acceso basado en roles de usuario. |
| **ABAC** | Attribute-Based Access Control: Modelo de control de acceso basado en atributos (rol, unidad, territorio, tiempo). |
| **Audit Trail** | Registro cronológico inmutable de todas las acciones realizadas en el sistema. |
| **JWT** | JSON Web Token: Estándar abierto para transmisión segura de información entre partes. |
| **SHA-256** | Algoritmo criptográfico de hash utilizado para garantizar integridad de datos. |

---

## 12. DEFINICIÓN DE TERMINADO (DoD - Definition of Done)

Para considerar la HU-15 como completamente terminada y lista para despliegue a producción, se deben cumplir **todos** los siguientes criterios:

### Documentación
- [ ] Historia de usuario completa y aprobada por Oficina Jurídica.
- [ ] Diagramas de flujo BPMN del proceso de indagación previa actualizados.
- [ ] Manual de usuario técnico y funcional redactado y revisado.
- [ ] Matriz de trazabilidad normativa firmada por el líder jurídico.

### Desarrollo
- [ ] Código fuente implementado siguiendo estándares de codificación segura (OWASP Top 10).
- [ ] Widget de término calculando correctamente días calendario sin prórrogas.
- [ ] Las 5 pestañas funcionales integradas con backend.
- [ ] Plantillas de autos (archivo/apertura) generadas dinámicamente.
- [ ] Notificaciones electrónicas configuradas y probadas.

### Pruebas
- [ ] Pruebas unitarias con cobertura mínima del 85%.
- [ ] Pruebas de integración entre módulos (expediente, notificaciones, auditoría).
- [ ] Pruebas de aceptación con usuarios reales (instructores).
- [ ] Pruebas de seguridad (pentesting básico) sin hallazgos críticos.
- [ ] Pruebas de carga con 100 expedientes simultáneos.

### Despliegue
- [ ] Entrenamiento realizado a todos los instructores de la entidad.
- [ ] Plan de rollback documentado y probado.
- [ ] Monitoreo configurado en herramientas de observabilidad (logs, métricas, alertas).
- [ ] Aprobación formal del Comité de Gobierno TI para paso a producción.

### Legal
- [ ] Concepto jurídico favorable de la Oficina Jurídica sobre cumplimiento normativo.
- [ ] Validación de la Procuraduría Delegada (si aplica).
- [ ] Registro en inventario de sistemas de información ante la entidad.

---

## 13. HISTORIAS HIJAS DERIVADAS DE HU-15

La HU-15 se descompone en las siguientes historias hijas para facilitar el desarrollo incremental:

| ID Hija | Nombre | Prioridad | Dependencia |
|---------|--------|-----------|-------------|
| HU-15-01 | Consultar y Validar Término de Indagación Previa | Alta | Ninguna |
| HU-15-02 | Gestionar Pruebas de Identificación | Alta | HU-15-01 |
| HU-15-03 | Visualizar Persona en Averiguación | Media | HU-15-01 |
| HU-15-04 | Gestionar Documentos con Reserva | Alta | HU-15-01 |
| HU-15-05 | Registrar Actuaciones Procesales | Alta | HU-15-02, HU-15-04 |
| HU-15-06 | Consultar Historial Auditado | Media | HU-15-05 |
| HU-15-07 | Proyectar Decisión Final (Archivo/Apertura) | Crítica | HU-15-01, HU-15-02, HU-15-05 |

---

**Fin del Documento HU-15**

*Documento generado conforme al estándar PGN para Historias de Usuario. Última actualización: 13/05/2026.*
