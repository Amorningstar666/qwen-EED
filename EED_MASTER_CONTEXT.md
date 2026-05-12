# 🏛️ EED - Expediente Electrónico Disciplinario
## Procuraduría General de la Nación de Colombia

**Documento Maestro de Contexto e Instrucciones**  
**Versión:** 1.0 | **Última actualización:** 2026-05-12

---

## 📌 PROPÓSITO DE ESTE DOCUMENTO

Este archivo centraliza TODO el contexto necesario para trabajar en el proyecto EED sin necesidad de leer múltiples carpetas. Úsalo como punto de partida en cada sesión.

### ⚡ Cómo usar este documento

**Opción rápida (recomendada):**
```
"Basado en el EED_MASTER_CONTEXT.md, [tu solicitud específica]"
```

**Ejemplos:**
- *"Basado en el EED_MASTER_CONTEXT.md, genera la HU-08 para el módulo de Investigación Disciplinaria"*
- *"Basado en el EED_MASTER_CONTEXT.md, revisa si el diseño de la pantalla de Notificaciones cumple con el Art. 133 CGD"*
- *"Basado en el EED_MASTER_CONTEXT.md, ¿qué agentes debo activar para validar un prototipo de juzgamiento?"*

---

## 🔗 LINKS DIRECTOS A ARCHIVOS CLAVE

### 🧠 Sistema de Agentes (`/workspace/claude/`)

| Archivo | Propósito | Cuándo usarlo |
|---|---|---|
| [`claude/instructions.md`](/workspace/claude/instructions.md) | **Super Orquestador EED** - Coordina todos los agentes especializados | Para tareas complejas que requieren múltiples validaciones (legal + UX + técnico) |
| [`claude/agents/hu-architect.md`](/workspace/claude/agents/hu-architect.md) | Generador de Historias de Usuario formato PGN con Gherkin | Cuando necesites documentar requerimientos funcionales |
| [`claude/agents/legal-compliance.md`](/workspace/claude/agents/legal-compliance.md) | Validador jurídico contra Código General Disciplinario | Para verificar cumplimiento normativo de cualquier entregable |
| [`claude/agents/ux-designer.md`](/workspace/claude/agents/ux-designer.md) | Diseñador UI/UX con tokens de marca PGN | Para crear prototipos y componentes visuales |
| [`claude/agents/qa-critic.md`](/workspace/claude/agents/qa-critic.md) | Revisor crítico de calidad, gaps y riesgos | Antes de entregar cualquier producto final |
| [`claude/agents/tech-architect.md`](/workspace/claude/agents/tech-architect.md) | Arquitecto técnico STI Gobierno Digital | Para definir arquitectura, integraciones y seguridad |
| [`claude/memory/EED_INSTRUCCIONES_PROYECTO.md`](/workspace/claude/memory/EED_INSTRUCCIONES_PROYECTO.md) | **Memoria completa del proyecto** - Flujo procesal detallado | Como referencia jurídica y funcional exhaustiva |
| [`claude/memory/EED_PROJECT_MEMORY.md`](/workspace/claude/memory/EED_PROJECT_MEMORY.md) | Decisiones tomadas, iteraciones y trazabilidad | Para consultar precedentes del proyecto |

### 📂 Historias de Usuario Documentadas

