# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por |
|-------|-------|------------|--------------|
| 15/05/2026 | HU-11-02 | Analista de Negocio | Líder Técnico |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica | P17-Apoyo a la Investigación | A41-Incorporación Manual de Expedientes | Funcionalidad Específica | Define claramente qué expediente liderará el proceso acumulado, garantizando que el expediente principal tenga la mayor complejidad probatoria o la sanción potencial más grave para optimizar la gestión procesal |

### Descripción

**¿Quién?** El Funcionario de Instrucción (rol: instructor) o el Procurador Delegado (rol: juez) que ha completado la selección múltiple de expedientes en el paso anterior y ahora debe definir cuál será el expediente principal que absorberá los demás.

**¿Qué?** Selecciona uno de los expedientes previamente marcados como candidato para que actúe como expediente principal dentro del proceso de incorporación, visualizando tarjetas comparativas con información clave de cada expediente que facilitan la decisión basada en criterios de complejidad, antigüedad y gravedad de la falta disciplinaria.

**¿Para qué?** Para establecer correctamente el expediente rector del proceso acumulado, conforme al principio de especialidad y economía procesal, asegurando que el expediente con mayor desarrollo probatorio, la sanción potencial más grave o la mayor antigüedad sea el que lidere la tramitación conjunta, lo cual impacta directamente en la organización del archivo físico y digital, la numeración de folios y la secuencia lógica de las actuaciones.

**Referencias Normativas:**
- Ley 1952 de 2019 (Código General Disciplinario), Artículo 14: Principios del procedimiento disciplinario (economía procesal).
- Ley 1952 de 2019, Artículo 188: Acumulación de procesos (criterios de determinación del proceso principal).
- Ley 2094 de 2021, Artículo 1: Principios rectores de la función disciplinaria (eficiencia).
- Decreto 1069 de 2015: Compilación del Sector Justicia (gestión documental).
- Código General de Archivo de la Nación (Ley 594 de 2000): Organización de fondos documentales.
- Resolución 000191 de 2021 de la PGN: Lineamientos para la gestión documental de expedientes disciplinarios.

## Dependencias y Precondiciones

1. El usuario debe haber completado exitosamente el Paso 1 (Búsqueda y Selección Múltiple) con al menos dos (2) expedientes seleccionados.
2. Los expedientes seleccionados deben estar almacenados temporalmente en la sesión del asistente de incorporación con toda su metadata disponible (radicado, disciplinado, hechos, fecha apertura, etapa, gravedad de falta).
3. El sistema debe tener acceso a información adicional de cada expediente para mostrar en las tarjetas comparativas: número de pruebas allegadas, número de actuantes, valor del daño potencial, cuantía si aplica.
4. El módulo de shell corporativo (HU-02) debe mantener la sesión activa del usuario con validación continua de permisos RBAC.
5. Debe existir un criterio objetivo y automatizado para sugerir automáticamente cuál expediente debería ser el principal (por ejemplo: mayor antigüedad, mayor número de pruebas, falta más grave).
6. El sistema debe permitir retroceder al Paso 1 si el usuario considera que necesita seleccionar expedientes adicionales antes de definir el principal.
7. La interfaz debe mantener el indicador de pasos actualizado mostrando el Paso 2 como activo y el Paso 1 como completado.
8. Debe existir trazabilidad de la selección del expediente principal con registro de qué usuario tomó la decisión y en qué fecha.

## Restricciones

1. Solo se puede seleccionar UN único expediente como principal; no se permiten co-principales ni principales compartidos bajo ninguna circunstancia.
2. Una vez confirmado el expediente principal en el Paso 4 (Confirmación), no se puede modificar esta selección salvo mediante acto administrativo motivado de separación de procesos.
3. El sistema debe validar que el expediente seleccionado como principal no esté en una etapa procesal inferior a la de los demás expedientes incorporados (no puede ser principal un expediente en indagación previa si hay otro en investigación disciplinaria).
4. Si todos los expedientes están en la misma etapa procesal, el sistema debe sugerir como principal aquel con mayor antigüedad (fecha de apertura más temprana).
5. La tarjeta del expediente principal seleccionado debe mostrar un indicador visual distintivo (borde azul institucional, icono de estrella) que la diferencie claramente de las demás.
6. El usuario no puede avanzar al Paso 3 sin haber seleccionado explícitamente un expediente principal; el botón "Continuar" permanece deshabilitado hasta cumplir este requisito.
7. La información mostrada en las tarjetas debe ser consistente con los datos oficiales del sistema; cualquier discrepancia debe ser reportada como incidencia de integridad de datos.
8. El tiempo máximo de inactividad permitido en este paso es de 15 minutos; superado este tiempo, la sesión expira y se pierden las selecciones previas.
9. La interfaz debe cumplir con los estándares de accesibilidad WCAG 2.1 nivel AA, utilizando tokens de diseño PGN.

