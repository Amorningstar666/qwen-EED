| **Fecha** | **ID HU** | **Creado por** | **Validado por** |
|-----------|-----------|----------------|------------------|
| 2024-01-15 | HU-15-01 | Agente hu-architect | Líder de Producto PGN |

---

## **MACROPROCESO / PROCESO / ACTIVIDAD**

| **Macroproceso** | **Proceso** | **Actividad** | **Clasificación** | **Valor de Negocio** |
|------------------|-------------|---------------|-------------------|----------------------|
| Control Disciplinario | Investigación Disciplinaria | Consultar término de indagación previa | Funcional - Crítica | Alta - Garantiza el debido proceso y evita la prescripción por vencimiento de términos (Art. 208 CGD) |

---

## **1. DESCRIPCIÓN DE LA HISTORIA DE USUARIO**

### **¿Quién?**
Como **Funcionario de Instrucción** (rol: `instructor`), con competencia asignada según el Art. 76 de la Ley 734 de 2002 (CGD), quien tiene la facultad legal de adelantar las actuaciones de indagación previa.

### **¿Qué?**
Necesito **consultar el widget de términos de la indagación previa** que calcule automáticamente los días hábiles transcurridos y faltantes, visualice el estado del término mediante semáforo (verde/amarillo/rojo), y muestre alertas tempranas de vencimiento, incluyendo el cálculo de prórrogas aplicables por causas de DDHH/DIH o complejidad probatoria.

### **¿Para qué?**
Para **garantizar el cumplimiento del término perentorio de seis (6) meses** establecido en el Artículo 208 de la Ley 734 de 2002 (Código General Disciplinario), evitando la caducidad de la acción disciplinaria, asegurando la legalidad de la actuación, y permitiendo la planificación oportuna de la decisión final (archivo o apertura de investigación).

**Referencia Normativa Directa:**
- **Art. 208 CGD**: "La indagación previa tendrá una duración máxima de seis (6) meses..."
- **Art. 208 Parágrafo CGD**: Prórrogas excepcionales por DDHH/DIH.
- **Art. 12 CGD**: Principio de celeridad y eficacia.
- **Sentencia C-818 de 2005**: Constitucionalidad del término de indagación.

---

## **2. DEPENDENCIAS Y/O PRECONDICIONES**

| # | Dependencia / Precondición | Estado Requerido | Referencia |
|---|----------------------------|------------------|------------|
| 1 | El expediente disciplinario debe estar creado y en estado **"En Indagación Previa"** | Activo | Art. 208 CGD |
| 2 | El usuario autenticado debe tener el rol **`instructor`** asignado mediante acto administrativo de designación | Validado en sesión | Art. 76 CGD + HU-02 (Shell/RBAC) |
| 3 | La fecha de inicio de la indagación previa (`fecha_auto_apertura_indagacion`) debe estar registrada en el sistema | Dato obligatorio | Art. 208 CGD |
| 4 | El calendario oficial colombiano (días hábiles, festivos, puentes) debe estar configurado y actualizado en el motor de cálculo | Configurado | Ley 51 de 1983 (Festivos) |
| 5 | El módulo de notificaciones electrónicas debe estar habilitado para alertas automáticas | Operativo | Art. 122 CGD |
| 6 | La HU-02 (Shell de navegación y autenticación) debe estar implementada y desplegada | Completada | Arquitectura EED |

---

## **3. RESTRICCIONES**

| # | Restricción | Tipo | Justificación Normativa / Técnica |
|---|-------------|------|-----------------------------------|
| 1 | El cálculo de días hábiles **NO puede incluir sábados, domingos ni festivos oficiales** de Colombia | Regla de Negocio | Art. 12 CGD + Jurisprudencia Consejo de Estado sobre cómputo de términos |
| 2 | El widget de semáforo **debe actualizarse en tiempo real** cada vez que se registre una actuación procesal | Técnica | Principio de inmediación y actualización de estado |
| 3 | Las alertas de vencimiento **deben generarse a 30, 15 y 5 días hábiles** antes del vencimiento | Regla de Negocio | Deber de prevención de caducidad (Art. 12 CGD) |
| 4 | El sistema **NO debe permitir registrar actuaciones** si el término ha vencido (bloqueo preventivo) | Seguridad / Legal | Caducidad de la acción disciplinaria (Art. 152 CGD) |
| 5 | La información de prórrogas por DDHH/DIH **debe estar soportada por documento oficial** cargado en el expediente | Validación | Art. 208 Parágrafo CGD |
| 6 | El acceso al widget está **restringido exclusivamente al instructor asignado y su equipo de apoyo** (rol `apoyo_instructor`) | Seguridad | Reserva de actuación (Art. 115 CGD) |
| 7 | El historial de cambios en el cálculo de términos **debe quedar registrado en audit log inmutable** | Auditoría | Art. 76 numeral 10 CGD + Ley 2094 de 2021 |
| 8 | La interfaz debe cumplir con **accesibilidad WCAG 2.1 nivel AA** para funcionarios con discapacidad | Técnica / Legal | Ley 1341 de 2009 + Decreto 19 de 2012 |

