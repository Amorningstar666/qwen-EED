# HU-08-01: Búsqueda y Selección de Expedientes Activos para Incorporación Manual

## 1. Identificación de la Historia
| Campo | Valor |
| :--- | :--- |
| **ID** | HU-08-01 |
| **Título** | Búsqueda y Selección de Expedientes Activos para Incorporación Manual |
| **Rol Principal** | Instructor Disciplinario |
| **Roles Secundarios** | Secretario de Instrucción, Juez de Primera Instancia |
| **Prioridad** | ALTA (Crítica para el flujo de acumulación procesal) |
| **Estado** | Pendiente de Desarrollo |
| **Épica Relacionada** | Gestión de Investigación y Acumulación Procesal |
| **Pantalla Asociada** | Pantalla 11: Incorporación Manual (Modal - Paso 1) |
| **Prototipo** | `Pantallas VEED/11_incorporacion_manual.html` |

## 2. Narrativa de Usuario (User Story)

### ¿Quién? (El Que)
Como **Instructor Disciplinario** encargado de la dirección de una investigación en curso (Expediente Principal), que ha identificado la existencia de otras investigaciones abiertas que guardan relación de conexidad por los hechos, los sujetos o la naturaleza de la falta.

### ¿Qué? (El Qué)
Necesito **buscar, filtrar y seleccionar múltiples expedientes que se encuentren en estado ACTIVO** dentro del sistema, mediante un modal especializado de incorporación, validando que cumplan con los requisitos de elegibilidad (mismo estado procesal o anterior, no cerrados ni archivados).

### ¿Para qué? (El Para Qué)
Para **iniciar el proceso técnico de acumulación de expedientes**, asegurando que solo se vinculen procesos vigentes que puedan ser legalmente incorporados al expediente principal, garantizando el principio de unidad de proceso, evitando decisiones contradictorias y centralizando la prueba antes del cierre de la etapa de indagación o instrucción.

## 3. Criterios de Aceptación (Escenarios de Prueba)

### Escenario 1: Búsqueda exitosa por número de expediente (IUS+IUC)
**Dado** que el Instructor se encuentra en el Paso 1 del modal de Incorporación Manual
**Cuando** ingresa un número de expediente válido (ej. `EXP-2024-001234-AGN`) en el campo de búsqueda y presiona "Buscar"
**Entonces** el sistema muestra el expediente en la tabla de resultados indicando claramente su estado **ACTIVO** y habilita el checkbox para su selección.

### Escenario 2: Búsqueda por asunto o palabras clave
**Dado** que el Instructor desea encontrar expedientes relacionados temáticamente
**Cuando** ingresa palabras clave del asunto (ej. "incumplimiento deberes", "contratación") y ejecuta la búsqueda
**Entonces** el sistema lista todos los expedientes **ACTIVOS** que contienen esas palabras en su descripción o carátula, ordenados por fecha de radicación.

### Escenario 3: Filtrado automático de estados no elegibles
**Dado** que solo los expedientes activos pueden ser incorporados
**Cuando** se realiza una búsqueda general
**Entonces** el sistema **oculta o deshabilita** visualmente los expedientes con estado **CERRADO**, **ARCHIVADO** o **INCORPORADO**, mostrando un tooltip que indica: "Expediente no elegible para incorporación".

### Escenario 4: Selección múltiple válida
**Dado** que la incorporación requiere al menos un expediente origen y uno destino
**Cuando** el Instructor marca los checkboxes de dos o más expedientes **ACTIVOS**
**Entonces** el botón "Siguiente" cambia a estado habilitado (color primario PGN) permitiendo avanzar al Paso 2.

### Escenario 5: Validación de selección insuficiente
**Dado** que no se puede incorporar un expediente consigo mismo o sin origen
**Cuando** el Instructor selecciona solo un expediente
**Entonces** el botón "Siguiente" permanece deshabilitado (gris) y muestra el mensaje de ayuda: "Seleccione al menos 2 expedientes para continuar".

