# PRD — Asistente Inteligente de Compras y Ventas para Pymes

**Versión:** 2.0  
**Estado:** Propuesta para aprobación del piloto  
**Tipo de documento:** Product Requirements Document (PRD)  
**Fase:** Descubrimiento y validación funcional

---

## 1. Resumen ejecutivo

Se propone desarrollar un asistente inteligente que permita a pequeños negocios y empresas registrar, organizar y analizar sus movimientos de compras y ventas de manera sencilla, utilizando canales de comunicación que ya forman parte de su operación diaria.

El usuario podrá enviar una fotografía, PDF o documento de una factura, identificando si corresponde a una compra o una venta.

El asistente interpretará el documento mediante inteligencia artificial, extraerá la información relevante, realizará validaciones y registrará el movimiento en el historial financiero del comercio.

Posteriormente, el negocio podrá consultar sus compras y ventas mediante un panel visual con indicadores, gráficas de evolución temporal y filtros por fechas.

**El producto debe ser independiente del canal utilizado.** WhatsApp, Telegram, correo electrónico y futuros medios funcionarán como mecanismos alternativos de recepción, sin modificar el proceso principal de negocio.

## 2. Problema que buscamos resolver

Muchos pequeños negocios llevan el control de sus compras y ventas mediante procedimientos manuales, hojas de cálculo, fotografías de recibos o registros dispersos.

Esto genera diferentes dificultades:

- Pérdida o duplicación de comprobantes.
- Dificultad para conocer el total de compras y ventas.
- Tiempo invertido en registrar información manualmente.
- Falta de visibilidad de la evolución financiera del negocio.
- Dificultad para identificar los principales proveedores, productos y categorías de gasto.
- Barreras de adopción de sistemas administrativos complejos.

### Oportunidad

Crear una experiencia que permita convertir una actividad cotidiana, como enviar una fotografía por mensajería, en un registro financiero organizado y consultable.

## 3. Objetivos del producto

### Objetivo principal

Simplificar y automatizar el registro de compras y ventas de pequeños negocios mediante inteligencia artificial, proporcionando información confiable para comprender su actividad comercial.

### Objetivos específicos

1. Reducir la necesidad de transcripción manual de facturas.
2. Permitir el registro de movimientos desde distintos canales.
3. Clasificar los documentos como compras o ventas.
4. Extraer y organizar la información comercial.
5. Validar los datos antes de incorporarlos al historial.
6. Proporcionar trazabilidad de los documentos procesados.
7. Facilitar la consulta de compras y ventas por períodos.
8. Presentar indicadores visuales que ayuden a tomar decisiones.

## 4. Usuarios objetivo

### Propietario o administrador

Persona responsable de supervisar las operaciones financieras del comercio.

**Necesidades:**
- Conocer cuánto compra y vende.
- Consultar información sin consolidarla manualmente.
- Identificar tendencias y cambios en la actividad comercial.

### Empleado autorizado

Persona que realiza compras, ventas o tareas administrativas.

**Necesidades:**
- Registrar documentos rápidamente.
- Recibir confirmación del registro.
- Corregir información cuando sea necesario.

### Responsable administrativo o contable

Persona que revisa y organiza la información comercial.

**Necesidades:**
- Consultar los movimientos registrados.
- Revisar inconsistencias.
- Acceder a documentos originales.
- Obtener información estructurada y exportable.

## 5. Alcance del producto

### Incluido en el MVP

- Registro y configuración básica de un comercio.
- Vinculación de usuarios autorizados.
- Recepción de imágenes y PDF.
- Clasificación de movimientos como compra o venta.
- Extracción automática de información mediante IA.
- Validación de información extraída.
- Detección de posibles documentos duplicados.
- Registro de transacciones aprobadas.
- Confirmación del resultado al usuario.
- Historial de movimientos.
- Dashboard de compras y ventas.
- Filtros por rangos de fechas.
- Visualización de series temporales.

### Decisiones propuestas para el piloto

