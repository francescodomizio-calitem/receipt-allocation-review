# Revisión de asignaciones de recepciones / Receipt allocation review

[Descargar la plantilla Excel / Download the workbook](receipt-allocation-review.xlsx?raw=true)

Una recepción puede aparecer en varias facturas. Esta plantilla suma las cantidades asignadas a cada recepción y a cada línea de factura para señalar si se utiliza más cantidad de la disponible o facturada. Complementa el comprobador de precios de una línea y su CSV manual: aquí la relación entre recepciones y líneas se registra explícitamente.

Recurso de Francesco Domizio, fundador de Calitem. Todos los ejemplos son inventados. Preparado con asistencia de IA y revisión de casos sintéticos.

## Dos formatos / Two formats

- **Excel:** descarga el archivo de arriba y ábrelo en una aplicación compatible con BUSCARX/XLOOKUP. Excel de escritorio no se probó por separado.
- **Google Sheets:** [abre la edición pública de solo lectura](https://docs.google.com/spreadsheets/d/1uluuYLthRvtK7nTa-tDrHwK24ebaJbvmg6uFpKhZzPk/edit?usp=drivesdk). **Crea primero una copia privada en tu propio Drive** y comprueba sus permisos antes de introducir datos reales. Google aloja esta edición y tus copias; las indicaciones de archivo local se refieren al XLSX descargado. No escribas datos propios en la plantilla pública.

Las dos ediciones comprueban las mismas asignaciones y tienen la misma capacidad fija. La edición nativa de Google Sheets se comprobó con 21 casos sintéticos, 139 resultados esperados y 1.192 comprobaciones de entradas. No amplíes filas ni rangos sin volver a verificar las fórmulas.

**English:** download the XLSX above, or open the read-only Google Sheets edition. **Make a private copy in your own Drive first**, then check its sharing settings before entering real data. Google hosts the online edition and your copies; local-file guidance applies to the downloaded XLSX. The native edition passed the same 21 synthetic cases, with 139 expected results and 1,192 input checks. Both editions retain the fixed capacity described below. Desktop Excel was not separately tested.

## Español

1. Sustituye los ejemplos en las celdas ámbar. Conserva las columnas de cálculo grises.
2. En **Recepciones**, registra un ID único por línea de recepción, proveedor, pedido, artículo, unidad base y cantidad recibida. Dos artículos del mismo albarán necesitan IDs de línea distintos.
3. En **LíneasFactura**, registra un ID único por línea y su documento de factura. El documento puede repetirse en distintas líneas.
4. En **Asignaciones**, indica un ID único de asignación, el ID de recepción, el ID de línea y la cantidad que los relaciona. Puedes repartir una recepción entre varias líneas, o usar varias asignaciones con el mismo par de IDs, siempre con IDs de asignación distintos.
5. Consulta **Revisión** y los estados de cada fila. Una asignación parcial dentro de los límites es válida para estas comprobaciones; su saldo pendiente sigue visible. No significa que toda la factura esté conciliada o aprobada.

Incluye también las asignaciones previas de cada recepción: el archivo no conoce las facturas omitidas. Cada línea pertenece a un único proveedor, pedido, artículo y unidad; separa antes un caso que agrupe varios.

**Reglas de entrada.** Prepara antes todas las cantidades en la misma unidad base por artículo. Proveedor, pedido, artículo y unidad deben coincidir exactamente, incluidas mayúsculas. No hay OCR ni conversión automática. Los IDs de recepción, línea y asignación y sus referencias deben ser texto de hasta 64 caracteres, sin espacios exteriores, caracteres de control ni `*`, `?`, `~`. La unicidad de los IDs no distingue mayúsculas de minúsculas, para rechazar colisiones ambiguas. Las referencias deben, además, reproducir exactamente el ID de origen. Los otros campos identificativos también requieren texto sin espacios exteriores y hasta 64 caracteres.

Las cantidades deben ser números de **0 a 1.000.000**, con **hasta seis decimales**. Cero es válido; una celda vacía, texto numérico, un booleano o un negativo no lo son. Son límites de precisión de esta plantilla, no límites de Calitem. Las filas completamente vacías no son registros; una fila parcialmente completada requiere revisión.

**Resultados.** «Solicitado conocido» suma las cantidades numéricas admitidas del rango gestionado, incluso si otra parte de una asignación es inválida. Los negativos no compensan otras asignaciones. «Exceso provisional» mantiene visible una posible asignación excesiva incluso cuando falta información. El saldo es `n.d.` (no disponible) si falla un origen o vínculo relacionado. Los IDs duplicados invalidan todas sus apariciones. No se elige silenciosamente la primera coincidencia.

Una recepción de **85** con asignaciones de **30 + 60** muestra **5** de exceso. El saldo calculado de **−5** solo es utilizable como diagnóstico de esa diferencia. Otra recepción de **25** asignada a **25** tiene saldo **0**. No se suman unidades de artículos diferentes.

**Capacidad fija.** Hay 50 recepciones y 50 líneas de factura en las filas **8 a 57**, y 100 asignaciones en las filas **8 a 107**. Usa las filas vacías ya preparadas, incluso después de un hueco. No insertes filas ni amplíes el rango como si fuera una tabla automática. Las diez filas inmediatamente posteriores son una zona de aviso: cualquier entrada en ellas activa «Fuera de capacidad» y deja todos los saldos en `n.d.`. El contador mide celdas ocupadas de esa zona, no registros. Las filas posteriores a esa zona no están cubiertas y no deben utilizarse. Ampliar la capacidad requiere actualizar y volver a comprobar todas las fórmulas.

El archivo no incluye macros, precios, ahorros, recuperación de importes ni ejecución de pagos. No consulta servicios externos ni envía las entradas a Calitem. Las fórmulas requieren un motor compatible con BUSCARX/XLOOKUP. Se probó el recálculo en el motor utilizado para crear el archivo; Excel de escritorio no se probó por separado. Revisa los resultados después de abrirlo en tu aplicación.

## English

Enter prepared common-base quantities in the amber cells. **Recepciones** holds receipts, **LíneasFactura** holds unique invoice lines, and **Asignaciones** links each receipt to a line with an allocated quantity. Invoice document numbers may repeat. Allocation IDs and line IDs must be unique. Source identity and reference IDs must match exactly; case-colliding IDs are rejected conservatively. Zero is valid; blank, text, boolean, negative, excessive and overprecision quantities remain invalid.

Include earlier allocations too; omitted invoices are unknown to the workbook. Receipt IDs identify individual item lines, not entire delivery documents. Prepare separate invoice lines for different supplier/PO/item/unit identities.

The workbook checks both receipt and invoice-line caps. Partial allocations within those caps are valid, with unallocated quantity still visible. They do not establish that the entire invoice is matched or approved. Known nonnegative quantities expose provisional overuse even if another field is invalid; trusted balances become `n.d.` when related prerequisites fail.

Capacity is **50 receipts, 50 invoice lines and 100 allocations**, with ten overflow-warning rows after each managed range. Any entry in that warning zone blocks all trusted balances. Rows beyond the warning zone are unsupported. Do not insert rows or assume automatic table expansion. Quantities support **0 to 1,000,000 and up to six decimal places**. These are template precision limits, not product-plan limits.

All data is synthetic. This macro-free local workbook performs no OCR, unit conversion, pricing, savings calculation or payment action. Formulas require XLOOKUP support. Desktop Excel was not separately tested.

## Recursos oficiales / Official resources

- [Plantilla de conciliación de una línea](https://www.calitem.com/es/resources/plantilla-conciliacion/)
- [Conciliación de facturas, pedidos y albaranes en Calitem](https://www.calitem.com/es/features/three-way-matching/)