| Módulo | Ubicación | Estado |
|---|---|---|
| **HU-01: Login EED** | [`/workspace/Proyecto Expediente Electronico/Historias/HU-01_Login_EED.docx`](/workspace/Proyecto%20Expediente%20Electronico/Historias/HU-01_Login_EED.docx) | ✅ Documentado |
| **HU-02: Shell por Roles** | [`/workspace/Proyecto Expediente Electronico/Historias/HU-02-Shell/`](/workspace/Proyecto%20Expediente%20Electronico/Historias/HU-02-Shell/) | ✅ 6 roles documentados |
| **HU-03: Radicación Noticia** | [`/workspace/Proyecto Expediente Electronico/Historias/HU-03-Radicacion%20noticia/`](/workspace/Proyecto%20Expediente%20Electronico/Historias/HU-03-Radicacion%20noticia/) | ✅ 5 documentos |
| **HU-04: Reparto** | [`/workspace/Proyecto Expediente Electronico/Historias/HU-04-REPARTO/`](/workspace/Proyecto%20Expediente%20Electronico/Historias/HU-04-REPARTO/) | 📁 En revisión |
| **HU-05: Evaluación Noticia** | [`/workspace/Proyecto Expediente Electronico/Historias/HU-05-Evaluacion_Noticia_Disciplinaria/`](/workspace/Proyecto%20Expediente%20Electronico/Historias/HU-05-Evaluacion_Noticia_Disciplinaria/) | 📁 En revisión |
| **HU-06: Decisión Inhibitoria** | [`/workspace/Proyecto Expediente Electronico/Historias/HU-06%20Decision%20Inhibitoria/`](/workspace/Proyecto%20Expediente%20Electronico/Historias/HU-06%20Decision%20Inhibitoria/) | 📁 En revisión |
| **HU-07: Indagación** | [`/workspace/Proyecto Expediente Electronico/Historias/HU-07_INDAGACION/`](/workspace/Proyecto%20Expediente%20Electronico/Historias/HU-07_INDAGACION/) | 📁 En revisión |

---

## 🎯 EJEMPLOS DE PROMPTS LISTOS PARA COPIAR/PEGAR

### 📝 Generar Historia de Usuario Nueva
```markdown
Basado en el EED_MASTER_CONTEXT.md y usando el agente hu-architect:

Genera la HU-08 para el módulo de "Investigación Disciplinaria - Auto de Apertura" siguiendo el formato obligatorio PGN.

Contexto:
- Rol: Funcionario de Instrucción
- Etapa CGD: Investigación Disciplinaria (Art. 211-216 CGD)
- Acción: Generar auto de apertura de investigación disciplinaria
- Requisitos legales: Debe incluir todos los elementos del Art. 215 CGD

Entregables esperados:
1. Historia de usuario completa con estructura PGN
2. Criterios de aceptación en Gherkin con validación normativa
3. Referencia a prototipo de pantalla
4. Dependencias y precondiciones legales
```

### 🎨 Diseñar Pantalla con Validación Legal
```markdown
Basado en el EED_MASTER_CONTEXT.md, activa los modos ux_designer y legal_compliance:

Diseña la pantalla de "Notificaciones Personales y Electrónicas" para el módulo de Juzgamiento.

Requisitos:
- Cumplir Art. 121, 122, 123, 127 y 133 CGD (notificaciones)
- Aplicar tokens de marca PGN (#063853, #FFE601, #E3201B)
- Tipografía: Montserrat (títulos), Poppins (cuerpo)
- Incluir widget de términos con cálculo en días hábiles colombianos
- Botón flotante procuradurIA con trazabilidad auditada

Entregables:
1. Prototipo HTML/CSS funcional
2. Validación legal artículo por artículo
3. Justificación UX de decisiones de diseño
4. Criterios de accesibilidad WCAG 2.1 AA
```

### 🔍 Validar Entregable Existente
```markdown
Basado en el EED_MASTER_CONTEXT.md, activa el modo qa_critic:

Revisa críticamente las historias de usuario del módulo HU-03 (Radicación de Noticia) ubicadas en /workspace/Proyecto Expediente Electronico/Historias/HU-03-Radicacion noticia/

Checklist de validación:
- ¿Cumplen formato PGN obligatorio?
- ¿Tienen criterios Gherkin testeables?
- ¿Citan normas CGD aplicables?
- ¿Consideran reserva de proceedings (Art. 115 CGD)?
- ¿Hay gaps funcionales o riesgos de nulidad?

Entrega:
1. Issues críticos con impacto y acción requerida
2. Mejoras sugeridas con beneficio
3. Fortalezas identificadas
4. Recomendación final: Aprobar | Iterar | Rechazar
```

### 🏗️ Definir Arquitectura Técnica
```markdown
Basado en el EED_MASTER_CONTEXT.md, activa el modo technical_architect:

Define la arquitectura técnica para el módulo de "Impedimentos y Recusaciones" (Art. 104-108 CGD).

Requisitos técnicos:
- Integración con DOKUS para notificaciones
- OAuth 2.0 + JWT para autenticación
- AES-256 para datos sensibles, TLS 1.3 en tránsito
- Audit logs inmutables con timestamp certificado
- Cálculo de términos en días hábiles (calendario oficial colombiano)
- Interoperabilidad: export PDF/A + XML, reporte SIRI/SCC

Entregables:
1. Diagrama de componentes
2. Especificación de interfaces API
3. Requisitos no funcionales (seguridad, performance, escalabilidad)
4. Puntos de integración y contratos de interfaz
5. Riesgos técnicos y mitigaciones
```