---

## **4. SUPUESTOS**

| # | Supuesto | Escenario |
|---|----------|-----------|
| 1 | Se asume que la **fecha de notificación personal del auto de apertura de indagación** es la que inicia el cómputo del término | Si la notificación se realiza fuera de día hábil, el término inicia el siguiente día hábil |
| 2 | Se asume que **existen festivos declarados oficialmente** por el Ministerio del Interior que pueden variar año tras año | El sistema debe consumir API de festivos o tener tabla actualizable anualmente |
| 3 | Se asume que el funcionario instructor **puede solicitar prórroga excepcional** por casos de DDHH/DIH con aprobación del superior jerárquico | La prórroga no puede exceder el 50% del término original (3 meses adicionales máx.) |
| 4 | Se asume que **pueden presentarse suspensiones del término** por fuerzas mayores o situaciones de orden público | El sistema debe permitir pausar el contador y reanudar posteriormente con justificación documentada |

---

## **5. CRITERIOS DE ACEPTACIÓN (Gherkin)**

### **Escenario 1: Visualización exitosa del widget con término vigente (Camino Feliz)**
```gherkin
DADO que el funcionario de instrucción está autenticado con rol "instructor"
Y el expediente EXP-2024-001234 está en estado "En Indagación Previa"
Y la fecha de inicio de indagación fue hace 45 días hábiles
CUANDO el usuario accede a la pestaña "Términos" del módulo de Gestión de Indagación
ENTONCES el sistema debe mostrar un widget de semáforo en color VERDE
Y debe mostrar el texto "Días transcurridos: 45 de 126 días hábiles (6 meses)"
Y debe mostrar la fecha estimada de vencimiento: "Vence: 15 de Agosto de 2024"
Y debe mostrar un indicador de progreso del 35.7%
```

### **Escenario 2: Alerta amarilla por proximidad de vencimiento (Camino Alterno 1)**
```gherkin
DADO que el término de indagación previa está por vencer en 20 días hábiles
Y el expediente no tiene prórroga solicitada
CUANDO el usuario accede al widget de términos
ENTONCES el semáforo debe cambiar a color AMARILLO
Y debe mostrar una alerta visible: "⚠️ Atención: Quedan 20 días hábiles para vencer el término"
Y debe sugerir la acción: "Se recomienda proyectar decisión o solicitar prórroga si aplica"
Y el sistema debe enviar notificación automática al correo institucional del instructor
```

### **Escenario 3: Alerta roja crítica por vencimiento inminente (Camino Alterno 2)**
```gherkin
DADO que el término de indagación previa está por vencer en 5 días hábiles o menos
Y no se ha registrado decisión de archivo o apertura de investigación
CUANDO el usuario accede al widget de términos
ENTONCES el semáforo debe cambiar a color ROJO parpadeante
Y debe mostrar alerta crítica: "🚨 CRÍTICO: Vencimiento inminente en X días hábiles"
Y debe bloquear el registro de nuevas pruebas que no sean urgentes
Y debe notificar automáticamente al Jefe de la Oficina de Control Disciplinario
Y debe registrar evento de riesgo en el audit log con prioridad ALTA
```

