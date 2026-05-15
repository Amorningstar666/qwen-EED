# 📄 HISTORIAS DE USUARIO — EED PROCURADURÍA
## Módulo: Incorporación Manual de Expedientes
**Pantalla Asociada:** `11_incorporacion_manual.html`  
**Fecha:** 15-05-2025 | **Creado por:** Consultora EED | **Validado por:** [Pendiente]  
**Macroproceso:** Proceso Disciplinario | **Proceso:** Gestión de Investigación Disciplinaria  
**Actividad:** Acumulación Procesal por Incorporación de Expedientes  
**Clasificación:** Funcional | **Valor de negocio:** Garantizar unidad de proceso, evitar fallos contradictorios y centralizar prueba  

---

# HU-11-01: Búsqueda y Selección Múltiple de Expedientes Activos para Incorporación

## 👥 DESCRIPCIÓN DE LA HISTORIA DE USUARIO
**¿Quién?** Instructor Disciplinario encargado de una investigación en curso (Expediente Principal) que ha identificado la existencia de otras investigaciones abiertas relacionadas.

**¿Qué?** Necesito buscar, filtrar y seleccionar múltiples expedientes que se encuentren en estado **ACTIVO** dentro del sistema, mediante un modal especializado de incorporación (Paso 1), validando que cumplan con los requisitos de elegibilidad.

**¿Para qué?** Para iniciar el proceso técnico de acumulación de expedientes, asegurando que solo se vinculen procesos vigentes que puedan ser legalmente incorporados al expediente principal, garantizando el principio de unidad de proceso (Art. 188 CGD) y evitando decisiones contradictorias.

## 🔗 DEPENDENCIA(S) Y/O PRECONDICIÓN(ES)
1. El usuario debe tener rol de **Instructor Disciplinario** o **Secretario de Instrucción** con permisos de escritura sobre el expediente principal.
2. Debe existir al menos un expediente en estado **ACTIVO** asignado al despacho del usuario o con permiso de lectura por jerarquía.
3. El módulo de Gestión de Investigaciones (CRUD de Expedientes) debe estar operativo.
4. **Art. 188 Ley 1952/2019 (CGD):** Faculta al instructor para reunir elementos necesarios para la investigación, incluyendo acumulación por conexidad.

## 🚫 RESTRICCIONES
1. **RN-11-01 (Elegibilidad de Estado):** Únicamente los expedientes con estado **ACTIVO** pueden ser seleccionados. Los estados **CERRADO**, **ARCHIVADO** o **INCORPORADO** bloquean la selección visualmente.
2. **RN-11-02 (Cantidad Mínima):** Se deben seleccionar como mínimo **2 expedientes** para habilitar el botón "Siguiente" (uno será principal, los demás incorporados).
3. **RN-11-03 (Separación RBAC):** El sistema valida que el usuario tenga permiso de acceso a cada expediente seleccionado según su asignación o jerarquía.
4. **RN-11-04 (Exclusión de Trámites Pendientes):** No se pueden seleccionar expedientes que tengan una solicitud de incorporación pendiente de aprobación por otro usuario.
5. **Accesibilidad WCAG 2.1 AA:** Los checkboxes de selección deben ser accesibles por teclado y lectores de pantalla.

## 📌 SUPUESTOS
1. La búsqueda se realiza contra un índice actualizado en tiempo real de expedientes activos.
2. El sistema aplica *debounce* de 500ms en el input de búsqueda para optimizar llamadas al API.
3. Los datos mock de demostración serán reemplazados por el endpoint real: `GET /api/v1/expedientes/buscar?filtro={texto}&estado=ACTIVO`.

## ✅ CRITERIO(S) DE ACEPTACIÓN (GHERKIN)

