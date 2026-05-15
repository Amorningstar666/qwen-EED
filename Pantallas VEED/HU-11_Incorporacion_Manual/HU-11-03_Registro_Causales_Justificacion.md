# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por |
|-------|-------|------------|--------------|
| 15/05/2026 | HU-11-03 | Analista de Negocio | Líder Técnico |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica | P17-Apoyo a la Investigación | A41-Incorporación Manual de Expedientes | Funcionalidad Específica | Garantiza que toda incorporación de expedientes esté debidamente motivada jurídicamente mediante la selección de causales legales previstas en el CGD y una justificación escrita que permita el control posterior de legalidad del acto |

### Descripción

**¿Quién?** El Funcionario de Instrucción (rol: instructor) o el Procurador Delegado (rol: juez) que ha completado la selección de expedientes y la definición del expediente principal, y ahora debe fundamentar jurídicamente la decisión de incorporar.

**¿Qué?** Selecciona una o más causales legales de incorporación de un listado predefinido basado en el artículo 188 de la Ley 1952 de 2019, y redacta una justificación detallada que explique los hechos y fundamentos de derecho que motivan la acumulación procesal, utilizando un formulario con validaciones de longitud y obligatoriedad.

**¿Para qué?** Para cumplir con el principio de motivación de los actos administrativos establecido en el artículo 3 de la Ley 1437 de 2011 (Código de Procedimiento Administrativo), asegurando que la decisión de incorporar expedientes tenga sustento jurídico claro y explícito, lo cual es esencial para garantizar el debido proceso, permitir el control de legalidad y evitar nulidades por falta de fundamentación.

**Referencias Normativas:**
- Ley 1952 de 2019 (Código General Disciplinario), Artículo 188: Acumulación de procesos (causales taxativas).
- Ley 1437 de 2011 (Código de Procedimiento Administrativo), Artículo 3: Principio de motivación de actos administrativos.
- Ley 1952 de 2019, Artículo 14: Principios del procedimiento disciplinario (debido proceso).
- Ley 2094 de 2021, Artículo 1: Principios rectores de la función disciplinaria.
- Jurisprudencia del Consejo de Estado sobre motivación de actos administrativos de acumulación procesal.
- Sentencia C-836 de 2001 de la Corte Constitucional: Derecho al debido proceso en materia disciplinaria.

## Dependencias y Precondiciones

1. El usuario debe haber completado exitosamente el Paso 2 (Selección del Expediente Principal) con un expediente principal definido y al menos dos expedientes seleccionados en total.
2. El sistema debe tener cargadas en memoria las causales legales de incorporación disponibles según el artículo 188 del CGD, presentadas en lenguaje claro y comprensible para el usuario.
3. El módulo de shell corporativo (HU-02) debe mantener la sesión activa del usuario con validación continua de permisos RBAC.
4. Debe existir un componente de validación de texto en tiempo real que verifique longitud mínima (50 caracteres) y máxima (2000 caracteres) de la justificación.
5. El sistema debe permitir seleccionar múltiples causales simultáneamente mediante checkboxes, ya que una incorporación puede estar motivada por más de una causal legal.
6. La interfaz debe mantener el indicador de pasos actualizado mostrando el Paso 3 como activo y los Pasos 1 y 2 como completados.
7. Debe existir trazabilidad completa de las causales seleccionadas y la justificación redactada, con registro de fecha, hora e identificación del funcionario.
8. El sistema debe ofrecer asistencia contextual mediante procuradurIA para ayudar al funcionario a redactar la justificación cuando seleccione la causal "Otro".

## Restricciones