### ⚖️ Consultar Marco Normativo
```markdown
Basado en el EED_MASTER_CONTEXT.md y EED_INSTRUCCIONES_PROYECTO.md:

¿Cuáles son los términos perentorios para la etapa de Indagación Previa según el Art. 208 CGD y sus prorrogas?

Adicionalmente:
- ¿Qué decisiones puede tomar el funcionario al finalizar la indagación?
- ¿Qué recursos proceden contra cada decisión?
- ¿Cómo se calculan los términos en días hábiles colombianos?

Incluye cita textual de los artículos aplicables.
```

---

## 🗺️ MAPA MENTAL DEL PROYECTO (1 PÁGINA)

```
┌─────────────────────────────────────────────────────────────────────────────────┐
│                    EED - EXPEDIENTE ELECTRÓNICO DISCIPLINARIO                   │
│                    Procuraduría General de la Nación                            │
│                    Ley 1952/2019 mod. Ley 2094/2021 (CGD)                       │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
         ┌────────────────────────────┼────────────────────────────┐
         ▼                            ▼                            ▼
┌─────────────────┐      ┌──────────────────┐      ┌─────────────────────┐
│  MARCO LEGAL    │      │   ARQUITECTURA   │      │     USUARIOS        │
│                 │      │                  │      │                     │
│ • Ley 1952/2019 │      │ • API-first      │      │ Internos:           │
│ • Ley 2094/2021 │      │ • Modular        │      │ • Jefe Dependencia  │
│ • Decreto 1081  │      │ • DOKUS-ready    │      │ • Func. Instrucción │
│ • Decreto 1083  │      │ • OAuth 2.0+JWT  │      │ • Func. Juzgamiento │
│ • Ley 1581/2012 │      │ • AES-256/TLS1.3 │      │ • Secretario Juríd. │
│ • Ley 1712/2014 │      │ • Audit inmutable│      │ • Revisor           │
│                 │      │ • PDF/A + XML    │      │ • Aprobador         │
│ Principios:     │      │                  │      │                     │
│ • Debido proceso│      │ Tokens PGN:      │      │ Externos:           │
│ • Presunción    │      │ • #063853 (azul) │      │ • Quejoso           │
│   inocencia     │      │ • #FFE601 (amar) │      │ • Disciplinado      │
│ • Defensa       │      │ • #E3201B (rojo) │      │ • Defensor          │
│ • Celeridad     │      │ • Montserrat     │      │ • Víctimas          │
│ • Reserva       │      │ • Poppins        │      │                     │
└─────────────────┘      └──────────────────┘      └─────────────────────┘
                                      │
         ┌────────────────────────────┼────────────────────────────┐
         ▼                            ▼                            ▼
┌─────────────────────────────────────────────────────────────────────────────────┐
│                           FLUJO PROCESAL (CGD)                                  │
│                                                                                 │
│  BLOQUE 0: EVALUACIÓN NOTICIA DISCIPLINARIA (Art. 86 CGD)                       │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │ Tipos: Queja, Info servidor, De oficio, Anónimo, Otro medio            │   │
│  │ Decisiones: Inhibitorio │ Indagación │ Investigación │ Traslado       │   │
│  │           Acumulación │ Compulsa copias │ Devolución │ Incorporación  │   │
│  └─────────────────────────────────────────────────────────────────────────┘   │
│                                    │                                            │
│         ┌──────────────────────────┼──────────────────────────┐                │
│         ▼                          ▼                          ▼                │
│  ┌─────────────┐         ┌─────────────────┐        ┌─────────────────┐       │
│  │ BLOQUE 1:   │         │ BLOQUE 2:       │        │ BLOQUE 3:       │       │
│  │ INHIBITORIO │         │ TRASLADO/       │        │ IMPEDIMENTOS/   │       │
│  │             │         │ COMPETENCIA     │        │ RECUSACIONES    │       │
│  │ Art. 209    │         │ Art. 76, 91-101 │        │ Art. 104-108    │       │
│  │ • Cierra    │         │ • Poder pref.   │        │ • Suspende      │       │
│  │   expediente│         │ • Incompetencia │        │   términos      │       │
│  │ • Sin       │         │ • Conflicto     │        │ • 3 días decidir│       │
│  │   actuación │         │   competencia   │        │                 │       │
│  └─────────────┘         └─────────────────┘        └─────────────────┘       │
│                                    │                                            │
│                                    ▼                                            │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │ BLOQUE 4: INSTRUCCIÓN                                                   │   │
│  │                                                                         │   │
│  │  ETAPA A: INDAGACIÓN PREVIA (Art. 208 CGD)                              │   │
│  │  • Término: 6 meses (+6 DDHH/DIH)                                       │   │
│  │  • Finalidad: Identificar autor                                         │   │
│  │  • Decisiones: Archivo │ Apertura investigación                         │   │
│  │                                                                         │   │
│  │  ETAPA B: INVESTIGACIÓN DISCIPLINARIA (Art. 211-216 CGD)                │   │
│  │  • Término: 6 meses (+6/+18 DDHH/DIH)                                   │   │
│  │  • Auto apertura (Art. 215): Elementos obligatorios                     │   │
│  │  • Medidas preventivas: Suspensión provisional (Art. 127)               │   │
│  │  • Pruebas: Decretar, practicar, valorar                                │   │
│  │  • Alegatos precalificatorios: 10 días (Art. 220)                       │   │
│  │                                                                         │   │
│  │  ETAPA C: CALIFICACIÓN PROVISIONAL (Art. 221-222 CGD)                   │   │
│  │  • Pliego de cargos: Elementos obligatorios                             │   │
│  │  • Traslado alegatos: 10 días                                           │   │
│  │  • Audiencia preliminar                                                 │   │
│  └─────────────────────────────────────────────────────────────────────────┘   │
│                                    │                                            │
│                                    ▼                                            │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │ BLOQUE 5: JUZGAMIENTO                                                   │   │
│  │                                                                         │   │
│  │  • Juicio verbal disciplinario (Art. 225A-H CGD)                        │   │
│  │  • Pruebas en juicio                                                    │   │
│  │  • Alegatos finales                                                     │   │
│  │  • Fallo: Absolutorio │ Condenatorio                                    │   │
│  │  • Notificación personal (Art. 121, 133)                                │   │
│  └─────────────────────────────────────────────────────────────────────────┘   │
│                                    │                                            │
│                                    ▼                                            │
│  ┌─────────────────────────────────────────────────────────────────────────┐   │
│  │ BLOQUE 6: SEGUNDA INSTANCIA Y EJECUCIÓN                                 │   │
│  │                                                                         │   │
│  │  • Apelación (Art. 224 CGD)                                             │   │
│  │  • Doble conformidad                                                    │   │
│  │  • Ejecución de sanción                                                 │   │
│  │  • Reporte sistemas estatales (SIRI/SCC)                                │   │
│  └─────────────────────────────────────────────────────────────────────────┘   │
│                                                                                 │
│  ═══════════════════════════════════════════════════════════════════════════   │
│  ACTUACIONES TRANSVERSALES (aplican en todo el flujo):                          │
│  • Nulidades • Revocatoria directa • Tutela • Petición • Acumulación           │
│  ═══════════════════════════════════════════════════════════════════════════   │
└─────────────────────────────────────────────────────────────────────────────────┘
                                      │
         ┌────────────────────────────┼────────────────────────────┐
         ▼                            ▼                            ▼
┌─────────────────┐      ┌──────────────────┐      ┌─────────────────────┐
│  AGENTES IA     │      │  ENTREGABLES     │      │   GOBERNANZA IA     │
│                 │      │                  │      │                     │
│ • Orquestador   │      │ • Pantallas HTML │      │ • procuradurIA:     │
│ • HU Architect  │      │ • Historias HU   │      │   - Solo asiste     │
│ • Legal Comp.   │      │ • Validaciones   │      │   - Nunca decide    │
│ • UX Designer   │      │ • Arquitectura   │      │   - Trazabilidad    │
│ • QA Critic     │      │ • Decision log   │      │   - Consentimiento  │
│ • Tech Arch.    │      │                  │      │   - Audit log       │
│                 │      │ Formato PGN:     │      │                     │
│ Trigger words:  │      │ • ID HU-XX       │      │ Límites éticos:     │
│ Ver docs agents │      │ • Quién/Qué/     │      │ • Datos sensibles:  │
│                 │      │ • Para qué       │      │   anonimizar        │
│                 │      │ • Gherkin        │      │ • Nullity risks:    │
│                 │      │ • Norma citada   │      │   alertar siempre   │
└─────────────────┘      └──────────────────┘      └─────────────────────┘
```

