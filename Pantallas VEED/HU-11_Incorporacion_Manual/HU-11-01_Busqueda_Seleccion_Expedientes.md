# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por |
|-------|-------|------------|--------------|
| 15/05/2026 | HU-11-01 | Analista de Negocio | Líder Técnico |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica | P17-Apoyo a la Investigación | A41-Incorporación Manual de Expedientes | Funcionalidad Específica | Permite la acumulación procesal de expedientes relacionados garantizando el debido proceso, la economía procesal y evitando decisiones contradictorias sobre hechos idénticos |

### Descripción

**¿Quién?** El Funcionario de Instrucción (rol: instructor) o el Procurador Delegado (rol: juez) que tiene asignado un expediente disciplinario en etapa de indagación previa o investigación disciplinaria.

**¿Qué?** Realiza la búsqueda, selección múltiple y incorporación manual de dos o más expedientes disciplinarios activos que guardan relación de conexidad, identidad de sujetos o identidad de hechos, mediante un asistente guiado de cuatro pasos que incluye validación de causales legales, justificación motivada y confirmación irreversible con registro auditado.

**¿Para qué?** Para garantizar la acumulación procesal de expedientes relacionados conforme al principio de unidad de actuación establecido en el artículo 14 de la Ley 1952 de 2019 (Código General Disciplinario), asegurando que procesos que versan sobre los mismos hechos, sujetos o conductas sean tramitados conjuntamente para evitar fallos contradictorios, optimizar recursos del Estado y garantizar la coherencia en la aplicación del régimen disciplinario.

**Referencias Normativas:**
- Ley 1952 de 2019 (Código General Disciplinario), Artículo 14: Principios del procedimiento disciplinario (unidad de actuación).
- Ley 1952 de 2019, Artículo 115: Reserva de las actuaciones disciplinarias.
- Ley 1952 de 2019, Artículo 188: Acumulación de procesos.
- Ley 2094 de 2021, Artículo 1: Principios rectores de la función disciplinaria.
- Decreto 1069 de 2015: Compilación del Sector Justicia.
- Código General de Archivo de la Nación (Ley 594 de 2000): Gestión documental y conservación de expedientes.

## Dependencias y Precondiciones

1. El usuario debe estar autenticado con credenciales válidas en el sistema EED y tener asignado el rol de "Funcionario de Instrucción" o "Procurador Delegado" para el expediente principal desde el cual se origina la incorporación.
2. Deben existir al menos dos (2) expedientes disciplinarios en estado "Activo" (en indagación previa o investigación disciplinaria) en la base de datos del sistema que cumplan con al menos una causal de incorporacion legalmente válida.
3. El módulo de shell corporativo (HU-02) debe estar activo con configuración de RBAC (Role-Based Access Control) y ABAC (Attribute-Based Access Control) habilitado para validación de permisos por tipo de expediente.
4. El sistema debe contar con un índice de búsqueda full-text que permita localizar expedientes por número de radicado, nombre del disciplinado, objeto de la investigación, fecha de apertura y estado procesal.
5. El expediente principal seleccionado debe encontrarse en la misma etapa procesal o en etapa posterior a los expedientes que se van a incorporar (no se puede incorporar un expediente en juzgamiento a uno en indagación previa).
6. Debe existir trazabilidad completa de todas las actuaciones procesales de cada expediente candidato a incorporación, incluyendo historial de consultas, descargas y modificaciones.
7. El componente de procuradurIA debe estar disponible para brindar asistencia contextual durante el proceso de incorporación, con registro auditado de todas las interacciones.
8. La base de datos debe mantener integridad referencial entre expedientes principales e incorporados mediante tabla de relacion muchos-a-muchos con fecha cierta de vinculación.

## Restricciones