### **Escenario 4: Cálculo correcto con prórroga por DDHH/DIH (Camino Alterno 3)**
```gherkin
DADO que el expediente involucra hechos relacionados con DDHH/DIH
Y el instructor ha cargado el acto administrativo de prórroga aprobado (máximo 3 meses)
Y el término original ya había transcurrido en 100 días hábiles
CUANDO el sistema recalcula el término con la prórroga
ENTONCES el nuevo plazo total debe ser de 189 días hábiles (9 meses)
Y el semáforo debe recalcular el porcentaje de avance basado en el nuevo plazo
Y debe mostrar etiqueta: "Prórroga DDHH/DIH activa hasta: [fecha]"
Y debe mostrar el documento de soporte enlazado en el widget
```

### **Escenario 5: Bloqueo por término vencido (Camino de Error)**
```gherkin
DADO que han transcurrido más de 126 días hábiles desde el inicio de la indagación
Y no se ha registrado decisión ni prórroga válida
CUANDO el usuario intenta registrar una nueva actuación procesal
ENTONCES el sistema debe mostrar mensaje de error: "❌ El término de indagación previa ha vencido. No se permiten actuaciones."
Y debe deshabilitar el botón "Registrar Actuación"
Y debe mostrar instrucción: "Proceda a proyectar auto de archivo por caducidad conforme al Art. 152 CGD"
Y debe generar reporte automático de posible caducidad para la Oficina Jurídica
```

### **Escenario 6: Suspensión temporal del término por fuerza mayor (Camino Alterno 4)**
```gherkin
DADO que se presenta una suspensión del término justificada (ej: calamidad pública, imposibilidad de notificar)
Y el instructor carga el acto administrativo de suspensión
CUANDO el sistema procesa la suspensión
ENTONCES el contador de días hábiles debe pausarse
Y debe mostrar etiqueta: "⏸️ Término suspendido desde: [fecha] hasta: [fecha]"
Y los días transcurridos antes de la suspensión deben conservarse
Y al reanudar, el cálculo debe continuar desde donde se pausó
```

### **Escenario 7: Error de acceso por rol no autorizado (Camino de Error)**
```gherkin
DADO que un usuario con rol "ciudadano" o "investigado" intenta acceder al widget de términos
CUANDO el usuario navega a la URL del módulo de Gestión de Indagación
ENTONCES el sistema debe denegar el acceso con código HTTP 403
Y debe mostrar mensaje: "Acceso restringido. Solo funcionarios de instrucción autorizados."
Y debe registrar intento de acceso no autorizado en el audit log de seguridad
```

---

## **6. PROTOTIPO / ANEXOS**

### **Referencia a Pantalla:**
- **Archivo HTML**: `/workspace/Pantallas VEED/15_gestion_indagacion_v1.html`
- **Sección Específica**: Pestaña 1 - "Términos y Alertas"
- **Componentes UX Identificados**:
  - Widget circular de semáforo (verde/amarillo/rojo)
  - Contador de días hábiles transcurridos vs. totales
  - Barra de progreso porcentual
  - Etiquetas de estado: "Vigente", "Por Vencer", "Vencido"
  - Botón de acción: "Solicitar Prórroga"
  - Timeline de hitos del término
  - Panel de alertas notificadas

### **Tokens de Marca PGN Aplicados:**
| Elemento | Token | Valor Hex |
|----------|-------|-----------|
| Color Primario (Encabezados) | `--pgn-navy` | `#063853` |
| Color Semáforo Verde | `--pgn-success` | `#28A745` |
| Color Semáforo Amarillo | `--pgn-warning` | `#FFC107` |
| Color Semáforo Rojo | `--pgn-danger` | `#E3201B` |
| Color Acento (Botones) | `--pgn-yellow` | `#FFE601` |