### Escenario 1: Búsqueda exitosa por número de expediente (IUS+IUC)
**Dado que** el Instructor se encuentra en el Paso 1 del modal de Incorporación Manual  
**Cuando** ingresa un número de expediente válido (ej. `IUS-2026-00521-IUC-110001`) en el campo de búsqueda y presiona "Buscar"  
**Entonces** el sistema muestra el expediente en la tabla de resultados indicando claramente su estado **ACTIVO** con badge verde (`#28a745` o `--verde`) y habilita el checkbox para su selección.

### Escenario 2: Búsqueda por asunto o palabras clave
**Dado que** el Instructor desea encontrar expedientes relacionados temáticamente  
**Cuando** ingresa palabras clave del asunto (ej. "irregularidad contratación", "conflicto intereses") y ejecuta la búsqueda  
**Entonces** el sistema lista todos los expedientes **ACTIVOS** que contienen esas palabras en su descripción o carátula, ordenados por fecha de radicación descendente.

### Escenario 3: Filtrado automático de estados no elegibles
**Dado que** solo los expedientes activos pueden ser incorporados  
**Cuando** se realiza una búsqueda general  
**Entonces** el sistema **oculta o deshabilita** visualmente los expedientes con estado **CERRADO**, **ARCHIVADO** o **INCORPORADO**, mostrando tooltip: "Expediente no elegible para incorporación".

### Escenario 4: Selección múltiple válida
**Dado que** la incorporación requiere al menos dos expedientes (uno principal + uno incorporado)  
**Cuando** el Instructor marca los checkboxes de dos o más expedientes **ACTIVOS**  
**Entonces** el botón "Siguiente" cambia a estado habilitado (color primario PGN `#063853`) permitiendo avanzar al Paso 2.

### Escenario 5: Validación de selección insuficiente
**Dado que** no se puede incorporar un expediente consigo mismo o sin origen  
**Cuando** el Instructor selecciona solo un expediente  
**Entonces** el botón "Siguiente" permanece deshabilitado (gris `#949494`) y muestra mensaje de ayuda: "Seleccione al menos 2 expedientes para continuar".

### Escenario 6: Visualización de detalles críticos
**Dado que** el Instructor debe verificar la identidad del expediente antes de seleccionar  
**Cuando** visualiza la fila de un expediente en la tabla  
**Entonces** puede ver claramente: Número de Radicado (IUS+IUC), Disciplinado, Hechos resumidos, Fecha, Estado actual (badge verde ACTIVO) y cantidad de documentos asociados.

### Escenario 7: Manejo de sin resultados
**Dado que** la búsqueda puede no coincidir con ningún expediente activo  
**Cuando** el Instructor busca un término que no existe o solo coincide con expedientes **CERRADOS/ARCHIVADOS**  
**Entonces** el sistema muestra toast de notificación: "No se encontraron expedientes activos que coincidan con su búsqueda".

### Escenario 8: Deselección de expediente
**Dado que** el Instructor puede cambiar de opinión antes de avanzar  
**Cuando** hace clic en un checkbox ya seleccionado  
**Entonces** el expediente se remueve de la lista de seleccionados, el contador se actualiza y el botón "Siguiente" se deshabilita si quedan menos de 2 expedientes.

## 🖼️ PROTOTIPO / ANEXOS
- **Prototipo:** `Pantallas VEED/11_incorporacion_manual.html` (Paso 1: Líneas 893-933)
- **Componentes UI:** Tabla `.results-table`, badges `.estado-chip.activo`, botones `.select-row-btn`
- **Tokens PGN:** Verde institucional `--verde: #33FFCC` para estado ACTIVO, Azul `--azul: #063853` para acciones principales
- **Stakeholders:** Instructor Disciplinario | Secretario de Instrucción | Juez de Primera Instancia

---

# HU-11-02: Selección del Expediente Principal para Incorporación

## 👥 DESCRIPCIÓN DE LA HISTORIA DE USUARIO
**¿Quién?** Instructor Disciplinario que ha seleccionado múltiples expedientes activos y debe definir cuál permanecerá como expediente principal.