## Reglas de Negocio

| ID Regla | Descripción | Fundamento Legal | Prioridad |
|----------|-------------|------------------|-----------|
| RN-11-02-01 | Solo se permite seleccionar un único expediente como principal | Principio de unidad de dirección procesal | Crítica |
| RN-11-02-02 | El sistema debe sugerir automáticamente el expediente principal basándose en: mayor antigüedad, mayor número de pruebas o falta más grave | Art. 188 Ley 1952/2019 | Alta |
| RN-11-02-03 | No se puede seleccionar como principal un expediente en etapa procesal inferior a la de los demás incorporados | Principio de preclusión | Alta |
| RN-11-02-04 | Si hay empate en etapa procesal, se prioriza el expediente con fecha de apertura más antigua | Principio de celeridad | Media |
| RN-11-02-05 | El botón "Continuar" permanece deshabilitado hasta que se seleccione un expediente principal | Regla de usabilidad | Media |
| RN-11-02-06 | El sistema debe permitir retroceder al Paso 1 manteniendo las selecciones previas | Principio de flexibilidad | Media |
| RN-11-02-07 | La selección del expediente principal queda registrada en audit log con marca de tiempo | Art. 76 Ley 1952/2019 | Media |
| RN-11-02-08 | Las tarjetas deben mostrar información comparable: radicado, disciplinado, fecha apertura, etapa, número de pruebas | Principio de transparencia | Baja |

## Supuestos

1. Se asume que el funcionario conoce los criterios legales para determinar qué expediente debe ser el principal (mayor complejidad, antigüedad o gravedad).
2. Se asume que la información mostrada en las tarjetas comparativas está actualizada y es consistente con la base de datos central de expedientes.
3. Se asume que el funcionario tiene la facultad legal para decidir cuál expediente será el principal dentro del proceso de incorporación.
4. Se asume que no existen conflictos de competencia territorial o funcional entre los expedientes seleccionados que impidan la incorporación.
5. Se asume que el sistema cuenta con mecanismos de persistencia temporal para mantener las selecciones mientras el usuario toma la decisión.

## Criterios de Aceptación

### Escenario 1: Visualización correcta de tarjetas comparativas de expedientes seleccionados

**Dado** que he completado el Paso 1 con tres (3) expedientes seleccionados  
**Cuando** avanzo al Paso 2 del asistente de incorporación  
**Entonces** el sistema muestra una tarjeta individual para cada expediente seleccionado  
**Y** cada tarjeta contiene: número de radicado, nombre del disciplinado, fecha de apertura, etapa procesal, número de pruebas allegadas y gravedad de la falta  
**Y** las tarjetas se muestran en un grid responsive (2 columnas en desktop, 1 columna en móvil)  
**Y** el título del paso indica: "Seleccione el expediente principal"  

**Evidencia:** Captura de pantalla mostrando 3 tarjetas con información completa de expedientes "2026-001234", "2025-009876", "2025-008765".

### Escenario 2: Sugerencia automática del expediente principal por mayor antigüedad

**Dado** que los expedientes seleccionados tienen fechas de apertura diferentes  
**Cuando** cargo el Paso 2  
**Entonces** el sistema resalta automáticamente la tarjeta del expediente con fecha de apertura más antigua  
**Y** muestra un badge: "Sugerido: Expediente más antiguo"  
**Y** el radio button de esa tarjeta aparece preseleccionado pero permite cambiar la selección  
**Y** un tooltip explica: "Se sugiere este expediente por tener la fecha de apertura más antigua (principio de celeridad)"  

**Evidencia:** Captura de pantalla con tarjeta de expediente "2024-005432" (fecha: 15/01/2024) resaltada con badge amarillo y radio button marcado.

### Escenario 3: Selección manual de expediente principal diferente al sugerido

