# catalogo-clarios-assets

Repositorio de imágenes maestras de producto para el Catálogo Comercial de Baterías — Clarios Perú.

Este repositorio contiene **únicamente activos de imagen** (fotografías de producto). No contiene código de la aplicación del catálogo (`app.js` / `app.html` / `products.json`), que vive en un repositorio/entorno separado y no se modifica desde aquí.

## Estructura de carpetas

```
catalogo-clarios-assets/
├── README.md
├── mapping.csv          ← mapeo ligero SKU → archivo (para consumo automático desde el catálogo)
├── mapping.json          ← mapeo completo con fuente, justificación y nivel de confianza (trazabilidad/auditoría)
└── images/
    ├── capsa/
    │   ├── 311005651.png
    │   ├── 311005634.png
    │   └── ...
    ├── varta/
    ├── lth/
    ├── silvercast/
    ├── optima/
    └── motoracing/
```

Una carpeta por marca comercial (en minúsculas, sin espacios ni tildes). Dentro de cada carpeta, un archivo PNG por SKU.

## Nomenclatura definitiva de archivos

**`images/{marca}/{sku}.png`**

- `{marca}`: slug en minúsculas de la marca comercial — `capsa`, `varta`, `lth`, `silvercast`, `optima`, `motoracing`.
- `{sku}`: el código SKU de Clarios exactamente como aparece en `products.json` (ej. `311005651.png`).

**Por qué SKU y no el nombre del modelo:** varios nombres de modelo contienen caracteres problemáticos para nombres de archivo multiplataforma (`/`, `(`, `)`, espacios, tildes) — por ejemplo `L-48/91(LN3)-615` o `24R/900`. El SKU es único, estable y ya es la clave que usa el catálogo para vincular cada producto con su ficha — evita cualquier ambigüedad o colisión, y hace que la carga de imagen en la app sea una búsqueda directa por SKU, sin necesidad de "slugificar" nombres de modelo.

## Formato de imagen

- PNG con fondo transparente.
- Las 35 imágenes nuevas (extraídas o mejoradas en esta fase) están normalizadas a 1400×1400px, producto centrado, con mejora de nitidez y limpieza de fondo aplicada — ver `mapping.json` columna `tipo` para identificar cuáles.
- Las 76 imágenes ya existentes se incorporan en su resolución y formato original (sin reprocesar), tal como estaban en la carpeta de trabajo del proyecto.

## Mapeo SKU → Imagen

`mapping.csv` es el archivo pensado para que el catálogo (`app.js`) resuelva la imagen de cada producto en producción: dado un SKU, la ruta de la imagen es siempre `images/{marca}/{sku}.png` (columna `archivo`).

`mapping.json` conserva además la trazabilidad completa: de dónde viene cada imagen (`fuente`), por qué (`justificacion`) y el nivel de confianza (`confianza`) — útil para auditoría y para decidir cuáles imágenes revisar antes de tratarlas como definitivas.

### Tipos de imagen (columna `tipo`)

| Tipo | Cantidad | Significado |
|---|---|---|
| Existente (ya en IMAGEN BATERIA) | 76 | Foto real ya presente en la biblioteca de trabajo del proyecto, sin cambios. |
| Extraída del PDF multimarca (nueva) | 24 | Foto real extraída y mejorada del PDF "CATALOGO CLARIOS MULTIMARCA". |
| Extraída de fichas técnicas SILVERCAST (nueva) | 6 | Foto real extraída y mejorada de la ficha técnica individual de cada SKU en el PDF SILVERCAST PE (antes solo existía como referencia al PDF, no como imagen maestra independiente). |
| Reutilizada de familia (nueva) | 3 | Copia directa de la foto real de un SKU hermano de la misma familia visual (misma carcasa/etiqueta, confirmado por dimensiones y polaridad). |
| Extraída del PDF — PENDIENTE VALIDACIÓN | 2 | Extraída del PDF, pero el PDF reutiliza esa misma imagen para otro modelo de dimensiones físicas distintas. No se recomienda tratarla como definitiva sin una foto real adicional. Ver detalle en `Biblioteca_Visual_Final_111_SKU.xlsx`. |

**SKU pendientes de validación:** `311004752` (SILVER CAST NS40L HD SC 540) y `310800010` (MOTORACING 12N7-3BFA).

## Estado

- Cobertura: 111/111 SKU del catálogo (100%), de los cuales 109 con imagen real e independiente de alta confianza y 2 pendientes de validación adicional.
- No se ha creado ni modificado ningún repositorio en GitHub todavía — este contenido está preparado localmente para publicación, pendiente de autorización.
- No se ha modificado el catálogo publicado (`app.js` / `app.html` / `products.json`).