---

## 📋 RESUMEN EJECUTIVO DEL PROYECTO

### ¿Qué es el EED?
Sistema de información institucional para digitalizar, orquestar y garantizar la validez jurídica del **proceso disciplinario** de la Procuraduría General de la Nación.

### Objetivo Principal
Reemplazar el expediente físico por un **expediente electrónico jurídicamente válido**, seguro, interoperable y usable.

### Características Clave
| Característica | Descripción |
|---|---|
| **Validez Jurídica** | Cumplimiento total CGD (Ley 1952/2019 + Ley 2094/2021) |
| **Seguridad** | OAuth 2.0+JWT, AES-256, TLS 1.3, audit logs inmutables |
| **Interoperabilidad** | DOKUS, PDF/A+XML, SIRI/SCC, firma digital con timestamp |
| **Usabilidad** | Tokens PGN, WCAG 2.1 AA, roles diferenciados |
| **Trazabilidad** | Toda acción queda registrada con usuario, timestamp, contexto |
| **IA Ética** | procuradurIA solo asiste, nunca decide, con consentimiento explícito |

### Reglas de Diseño Críticas
1. **El expediente existe desde la radicación**: Independientemente del resultado (inhibición, traslado, etc.), siempre hay número de radicado.
2. **Separación instructor/juzgador**: Separación funcional reforzada a nivel de permisos (RBAC/ABAC).
3. **Reserva por etapa (Art. 115 CGD)**: Controles de acceso diferenciados según estado procesal.
4. **Términos en días hábiles**: Cálculo automático con calendario oficial colombiano.
5. **Anti-hallucination**: Si hay duda sobre norma, declarar incertidumbre y recomendar revisión legal humana.