1. Solo se pueden incorporar expedientes que se encuentren en estado "Activo", excluyendo aquellos que hayan sido archivados, ejecutoriados o que se encuentren en etapa de ejecución de fallo.
2. La incorporación de expedientes es irreversible una vez confirmada; no existe funcionalidad de "desincorporación" salvo mediante acto administrativo motivado del superior jerárquico que ordene la separación de procesos.
3. El funcionario que realiza la incorporación debe ser el mismo que tenga asignada la competencia territorial y funcional para conocer del expediente principal, conforme a las reglas de reparto establecidas en el sistema.
4. El sistema debe validar que los expedientes seleccionados no hayan sido previamente incorporados al mismo expediente principal para evitar duplicidades en la relación.
5. La justificación de la incorporación debe ser obligatoria y tener una longitud mínima de 50 caracteres y máxima de 2000 caracteres, debiendo expresar de manera clara y motivada la causal legal aplicable.
6. Todos los expedientes incorporados heredan el estado procesal del expediente principal; si el principal se archiva, los incorporados también deben archivarse salvo decisión expresa en contrario.
7. La reserva de las actuaciones (Art. 115 CGD) se extiende a todos los expedientes incorporados; solo los funcionarios con acceso al expediente principal pueden consultar los incorporados.
8. El sistema debe generar un acta de incorporación automática que incluya: fecha y hora de la incorporación, identificación del funcionario que la realiza, expedientes vinculados, causales invocadas y justificación registrada.
9. La interfaz debe cumplir con los estándares de accesibilidad WCAG 2.1 nivel AA, utilizando la fuente Poppins en todos sus componentes visuales y los tokens de diseño institucional PGN.
10. Cualquier intento de incorporar expedientes sin cumplir las causales legales o sin la justificación requerida quedará registrado en el audit log como evento de seguridad potencial.

## Reglas de Negocio

| ID Regla | Descripción | Fundamento Legal | Prioridad |
|----------|-------------|------------------|-----------|
| RN-11-01-01 | Solo se permiten incorporar expedientes en estado "Activo" (indagación previa o investigación disciplinaria) | Art. 188 Ley 1952/2019 | Crítica |
| RN-11-01-02 | Se requieren mínimo 2 expedientes seleccionados para habilitar el botón de continuar al paso siguiente | Principio de acumulación procesal | Crítica |
| RN-11-01-03 | El sistema debe validar que el usuario tenga competencia sobre todos los expedientes seleccionados antes de permitir la incorporación | Art. 76 Ley 1952/2019 | Crítica |
| RN-11-01-04 | No se permite incorporar un expediente que ya haya sido incorporado anteriormente al mismo expediente principal | Principio de non bis in idem | Alta |
| RN-11-01-05 | Las causales de incorporación válidas son: mismos hechos, mismo sujeto procesal, conexidad u otra debidamente motivada | Art. 188 Ley 1952/2019 | Alta |
| RN-11-01-06 | La justificación de incorporación es obligatoria y debe tener entre 50 y 2000 caracteres | Principio de motivación de actos administrativos | Alta |
| RN-11-01-07 | El sistema debe mostrar advertencia explícita de que la incorporación es irreversible antes de confirmar | Principio de seguridad jurídica | Media |
| RN-11-01-08 | Todos los eventos de incorporación quedan registrados en audit log inmutable con marca de tiempo y huella digital | Art. 76 Ley 1952/2019 | Media |
| RN-11-01-09 | Los expedientes incorporados heredan automáticamente el estado procesal del expediente principal | Principio de unidad de actuación | Media |
| RN-11-01-10 | El sistema debe impedir la incorporación si el expediente principal está en etapa de ejecución de fallo | Principio de preclusión procesal | Baja |

## Supuestos

1. Se asume que el funcionario instructor o procurador delegado conoce las causales legales de incorporación establecidas en el artículo 188 del Código General Disciplinario y sabe identificar cuándo aplican.
2. Se asume que todos los expedientes candidatos a incorporación cuentan con metadata completa y actualizada en el sistema (radicado, disciplinado, hechos, estado, etapa procesal).
3. Se asume que el sistema cuenta con conectividad continua a la base de datos central de expedientes para realizar búsquedas en tiempo real con información actualizada.
4. Se asume que el funcionario tiene acceso a su correo institucional para recibir notificaciones automáticas relacionadas con la incorporación realizada.
5. Se asume que不存在 causales de impedimento o conflicto de interés del funcionario que realiza la incorporación respecto de los expedientes seleccionados.
6. Se asume que la incorporación de expedientes no modifica los términos procesales individuales de cada expediente; cada uno mantiene su cómputo de términos original.