- **Segmento.** Comercios pequeños en Colombia, con COP como moneda inicial del tablero y soporte de moneda original para cada factura. Usar `America/Bogota` como configuración inicial del comercio.
- **Captura.** Un canal operativo. Priorizar WhatsApp si los comercios ya lo usan y se completa su habilitación. Usar Telegram como alternativa si permite pilotar con los mismos usuarios antes. Correo y los demás adaptadores quedan para una fase posterior. Aceptar una factura por imagen JPEG/PNG o PDF, hasta 10 MiB y 10 páginas, sujeto al límite del canal. Rechazar archivos protegidos o incompatibles con instrucciones para reenviar.
- **Etiquetas.** `#compra` y `#venta` expresan intención. Si faltan o hay contradicción verificable, pedir confirmación. La IA propone campos, el sistema valida y el usuario autorizado decide los casos ambiguos.
- **Aprobación.** Comenzar en revisión asistida. Habilitar el registro automático por comercio tras cumplir los criterios de calidad y comprobar campos obligatorios, coherencia, tipo y duplicados. Los documentos pendientes se corrigen desde la web. Un enlace desde el canal exige inicio de sesión y autorización.
- **Permisos.** El administrador configura, vincula identidades y anula. El operador envía documentos, consulta sus estados y corrige sus propios pendientes. El responsable administrativo revisa y corrige cualquier pendiente del comercio y consulta historial, tablero y originales. El administrador también puede ejecutar las acciones del responsable administrativo.
- **Documentos especiales.** Las anulaciones conservan historial y excluyen el movimiento de los indicadores. Notas crédito, devoluciones y ventas sin soporte quedan para una fase posterior. Si se identifica una nota crédito, informar que el tipo documental queda fuera del piloto.
- **Tablero.** Comparación con el período anterior de igual duración como primer alcance. Mostrar totales, series y diferencia operativa para una moneda a la vez. Exportaciones y personalización avanzada de categorías quedan para una fase posterior.

### Fuera del alcance inicial

- Emisión de facturación electrónica.
- Integración directa con entidades bancarias.
- Declaraciones tributarias.
- Conciliación bancaria.
- Gestión completa de inventarios.
- Nómina y obligaciones laborales.
- Contabilidad de doble partida.
- Cálculo de utilidades contables o fiscales.
- Predicciones financieras.

Estas capacidades podrán evaluarse en versiones posteriores.

## 6. Flujo general de negocio

El proceso debe ser uniforme para todos los canales de comunicación.

**Flujo principal:**

Usuario envía factura  
↓  
Identificación del comercio y tipo de movimiento  
↓  
Recepción del documento  
↓  
Extracción de datos mediante IA  
↓  
Validación y clasificación  
↓  
**¿Información correcta?**

- **Sí:** Registrar movimiento → Actualizar información financiera → Confirmar al usuario.
- **No:** Solicitar revisión o corrección → Validar nuevamente → Registrar cuando corresponda.

La aprobación de una transacción debe ser independiente del canal desde el cual fue recibida.

## 7. Historias de usuario

### HU-01 — Registrar una compra

**Como** propietario o empleado autorizado,  
**quiero** enviar una factura acompañada de la etiqueta `#compra`,  
**para** registrar automáticamente una adquisición realizada por el negocio.

**Criterios de aceptación:**
- El asistente reconoce la intención de compra.
- Recibe una fotografía o documento válido.
- Extrae la información disponible.
- Solicita revisión cuando existen inconsistencias.
- Confirma el registro satisfactorio.

### HU-02 — Registrar una venta

**Como** propietario o empleado autorizado,  
**quiero** enviar una factura acompañada de la etiqueta `#venta`,  
**para** mantener actualizado el historial de ventas del comercio.

**Criterios de aceptación:**
- El asistente identifica el movimiento como venta.
- Obtiene la fecha, el valor y los datos del documento.
- Registra la venta cuando supera las validaciones.
- Actualiza los indicadores correspondientes.

### HU-03 — Consultar el estado de un documento

**Como** usuario,  
**quiero** conocer si un documento fue procesado, registrado o requiere corrección,  
**para** tener certeza de que la operación quedó registrada correctamente.

### HU-04 — Corregir información

**Como** usuario autorizado,  
**quiero** revisar y modificar información extraída incorrectamente,  
**para** garantizar que las transacciones reflejen los documentos reales.

### HU-05 — Consultar evolución financiera

**Como** propietario,  
**quiero** visualizar las compras y ventas por día, semana o mes,  
**para** identificar tendencias y comparar períodos.

### HU-06 — Consultar movimientos históricos