**Dado** que el sistema ha sugerido automáticamente el expediente "2024-005432" como principal  
**Cuando** hago clic en la tarjeta del expediente "2026-001234" (diferente al sugerido)  
**Entonces** el sistema marca el radio button de la tarjeta seleccionada  
**Y** remueve el resaltado de la tarjeta anteriormente sugerida  
**Y** aplica borde azul institucional (#063853) y fondo azul claro (#EBF4FA) a la tarjeta seleccionada  
**Y** habilita el botón "Continuar" que estaba previamente deshabilitado  

**Evidencia:** Captura de pantalla mostrando tarjeta "2026-001234" con borde azul y fondo claro, botón "Continuar" en estado enabled.

### Escenario 4: Validación de intento de avance sin selección de principal

**Dado** que estoy en el Paso 2 sin haber seleccionado ningún expediente principal  
**Cuando** intento hacer clic en el botón "Continuar"  
**Entonces** el botón permanece deshabilitado (color gris, cursor not-allowed)  
**Y** al pasar el cursor, se muestra tooltip: "Seleccione un expediente principal para continuar"  
**Y** el contador de pasos muestra "Paso 2 de 4: Pendiente" en color naranja  
**Y** no es posible avanzar mediante navegación directa (URL manipulation)  

**Evidencia:** Captura de pantalla con botón "Continuar" en estado disabled y tooltip visible.

### Escenario 5: Retroceso al Paso 1 manteniendo selecciones previas

**Dado** que estoy en el Paso 2 con tres expedientes cargados en tarjetas  
**Cuando** hago clic en el botón "Atrás"  
**Entonces** el sistema regresa al Paso 1 (Búsqueda y Selección)  
**Y** los expedientes previamente seleccionados mantienen su estado de selección (checkbox marcados)  
**Y** puedo agregar o quitar expedientes de la selección  
**Y** al volver a avanzar al Paso 2, las tarjetas se actualizan reflejando los cambios realizados  

**Evidencia:** Secuencia de capturas mostrando navegación atrás, modificación de selección (agregar cuarto expediente), y regreso al Paso 2 con 4 tarjetas.

### Escenario 6: Error por inconsistencia de datos en tarjeta de expediente

**Dado** que una tarjeta muestra información contradictoria (ejemplo: etapa "Investigación Disciplinaria" pero fecha de apertura posterior a la de un expediente en "Indagación Previa")  
**Cuando** el sistema detecta la inconsistencia mediante validación cruzada  
**Entonces** muestra un icono de advertencia amarillo en la esquina superior derecha de la tarjeta  
**Y** al pasar el cursor, tooltip indica: "Inconsistencia detectada: Verifique la etapa procesal de este expediente"  
**Y** registra el evento en audit log como "Inconsistencia de metadata en expediente [radicado]"  
**Y** permite la selección pero advierte al usuario antes de confirmar en el Paso 4  

**Evidencia:** Captura de pantalla con tarjeta mostrando icono de advertencia y tooltip explicativo.

### Escenario 7: Expired session por inactividad prolongada en Paso 2

**Dado** que permanezco 15 minutos sin interactuar con el sistema estando en el Paso 2  
**Cuando** intento realizar cualquier acción (seleccionar tarjeta o hacer clic en botones)  
**Entonces** el sistema muestra modal de "Sesión Expirada"  
**Y** indica: "Su sesión ha expirado por inactividad. Debe reiniciar el proceso de incorporación"  
**Y** las selecciones previas se pierden  
**Y** soy redirigido al dashboard principal del expediente  
**Y** se registra el evento en audit log como "Timeout de sesión en incorporación"  

**Evidencia:** Captura de pantalla del modal de sesión expirada y registro en audit log.

### Escenario 8: Visualización de información detallada al hacer clic en "Ver más" de tarjeta

**Dado** que estoy visualizando las tarjetas de expedientes en el Paso 2  
**Cuando** hago clic en el enlace "Ver más detalles" de una tarjeta específica  
**Entonces** el sistema despliega un panel expandible debajo de la tarjeta  
**Y** muestra información adicional: objeto detallado de la investigación, nombre del funcionario asignado, último movimiento procesal, número de folios, valor estimado del daño  
**Y** el panel puede colapsarse haciendo clic nuevamente en "Ver menos"  
**Y** esta acción no afecta la selección del expediente como principal  

**Evidencia:** Captura de pantalla con panel expandible abierto mostrando 10 campos adicionales de metadata del expediente.

## Prototipo / Anexos

- **Prototipo de pantalla:** `/workspace/Pantallas VEED/11_incorporacion_manual.html`
- **Componentes específicos del paso 2 (Selección del Principal):**
  - Grid de tarjetas comparativas de expedientes (líneas 934-959)
  - Radio button personalizado por tarjeta (líneas 507-534)
  - Badge de sugerencia automática (líneas 474-483)
  - Botones de navegación: "Atrás", "Continuar" (deshabilitado hasta selección)
  - Panel expandible de detalles adicionales
- **Tokens de diseño PGN aplicados:**
  - Fuente: Montserrat (títulos de tarjeta, badges), Poppins (información de tarjeta)
  - Color primario: #063853 (Azul institucional para selección activa)
  - Color de sugerencia: #FFE601 (Amarillo institucional para badge "Sugerido")
  - Color de fondo seleccionado: #EBF4FA (Azul muy claro)
  - Color de borde hover: #4DBFE2 (Azul claro)
- **Referencias a líneas del prototipo HTML:**
  - Paso 2: Selección del principal (líneas 933-960)
  - Estilos de principal-cards (líneas 484-506)
  - Estilos de principal-card selected (líneas 502-506)
  - Radio button custom (líneas 518-534)
- **Anexo técnico:** Documento de especificación de algoritmo de sugerencia automática (en elaboración)

## Stakeholders

| Rol | Nombre/Dependencia | Responsabilidad | Firma Requerida |
|-----|-------------------|-----------------|-----------------|
| Product Owner | Dirección de Investigación Disciplinaria | Definición de criterios de prioridad | Sí |
| Líder Técnico | Oficina de Sistemas - PGN | Validación de algoritmo de sugerencia | Sí |
| Funcionario Instructor | Procuraduría Delegada para la Investigación | Usuario primario, validación de usabilidad | Sí |
| Jefe de Grupo | Grupo de Gestión Procesal | Supervisor de criterios de acumulación | Sí |
| Área Jurídica | Oficina Asesora Jurídica | Validación de fundamentación legal de criterios | Sí |
| Archivista Central | Grupo de Gestión Documental - PGN | Validación de impacto en organización de archivo | Sí |

## Plan de Validación

| Tipo de Prueba | Responsable | Fecha Estimada | Criterio de Aprobación |
|----------------|-------------|----------------|------------------------|
| Prueba de algoritmo de sugerencia automática | Equipo de Desarrollo | 23/05/2026 | Sugiere correctamente en 95% de casos según criterios definidos |
| Prueba de usabilidad de tarjetas comparativas | UX/UI Team | 28/05/2026 | 90% de usuarios identifican información clave en menos de 10 segundos |
| Prueba de validación de regla de único principal | QA Lead | 31/05/2026 | Imposible seleccionar más de un principal simultáneamente |
| Prueba de persistencia de selecciones al navegar atrás/adelante | QA Lead | 02/06/2026 | Selecciones se mantienen intactas en navegación bidireccional |
| Prueba de timeout de sesión por inactividad | Security Team | 04/06/2026 | Session expira exactamente a los 15 minutos de inactividad |
| Validación jurídica de criterios de prioridad | Oficina Asesora Jurídica | 06/06/2026 | Certificación de conformidad con Art. 188 CGD |
| UAT (User Acceptance Testing) | Funcionarios Instructor | 13/06/2026 | Aprobación formal por parte de 5 usuarios clave |

## Matriz de Trazabilidad con Referencias Normativas

| Artículo | Norma | Descripción | Implementación en Sistema | Estado de Cumplimiento |
|----------|-------|-------------|--------------------------|------------------------|
| Art. 14 | Ley 1952/2019 | Principio de economía procesal | Sugerencia automática optimiza selección del principal | ✅ Cumple |
| Art. 188 | Ley 1952/2019 | Acumulación de procesos | Criterios objetivos para determinación del expediente principal | ✅ Cumple |
| Art. 1 | Ley 2094/2021 | Principio de eficiencia | Interfaz ágil para toma de decisión informada | ✅ Cumple |
| Art. 10 | Ley 1952/2019 | Principio de celeridad | Priorización por antigüedad cuando hay empate en etapa | ✅ Cumple |
| Art. 76 | Ley 1952/2019 | Funciones del instructor | Registro auditado de decisión de selección de principal | ✅ Cumple |

## Notas Adicionales

- Esta HU-11-02 cubre exclusivamente el **Paso 2: Selección del Expediente Principal**. 
- El algoritmo de sugerencia automática debe ser configurable por parámetros administrables para permitir ajustes futuros sin necesidad de despliegue de código.
- La información mostrada en las tarjetas debe provenir de queries optimizadas para evitar tiempos de carga superiores a 2 segundos.
- En casos de expedientes con igual antigüedad, mismo número de pruebas y misma gravedad de falta, el sistema debe sugerir aquel con el número de radicado más bajo (criterio de desempate objetivo).