### **Mockup Referencial:**
```
┌─────────────────────────────────────────────────────────────┐
│  📊 TÉRMINO DE INDAGACIÓN PREVIA                            │
│  Expediente: EXP-2024-001234                                │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│        ╭──────────────╮                                     │
│        │   [SEMÁFORO] │  🟢 VIGENTE                         │
│        │     35.7%    │                                     │
│        ╰──────────────╯                                     │
│                                                             │
│  Días transcurridos: 45 de 126 días hábiles                 │
│  Fecha de inicio: 01 de Febrero de 2024                     │
│  Fecha de vencimiento: 15 de Agosto de 2024                 │
│                                                             │
│  ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━                   │
│  [███████████░░░░░░░░░░░░░░░░░░░░░░░░░] 35.7%               │
│                                                             │
│  ⚠️ Próximos hitos:                                         │
│  • 30 días para vencer: 15 de Julio de 2024                 │
│  • 15 días para vencer: 30 de Julio de 2024                 │
│  • 5 días para vencer: 10 de Agosto de 2024                 │
│                                                             │
│  [📄 Solicitar Prórroga]  [📅 Ver Calendario]               │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## **7. STAKEHOLDERS Y VALIDACIÓN REQUERIDA**

| **Rol** | **Nombre / Área** | **Responsabilidad** | **Firma / Aprobación** |
|---------|-------------------|---------------------|------------------------|
| Dueño del Producto | Dirección de Investigación y Acusación | Validar regla de negocio de términos | Pendiente |
| Líder Técnico | Arquitecto de Software EED | Validar viabilidad técnica del cálculo | Pendiente |
| Asesor Jurídico | Oficina Asesora Jurídica PGN | Validar cumplimiento Art. 208 CGD | Pendiente |
| Usuario Final | Funcionario de Instrucción (rol piloto) | Validar usabilidad del widget | Pendiente |
| Auditor Interno | Oficina de Control Interno | Validar trazabilidad y audit log | Pendiente |

---

## **8. MATRIZ DE TRAZABILIDAD NORMATIVA**

| **Artículo / Norma** | **Requisito Legal** | **Cumplimiento en HU-15-01** | **Estado** |
|----------------------|---------------------|------------------------------|------------|
| Art. 208 CGD | Término máximo 6 meses | Widget calcula 126 días hábiles | ✅ Cumple |
| Art. 208 Parágrafo CGD | Prórroga por DDHH/DIH | Soporte de prórroga documental | ✅ Cumple |
| Art. 12 CGD | Principio de celeridad | Alertas tempranas 30/15/5 días | ✅ Cumple |
| Art. 152 CGD | Caducidad de la acción | Bloqueo por vencimiento | ✅ Cumple |
| Art. 115 CGD | Reserva de actuación | Restricción de acceso por rol | ✅ Cumple |
| Art. 76 numeral 10 CGD | Deber de llevar registro | Audit log inmutable | ✅ Cumple |
| Ley 2094 de 2021 Art. 13 | Separación instructor/juzgador | Acceso solo para instructor | ✅ Cumple |
| Decreto 19 de 2012 | Gobierno Digital - Accesibilidad | WCAG 2.1 AA | ✅ Cumple |

---

## **9. CONSIDERACIONES DE SEGURIDAD Y AUDITORÍA**

### **Seguridad:**
- **Autenticación**: OAuth 2.0 + JWT con validación de rol `instructor`
- **Autorización**: RBAC + ABAC (atributo: `expediente.asignado_a == usuario.id`)
- **Cifrado**: AES-256 para datos en reposo, TLS 1.3 para datos en tránsito
- **Prevención**: Rate limiting en consultas al widget (máx. 100 req/min)

### **Auditoría (Audit Log):**
| **Evento** | **Datos Registrados** | **Inmutabilidad** |
|------------|----------------------|-------------------|
| Consulta de término | usuario_id, expediente_id, timestamp, IP | Blockchain o WORM storage |
| Cambio de estado (semáforo) | estado_anterior, estado_nuevo, causa, usuario | Hash criptográfico |
| Solicitud de prórroga | documento_id, fecha_solicitud, aprobador | Firma digital |
| Alerta generada | tipo_alerta, destinatarios, canal, timestamp | Log centralizado SIEM |

---

## **10. DEFINICIÓN DE TERMINADO (DoD)**

- [ ] Código implementado y probado en ambiente de desarrollo
- [ ] Pruebas unitarias con cobertura ≥ 90%
- [ ] Pruebas de integración con módulo de calendario oficial
- [ ] Pruebas de aceptación ejecutadas con 100% de escenarios Gherkin aprobados
- [ ] Documentación técnica actualizada (Swagger/OpenAPI)
- [ ] Audit log verificado con eventos de prueba
- [ ] Validación jurídica de cálculos de términos
- [ ] Despliegue en ambiente de QA para UAT
- [ ] Capacitación a funcionarios pilotos realizada
- [ ] Aprobación formal del dueño del producto

---

**Fin de la Historia de Usuario HU-15-01**