---

## 🚀 PRÓXIMOS PASOS RECOMENDADOS

1. **Módulos pendientes de HU**: HU-04 a HU-07 necesitan revisión y completación
2. **Prototipos faltantes**: Juzgamiento, Segunda Instancia, Ejecución de Sanción
3. **Integraciones técnicas**: Definir contratos API con DOKUS y sistemas externos
4. **Validación legal completa**: Cada módulo debe pasar por legal_compliance mode

---

## 📋 ESTÁNDAR DE HISTORIAS DE USUARIO PGN - LECCIONES APRENDIDAS (HU-08)

### ✅ Estructura Obligatoria Detectada en HU-08 (Referencia)

Cada historia de usuario hija debe contener **mínimo 15-20 párrafos/tablas** con la siguiente estructura:

| Sección | Contenido Mínimo | Ejemplo HU-08 |
|---|---|---|
| **Encabezado** | Fecha, ID HU, Creado por, Validado por, Macroproceso, Proceso, Actividad, Clasificación, Valor de negocio | HU-08-01 a HU-08-05 |
| **DESCRIPCIÓN** | ¿Quién?, ¿Qué?, ¿Para qué? con referencias normativas explícitas | Funcionario Instrucción + Art. 215 CGD |
| **DEPENDENCIAS** | Mínimo 3 condiciones previas + artículos CGD aplicables | Expediente creado, rol asignado, shell activo |
| **RESTRICCIONES** | Mínimo 5 reglas de negocio/normativas/técnicas | Separación instructor/juzgador, reserva, términos |
| **SUPUESTOS** | Mínimo 3 escenarios operativos asumidos | Calendario oficial, firma digital, sesión timeout |
| **CRITERIOS ACEPTACIÓN** | Mínimo 3 escenarios Gherkin (Feliz/Alterno/Error) con validación normativa | Escenarios detallados con Dado/Cuando/Entonces |
| **PROTOTIPO** | Referencia al HTML específico + componentes UX identificados | 08_auto_apertura_investigacion.html |
| **STAKEHOLDERS** | Lista de roles con firma pendiente | Funcionario, Oficina Control Interno, Área Jurídica |

