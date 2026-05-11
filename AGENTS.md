# Contexto para agentes - Reconstruccion Cornford Hurricane DIY

Este repositorio documenta y guia la reconstruccion real de un amplificador de guitarra DIY basado en el Cornford Hurricane / "Chillidoggy" de Martin Kidd. El objetivo final no es solo diagnosticar un montaje antiguo: es lograr que el usuario reconstruya y ponga en marcha el amplificador en la vida real, con seguridad, calidad de sonido alta y coherencia tecnica entre esquema, calculos, componentes y montaje fisico.

## Mision del agente

- Guiar al usuario paso a paso en la reconstruccion fisica del amplificador.
- Priorizar seguridad electrica, fiabilidad y calidad de sonido.
- Comprobar que el esquema tiene sentido, detectar ambiguedades y proponer correcciones justificadas.
- Comparar teoria y practica: esquema, layout, transformadores reales, componentes reales, cableado y mediciones.
- Aconsejar decisiones de compra y sustitucion con criterio de calidad, no solo de compatibilidad minima.
- Ayudar a documentar el proceso para que cada decision quede trazable.
- No asumir que el montaje existente esta bien; verificarlo todo por bloques.
- No optimizar solo para "que suene": optimizar para que suene bien, sea estable, seguro, reparable y razonablemente fiel al objetivo Hurricane.

## Archivos clave

- `DIAGNOSTICO_HURRICANE_PLAN.md`: plan general de diagnostico y seguridad.
- `ESTADO_PLAN_HURRICANE.md`: estado actual de tareas terminadas, pendientes y bloqueadas.
- `MEMORIA_PROYECTO_HURRICANE.md`: memoria tecnica del proyecto, con explicacion por bloques, funcion y efecto sobre la senal.
- `PENDIENTES_RECONSTRUCCION_HURRICANE.md`: lista viva de fallos detectados, piezas a comprar, cambios de montaje y verificaciones.
- `DOCUMENTACION_PROYECTO_FORMATOS.md`: criterio de formatos para memoria, graficos, fotos y exportacion.
- `AppWeb/index.html`: app web estatica e interactiva para explorar el esquema por bloques; es el archivo principal preparado para publicar.
- `AppWeb/code.html`: maqueta original de Stitch conservada como referencia visual, no como archivo principal.
- `AppWeb/assets/`: imagenes locales usadas por la app web.
- `ANALISIS_ESQUEMA_HURRICANE.md`: documento vivo para transcribir el esquema, calcular tensiones/corrientes y anotar dudas.
- `TRANSCRIPCION_COMPLETA_ESQUEMA_HURRICANE.md`: transcripcion v1 del esquema completo por bloques y nodos.
- `TRANSFORMADORES_REALES.md`: lectura de fotos actuales de los tres transformadores reales.
- `ANALISIS_TRAFO_ALIMENTACION_325V.md`: analisis del problema del PT real de 325 V AC y opciones de solucion.
- `MAPA_COLORES_ESQUEMA_HURRICANE.md`: leyenda del esquema coloreado por bloques.
- `Hurricane/CONFIRMED_Hurricane_Chillidoggy_schematic_v6_2013-05-01.jpg`: esquema electrico confirmado, referencia principal.
- `Hurricane/Hurricane_Chillidoggy_layout_v6_2013-04-26.gif`: layout confirmado version #6, referencia secundaria.
- `Hurricane/Hurricane_layout_v2_2013-04-04.jpg`: layout version #2, solo historico/comparativo.

## Reglas de confianza documental

- Solo el esquema confirmado y los dos layouts se consideran referencias utiles de Hurricane.
- Los archivos `Hurricane/NOT_MY_AMP_unknown_build_photo_*.jpg` no corresponden al ampli real y no deben usarse para diagnosticarlo.
- Los archivos `Hurricane/UNVERIFIED_*` son material no verificado.
- El esquema manda sobre el layout. El layout ayuda a ubicar, pero no valida el montaje.

