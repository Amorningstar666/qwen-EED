# Historia de Usuario

| Fecha | ID HU | Creado por | Validado por | Estado |
|-------|-------|------------|--------------|--------|
| 13/05/2026 | HU-15-07 | Analista de Negocio | Líder Técnico / Oficina Jurídica | Pendiente |

## Información General

| Macroproceso | Proceso | Actividad | Clasificación | Valor de Negocio |
|--------------|---------|-----------|---------------|------------------|
| M4-Gestión Jurídica Disciplinaria | P17-Apoyo a la Investigación Disciplinaria | A37-Decisión de Indagación Previa | Funcionalidad Crítica | Permite culminar la etapa de indagación previa con decisión motivada de archivo o apertura, garantizando el debido proceso y los términos del Art. 208 CGD |

### Descripción

**¿Quién?** 
El Funcionario de Instrucción (rol: instructor) quien tiene la competencia legal para evaluar el material probatorio recolectado durante la indagación previa y proyección de la decisión correspondiente.

**¿Qué?** 
Proyecta la decisión final de la etapa de Indagación Previa, seleccionando entre dos opciones excluyentes: (1) Proyección de Auto de Archivo por falta de mérito para investigar, o (2) Proyección de Auto de Apertura de Investigación Disciplinaria cuando existen motivos graves y fundados.

**¿Para qué?** 
Para dar cumplimiento al término perentorio de seis (6) meses establecido en el artículo 208 de la Ley 1952 de 2019, garantizando que toda decisión esté debidamente motivada, notificada y permita los recursos legales correspondientes, evitando la caducidad de la acción disciplinaria.

**Referencias Normativas:**
- **Ley 1952 de 2019 (CGD):** Art. 208 (Indagación Previa - Término y decisión), Art. 214 (Ruptura de la unidad procesal), Art. 215 (Apertura de la investigación disciplinaria), Art. 224 (Recurso de apelación).
- **Ley 2094 de 2021:** Art. 13 (Separación de funciones), Art. 38 (Debido proceso).
- **Decreto 1083 de 2015:** Notificaciones electrónicas y gestión documental.
- **Acuerdo 01 de 2023 PGN:** Lineamientos para proyección de actos administrativos.
- **Sentencia C-579/2013 Corte Constitucional:** Motivación de decisiones disciplinarias.

## Dependencias y Precondiciones

1. La indagación previa debe haber agotado todas las actuaciones probatorias necesarias (HU-15-02 completada).
2. El término de seis (6) meses de indagación previa no debe estar vencido al momento de proyectar la decisión.
3. Debe existir el material probatorio suficiente en el expediente digital para fundamentar la decisión.
4. El usuario debe tener rol de "Instructor" activo y asignado al expediente.
5. Debe estar habilitado el módulo de notificaciones electrónicas para envío automático tras aprobación.
6. El sistema debe contar con plantillas pre-aprobadas de Autos de Archivo y Apertura.
7. Debe existir validación de que no hay procesos de suspensión activos que impidan la decisión.

## Restricciones

1. **Exclusividad:** Solo se permite una decisión final por indagación previa; una vez ejecutoriada, no puede modificarse salvo por recurso de apelación.
2. **Término Perentorio:** El sistema debe bloquear la proyección si el término de 6 meses está vencido (caducidad).
3. **Motivación Obligatoria:** No se permite proyectar sin diligenciar los campos de fundamentación fáctica y jurídica.
4. **Separación Funcional:** El mismo funcionario que proyecta no puede aprobar si requiere firma de superior jerárquico según nivel.
5. **No Recurso contra Archivo Parcial:** El auto de archivo parcial no tiene recurso (Art. 208 parágrafo CGD), solo el total.
6. **Reserva:** La decisión permanece en reserva hasta tanto sea notificada personalmente al investigado.
7. **Integridad:** Una vez firmada digitalmente, la decisión no puede ser alterada; cualquier corrección requiere acto administrativo posterior.
8. **Notificación Personal:** El auto de apertura requiere notificación personal obligatoria dentro de los 5 días siguientes.

## Reglas de Negocio

1. **RN-01:** El sistema debe validar automáticamente que la fecha de proyección esté dentro del término de 6 meses contado desde la apertura de la indagación.
2. **RN-02:** Si se selecciona "Archivo", el sistema debe exigir especificar si es archivo total o parcial (respecto a algunos hechos o personas).
3. **RN-03:** Si se selecciona "Apertura", el sistema debe exigir la descripción clara de los cargos imputados, hechos constitutivos de falta y normas presuntamente violadas.
4. **RN-04:** Para archivo parcial, el sistema debe mantener abierto el expediente respecto a los hechos o personas no archivadas.
5. **RN-05:** El sistema debe generar automáticamente el calendario de términos para la siguiente etapa si hay apertura (investigación disciplinaria: 6 meses prorrogables).
6. **RN-06:** La proyección debe pasar por flujo de aprobación según nivel jerárquico antes de convertirse en acto administrativo.
7. **RN-07:** El sistema debe verificar que todos los documentos probatorios estén debidamente allegados antes de permitir proyectar decisión.
8. **RN-08:** Tras la notificación del auto de apertura, el sistema debe cambiar automáticamente el estado del expediente a "En Investigación Disciplinaria".
9. **RN-09:** El auto de archivo total debe cerrar el expediente y activar la tabla de retención documental.
10. **RN-10:** Debe quedar registro de la fecha exacta de proyección para cálculo de términos de notificación.