**Como** responsable administrativo,  
**quiero** filtrar los movimientos por fecha, tipo y categoría,  
**para** revisar la actividad comercial del negocio.

### HU-07 — Utilizar diferentes canales

**Como** usuario,  
**quiero** enviar documentos desde cualquiera de los canales habilitados,  
**para** no depender de una aplicación específica.

## 8. Reglas de negocio

**RN-01. Identificación del movimiento**

Los movimientos principales serán compra y venta.

La etiqueta enviada por el usuario determinará la intención inicial. Si el contenido del documento presenta contradicciones, el sistema deberá solicitar confirmación.

**RN-02. Identificación del comercio**

Cada documento deberá asociarse a un comercio y a un usuario autorizado antes de su procesamiento.

**RN-03. Información obligatoria**

Para registrar una transacción deberán identificarse, como mínimo:

- Comercio asociado.
- Tipo de movimiento.
- Fecha de la operación.
- Moneda.
- Valor total.

Cuando estos campos no sean confiables, el documento quedará pendiente de revisión.

**RN-04. Extracción detallada**

Siempre que el documento lo permita, se capturarán:

- Número de factura.
- Nombre e identificación del proveedor o cliente.
- Productos o servicios.
- Cantidades.
- Precios unitarios.
- Descuentos.
- Impuestos.
- Subtotal y total.

La ausencia de información opcional no necesariamente impedirá registrar una operación.

**RN-05. Duplicados**

El sistema deberá detectar documentos potencialmente duplicados y evitar que una misma transacción se registre más de una vez por error.

**RN-06. Validación**

Se revisará la consistencia de importes, cantidades e impuestos. Los errores deberán resolverse antes del registro definitivo.

**RN-07. Correcciones**

Las modificaciones realizadas por usuarios autorizados deberán conservar trazabilidad.

**RN-08. Información financiera**

Las gráficas y métricas se calcularán exclusivamente con movimientos registrados y vigentes.

**RN-09. Independencia del canal**

Las reglas de extracción, clasificación, validación y registro serán las mismas independientemente del medio utilizado.

**RN-10. Clasificación comercial**

Los movimientos podrán organizarse por categorías como insumos, mercancía, servicios, gastos operativos y productos vendidos. Las categorías deberán poder ajustarse a cada negocio.

## 9. Experiencia de usuario

### Escenario A: compra registrada exitosamente

**Usuario:**

`#compra`

Adjunta una fotografía de una factura.

**Respuesta esperada del asistente:**

"Tu compra fue registrada correctamente.

Proveedor: Distribuidora ABC  
Fecha: 18/11/2026  
Categoría: Insumos  
Total: $185.000 COP

La información ya se encuentra disponible en el resumen de tu negocio."

### Escenario B: documento con errores

**Usuario:**

`#venta`

Adjunta una fotografía borrosa.

**Respuesta esperada:**

"No pude identificar con seguridad el valor total de esta factura.

Detecté los siguientes datos:

Fecha: 18/11/2026  
Total: Pendiente de confirmar

¿Puedes confirmar el valor o enviar una imagen más clara?"

### Escenario C: documento duplicado

**Respuesta esperada:**

"Esta factura parece haber sido registrada anteriormente.

Factura: FAC-00124  
Fecha: 18/11/2026  
Valor: $250.000 COP

No se creó un nuevo movimiento para evitar duplicaciones."

### Escenario D: procesamiento en curso

**Respuesta esperada:**

"Recibí tu factura y estoy procesando la información. Te confirmaré cuando el registro esté completo o si necesito algún dato adicional."

## 10. Estados del procesamiento

Cada documento tendrá un estado identificable:

| Estado | Descripción |
|---|---|
| Recibido | Documento recibido correctamente |
| En procesamiento | Información en extracción y análisis |
| En validación | Revisión de datos y reglas |
| Requiere revisión | Se necesita intervención del usuario |
| Registrado | Movimiento incorporado al historial |
| Duplicado | Documento potencialmente repetido |
| Fallido | No fue posible completar el procesamiento |

El usuario deberá poder conocer el estado de los documentos que ha enviado.

## 11. Dashboard y análisis de información

El dashboard tendrá como objetivo convertir los movimientos comerciales registrados en información fácil de interpretar.