**¿Qué?** Necesito seleccionar uno de los expedientes previamente marcados como **PRINCIPAL** (el que mantendrá su numeración original y estado activo), mediante cards interactivas en el Paso 2 del modal.

**¿Para qué?** Para establecer inequívocamente el expediente destino de la incorporación, garantizando que los demás expedientes se cerrarán definitivamente y todos sus documentos pasarán a formar parte integral del principal, conforme al principio de economía procesal.

## 🔗 DEPENDENCIA(S) Y/O PRECONDICIÓN(ES)
1. **Precondición:** El usuario debe haber completado exitosamente el Paso 1 (seleccionado ≥2 expedientes activos).
2. El sistema debe mantener en memoria temporal la lista de expedientes seleccionados en el Paso 1.
3. **Art. 188 CGD:** La acumulación procesal requiere definir un expediente principal que centralice la actuación.
4. **Art. 14 CGD (Motivación):** La decisión de qué expediente será principal debe estar motivada en el acto administrativo.

## 🚫 RESTRICCIONES
1. **RN-11-05 (Unicidad del Principal):** Solo se puede seleccionar **un único expediente** como principal. Al seleccionar uno nuevo, el anterior se deselecciona automáticamente.
2. **RN-11-06 (Irreversibilidad Parcial):** Una vez confirmada la incorporación en el Paso 4, no se puede modificar el expediente principal seleccionado.
3. **RN-11-07 (Advertencia Obligatoria):** El sistema debe mostrar el banner de advertencia (`.warning-banner`) explicando las consecuencias de la selección antes de permitir avanzar.
4. **UI/UX:** Las cards deben usar border azul (`--azul: #063853`) y background `#EBF4FA` cuando están seleccionadas.

## 📌 SUPUESTOS
1. El Instructor seleccionará como principal el expediente con mayor antigüedad, mayor cantidad de prueba o mayor gravedad de los hechos.
2. El sistema podría sugerir automáticamente el expediente más antiguo como principal (feature futura de procuradurIA).

## ✅ CRITERIO(S) DE ACEPTACIÓN (GHERKIN)

### Escenario 1: Selección válida de expediente principal
**Dado que** el usuario ha seleccionado 3 expedientes en el Paso 1  
**Cuando** ingresa al Paso 2 y hace clic en una de las cards de expediente  
**Entonces** la card seleccionada cambia a estado activo (border azul `#063853`, background `#EBF4FA`, radio button relleno) y el botón "Siguiente" se habilita.

### Escenario 2: Cambio de selección del principal
**Dado que** el usuario ya había seleccionado un expediente como principal  
**Cuando** hace clic en una card diferente  
**Entonces** la selección anterior se remueve (vuelve a estado normal) y la nueva card se marca como principal, actualizando el valor en memoria.

### Escenario 3: Visualización de advertencia legal
**Dado que** la incorporación tiene consecuencias procesales irreversibles  
**Cuando** el usuario ingresa al Paso 2  
**Entonces** el sistema muestra un banner amarillo (`.warning-banner`) con icono `alert-triangle` y lista de 4 puntos explicando: (1) numeración original se mantiene, (2) expedientes incorporados se cierran definitivamente, (3) documentos pasan al principal, (4) vinculación sin cambio de numeración.

### Escenario 4: Validación de selección obligatoria
**Dado que** es obligatorio definir un expediente principal  
**Cuando** el usuario intenta avanzar sin seleccionar ninguna card  
**Entonces** el botón "Siguiente" permanece deshabilitado y al hacer hover muestra tooltip: "Debe seleccionar el expediente PRINCIPAL para continuar".

### Escenario 5: Información completa en cards
**Dado que** el usuario necesita contexto para decidir  
**Cuando** visualiza las cards de expedientes  
**Entonces** cada card muestra: Radicado (IUS+IUC), Disciplinado, Cantidad de documentos, Fecha de radicación y un radio button visual para selección.