## Criterios de Aceptación

### Escenario 1: Búsqueda exitosa de expedientes activos por número de radicado

**Dado** que soy un Funcionario de Instrucción autenticado en el sistema EED  
**Cuando** accedo al módulo de incorporación manual desde un expediente principal  
**Y** ingreso uno o más números de radicado en el campo de búsqueda  
**Y** presiono el botón "Buscar"  
**Entonces** el sistema muestra una tabla con los expedientes encontrados que están en estado "Activo"  
**Y** cada fila muestra: número de radicado, nombre del disciplinado, objeto de la investigación, fecha de apertura, etapa procesal y estado  
**Y** cada fila incluye un botón de selección (checkbox) para marcar el expediente como candidato a incorporación  
**Y** el sistema indica cuántos expedientes han sido seleccionados en tiempo real  

**Evidencia:** Captura de pantalla de la tabla de resultados mostrando 5 expedientes encontrados tras buscar "2026-001234", con 3 seleccionados y contador "3 expedientes seleccionados".

### Escenario 2: Búsqueda de expedientes por nombre del disciplinado

**Dado** que soy un Funcionario de Instrucción autenticado en el sistema EED  
**Cuando** accedo al módulo de incorporación manual  
**Y** ingreso el nombre completo o parcial de un disciplinado en el campo de búsqueda  
**Y** presiono el botón "Buscar"  
**Entonces** el sistema muestra todos los expedientes activos donde esa persona figura como disciplinado  
**Y** los resultados incluyen expedientes donde el disciplinado aparece como único investigado y donde es co-disciplinado  
**Y** el sistema ordena los resultados por fecha de apertura (más reciente primero)  
**Y** se muestra un mensaje indicando el total de resultados encontrados  

**Evidencia:** Captura de pantalla tras buscar "Juan Pérez", mostrando 8 expedientes activos con ese disciplinado, ordenados cronológicamente descendente.

### Escenario 3: Validación de selección mínima de dos expedientes

**Dado** que soy un Funcionario de Instrucción en el paso 1 del asistente de incorporación  
**Cuando** selecciono únicamente un expediente de la tabla de resultados  
**Y** presiono el botón "Continuar"  
**Entonces** el sistema muestra un mensaje de error: "Debe seleccionar al menos dos (2) expedientes para continuar con la incorporación"  
**Y** el botón de "Continuar" permanece deshabilitado hasta que se cumpla el requisito  
**Y** el contador de expedientes seleccionados muestra "1 de 2 mínimos requeridos"  

**Evidencia:** Captura de pantalla con mensaje de error visible y botón "Continuar" en estado disabled (gris).

### Escenario 4: Filtrado de expedientes ya incorporados previamente

**Dado** que un expediente "2025-009876" ya fue incorporado anteriormente al expediente principal "2026-001234"  
**Cuando** realizo una nueva búsqueda de expedientes para incorporar  
**Entonces** el sistema excluye automáticamente el expediente "2025-009876" de los resultados de búsqueda  
**O** en su defecto, lo muestra marcado como "Ya incorporado" con el checkbox deshabilitado  
**Y** al pasar el cursor sobre el expediente, se muestra tooltip: "Este expediente ya fue incorporado el [fecha] por [funcionario]"  

**Evidencia:** Captura de pantalla mostrando expediente con etiqueta "Ya incorporado" y checkbox en estado disabled.

### Escenario 5: Error por expediente en estado no válido para incorporación

**Dado** que realizo una búsqueda de expedientes por palabra clave  
**Cuando** entre los resultados aparece un expediente en estado "Archivado" o "Ejecutoriado"  
**Entonces** el sistema muestra ese expediente en la tabla pero con el checkbox deshabilitado  
**Y** la columna de estado muestra un badge con color gris y texto "No incorporable"  
**Y** al pasar el cursor, se muestra tooltip: "Solo se pueden incorporar expedientes en estado Activo (Indagación Previa o Investigación Disciplinaria)"  

