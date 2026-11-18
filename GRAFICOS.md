# Flujos y diseño de producto

## De la factura al tablero

```mermaid
flowchart TD
  A["Envío de factura y etiqueta"] --> B["Verificar remitente, comercio y adjunto"]
  B -->|Entrada inválida| X["Informar motivo de rechazo"]
  B -->|Entrada autorizada| C["Guardar original y emitir acuse"]
  C --> D["Extraer campos y evaluar reglas"]
  D -->|Duplicado concluyente| E["Informar duplicado"]
  D -->|Dato dudoso o revisión obligatoria| F["Revisar original y campo pendiente"]
  F -->|Confirmar o corregir| D
  D -->|Aprobado según política| G["Registrar movimiento y auditoría"]
  G --> H["Actualizar historial y tablero"]
  G --> I["Enviar confirmación por el canal"]
  D -->|Reintentos agotados| J["Mostrar fallo y permitir reproceso"]
  J --> D
```

## Estado del documento

```mermaid
stateDiagram-v2
  [*] --> Recibido
  Recibido --> Procesando
  Procesando --> Validando
  Procesando --> Fallido: Reintentos agotados
  Fallido --> Procesando: Reproceso autorizado
  Validando --> Revision: Inconsistencia o aprobación requerida
  Revision --> Validando: Corrección o aprobación
  Validando --> Duplicado: Coincidencia concluyente
  Validando --> Registrado: Reglas y aprobación satisfechas
  RevisionMovimiento: Corrección o anulación auditada del movimiento
  Registrado --> RevisionMovimiento
```

Las correcciones y anulaciones posteriores versionan el movimiento, conservan el estado histórico del documento y actualizan sus indicadores vigentes.

## Pantallas del MVP

| Pantalla | Diseño y comportamiento |
|---|---|
| Resumen | Campos de fecha de inicio y de finalización arriba, junto a la moneda. El rango incluye ambos días y actualiza tarjetas, gráfica y detalle. Tarjetas de ventas, compras y diferencia operativa. Dos series sobre el mismo eje. El rango anterior se consulta con comparación y los períodos vacíos aparecen con cero. |
| Historial | Fecha, tipo, referencia, tercero, categoría, moneda, valor, estado y acceso al original. La vista filtrada usa las mismas reglas de vigencia que el resumen. |
| Bandeja de revisión | Pendientes ordenados por antigüedad. Cada fila indica motivo y estado. El operador ve sus documentos. Administración ve el comercio completo. |
| Detalle de revisión | Original y formulario lado a lado en escritorio, apilados en móvil. Resaltar campos dudosos con texto. Mostrar el motivo de una coincidencia y pedir confirmación antes de aplicar correcciones. |
| Configuración | Comercio, zona horaria y permisos. Vincular una identidad del canal a un usuario autenticado mediante código de un solo uso. |

Enlaces a detalle y originales requieren autorización del comercio. Colores y etiquetas de las series deben permitir distinguir compras y ventas sin depender del color.