## 🖼️ PROTOTIPO / ANEXOS
- **Prototipo:** `Pantallas VEED/11_incorporacion_manual.html` (Paso 2: Líneas 934-961)
- **Componentes UI:** `.principal-selection`, `.principal-cards`, `.principal-card`, `.warning-banner`
- **Tokens PGN:** Amarillo `--amarillo: #FFE601` para advertencias, Azul `--azul: #063853` para selección activa
- **Iconografía:** Lucide `target`, `alert-triangle`

---

# HU-11-03: Registro de Causales y Justificación de Incorporación

## 👥 DESCRIPCIÓN DE LA HISTORIA DE USUARIO
**¿Quién?** Instructor Disciplinario que ha definido los expedientes a incorporar y debe fundamentar jurídicamente la decisión.

**¿Qué?** Necesito seleccionar las causales legales que justifican la incorporación (mismos hechos, mismo sujeto, conexidad u otro) y redactar una justificación detallada en el Paso 3 del modal.

**¿Para qué?** Para cumplir con el requisito de motivación del acto administrativo de incorporación (Art. 14 CGD), dejando trazabilidad de las razones jurídicas que permiten la acumulación procesal y facilitando la revisión por parte del Juez o Superior Jerárquico.

## 🔗 DEPENDENCIA(S) Y/O PRECONDICIÓN(ES)
1. **Precondición:** El usuario debe haber completado exitosamente el Paso 2 (seleccionado expediente principal).
2. **Art. 14 Ley 1952/2019 (CGD):** Toda actuación administrativa debe estar motivada, incluyendo la incorporación de expedientes.
3. **Art. 188 CGD:** Establece las causales de acumulación procesal (conexidad por hechos, sujetos o naturaleza de la falta).
4. El sistema debe calcular el total de documentos que se transferirán para mostrar vista previa.

## 🚫 RESTRICCIONES
1. **RN-11-08 (Causal Obligatoria):** Al menos **una causal** debe ser seleccionada. Si se marca "Otro", el campo de especificación es obligatorio.
2. **RN-11-09 (Justificación Mínima):** La justificación debe tener **mínimo 50 caracteres** y será incluida textualmente en el acto administrativo.
3. **RN-11-10 (Vista Previa de Documentos):** El sistema debe listar los documentos que se transferirán, excluyendo los del expediente principal.
4. **Accesibilidad:** Los checkboxes de causales deben ser operables por teclado y anunciar cambios a lectores de pantalla.

## 📌 SUPUESTOS
1. Las causales predefinidas cubren el 90% de los casos de incorporación en la PGN.
2. La opción "Otro" permite flexibilidad para causales atípicas no contempladas explícitamente.
3. El campo de justificación podría integrar en el futuro asistencia de procuradurIA para redacción automática.

## ✅ CRITERIO(S) DE ACEPTACIÓN (GHERKIN)

### Escenario 1: Selección de causal predefinida
**Dado que** el usuario necesita fundamentar la incorporación  
**Cuando** hace clic en una opción de causal (ej. "Mismos hechos")  
**Entonces** la opción se marca visualmente (border azul `#063853`, background `#EBF4FA`, check visible) y el checkbox interno se activa.

### Escenario 2: Selección múltiple de causales
**Dado que** pueden concurrir varias causales simultáneamente  
**Cuando** el usuario selecciona "Mismos hechos" y "Mismo sujeto procesal"  
**Entonces** ambas opciones permanecen marcadas y el sistema las registrará como causales concurrentes en el acto administrativo.

### Escenario 3: Activación de campo "Otro"
**Dado que** ninguna causal predefinida aplica al caso  
**Cuando** el usuario selecciona la opción "Otro"  
**Entonces** el sistema despliega un campo de texto adicional (`textarea#otraCausal`) marcado como obligatorio con asterisco rojo.