**Evidencia:** Captura de pantalla con expediente "2024-005678" en estado "Archivado" mostrado en la tabla con checkbox deshabilitado y badge gris.

### Escenario 6: Búsqueda sin resultados encontrados

**Dado** que realizo una búsqueda con un criterio que no coincide con ningún expediente activo  
**Cuando** presiono el botón "Buscar"  
**Entonces** el sistema muestra un mensaje: "No se encontraron expedientes activos que coincidan con su búsqueda"  
**Y** se sugiere verificar la ortografía o ampliar los criterios de búsqueda  
**Y** se ofrece la opción de "Limpiar filtros" para reiniciar la búsqueda  
**Y** el botón "Continuar" permanece deshabilitado  

**Evidencia:** Captura de pantalla mostrando mensaje de "sin resultados" con ilustración vacía y sugerencias de búsqueda.

### Escenario 7: Acceso denegado por falta de competencia sobre expediente

**Dado** que soy un Funcionario de Instrucción asignado al expediente "2026-001234"  
**Cuando** intento seleccionar un expediente "2025-008765" que está asignado a otro funcionario de otra procuraduría delegada  
**Entonces** el sistema muestra un mensaje de advertencia: "No tiene competencia sobre este expediente. La incorporación requiere autorización del superior jerárquico"  
**Y** el checkbox del expediente queda marcado pero con icono de advertencia amarillo  
**Y** al intentar continuar, el sistema solicita justificación adicional de la extensión de competencia  
**Y** registra el evento en audit log como "Incorporación con extensión de competencia pendiente de aprobación"  

**Evidencia:** Captura de pantalla con expediente marcado con icono de advertencia y modal solicitando justificación de extensión de competencia.

### Escenario 8: Paginación de resultados de búsqueda cuando exceden 20 registros

**Dado** que realizo una búsqueda que retorna 57 expedientes activos  
**Cuando** el sistema carga los resultados  
**Entonces** muestra únicamente los primeros 20 expedientes en la página 1  
**Y** habilita controles de paginación en la parte inferior de la tabla (Página 1 de 3)  
**Y** puedo navegar entre páginas usando botones "Anterior", "Siguiente" y números de página  
**Y** el contador de expedientes seleccionados se mantiene al cambiar de página  
**Y** puedo seleccionar expedientes de múltiples páginas y todos se mantienen en la selección  

**Evidencia:** Captura de pantalla mostrando tabla paginada con 20 resultados, controles de paginación visibles y contador "5 expedientes seleccionados (de 3 páginas)".

## Prototipo / Anexos

- **Prototipo de pantalla:** `/workspace/Pantallas VEED/11_incorporacion_manual.html`
- **Componentes específicos del paso 1 (Búsqueda y Selección):**
  - Barra de búsqueda con campo de texto y botón "Buscar"
  - Tabla de resultados con columnas: Radicado, Disciplinado, Objeto, Fecha Apertura, Etapa, Estado, Selección
  - Checkbox de selección múltiple por fila con estado visual (normal/seleccionado/deshabilitado)
  - Contador de expedientes seleccionados en tiempo real
  - Botones de acción: "Limpiar", "Continuar" (deshabilitado hasta tener 2+ selecciones)
  - Mensajes de error y validación inline
- **Tokens de diseño PGN aplicados:**
  - Fuente: Montserrat (títulos, badges), Poppins (cuerpo, inputs)
  - Color primario: #063853 (Azul institucional PGN)
  - Color de acción: #FFE601 (Amarillo institucional para botones principales)
  - Color de error: #E3201B (Rojo institucional)
  - Color de éxito: #33FFCC (Verde azulado para estados positivos)
  - Color secundario: #074C84 (Azul medio para hover)
- **Referencias a líneas del prototipo HTML:**
  - Indicador de pasos (líneas 872-890)
  - Paso 1: Buscador y resultados (líneas 892-931)
  - Estilos de tabla de resultados (líneas 400-464)
  - Botones de selección (líneas 445-464)