## Supuestos

1. Se asume que el funcionario conoce los elementos estructurales de la falta disciplinaria (típica, antijurídica, culpable).
2. Se asume que las plantillas de autos están actualizadas conforme a la jurisprudencia vigente.
3. Se asume que el sistema de firma digital está operativo y los certificados son válidos.
4. Se asume que la conectividad permite la notificación electrónica inmediata tras la aprobación.
5. Se asume que no hay fallas en el servicio de correo certificado para notificaciones personales.

## Criterios de Aceptación (Gherkin)

**Escenario 1: Proyección exitosa de Auto de Archivo Total**
Dado que soy un Funcionario de Instrucción con un expediente en indagación previa
Cuando selecciono la opción "Proyectar Decisión" y elijo "Archivo Total"
Y diligencio la fundamentación fáctica y jurídica de la ausencia de mérito
Entonces el sistema valida que estoy dentro del término de 6 meses
Y genera el proyecto de Auto de Archivo Total con la plantilla aprobada
Y lo envía a la bandeja del aprobador correspondiente.

**Escenario 2: Proyección exitosa de Auto de Apertura**
Dado que existen motivos graves y fundados en el material probatorio
Cuando selecciono la opción "Proyectar Decisión" y elijo "Apertura Investigación"
Y describo los cargos, hechos y normas presuntamente violadas
Entonces el sistema valida la completitud de los campos obligatorios
Y genera el proyecto de Auto de Apertura de Investigación Disciplinaria
Y calcula automáticamente la nueva fecha de vencimiento (6 meses + prórrogas).

**Escenario 3: Validación de término vencido**
Dado que el término de indagación previa ha superado los 6 meses calendario
Cuando intento proyectar una decisión final
Entonces el sistema bloquea la acción con mensaje de error "Término vencido - Caducidad de la acción"
Y registra el incidente en el log de alertas jurídicas.

**Escenario 4: Archivo Parcial sin recurso**
Dado que decido archivar solo respecto a uno de varios investigados
Cuando proyecto "Archivo Parcial"
Entonces el sistema indica claramente que esta decisión no admite recurso de apelación (Art. 208 parágrafo)
Y mantiene el expediente abierto para los demás investigados.

**Escenario 5: Validación de campos obligatorios en apertura**
Dado que selecciono "Apertura Investigación"
Cuando intento guardar sin diligenciar los cargos imputados
Entonces el sistema muestra mensaje de error "Campo obligatorio: Descripción de cargos"
Y no permite avanzar hasta completar la información.

**Escenario 6: Flujo de aprobación**
Dado que he proyectado un Auto de Apertura
Cuando el aprobador revisa el proyecto
Y lo aprueba con firma digital
Entonces el sistema convierte el proyecto en acto administrativo oficial
Y activa el proceso de notificación personal automática.

**Escenario 7: Error por documentos faltantes**
Dado que intento proyectar decisión sin haber allegado pruebas clave
Cuando el sistema detecta que faltan documentos requeridos según tipo de falta
Entonces muestra advertencia "Existen documentos pendientes de allegación"
Y permite continuar solo con justificación explícita del funcionario.

**Escenario 8: Notificación fallida**
Dado que fue aprobado un Auto de Apertura
Cuando el sistema intenta notificar personalmente y falla por datos incorrectos del investigado
Entonces genera alerta "Notificación fallida - Revisar datos de contacto"
Y pausa el cómputo de términos hasta subsanar el error.

## Prototipo / Anexos

- **Pantalla Referencia:** `Pantallas VEED/15_gestion_indagacion_v1.html` (Sección: Botón "Proyectar Decisión" y Modal emergente)
- **Componentes UX:**
  - Botón primario "Proyectar Decisión Final" habilitado solo si cumple precondiciones.
  - Modal con selector de tipo de decisión (Radio button: Archivo Total / Archivo Parcial / Apertura).
  - Formulario dinámico que cambia campos según selección:
    - Para Archivo: Campo de texto para fundamentación de ausencia de mérito.
    - Para Apertura: Campos estructurados para cargos, hechos, normas violadas, pruebas trasladadas.
  - Validador de términos en tiempo real (semáforo verde/rojo).
  - Vista previa del documento generado con plantilla institucional.
  - Botones de acción: "Guardar Borrador", "Enviar a Aprobación", "Cancelar".