### Escenario 4: Validación de justificación insuficiente
**Dado que** la justificación debe estar debidamente motivada  
**Cuando** el usuario ingresa menos de 50 caracteres en el campo de justificación e intenta avanzar  
**Entonces** el sistema muestra toast de error: "La justificación debe tener al menos 50 caracteres" y el botón "Siguiente" permanece deshabilitado.

### Escenario 5: Vista previa de documentos a transferir
**Dado que** el usuario debe conocer el alcance de la incorporación  
**Cuando** ingresa al Paso 3  
**Entonces** el sistema muestra una sección (`.docs-preview`) listando los documentos de los expedientes incorporados (excluyendo el principal), con iconos diferenciados por tipo (PDF/Word) y flechas indicando origen→destino.

### Escenario 6: Validación de causal "Otro" sin especificar
**Dado que** la opción "Otro" requiere descripción explícita  
**Cuando** el usuario marca "Otro" pero deja vacío el campo de especificación e intenta avanzar  
**Entonces** el sistema muestra toast: "Debe especificar la causal otro" y no permite continuar.

### Escenario 7: Deselección de causal
**Dado que** el usuario puede rectificar su selección  
**Cuando** hace clic en una causal ya marcada  
**Entonces** la opción se desmarca visualmente, el checkbox interno se desactiva y el sistema la remueve de la lista de causales seleccionadas.

## 🖼️ PROTOTIPO / ANEXOS
- **Prototipo:** `Pantallas VEED/11_incorporacion_manual.html` (Paso 3: Líneas 962-1035)
- **Componentes UI:** `.causales-section`, `.causales-grid`, `.causal-option`, `.docs-preview`, `.form-textarea`
- **Tokens PGN:** Rojo `--rojo: #E3201B` para campos obligatorios, Azul `--azul: #063853` para selección
- **Iconografía:** Lucide `check`, `file-text`, `file`, `arrow-right`

---

# HU-11-04: Confirmación Irreversible de Incorporación de Expedientes

## 👥 DESCRIPCIÓN DE LA HISTORIA DE USUARIO
**¿Quién?** Instructor Disciplinario que ha completado los pasos previos y está listo para ejecutar la incorporación.

**¿Qué?** Necesito revisar un resumen consolidado de la operación (expediente principal, expedientes a incorporar, causales, total de documentos) y confirmar explícitamente mediante checkbox de aceptación antes de ejecutar la acción irreversible.

**¿Para qué?** Para garantizar que el usuario comprende plenamente las consecuencias procesales de la incorporación (cierre definitivo de expedientes incorporados) y dejar constancia auditada de su consentimiento informado, conforme a los principios de seguridad jurídica y buena fe.

## 🔗 DEPENDENCIA(S) Y/O PRECONDICIÓN(ES)
1. **Precondición:** El usuario debe haber completado exitosamente los Pasos 1, 2 y 3.
2. **Art. 115 CGD (Reserva de Actuaciones):** La incorporación debe registrarse en la trazabilidad del expediente con fecha, hora y usuario responsable.
3. **Art. 14 CGD:** El acto administrativo de incorporación debe generarse automáticamente tras la confirmación.
4. El sistema de auditoría (audit trail) debe estar operativo para registrar la acción.

## 🚫 RESTRICCIONES
1. **RN-11-11 (Irreversibilidad):** Una vez confirmada la incorporación, **NO se puede deshacer**. Los expedientes incorporados quedarán cerrados permanentemente.
2. **RN-11-12 (Checkbox Obligatorio):** El botón "Confirmar incorporación" permanece deshabilitado hasta que el usuario marque explícitamente el checkbox de aceptación.
3. **RN-11-13 (Banner de Advertencia Reforzado):** El Paso 4 debe mostrar un banner rojo (`.warning-banner` con border-color `--rojo`) enfatizando la irreversibilidad.
4. **RN-11-14 (Generación de Acto Administrativo):** Tras la confirmación, el sistema debe generar automáticamente el acto administrativo de incorporación con firma digital del Instructor.

