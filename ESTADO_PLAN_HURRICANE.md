# Estado del plan - Reconstruccion Cornford Hurricane

Fecha de actualizacion: 2026-05-10

## Resumen

| Area | Estado | Archivo / referencia | Notas |
|---|---|---|---|
| Inventario inicial de carpeta | Terminado | `DIAGNOSTICO_HURRICANE_PLAN.md` | Se identificaron carpetas `Hurricane`, `Harlequin` y `Otros`. |
| Separacion de documentacion fiable y dudosa | Terminado | `Hurricane/` | Los nombres ahora distinguen `CONFIRMED`, `UNVERIFIED` y `NOT_MY_AMP`. |
| Esquema electrico base confirmado | Terminado | `Hurricane/CONFIRMED_Hurricane_Chillidoggy_schematic_v6_2013-05-01.jpg` | Es la referencia principal para estudiar el circuito. |
| Layout Hurricane v6 confirmado | Terminado | `Hurricane/Hurricane_Chillidoggy_layout_v6_2013-04-26.gif` | Referencia de montaje, subordinada al esquema. |
| Layout Hurricane v2 conservado | Terminado | `Hurricane/Hurricane_layout_v2_2013-04-04.jpg` | Solo historico/comparativo. |
| Fotos ajenas o dudosas marcadas | Terminado | `Hurricane/NOT_MY_AMP_unknown_build_photo_*.jpg` | No usarlas como referencia del ampli real. |
| Plan de diagnostico general | Terminado | `DIAGNOSTICO_HURRICANE_PLAN.md` | Plan por fases, seguridad primero. |
| Objetivo de reconstruccion real | Terminado v1 | `AGENTS.md` / `DIAGNOSTICO_HURRICANE_PLAN.md` | El agente debe guiar reconstruccion fisica, calidad sonora, seguridad y verificacion teoria-practica. |
| Memoria tecnica del proyecto | Iniciado | `MEMORIA_PROYECTO_HURRICANE.md` | Estructura por bloques con funcion, efecto sobre la senal y graficos SVG iniciales. |
| Formatos de documentacion | Terminado v1 | `DOCUMENTACION_PROYECTO_FORMATOS.md` | Markdown para memoria/tablas, SVG para ondas, Mermaid para flujos. |
| Registro de pendientes y compras | En progreso | `PENDIENTES_RECONSTRUCCION_HURRICANE.md` | Incluye PT de 325 V AC y resistencias de fuente A-B-C-D-E mal montadas. |
| App web interactiva | En progreso | `AppWeb/index.html` | Branding definido como SchemaLab, subtitulo `MAP THE SIGNAL`, logo propio en cabecera, favicon y titulo `SCHEMA LAB`; conserva tarjetas laterales, tarjeta de proyecto `Cornford Hurricane` con progreso y menu de descarga del esquema, vista de esquema como capa completa bajo la interfaz para que pueda desplazarse bajo tarjetas/titulo/botones, bloque de datos dinamico, zoom con rueda, pan con click de rueda, barra inferior con vistas y lista de componentes detallada filtrable por bloque desde la columna izquierda, incluyendo `0 Todo el circuito`; la lista se agrupa por tipo en tablas separadas, admite componentes compartidos entre bloques, enumera valvulas fisicas y muestra resistencias con simbolo `Ω` y codigo de colores. `AppWeb/code.html` queda como referencia Stitch original. |
| Documento de analisis del esquema | En progreso | `ANALISIS_ESQUEMA_HURRICANE.md` | Ya contiene identificacion de bloques, convenciones de valvulas, fuente, potencia, inversor y primeras etapas de previo. |
| Transcripcion completa del esquema | Terminado v1 | `TRANSCRIPCION_COMPLETA_ESQUEMA_HURRICANE.md` | Transcripcion por bloques y nodos; mantiene zonas ambiguas marcadas como pendientes de confirmar. |
| Netlist humano por bloques | Terminado v1 | `TRANSCRIPCION_COMPLETA_ESQUEMA_HURRICANE.md` | Incluye fuente, previo, loop, tonestack, master, PI, potencia, reverb y footswitch. |
| Mapa de colores del esquema | Terminado v1 | `Hurricane_schematic_color_blocks_clean.png` / `MAPA_COLORES_ESQUEMA_HURRICANE.md` | Bloques funcionales coloreados sobre el esquema original. |
| Identificacion de transformadores reales | Terminado v1 | `TRANSFORMADORES_REALES.md` | PT real 325 VAC/130 mA; OT Hammond 1750H; reverb Hammond 1750A. |
| Analisis del PT real de 325 V AC | Terminado v1 | `ANALISIS_TRAFO_ALIMENTACION_325V.md` | Recomienda no encender y decidir entre PT correcto o rediseno de fuente con margen superior. |
| Opciones de compra de PT | Terminado v1 | `OPCIONES_COMPRA_TRAFO_ALIMENTACION.md` | Incluye Hammond 290PAZ, TAD MJTM18WP, opcion a medida y BTB toroidal. |
| Calculos de fuente A-B-C-D-E | Parcial | `ANALISIS_ESQUEMA_HURRICANE.md` / `TRANSFORMADORES_REALES.md` | Con PT real: 325 VAC * sqrt(2) ~= 460 VDC antes de carga. |
| Calculos de etapa de potencia EL84 | Pendiente | `ANALISIS_ESQUEMA_HURRICANE.md` | Falta corriente de catodo, disipacion y rangos seguros. |
| Identificacion fisica del ampli real | Parcial | `TRANSFORMADORES_REALES.md` / fotos nuevas | Transformadores identificados; faltan zocalos, jacks, valvulas, reverb, loop y cableado. |
| Identificacion fisica de nodos A-B-C-D-E | Pendiente | Ampli real | Antes de encender. |
| Mediciones en frio de fuente | Pendiente | Multimetro | Tras corregir resistencias: A-B 2k2, B-C 10k, C-D 1k, D-E 10k; cortos a masa; polaridad de electroliticos. |
| Revision IEC, fusible, power, standby | Pendiente | Ampli real | Confirmar fase, neutro, tierra y aislamiento. |
| Continuidad de transformador de alimentacion | Pendiente | Ampli real | Primario azul-azul, HT rojo-rojo, filamentos marron-marron y toma central. |
| Continuidad de transformador de salida | Pendiente | Ampli real | Hammond 1750H: primario brown-red-blue, secundario black-green. |
| Revision pin a pin de zocalos ECC83/EL84 | Pendiente | Ampli real | Fundamental antes de alimentar. |
| Revision de masas | Pendiente | Ampli real | Distinguir chasis, tierra de red y masa de circuito. |
| Primer encendido sin valvulas | Bloqueado | Solo tras mediciones en frio | No hacerlo hasta cerrar seguridad y fuente. |
| Encendido con EL84 | Bloqueado | Solo con carga de altavoz | Nunca con EL84 sin altavoz/carga ficticia adecuada. |

## Siguiente trabajo recomendado

1. Revisar `TRANSCRIPCION_COMPLETA_ESQUEMA_HURRICANE.md` contra el layout v6.
2. Revisar las zonas ambiguas del inversor, tonestack, reverb y jacks contra el layout v6.
3. Decidir ruta de fuente de alimentacion para la reconstruccion: PT nuevo correcto o rediseño seguro.
4. Anotar fallos detectados por el usuario en `PENDIENTES_RECONSTRUCCION_HURRICANE.md`.
5. Pedir o tomar fotos actuales del ampli real antes de cualquier medicion con tension.
6. Construir una tabla de mediciones en frio para rellenar con el multimetro.
