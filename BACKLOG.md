# Backlog para GitHub Projects

Crear un elemento por fila. Usar el ID en el título, el resultado verificable como criterio de aceptación y la columna de dependencia para vincular los pendientes. Convertir épicas en issues principales, historias en subissues de su épica y tareas en subissues de su historia. Usar los identificadores del PRD para conservar la trazabilidad.

Campos propuestos para el tablero: estado, prioridad y fase. Todas las filas empiezan en **Pendiente**. P0 corresponde al flujo base del piloto y P1 a la extensión de canales.

| ID | Tipo | Padre | Fase | Prioridad | Título | Depende de | Resultado verificable |
|---|---|---|---|---|---|---|---|
| EP-01 | Épica | — | 0–1 | P0 | Captura multicanal | — | Un usuario autorizado entrega documentos por el canal elegido para el piloto. |
| HU-07 | Historia | EP-01 | 1 | P0 | Enviar una factura por un canal habilitado | T-01 | Una imagen o PDF con etiqueta se acepta y se asocia al comercio correcto. |
| T-01 | Tarea | HU-07 | 0 | P0 | Validar alcance, muestra y canal del piloto | — | El equipo acuerda formatos, aprobación, canal, retención y medidas de éxito. |
| T-02 | Tarea | HU-07 | 1 | P0 | Vincular identidades y normalizar entradas | T-01 | Un usuario vinculado puede enviar al comercio correcto y un remitente ajeno queda rechazado. |
| T-03 | Tarea | HU-07 | 1 | P0 | Conectar el canal elegido y guardar originales | T-02 | Un evento repetido conserva un solo documento y el original tiene acceso restringido. |
| T-04 | Tarea | HU-07 | 4 | P1 | Adaptador WhatsApp | T-03 | Cumple el contrato de recepción y avisos. Si fue el primer canal, vincular la evidencia de T-03. |
| T-05 | Tarea | HU-07 | 4 | P1 | Adaptador Telegram | T-03 | Cumple el contrato de recepción y avisos. Si fue el primer canal, vincular la evidencia de T-03. |
| T-06 | Tarea | HU-07 | 4 | P1 | Adaptador de correo electrónico | T-03 | Cumple el contrato de recepción y avisos. Si fue el primer canal, vincular la evidencia de T-03. |
| EP-02 | Épica | — | 1–2 | P0 | Extracción, revisión y registro | — | Los movimientos aprobados se registran una sola vez con trazabilidad. |
| HU-01 | Historia | EP-02 | 2 | P0 | Registrar una compra | T-07, T-08 | Una factura etiquetada como compra genera un movimiento válido y confirmado. |
| HU-02 | Historia | EP-02 | 2 | P0 | Registrar una venta | T-07, T-08 | Una factura etiquetada como venta registra fecha, moneda y total en el historial. |
| HU-03 | Historia | EP-02 | 2 | P0 | Consultar estado del documento | T-03 | El usuario recibe acuse y puede conocer el resultado o la acción requerida. |
| HU-04 | Historia | EP-02 | 2 | P0 | Corregir datos extraídos | T-08 | Un usuario autorizado corrige un total dudoso y la nueva validación queda auditada. |
| T-07 | Tarea | HU-01 | 1 | P0 | Definir contrato y evaluar extracción de IA | T-03 | Imágenes y PDF de muestra devuelven campos y detalle con ausencias explícitas. |
| T-08 | Tarea | HU-01 | 2 | P0 | Validar y persistir movimientos con idempotencia | T-07 | Las etiquetas contradictorias, totales inválidos y duplicados ambiguos quedan en revisión. Los reintentos no crean movimientos adicionales. |
| T-09 | Tarea | HU-03 | 2 | P0 | Implementar estados, avisos y reintentos | T-08 | Un fallo temporal se recupera y la confirmación se envía después del registro. |
| EP-03 | Épica | — | 3–4 | P0 | Historial, series temporales y piloto | — | El comercio puede reconciliar su dashboard con los movimientos vigentes del historial. |
| HU-05 | Historia | EP-03 | 3 | P0 | Comparar compras y ventas en el tiempo | T-10 | Se muestran ambas series por día, semana o mes, con filtros y comparación de períodos. |
| HU-06 | Historia | EP-03 | 3 | P0 | Consultar el historial | T-08 | Se filtra por fecha, tipo y categoría y se abre el original con autorización. |
| T-10 | Tarea | HU-05 | 3 | P0 | Agregar por fecha, tipo y moneda | T-08 | Los totales coinciden con el historial, incluso cuando hay anulaciones o períodos vacíos. |
| T-11 | Tarea | HU-05 | 4 | P0 | Ejecutar y evaluar el piloto | HU-05, HU-06, T-15, T-16 | El equipo registra precisión, automatización, tiempos, correcciones y uso del dashboard. |
| T-12 | Tarea | HU-04 | 2 | P0 | Implementar revisión y corrección autorizadas | T-08 | Una corrección valida de nuevo el documento, registra el cambio y actualiza el historial cuando se aprueba. |
| T-13 | Tarea | HU-06 | 3 | P0 | Implementar historial y filtros | T-08 | Fecha, tipo, categoría, estado y acceso al original respetan los permisos del comercio. |
| T-14 | Tarea | HU-05 | 3 | P0 | Construir la vista temporal | T-10 | El usuario puede comparar dos rangos y consultar los valores de ambas series por período y moneda. |
| T-15 | Tarea | HU-07 | 0 | P0 | Cerrar la decisión de infraestructura | T-01 | Se documentan región, retención, opción de GCP, presupuesto, responsables y restauración. |
| T-16 | Tarea | HU-03 | 2 | P0 | Ensayar fallos de entrega y recuperación | T-09 | La caída después de persistir o antes de encolar se recupera, y una restauración verifica conciliación e integridad. |