### Indicadores principales

- Total de compras del período.
- Total de ventas del período.
- Diferencia entre ventas y compras.
- Número de transacciones registradas.
- Evolución de las compras.
- Evolución de las ventas.

La diferencia entre ventas y compras será un indicador operativo y no deberá presentarse como utilidad neta.

### Series temporales

El usuario podrá visualizar las compras y ventas sobre un eje temporal.

**Características:**
- Selección independiente de fecha de inicio y fecha de finalización. Ambos días se incluyen según la fecha de operación del comercio. El rango puede abarcar un solo día. Si falta una fecha o la finalización precede al inicio, mostrar un mensaje junto a los campos antes de actualizar los resultados.
- Agrupación diaria, semanal y mensual.
- Visualización conjunta o independiente de compras y ventas.
- Comparación de períodos.
- Filtros por categorías.
- Consulta de valores dentro de la gráfica.

### Historial de movimientos

Se presentará una tabla que permita consultar:

- Fecha.
- Tipo de movimiento.
- Número de factura.
- Proveedor o cliente.
- Categoría.
- Valor.
- Estado.
- Documento original.

## 12. Manejo de excepciones

El sistema deberá contemplar los siguientes escenarios:

| Escenario | Comportamiento esperado |
|---|---|
| Imagen ilegible | Solicitar nuevo documento |
| PDF sin información reconocible | Informar que no fue posible extraer los datos |
| Documento duplicado | Evitar nuevo registro y notificar |
| Etiqueta ausente | Solicitar tipo de movimiento |
| Etiqueta contradictoria | Pedir confirmación |
| Información incompleta | Solicitar los campos obligatorios |
| Totales inconsistentes | Requerir revisión |
| Usuario no autorizado | Rechazar la operación |
| Procesamiento interrumpido | Permitir reintento sin duplicar registros |
| Factura con múltiples productos | Registrar el detalle disponible |
| Factura en otra moneda | Conservar la moneda original e identificarla |
| Factura corregida o anulada | Mantener historial y actualizar indicadores |

## 13. Requerimientos no funcionales del producto

**Usabilidad:** el registro de una factura deberá requerir el menor número posible de interacciones.

**Confiabilidad:** una transacción no deberá considerarse registrada hasta completar sus validaciones.

**Trazabilidad:** el sistema permitirá consultar el documento original y su historial de procesamiento.

**Privacidad:** la información de cada negocio será accesible únicamente para usuarios autorizados.

**Extensibilidad:** incorporar nuevos canales no deberá modificar las reglas principales del producto.

**Escalabilidad funcional:** el procesamiento deberá admitir múltiples documentos y comercios concurrentemente.

**Disponibilidad:** una interrupción temporal del procesamiento no deberá provocar pérdida de documentos recibidos.

## 14. Indicadores de éxito del MVP

Los siguientes indicadores permitirán evaluar el valor y la efectividad de la solución:

| Indicador | Qué mide |
|---|---|
| Tasa de extracción exitosa | Documentos cuyos campos obligatorios fueron capturados correctamente |
| Automatización efectiva | Porcentaje de documentos registrados sin corrección manual |
| Tiempo de procesamiento | Duración entre recepción y resultado |
| Tasa de corrección | Porcentaje de documentos que requieren intervención |
| Precisión de clasificación | Compras y ventas identificadas correctamente |
| Tasa de duplicados | Documentos repetidos detectados |
| Adopción | Comercios y usuarios activos |
| Uso del dashboard | Frecuencia de consulta de indicadores |
| Retención | Comercios que continúan registrando movimientos |

### Criterios propuestos de salida del piloto

