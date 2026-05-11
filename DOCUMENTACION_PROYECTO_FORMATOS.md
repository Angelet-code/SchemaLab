# Formatos de documentacion del proyecto

Objetivo:

- Mantener una documentacion tecnica clara, ampliable y exportable.
- Separar memoria, calculos, pendientes, graficos y evidencias fotograficas.

## Formato principal: Markdown

Uso:

- Memoria tecnica.
- Registro de decisiones.
- Tablas de mediciones.
- Listas de compra.
- Checklists de reconstruccion.

Ventajas:

- Facil de editar.
- Versionable.
- Legible sin herramientas especiales.
- Exportable a PDF/HTML/DOCX mas adelante.

Archivos principales:

- `MEMORIA_PROYECTO_HURRICANE.md`
- `PENDIENTES_RECONSTRUCCION_HURRICANE.md`
- `TRANSCRIPCION_COMPLETA_ESQUEMA_HURRICANE.md`
- `ANALISIS_ESQUEMA_HURRICANE.md`

## Graficos tecnicos: SVG

Uso:

- Formas de onda.
- Diagramas de flujo de senal.
- Diagramas de bloques.
- Comparaciones antes/despues.

Ventajas:

- Vectorial, no pierde calidad.
- Se puede insertar directamente en Markdown.
- Editable a mano si hace falta.
- Exportable a PNG/PDF.

Carpeta:

- `docs_assets/`

## Diagramas de relaciones: Mermaid

Uso:

- Flujo de senal.
- Secuencia de diagnostico.
- Arbol de decisiones.

Ventajas:

- Muy rapido de escribir.
- Integrado en muchos visores Markdown.

Limitacion:

- No es ideal para formas de onda analogicas detalladas.

## Imagenes reales

Uso:

- Fotos del montaje.
- Fotos de transformadores.
- Evidencia de cableado y fallos.

Regla:

- No mezclar fotos dudosas con fotos reales.
- Usar siempre `Fotos Reales Implementacion/` para material del ampli real.
- Mantener `Hurricane/NOT_MY_AMP_*` fuera de la reconstruccion.

## Estructura recomendada

| Tipo | Archivo/carpeta | Funcion |
|---|---|---|
| Memoria | `MEMORIA_PROYECTO_HURRICANE.md` | Explicacion completa del ampli |
| Pendientes | `PENDIENTES_RECONSTRUCCION_HURRICANE.md` | Compra, fallos y cambios |
| Graficos | `docs_assets/` | SVG y diagramas |
| Fotos reales | `Fotos Reales Implementacion/` | Evidencia del montaje real |
| Referencias | `Hurricane/` | Esquema/layout confirmados |
| Web interactiva | `AppWeb/index.html` | Exploracion visual del esquema y proceso |

## Web del proyecto

La web del proyecto vive en:

- `AppWeb/index.html`

La maqueta original de Stitch se conserva en:

- `AppWeb/code.html`

Objetivo:

- Mostrar el esquema electrico limpio.
- Superponer zonas interactivas por colores.
- Abrir explicaciones por bloque al hacer click.
- Servir como interfaz visual para comprender el proceso de reconstruccion.
- Mantener el contenido central directamente sobre el fondo, sin tarjeta central, con zoom mediante rueda y desplazamiento mediante click de la rueda.

Recursos locales:

- `AppWeb/assets/schematic-original.jpg`
- `AppWeb/assets/schematic-color-reference.png`