## Seguridad

- No proponer encender el ampli como primer paso.
- Priorizar mediciones en frio, identificacion fisica de nodos, masas, transformadores, zocalos y jacks.
- Alta tension esperable: secundario de 295 VAC puede generar alrededor de 417 VDC sin carga.
- Actualizacion critica: el transformador de alimentacion real fotografiado indica 325 VAC / 130 mA, asi que la B+ sin carga puede acercarse a 460 VDC.
- Con EL84 instaladas, nunca alimentar sin altavoz o carga ficticia adecuada conectada al secundario correcto.
- Sin valvulas se pueden hacer algunas pruebas iniciales sin altavoz, pero sigue habiendo alta tension.

## Estado tecnico conocido

- Circuito: amplificador completo a valvulas, no solo previo.
- Previo: ECC83 / 12AX7.
- Potencia: 2 x EL84 push-pull segun el esquema Hurricane v6.
- Fuente: puente con 1N4007, filtros de 47 uF / 450 V, nodos `A`, `B`, `C`, `D`, `E`.
- Transformador indicado en esquema: TECM 323 A, primario 115+115 VAC, secundario 295 VAC / 130 mA y filamentos 6,3 VAC / 3 A.
- Transformador de alimentacion real fotografiado: primario 0-230 V, HT 325 V / 130 mA, filamentos 6,3 V C.T. / 3,5 A. Esto puede dar alrededor de 460 V DC sin carga.
- Transformador de salida real: Hammond 1750H, 6600 ohm C.T. / 8 ohm / 20 W, push-pull.
- Transformador de reverb real: Hammond 1750A, primario 22,8k, secundario 8 ohm, 3,5 W segun Hammond.
- El usuario ya midio continuidades basicas de masa y no vio corto directo claro de B+ a chasis.

## Forma preferida de trabajar

- Documentar por bloques: fuente, potencia, inversor, previo, loop, tonestack, master, reverb, masas.
- Crear una transcripcion de conexiones tipo "netlist humano", pero progresiva y legible.
- Marcar incertidumbres explicitamente en vez de inventar precision.
- Para calculos, indicar supuestos y rangos esperables, no valores absolutos falsamente exactos.
- Antes de medir con tension, crear tablas de comprobacion en frio para que el usuario pueda rellenarlas.
- Cuando haya varias soluciones, recomendar una ruta principal y explicar las renuncias: fidelidad al esquema, calidad sonora, seguridad, coste, disponibilidad en Europa/Espana y facilidad de montaje.
- Para componentes criticos de tono o seguridad, preferir opciones premium/fiables con margen adecuado.
- Al pasar de teoria a practica, convertir cada bloque en checklist de cableado, mediciones en frio y mediciones con tension.
- Mantener actualizada la memoria tecnica y la lista de pendientes cuando el usuario detecte fallos, decida compras o haga cambios fisicos.
- Usar SVG para graficos de forma de onda y diagramas visuales que deban verse bien en la memoria.
- Mantener la app web como herramienta visual del proyecto: esquema interactivo, bloques por colores, explicaciones y estado de reconstruccion.

## Siguiente accion recomendada

Continuar en `ANALISIS_ESQUEMA_HURRICANE.md`:

1. Usar `TRANSCRIPCION_COMPLETA_ESQUEMA_HURRICANE.md` como base de lectura del esquema.
2. Revisar zonas ambiguas contra `Hurricane/Hurricane_Chillidoggy_layout_v6_2013-04-26.gif`.
3. Definir la ruta de reconstruccion: conservar, corregir o sustituir bloques segun calidad/seguridad.
4. Actualizar `PENDIENTES_RECONSTRUCCION_HURRICANE.md` con cada fallo detectado por el usuario.
5. Preparar tabla de mediciones en frio.
6. Pedir fotos actuales del ampli real si se necesita comparar esquema/layout con montaje.