- **Estilos:** Fuente Poppins, colores PGN (#063853 fondo, #E3201B para alertas críticas de término).

## Stakeholders

- **Funcionario de Instrucción:** Proyecta la decisión.
- **Jefe de la Dependencia / Superior Jerárquico:** Aprueba o rechaza el proyecto.
- **Secretaría Judicial:** Gestiona notificaciones y seguimiento de términos.
- **Investigado y Defensor:** Destinatarios de la decisión, ejercen derecho de defensa.
- **Oficina Jurídica:** Revisión de legalidad de los autos proyectados.
- **Sistema de Gestión Documental:** Almacena y conserva la decisión final.

## Plan de Validación

1. **Prueba de Términos:** Verificar que el sistema bloquee proyecciones fuera del término de 6 meses con casos de prueba de fechas límite.
2. **Prueba de Plantillas:** Validar que los autos generados cumplan con la estructura exigida por la Oficina Jurídica.
3. **Prueba de Flujo:** Simular todo el ciclo desde proyección hasta notificación exitosa.
4. **Validación Legal:** Revisión de 10 casos reales por la Oficina Jurídica para confirmar que la lógica de negocio refleja correctamente el Art. 208, 214 y 215 CGD.
5. **Prueba de Carga:** Evaluar generación simultánea de 50 decisiones en hora pico.
6. **UX Testing:** Verificar claridad de mensajes de error y guía al usuario en el formulario.

## Matriz de Trazabilidad Normativa

| Artículo | Norma | Requisito Implementado | Cumplimiento |
|----------|-------|------------------------|--------------|
| Art. 208 | Ley 1952/2019 | Término 6 meses y decisión | ✅ Validador de términos |
| Art. 208 Parágrafo | Ley 1952/2019 | Archivo parcial sin recurso | ✅ Indicador de no apelable |
| Art. 214 | Ley 1952/2019 | Ruptura unidad procesal | ✅ Archivo parcial por hechos/personas |
| Art. 215 | Ley 1952/2019 | Apertura investigación | ✅ Formulario de cargos |
| Art. 224 | Ley 1952/2019 | Recurso de apelación | ✅ Diferenciación por tipo de auto |
| Art. 13 | Ley 2094/2021 | Separación instructor-juzgador | ✅ Flujo de aprobación separado |
| Art. 38 | Ley 2094/2021 | Debido proceso | ✅ Motivación obligatoria |
| Sent. C-579/2013 | Corte Constitucional | Motivación decisiones | ✅ Campos de fundamentación |

## Requisitos de Seguridad y Auditoría

- **Firma Digital:** Obligatória para el aprobador usando certificado cualificado.
- **No Repudio:** Registro criptográfico de quién proyectó, quién aprobó y cuándo.
- **Control de Versiones:** Cada modificación al borrador queda versionada hasta su aprobación final.
- **Acceso Restringido:** Solo el instructor asignado y su cadena de mando pueden acceder a la función de proyección.
- **Auditoría de Cambios:** Log detallado de cada campo modificado en el borrador antes de aprobación.
- **Sellado de Tiempo:** Timestamp certificado al momento de convertir proyecto en acto administrativo.
- **Encriptación:** Documento final cifrado en reposo y en tránsito durante notificación.

## Protocolo de Incidentes

1. **Detección:** Alerta por intento de proyección fuera de término o por usuario no autorizado.
2. **Contención:** Bloqueo preventivo del expediente y notificación inmediata al superior jerárquico.
3. **Investigación:** Revisión de logs para determinar si es error operativo o intento de vulneración.
4. **Reporte:** En caso de caducidad por falla del sistema, reporte inmediato a Control Interno y Jurídica en menos de 4 horas.
5. **Recuperación:** Si aplica, solicitud de reinstauración de término por causa de fuerza mayor ante autoridad competente.
6. **Documentación:** Informe detallado del incidente para eventual proceso de responsabilidad.

## Glosario

- **Auto de Archivo:** Decisión que pone fin a la indagación por falta de mérito.
- **Auto de Apertura:** Decisión que inicia formalmente la investigación disciplinaria con cargos específicos.
- **Archivo Parcial:** Decisión que archiva respecto a algunos hechos o personas pero continúa con otros.
- **Motivos Graves y Fundados:** Umbral probatorio necesario para abrir investigación (Art. 215 CGD).
- **Caducidad:** Extinción de la acción disciplinaria por vencimiento del término sin decisión.
- **Ruptura de Unidad Procesal:** Posibilidad de decidir separadamente sobre hechos o personas (Art. 214 CGD).
- **Notificación Personal:** Entrega formal del auto al interesado dentro de los 5 días siguientes.

## Definition of Done (DoD)

- [ ] Historia documentada y aprobada por líder técnico y oficina jurídica.
- [ ] Desarrollo del modal de proyección con validaciones completas.
- [ ] Implementación de plantillas dinámicas de Autos (Archivo/Apertura).
- [ ] Validador de términos de 6 meses funcional y preciso.
- [ ] Integración con sistema de firma digital certificado.
- [ ] Flujo de aprobación configurado según niveles jerárquicos.
- [ ] Módulo de notificación electrónica integrado y probado.
- [ ] Pruebas de carga y estrés superadas (50 decisiones simultáneas).
- [ ] Validación legal de 10 casos piloto por Oficina Jurídica.
- [ ] Capacitación a funcionarios instructores sobre uso de la funcionalidad.
- [ ] Manual de usuario actualizado con ejemplos de proyección.
- [ ] Aprobación final del Product Owner y Comité Jurídico.