### Escenario 6: Visualización de detalles críticos
**Dado** que el Instructor debe verificar la identidad del expediente antes de seleccionar
**Cuando** visualiza la fila de un expediente en la tabla
**Entonces** puede ver claramente: Número de Radicado (IUS+IUC), Asunto resumido, Estado actual (badge verde ACTIVO) y un botón "Ver" para previsualizar metadatos sin salir del modal.

### Escenario 7: Manejo de sin resultados
**Dado** que la búsqueda puede no coincidir con ningún expediente activo
**Cuando** el Instructor busca un término que no existe o solo coincide con expedientes **CERRADOS/ARCHIVADOS**
**Entonces** el sistema muestra un mensaje vacío amigable: "No se encontraron expedientes activos que coincidan con su búsqueda".

## 4. Reglas de Negocio

| ID | Regla de Negocio | Descripción |
| :--- | :--- | :--- |
| **RN-08-01** | **Elegibilidad de Estado** | Únicamente los expedientes con estado **ACTIVO** pueden ser seleccionados para incorporación. Los estados **CERRADO**, **ARCHIVADO** o **INCORPORADO** bloquean la selección. |
| **RN-08-02** | **Cantidad Mínima** | Se deben seleccionar como mínimo **2 expedientes** para iniciar el flujo (uno será el principal, los demás los incorporados). |
| **RN-08-03** | **Ámbito de Búsqueda** | La búsqueda se restringe a los expedientes asignados al despacho del usuario o aquellos a los que tenga permiso de lectura por jerarquía. |
| **RN-08-04** | **Exclusión de Trámites en Curso** | No se pueden seleccionar expedientes que tengan una solicitud de incorporación pendiente de aprobación por otro usuario. |

## 5. Citas Normativas y Marco Legal

*   **Ley 1952 de 2019 (Código General Disciplinario), Artículo 188:** Faculta al instructor para reunir los elementos necesarios para la investigación, incluyendo la acumulación de expedientes por conexidad.
*   **Principio de Unidad de Proceso:** Establece que las conductas relacionadas o los sujetos vinculados deben tramitarse en un mismo expediente para evitar fallos contradictorios y garantizar la economía procesal.
*   **Artículo 14 (Motivación):** Toda actuación administrativa debe estar motivada, lo que incluye la selección técnica de los expedientes a incorporar.

## 6. Dependencias

*   **Módulo Base:** Gestión de Investigaciones (CRUD de Expedientes) debe estar operativo.
*   **Seguridad:** Servicio de Autenticación y Autorización (RBAC) activo para validar permisos de Instructor.
*   **Datos:** Índice de búsqueda de expedientes actualizado en tiempo real.

## 7. Notas Técnicas para el Desarrollador

*   **Endpoint Sugerido:** `GET /api/v1/expedientes/buscar?filtro={texto}&estado=ACTIVO`
*   **UI/UX:**
    *   Utilizar la paleta de colores PGN: Badge verde (`#28a745` o variable `--pgn-success`) para estado ACTIVO.
    *   Implementar *debounce* de 500ms en el input de búsqueda para evitar llamadas excesivas al API.
    *   El checkbox de selección debe estar deshabilitado (`disabled`) si el estado del expediente no es ACTIVO.
*   **Manejo de Errores:** Si la búsqueda falla, mostrar notificación tipo "toast" roja con mensaje: "Error al consultar expedientes. Intente nuevamente."

## 8. Definición de Terminado (DoD)

*   [ ] Código frontend implementado siguiendo el prototipo `11_incorporacion_manual.html`.
*   [ ] Conexión con API de búsqueda de expedientes verificada.
*   [ ] Validaciones de estado (ACTIVO vs CERRADO/ARCHIVADO/INCORPORADO) funcionando correctamente.
*   [ ] Pruebas unitarias de los 7 escenarios aprobadas por QA.
*   [ ] Desplegado en ambiente de pruebas para validación del Instructor.