1. La selección de al menos una causal es obligatoria; no se puede avanzar al siguiente paso sin haber marcado mínimo un checkbox de causal.
2. La justificación escrita es obligatoria cuando se selecciona la causal "Otro", siendo opcional pero recomendada para las demás causales predefinidas.
3. La justificación debe tener una longitud mínima de 50 caracteres y máxima de 2000 caracteres; el sistema debe validar estos límites en tiempo real y mostrar contadores.
4. No se permiten justificacions genéricas o estandarizadas como "por conveniencia" o "para agilizar el trámite"; el sistema debe detectar patrones de texto repetitivo y advertir al usuario.
5. Las causales disponibles son taxativas y no modificables por el usuario: "Mismos hechos", "Mismo sujeto procesal", "Conexidad", "Otro". Cualquier otra causal debe ser justificada exhaustivamente.
6. El campo de justificación debe soportar formato de texto plano únicamente; no se permite HTML, markdown ni formatos ricos para evitar vulnerabilidades de inyección XSS.
7. El sistema debe realizar un escaneo básico de la justificación buscando palabras clave relacionadas con cada causal seleccionada para validar coherencia semántica.
8. Si el usuario selecciona la causal "Mismos hechos" pero la justificación no menciona términos relacionados con "hechos", "conductas" o "acciones", el sistema debe mostrar una advertencia de posible inconsistencia.
9. La interfaz debe cumplir con los estándares de accesibilidad WCAG 2.1 nivel AA, utilizando tokens de diseño PGN.
10. El tiempo máximo de permanencia en este paso es de 30 minutos; superado este tiempo sin guardar avances, la sesión expira.

## Reglas de Negocio

| ID Regla | Descripción | Fundamento Legal | Prioridad |
|----------|-------------|------------------|-----------|
| RN-11-03-01 | Al menos una causal debe ser seleccionada obligatoriamente para avanzar | Art. 188 Ley 1952/2019 | Crítica |
| RN-11-03-02 | La justificación es obligatoria cuando se selecciona la causal "Otro" | Art. 3 Ley 1437/2011 (motivación) | Crítica |
| RN-11-03-03 | La justificación debe tener entre 50 y 2000 caracteres | Principio de proporcionalidad | Alta |
| RN-11-03-04 | El sistema debe validar coherencia semántica entre causales seleccionadas y justificación | Principio de lógica administrativa | Alta |
| RN-11-03-05 | No se permiten justificacions con patrones repetitivos o genéricos | Jurisprudencia Consejo de Estado | Media |
| RN-11-03-06 | El contador de caracteres debe actualizarse en tiempo real mientras el usuario escribe | Regla de usabilidad | Media |
| RN-11-03-07 | Las causales seleccionadas quedan registradas en audit log con marca de tiempo | Art. 76 Ley 1952/2019 | Media |
| RN-11-03-08 | El sistema debe permitir retroceder al Paso 2 manteniendo causales y justificación guardadas temporalmente | Principio de flexibilidad | Baja |

## Supuestos

1. Se asume que el funcionario conoce las causales legales de incorporación y sabe identificar cuál o cuáles aplican al caso concreto que está tramitando.
2. Se asume que el funcionario tiene la capacidad de redactar una justificación clara, precisa y motivada que cumpla con los requisitos legales mínimos.
3. Se asume que el sistema cuenta con algoritmos básicos de procesamiento de lenguaje natural para validar coherencia semántica entre causales y justificación.
4. Se asume que不存在 plantillas predefinidas de justificación que puedan inducir al funcionario a copiar y pegar textos genéricos sin adaptación al caso concreto.
5. Se asume que el funcionario dispone del tiempo necesario para redactar una justificación adecuada sin presiones indebidas de tiempo.

## Criterios de Aceptación

### Escenario 1: Selección múltiple de causales predefinidas