- **Anexo técnico:** Documento de especificación de API de búsqueda de expedientes (en elaboración)

## Stakeholders

| Rol | Nombre/Dependencia | Responsabilidad | Firma Requerida |
|-----|-------------------|-----------------|-----------------|
| Product Owner | Dirección de Investigación Disciplinaria | Definición de reglas de negocio | Sí |
| Líder Técnico | Oficina de Sistemas - PGN | Validación de implementación técnica | Sí |
| Funcionario Instructor | Procuraduría Delegada para la Investigación | Usuario primario, validación de usabilidad | Sí |
| Procurador Delegado | Despachos de Juzgamiento | Usuario secundario, validación de flujo | Sí |
| Jefe de Grupo | Grupo de Gestión Procesal | Supervisor de acumulaciones procesales | Sí |
| Oficina de Control Interno | OCI-PGN | Auditoría de trazabilidad de incorporaciones | Sí |
| Área Jurídica | Oficina Asesora Jurídica | Validación de causales legales de incorporación | Sí |

## Plan de Validación

| Tipo de Prueba | Responsable | Fecha Estimada | Criterio de Aprobación |
|----------------|-------------|----------------|------------------------|
| Prueba de concepto de búsqueda full-text | Equipo de Desarrollo | 22/05/2026 | Búsqueda retorna resultados correctos en 100% de casos |
| Prueba de usabilidad con funcionarios instructores | UX/UI Team | 27/05/2026 | 90% de usuarios completan selección sin asistencia |
| Prueba de validación de reglas de negocio | QA Lead | 30/05/2026 | Todas las RN validadas correctamente en escenarios de prueba |
| Prueba de seguridad y audit log | Security Team | 03/06/2026 | Todos los eventos de incorporación registrados sin excepción |
| Validación jurídica de causales de incorporación | Oficina Asesora Jurídica | 05/06/2026 | Certificación de conformidad con Art. 188 CGD |
| Prueba de carga (búsquedas simultáneas) | Performance Team | 08/06/2026 | Tiempo de respuesta menor a 2 segundos con 100 usuarios |
| UAT (User Acceptance Testing) | Funcionarios Instructor | 12/06/2026 | Aprobación formal por parte de 5 usuarios clave |

## Matriz de Trazabilidad con Referencias Normativas

| Artículo | Norma | Descripción | Implementación en Sistema | Estado de Cumplimiento |
|----------|-------|-------------|--------------------------|------------------------|
| Art. 14 | Ley 1952/2019 | Principio de unidad de actuación | Incorporación permite acumular procesos relacionados | ✅ Cumple |
| Art. 115 | Ley 1952/2019 | Reserva de actuaciones disciplinarias | Acceso restringido por RBAC a expedientes incorporados | ✅ Cumple |
| Art. 188 | Ley 1952/2019 | Acumulación de procesos | Causales de incorporación implementadas en sistema | ✅ Cumple |
| Art. 1 | Ley 2094/2021 | Principios rectores de función disciplinaria | Economía procesal y celeridad en incorporación | ✅ Cumple |
| Art. 76 | Ley 1952/2019 | Funciones del instructor | Validación de competencia y rol para incorporar | ✅ Cumple |
| Art. 13 | Ley 2094/2021 | Separación instructor-juzgador | Ambos roles pueden incorporar según competencia | ✅ Cumple |

## Notas Adicionales

- Esta HU-11-01 cubre exclusivamente el **Paso 1: Búsqueda y Selección Múltiple de Expedientes**. Las HU siguientes cubrirán los pasos 2, 3 y 4 del asistente de incorporación.
- El término "incorporación" es equivalente a "acumulación procesal" en la terminología jurídica del CGD.
- La irreversibilidad de la incorporación busca garantizar seguridad jurídica, pero no impide que mediante acto administrativo motivado del superior jerárquico se ordene la separación de procesos cuando se configuren causales legales para ello.
- El sistema debe prevenir la incorporación circular (expediente A incorpora B, B incorpora C, C incorpora A) mediante validación de grafos en la base de datos.