| Medida | Umbral de trabajo |
|---|---|
| Cohorte y muestra | 5–10 comercios durante 4 semanas. Etiquetar manualmente al menos 300 documentos autorizados. Separar una muestra de evaluación por comercio o emisor y cubrir compras, ventas, fotos, PDF y casos ambiguos. |
| Calidad | Informar precisión por campo y formato. Antes de automatizar, registrar en modo sombra 150 candidatos elegibles revisados contra el original, sin errores observados en comercio, tipo, fecha, moneda o total. Si la muestra queda corta, seguir en revisión asistida. |
| Automatización | Al menos 70 % de documentos elegibles únicos listos para registro automático en la última semana, medidos en modo sombra o en operación. Reportar aparte el porcentaje de documentos entrantes que fueron elegibles. |
| Tiempo | p95 de hasta 120 s desde recepción durable hasta el primer resultado de procesamiento. Excluir la espera por respuesta humana y reportar fallos aparte. |
| Integridad | Cero movimientos duplicados en pruebas de reentrega y concurrencia. Cero accesos cruzados en pruebas de permisos. Totales del tablero iguales al historial con los mismos filtros. |
| Valor | Reducción mediana de al menos 50 % del tiempo activo por documento frente al método actual en tareas comparables. Al menos 60 % de comercios activados envían un documento en la cuarta semana. |

Registrar numeradores, denominadores y tamaño de muestra. Un comercio se activa cuando registra su primer movimiento. Estos umbrales son hipótesis a ratificar antes del piloto.

### Condiciones para recibir documentos reales

Aprobar región de datos, retención y eliminación de originales y derivados, acceso de soporte y tratamiento por terceros. Definir usuario responsable de incidentes y validar restauración de respaldo. Probar que los límites y reintentos del canal conservan un solo registro. Registrar métricas sin contenido de factura. Proponer exportación de datos como hito posterior con alcance acordado.

## 15. Plan de validación del producto

### Etapa 1 — Validación del problema

Confirmar con propietarios y administradores:

- Cómo registran actualmente sus compras y ventas.
- Qué dificultades enfrentan.
- Cuánto tiempo dedican al registro manual.
- Qué información les gustaría consultar.

### Etapa 2 — Validación del flujo

Presentar los escenarios de compra, venta, revisión y confirmación.

Verificar que los usuarios comprendan el uso de etiquetas y puedan completar las tareas sin capacitación extensa.

### Etapa 3 — Validación documental

Reunir facturas, recibos y comprobantes representativos.

Evaluar qué información puede extraerse, cuáles documentos presentan dificultades y qué correcciones serían necesarias.

### Etapa 4 — Validación del dashboard

Presentar un prototipo con datos simulados.

Confirmar si los indicadores, filtros y gráficas son comprensibles y útiles para el negocio.

### Etapa 5 — Piloto controlado

Evaluar el producto con un grupo reducido de comercios, utilizando documentos y operaciones reales bajo condiciones autorizadas.

Analizar resultados, errores y oportunidades de mejora antes de ampliar su alcance.

## 16. Preguntas abiertas para el equipo

Antes de cerrar el alcance funcional, deberán resolverse las siguientes preguntas:

1. ¿El usuario siempre deberá indicar `#compra` o `#venta`, o se permitirá que la IA proponga automáticamente el tipo de movimiento?
2. ¿El primer MVP estará enfocado únicamente en facturas o también aceptará recibos, tiquetes y otros soportes?
3. ¿El registro será automático cuando exista suficiente confianza o requerirá aprobación de todas las operaciones?
4. ¿Un comercio podrá vincular múltiples usuarios y múltiples canales desde el inicio?
5. ¿Las ventas podrán registrarse sin factura, por ejemplo mediante un mensaje de texto?
6. ¿Cómo se tratarán las notas crédito, devoluciones y cancelaciones?
7. ¿Qué información mínima necesita realmente el propietario para tomar decisiones?
8. ¿Qué nivel de detalle por producto será necesario en el MVP?
9. ¿Qué documentos se conservarán y durante cuánto tiempo?
10. ¿Cuál será el primer canal de comunicación que se validará con usuarios reales?

## 17. Definición de éxito

El MVP será considerado validado cuando un pequeño comercio pueda registrar sus compras y ventas enviando documentos desde un canal habilitado, recibir confirmación o solicitar correcciones cuando sea necesario y visualizar información consolidada y confiable sobre su actividad comercial.

El valor principal del producto deberá estar en **reducir el esfuerzo administrativo y transformar documentos dispersos en información financiera útil**, sin exigir al comerciante aprender a utilizar un sistema contable complejo.

---

**Estado del documento:** Pendiente de aprobación del piloto. Las decisiones propuestas se validan con los comercios y con el equipo.

**Próximo hito:** Validar el flujo de negocio, las reglas de captura y aprobación, los escenarios excepcionales y las funcionalidades mínimas del primer piloto.