## 📌 SUPUESTOS
1. El acto administrativo generado incluirá: número de resolución, expediente principal, expedientes incorporados, causales, justificación y fecha de ejecución.
2. La incorporación se ejecutará en una transacción atómica: si falla algún paso, se revierte toda la operación.
3. El sistema notificará electrónicamente a los sujetos procesales de los expedientes incorporados sobre la decisión.

## ✅ CRITERIO(S) DE ACEPTACIÓN (GHERKIN)

### Escenario 1: Visualización de resumen completo
**Dado que** el usuario ingresa al Paso 4  
**Cuando** accede a la sección de resumen  
**Entonces** el sistema muestra una caja (`.summary-box`) con 4 filas: Expediente principal, Expedientes a incorporar, Causales seleccionadas y Total de documentos a transferir, con datos reales de los pasos anteriores.

### Escenario 2: Advertencia de irreversibilidad reforzada
**Dado que** la acción tiene consecuencias permanentes  
**Cuando** el usuario visualiza el Paso 4  
**Entonces** ve un banner rojo (background `#FEF2F2`, border `--rojo: #E3201B`) con icono `alert-octagon` y lista de 4 puntos: (1) NO se puede deshacer, (2) expedientes se cierran permanentemente, (3) se genera acto administrativo, (4) se registra en trazabilidad.

### Escenario 3: Validación de checkbox de aceptación
**Dado que** el usuario debe aceptar explícitamente las consecuencias  
**Cuando** intenta hacer clic en "Confirmar incorporación" sin marcar el checkbox  
**Entonces** el botón permanece deshabilitado (gris) y no responde al clic.

### Escenario 4: Habilitación de confirmación tras aceptación
**Dado que** el usuario ha leído y comprendido las consecuencias  
**Cuando** marca el checkbox "He leído y comprendo..."  
**Entonces** el botón "Confirmar incorporación" cambia a estado habilitado (verde `--verde: #33FFCC`) permitiendo la ejecución.

### Escenario 5: Ejecución exitosa de incorporación
**Dado que** el usuario ha marcado el checkbox y presiona "Confirmar incorporación"  
**Cuando** el sistema procesa la solicitud  
**Entonces** (1) muestra toast de éxito "Incorporación realizada exitosamente", (2) genera acto administrativo, (3) registra en audit trail, (4) cierra el modal y (5) recarga/redirige a la vista de detalle del expediente principal.

### Escenario 6: Cancelación del proceso
**Dado que** el usuario decide no continuar con la incorporación  
**Cuando** hace clic en "Cancelar" o en la "X" del modal en cualquier paso  
**Entonces** el sistema cierra el modal sin guardar cambios, descarta toda la información ingresada y retorna a la pantalla de origen (lista de expedientes o evaluación).

### Escenario 7: Navegación atrás desde confirmación
**Dado que** el usuario quiere modificar algo antes de confirmar  
**Cuando** estando en Paso 4 hace clic en "Atrás"  
**Entonces** el sistema retorna al Paso 3 preservando los datos ingresados (causales, justificación) para permitir modificaciones.

## 🖼️ PROTOTIPO / ANEXOS
- **Prototipo:** `Pantallas VEED/11_incorporacion_manual.html` (Paso 4: Líneas 1036-1078, Footer: Líneas 1080-1095)
- **Componentes UI:** `.warning-banner` (rojo), `.summary-box`, `.summary-row`, checkbox de aceptación, botón `.btn-success`
- **Tokens PGN:** Rojo `--rojo: #E3201B` para advertencias críticas, Verde `--verde: #33FFCC` para confirmación exitosa
- **Iconografía:** Lucide `alert-octagon`, `check`, `arrow-left`
- **Audit Trail:** Registro obligatorio con timestamp, usuario, IP, expediente principal, expedientes incorporados, causales y justificación