### 🔢 Regla de Desglose de Historias Hijas

**Para módulos complejos con múltiples pestañas/funciones:**
- **1 historia hija por funcionalidad crítica** identificada en el prototipo HTML
- **No agrupar** funcionalidades distintas en una sola HU
- **Identificar** cada HU hija con formato `HU-XX-YY` donde XX=padre, YY=hija

### 📊 Ejemplo Aplicado: HU-15 Gestión Indagación Previa

Basado en pantalla `15_gestion_indagacion_v1.html` con 5 pestañas + funciones críticas:

| ID HU Hija | Nombre | Funcionalidad | Base Legal | Prioridad |
|---|---|---|---|---|
| **HU-15-01** | Consultar término de indagación previa | Widget semáforo con cálculo días hábiles, alertas vencimiento, prórrogas DDHH/DIH | Art. 208 CGD | 🔴 Alta |
| **HU-15-02** | Gestionar pruebas de identificación | Tabla de pruebas (documental, pericial, testimonial), estados, libramiento de oficios | Art. 208 + Art. 214 CGD | 🔴 Alta |
| **HU-15-03** | Visualizar persona en averiguación | Card informativa sin vinculación formal, datos de identificación | Art. 208 CGD | 🟡 Media |
| **HU-15-04** | Gestionar documentos del expediente | Carga, consulta y descarga con reserva de actuación | Art. 115 + Art. 121-123 CGD | 🟡 Media |
| **HU-15-05** | Registrar actuaciones procesales | Formulario de nuevas actuaciones con trazabilidad auditada | Art. 208 CGD | 🔴 Alta |
| **HU-15-06** | Consultar historial (audit log) | Timeline inmutable de todas las actuaciones | Art. 76 CGD + Ley 2094/2021 | 🟢 Baja |
| **HU-15-07** | Proyectar decisión final | Auto de archivo o apertura investigación disciplinaria | Art. 208 parágrafo + Art. 214/215 CGD | 🔴 Crítica |

### ⚠️ Errores Comunes a Evitar

1. ❌ **HU demasiado cortas** (<10 párrafos) - No cumplen estándar PGN
2. ❌ **Falta de citación normativa** - Cada criterio debe referenciar artículo CGD
3. ❌ **Criterios Gherkin genéricos** - Deben ser testeables y específicos
4. ❌ **Agrupar funcionalidades** - 1 HU = 1 funcionalidad atómica
5. ❌ **Olvidar supuestos operativos** - Contexto técnico y de negocio explícito
6. ❌ **Sin referencia a prototipo** - Siempre vincular al HTML correspondiente

### ✅ Checklist de Validación Antes de Entregar HU

- [ ] ¿Tiene mínimo 15-20 párrafos/tablas de contenido detallado?
- [ ] ¿Incluye mínimo 3 dependencias con artículos CGD?
- [ ] ¿Incluye mínimo 5 restricciones (negocio + técnicas + legales)?
- [ ] ¿Incluye mínimo 3 supuestos operativos?
- [ ] ¿Tiene mínimo 3 escenarios Gherkin (feliz, alterno, error)?
- [ ] ¿Cita normas CGD en cada sección aplicable?
- [ ] ¿Referencia prototipo HTML específico?
- [ ] ¿Lista stakeholders con validación pendiente?
- [ ] ¿Incluye tabla de validación normativa explícita?
- [ ] ¿Considera seguridad, auditoría y accesibilidad WCAG 2.1 AA?

---

## 📞 CONTACTO Y REFERENCIAS

- **Elaborado por**: Nathalia Carvajal
- **Fuentes oficiales**: 
  - Texto completo CGD: [Ley 1952 de 2019](https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=56610)
  - Modificaciones: [Ley 2094 de 2021](https://www.funcionpublica.gov.co/eva/gestornormativo/norma.php?i=173356)
  - Manual de Marca PGN: Documento interno institucional

---

*Documento vivo - Se actualiza con cada iteración del proyecto*