**Dado** que estoy en el Paso 3 del asistente de incorporación  
**Cuando** hago clic en los checkboxes de las causales "Mismos hechos" y "Conexidad"  
**Entonces** el sistema marca ambos checkboxes visualmente con color azul institucional (#063853)  
**Y** aplica fondo azul claro (#EBF4FA) a las tarjetas de las causales seleccionadas  
**Y** muestra un ícono de check blanco dentro de cada checkbox  
**Y** habilita el botón "Continuar" que estaba previamente deshabilitado  

**Evidencia:** Captura de pantalla mostrando dos causales seleccionadas simultáneamente con estilos visuales distintivos.

### Escenario 2: Validación de intento de avance sin causales seleccionadas

**Dado** que estoy en el Paso 3 sin haber seleccionado ninguna causal  
**Cuando** intento hacer clic en el botón "Continuar"  
**Entonces** el botón permanece deshabilitado (color gris, cursor not-allowed)  
**Y** al pasar el cursor, se muestra tooltip: "Seleccione al menos una causal para continuar"  
**Y** el sistema aplica borde rojo (#E3201B) temporalmente al contenedor de causales durante 2 segundos  
**Y** muestra mensaje inline: "Es obligatorio seleccionar al menos una causal de incorporación"  

**Evidencia:** Captura de pantalla con mensaje de error visible y contenedor de causales con borde rojo.

### Escenario 3: Redacción de justificación con validación de longitud en tiempo real

**Dado** que he seleccionado la causal "Otro"  
**Cuando** comienzo a redactar la justificación en el campo de texto  
**Entonces** el sistema muestra un contador de caracteres en formato "X / 2000" en la esquina inferior derecha del textarea  
**Y** el contador se actualiza con cada tecla presionada  
**Y** cuando alcanzo los 50 caracteres, el borde del campo cambia de rojo a verde indicando que se cumplió el mínimo  
**Y** cuando me acerco a 1900 caracteres, el contador cambia a color naranja como advertencia  
**Y** al llegar a 2000 caracteres exactos, el sistema bloquea la entrada de más texto  

**Evidencia:** Secuencia de capturas mostrando contador en 10, 50, 500 y 2000 caracteres con cambios de color correspondientes.

### Escenario 4: Error por justificación inferior al mínimo requerido

**Dado** que he seleccionado la causal "Otro" y he redactado una justificación de 35 caracteres  
**Cuando** intento hacer clic en el botón "Continuar"  
**Entonces** el sistema muestra mensaje de error: "La justificación es muy corta. Debe tener al menos 50 caracteres (lleva 35)"  
**Y** el botón "Continuar" permanece deshabilitado  
**Y** el campo de texto muestra borde rojo parpadeante durante 3 segundos  
**Y** el foco del cursor se reposiciona automáticamente en el campo de justificación  

**Evidencia:** Captura de pantalla con mensaje de error y contador mostrando "35 / 2000" en rojo.

### Escenario 5: Asistencia de procuradurIA para redacción de justificación

**Dado** que he seleccionado la causal "Otro" y tengo dificultad para redactar la justificación  
**Cuando** hago clic en el botón flotante de procuradurIA  
**Entonces** el asistente IA muestra un mensaje: "Puedo ayudarte a redactar la justificación. Por favor indícame: ¿qué relación específica existe entre los expedientes que motiva esta incorporación?"  
**Y** ofrece tres opciones de plantilla personalizable: "Relación por identidad de hechos", "Relación por conexidad probatoria", "Relación por unidad de sujeto"  
**Y** al seleccionar una opción, genera un borrador de justificación que puedo editar libremente  
**Y** registra en audit log: "Usuario solicitó asistencia de procuradurIA para redacción de justificación en incorporación [timestamp]"  

**Evidencia:** Captura de pantalla del chat de procuradurIA mostrando sugerencia de justificación generada.

### Escenario 6: Validación de coherencia semántica entre causal y justificación

**Dado** que he seleccionado la causal "Mismos hechos"  
**Cuando** redacto una justificación que no contiene términos relacionados como "hechos", "conducta", "acción" u "omisión"  
**Y** presiono el botón "Continuar"  
**Entonces** el sistema muestra advertencia: "Advertencia: La causal seleccionada es 'Mismos hechos' pero su justificación no parece mencionar los hechos comunes. ¿Desea continuar de todas formas?"  
**Y** ofrece botones: "Revisar justificación" y "Continuar igualmente"  
**Y** si selecciono "Revisar justificación", el foco vuelve al campo de texto  
**Y** registra la advertencia en audit log como posible inconsistencia  

**Evidencia:** Captura de pantalla del modal de advertencia con las dos opciones de acción.

### Escenario 7: Detección de patrón de texto genérico o repetitivo

**Dado** que pego en el campo de justificación un texto genérico como "Porque sí, para agilizar el trámite, por conveniencia del despacho"  
**Cuando** el sistema analiza el texto mediante algoritmo de detección de patrones  
**Entonces** muestra advertencia: "Advertencia: Hemos detectado que su justificación podría ser muy genérica. Le recomendamos especificar los hechos concretos que motivan esta incorporación"  
**Y** resalta en amarillo las frases detectadas como genéricas  
**Y** ofrece un enlace "Ver ejemplos de justificaciones adecuadas" que despliega tres casos modelo  
**Y** permite continuar de todas formas si el usuario insiste después de la advertencia  

**Evidencia:** Captura de pantalla con frases genéricas resaltadas en amarillo y ejemplos desplegables.

### Escenario 8: Retroceso al Paso 2 manteniendo causales y justificación guardadas

**Dado** que he seleccionado dos causales y redactado 300 caracteres de justificación en el Paso 3  
**Cuando** hago clic en el botón "Atrás"  
**Entonces** el sistema regresa al Paso 2 (Selección del Principal)  
**Y** mantiene en memoria temporal las causales seleccionadas y la justificación parcial  
**Y** puedo modificar la selección del expediente principal si lo considero necesario  
**Y** al volver a avanzar al Paso 3, encuentro mis causales y justificación exactamente como las dejé  

**Evidencia:** Secuencia de capturas mostrando navegación atrás/adelante con persistencia de datos del formulario.

### Escenario 9: Expired session por superar tiempo máximo de permanencia

**Dado** que permanezco 30 minutos redactando la justificación sin guardar ni interactuar  
**Cuando** intento hacer clic en cualquier botón o campo del formulario  
**Entonces** el sistema muestra modal de "Sesión Expirada"  
**Y** indica: "Ha superado el tiempo máximo de 30 minutos en este paso. Por seguridad, debe reiniciar el proceso de incorporación"  
**Y** las causales seleccionadas y la justificación redactada se pierden  
**Y** soy redirigido al dashboard del expediente principal  
**Y** se registra el evento en audit log como "Timeout de sesión en Paso 3 de incorporación"  

**Evidencia:** Captura de pantalla del modal de sesión expirada y registro en audit log.

### Escenario 10: Selección de causal "Mismo sujeto procesal" con validación cruzada de datos

**Dado** que he seleccionado la causal "Mismo sujeto procesal"  
**Cuando** el sistema valida cruzadamente los disciplinados de todos los expedientes incorporados  
**Entonces** verifica que al menos un disciplinado sea idéntico en todos los expedientes (mismo nombre y documento de identidad)  
**Y** si encuentra coincidencia exacta, muestra mensaje de confirmación: "Validación exitosa: Los expedientes comparten al disciplinado [Nombre Completo] con documento [Número]"  
**Y** si no encuentra coincidencia, muestra advertencia: "Advertencia: Ha seleccionado 'Mismo sujeto procesal' pero los expedientes no parecen compartir disciplinados. Verifique la causal seleccionada"  
**Y** registra el resultado de la validación en audit log  

**Evidencia:** Captura de pantalla con mensaje de validación exitosa o advertencia según corresponda.

## Prototipo / Anexos

- **Prototipo de pantalla:** `/workspace/Pantallas VEED/11_incorporacion_manual.html`
- **Componentes específicos del paso 3 (Causales y Justificación):**
  - Grid de opciones de causales con checkboxes custom (líneas 961-1010)
  - Textarea de justificación con contador de caracteres (líneas 1011-1018)
  - Mensajes de validación inline y tooltips de error
  - Botones de navegación: "Atrás", "Continuar"
- **Tokens de diseño PGN aplicados:**
  - Fuente: Montserrat (labels de causales), Poppins (descripciones y textarea)
  - Color primario: #063853 (Azul institucional para selección activa)
  - Color de error: #E3201B (Rojo institucional para validaciones fallidas)
  - Color de éxito: #33FFCC (Verde azulado para validaciones exitosas)
  - Color de advertencia: #FFC300 (Naranja para alertas semánticas)
- **Referencias a líneas del prototipo HTML:**
  - Paso 3: Causales de incorporación (líneas 961-1033)
  - Estilos de causales-grid (líneas 551-556)
  - Estilos de causal-option selected (líneas 572-575)
  - Form-textarea (líneas 623-632)
- **Anexo técnico:** Documento de especificación de algoritmo de validación semántica (en elaboración)

## Stakeholders

| Rol | Nombre/Dependencia | Responsabilidad | Firma Requerida |
|-----|-------------------|-----------------|-----------------|
| Product Owner | Dirección de Investigación Disciplinaria | Definición de causales válidas | Sí |
| Líder Técnico | Oficina de Sistemas - PGN | Validación de algoritmos de NLP | Sí |
| Funcionario Instructor | Procuraduría Delegada para la Investigación | Usuario primario, validación de usabilidad | Sí |
| Área Jurídica | Oficina Asesora Jurídica | Validación de fundamentación legal de causales | Sí |
| Oficina de Control Interno | OCI-PGN | Auditoría de motivación de actos de incorporación | Sí |
| Delegado de Protección de Datos | PGN | Validación de tratamiento de datos en justificaciones | Sí |

## Plan de Validación

| Tipo de Prueba | Responsable | Fecha Estimada | Criterio de Aprobación |
|----------------|-------------|----------------|------------------------|
| Prueba de selección múltiple de causales | Equipo de Desarrollo | 24/05/2026 | Múltiples causales seleccionables simultáneamente sin errores |
| Prueba de validación de longitud de justificación | QA Lead | 29/05/2026 | Contador en tiempo real preciso, bloqueos en límites correctos |
| Prueba de algoritmo de detección de patrones genéricos | Equipo de Desarrollo | 01/06/2026 | Detecta 90% de patrones genéricos conocidos |
| Prueba de validación semántica causal-justificación | QA Lead | 03/06/2026 | Advertencias coherentes en 85% de casos de inconsistencia |
| Prueba de integración con procuradurIA | AI Team | 05/06/2026 | Asistente genera borradores útiles en 80% de casos |
| Validación jurídica de causales por Oficina Asesora | Oficina Asesora Jurídica | 07/06/2026 | Certificación de conformidad con Art. 188 CGD |
| UAT (User Acceptance Testing) | Funcionarios Instructor | 14/06/2026 | Aprobación formal por parte de 5 usuarios clave |

## Matriz de Trazabilidad con Referencias Normativas

| Artículo | Norma | Descripción | Implementación en Sistema | Estado de Cumplimiento |
|----------|-------|-------------|--------------------------|------------------------|
| Art. 188 | Ley 1952/2019 | Causales taxativas de acumulación | Listado cerrado de 4 causales implementado | ✅ Cumple |
| Art. 3 | Ley 1437/2011 | Motivación de actos administrativos | Justificación escrita obligatoria con validación de longitud | ✅ Cumple |
| Art. 14 | Ley 1952/2019 | Debido proceso | Validación de coherencia semántica garantiza motivación adecuada | ✅ Cumple |
| Art. 1 | Ley 2094/2021 | Principios rectores | Interfaz ágil con validaciones en tiempo real | ✅ Cumple |
| Art. 76 | Ley 1952/2019 | Funciones del instructor | Registro auditado de causales y justificación | ✅ Cumple |
| Sentencia C-836/2001 | Corte Constitucional | Debido proceso en materia disciplinaria | Validaciones previenen nulidades por falta de motivación | ✅ Cumple |

## Notas Adicionales

- Esta HU-11-03 cubre exclusivamente el **Paso 3: Registro de Causales y Justificación**.
- El algoritmo de validación semántica debe ser entrenado progresivamente con justificaciones reales aprobadas para mejorar su precisión.
- Las plantillas sugeridas por procuradurIA deben ser marcadas claramente como "borradores" que requieren edición y personalización por el funcionario.
- El sistema debe prevenir el copy-paste masivo desde fuentes externas mediante detección de patrones de formato inconsistentes.
- En futuros iteraciones, se podría implementar validación cruzada automática con la base de datos de expedientes para pre-llenar fragmentos de justificación basados en metadata existente.