---

# HU-11-05: Asistencia de procuradurIA en Incorporación de Expedientes (Feature IA)

## 👥 DESCRIPCIÓN DE LA HISTORIA DE USUARIO
**¿Quién?** Instructor Disciplinario que está realizando una incorporación de expedientes y requiere asistencia inteligente.

**¿Qué?** Necesito acceder a un asistente de IA (procuradurIA) mediante botón flotante que me sugiera causales aplicables, expedientes relacionados potencialmente omitidos y ayude a redactar la justificación de la incorporación.

**¿Para qué?** Para mejorar la calidad y consistencia de las incorporaciones, reduciendo errores humanos, asegurando que no se omitan expedientes conexos relevantes y acelerando la redacción de actos administrativos, siempre bajo supervisión y responsabilidad del Instructor (la IA nunca decide).

## 🔗 DEPENDENCIA(S) Y/O PRECONDICIÓN(ES)
1. **Precondición:** El módulo de procuradurIA debe estar integrado y operativo con modelos de lenguaje entrenados en normativa disciplinaria colombiana.
2. **Art. 115 CGD (Trazabilidad):** Cada sugerencia de procuradurIA debe registrarse en audit log con indicación clara de que fue una recomendación de IA aceptada/rechazada por el usuario.
3. **Ética IA:** Principio de "Humano en el Loop": la IA solo sugiere, el Instructor decide y asume responsabilidad jurídica.
4. **Ley 1581/2012 (Habeas Data):** La IA no debe exponer datos sensibles de disciplinados en sus respuestas visibles.

## 🚫 RESTRICCIONES
1. **RN-11-15 (No Decisión Autónoma):** procuradurIA **NUNCA** puede ejecutar actos procesales ni tomar decisiones automáticas. Solo sugiere.
2. **RN-11-16 (Trazabilidad Auditada):** Cada interacción con procuradurIA queda registrada: timestamp, usuario, pregunta, sugerencia de IA, acción del usuario (aceptar/rechazar).
3. **RN-11-17 (Transparencia):** El tooltip del botón debe indicar claramente "Sugerencia asistida por IA".
4. **Seguridad:** Las respuestas de IA deben sanitizarse para prevenir inyección de código o contenido malicioso.

## 📌 SUPUESTOS
1. procuradurIA tiene acceso indexado a todos los expedientes activos del usuario para identificar conexidades potenciales.
2. El modelo de IA fue entrenado con jurisprudencia disciplinaria de la PGN y conoce las causales típicas de incorporación.
3. En fase inicial, procuradurIA operará en modo "solo lectura" sin capacidad de escritura en expedientes.

## ✅ CRITERIO(S) DE ACEPTACIÓN (GHERKIN)

### Escenario 1: Activación del botón flotante procuradurIA
**Dado que** el usuario se encuentra en el modal de incorporación  
**Cuando** visualiza la esquina inferior derecha de la pantalla  
**Entonces** ve un botón circular amarillo (`--amarillo: #FFE601`, 56x56px) con icono de asistente y tooltip "Sugerencia asistida por IA" al hacer hover.

### Escenario 2: Solicitud de sugerencia de causales
**Dado que** el usuario duda sobre qué causales seleccionar  
**Cuando** hace clic en el botón procuradurIA y selecciona "Verificar causales aplicables"  
**Entonces** la IA analiza los expedientes seleccionados y responde: "Basado en los hechos y sujetos comunes, las causales recomendadas son: Mismos hechos, Mismo sujeto procesal. ¿Desea aplicar estas sugerencias?" con botones "Aplicar" o "Rechazar".

### Escenario 3: Sugerencia de expedientes omitidos
**Dado que** podrían existir expedientes relacionados no identificados por el usuario  
**Cuando** el usuario solicita "Sugerir expedientes relacionados"  
**Entonces** la IA busca en todos los expedientes activos del usuario y responde: "Se identificaron 2 expedientes adicionales con posible conexidad: [IUS-XXX, IUS-YYY]. ¿Desea agregarlos a la selección?" con opción de previsualizar.

### Escenario 4: Redacción automática de justificación
**Dado que** el usuario requiere apoyo para redactar la justificación  
**Cuando** solicita "Redactar justificación automática"  
**Entonces** la IA genera un párrafo fundamentado citando Art. 188 CGD, describiendo los hechos comunes y la conveniencia de unidad de proceso, que el usuario puede editar antes de aceptar.

### Escenario 5: Registro de trazabilidad de IA
**Dado que** cada interacción con IA debe quedar auditada  
**Cuando** el usuario acepta una sugerencia de procuradurIA  
**Entonces** el sistema registra en audit log: `{timestamp, usuario, modulo: "Incorporación", tipo: "Sugerencia IA", sugerencia: "[texto]", accion: "ACEPTADA", impacto: "[campos modificados]"}`.

### Escenario 6: Rechazo de sugerencia de IA
**Dado que** el usuario puede discrepar con la IA  
**Cuando** rechaza una sugerencia de procuradurIA  
**Entonces** el sistema registra el rechazo en audit log y no modifica ningún campo, permitiendo al usuario continuar manualmente.

## 🖼️ PROTOTIPO / ANEXOS
- **Prototipo:** `Pantallas VEED/11_incorporacion_manual.html` (Botón flotante: Líneas 146-191, Inicialización: Líneas 1443-1467)
- **Componentes UI:** `.procuraduria-trigger`, `.procuraduria-tooltip`
- **Tokens PGN:** Amarillo `--amarillo: #FFE601` para el botón, Azul `--azul: #063853` para tooltip
- **Iconografía:** Lucide custom (ícono de asistente IA con nodos verticales)
- **Documentación Ética:** Ver `claude/agents/ia_ethics_specialist.md` para principios de trazabilidad

---

## 📊 RESUMEN DE HISTORIAS GENERADAS

| ID HU | Título | Prioridad | Estado | Complejidad |
| :--- | :--- | :--- | :--- | :--- |
| **HU-11-01** | Búsqueda y Selección Múltiple de Expedientes Activos | ALTA | Pendiente | Media |
| **HU-11-02** | Selección del Expediente Principal | ALTA | Pendiente | Baja |
| **HU-11-03** | Registro de Causales y Justificación | ALTA | Pendiente | Media |
| **HU-11-04** | Confirmación Irreversible de Incorporación | CRÍTICA | Pendiente | Alta |
| **HU-11-05** | Asistencia de procuradurIA en Incorporación | MEDIA | Pendiente | Alta (IA) |

**Total Historias:** 5  
**Puntos de Historia Estimados:** 34 (según escala Fibonacci: 8+5+8+13+13)  
**Dependencias Cruzadas:** HU-11-01 → HU-11-02 → HU-11-03 → HU-11-04 (flujo secuencial), HU-11-05 (transversal)

---

## 🔍 VALIDACIÓN FINAL

❓ **Preguntas de Validación:**
1. ¿Las 5 HUs cubren completamente los 4 pasos del modal más el feature de IA?
2. ¿Los criterios Gherkin incluyen flujos felices, alternos y de error para cada HU?
3. ¿Las citas normativas (Art. 14, 115, 188 CGD) son correctas y suficientes?
4. ¿Las reglas de negocio reflejan adecuadamente las restricciones de la pantalla prototipo?

**✅ Próximo Paso Esperado:** 
Una vez validadas estas HUs, se recomienda:
- Pasar a revisión del área jurídica de la PGN para validar citas normativas
- Priorizar HU-11-01 a HU-11-04 para MVP (HU-11-05 puede ser fase 2)
- Generar casos de prueba QA basados en los escenarios Gherkin

---

**Fin del Documento de Historias de Usuario - Módulo Incorporación Manual**
