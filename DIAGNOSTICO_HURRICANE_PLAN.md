# Plan de reconstruccion y diagnostico - Cornford Hurricane / Chillidoggy

Fecha de arranque: 2026-05-10

## Objetivo principal

Guiar la reconstruccion real del amplificador hasta convertirlo en un equipo seguro, estable y con alta calidad de sonido. El trabajo combina:

- Verificacion teorica del esquema.
- Seleccion y validacion de componentes.
- Comparacion entre esquema, layout y montaje fisico.
- Diagnostico del montaje existente.
- Reconstruccion ordenada por bloques.
- Mediciones en frio y con tension cuando proceda.
- Ajuste final orientado a buen sonido, bajo ruido, estabilidad y fiabilidad.

No se trata solo de lograr que el ampli "encienda"; el objetivo es que este correctamente implementado en la teoria y en la practica.

## 0. Estado documental encontrado

Documentacion principal en `Hurricane/`:

- `CONFIRMED_Hurricane_Chillidoggy_schematic_v6_2013-05-01.jpg`: esquema electrico Cornford Hurricane "Chillidoggy", Martin Kidd, schematic version #6, 01/05/2013. Confirmado como referencia.
- `Hurricane_Chillidoggy_layout_v6_2013-04-26.gif`: layout version #6, 26/04/2013. Confirmado como referencia.
- `Hurricane_layout_v2_2013-04-04.jpg`: layout version #2, 04/04/2013. Confirmado como referencia historica/comparativa.
- `UNVERIFIED_Hurricane_components_list.rtf`: lista parcial de componentes, no verificada contra el montaje real.
- `UNVERIFIED_chassis_drawing_01.jpg`, `UNVERIFIED_chassis_drawing_02.jpg`: planos/dimensiones de chasis no verificados.
- `NOT_MY_AMP_unknown_build_photo_*.jpg`: fotos de montaje que no deben asumirse como el ampli real ni como Hurricane.
- `UNVERIFIED_source_*.webloc`: enlaces originales a foro/imagen, no verificados como fuente fiable unica.

Documentacion relacionada en `Harlequin/`:

- Esquema y layouts del Cornford Harlequin.

Documentacion real del montaje:

- `Fotos Reales Implementacion/`: fotos actuales del ampli real.
- `TRANSFORMADORES_REALES.md`: lectura de las fotos de transformadores y comparacion con el esquema.

Documentacion de reconstruccion:

- `MEMORIA_PROYECTO_HURRICANE.md`: memoria tecnica por bloques, funcion y efecto sobre la senal.
- `PENDIENTES_RECONSTRUCCION_HURRICANE.md`: fallos detectados, compras, cambios de montaje y verificaciones.
- `DOCUMENTACION_PROYECTO_FORMATOS.md`: formatos recomendados para documentar el proyecto.
- `docs_assets/`: graficos SVG, incluidas formas de onda conceptuales.

## 1. Advertencia importante de reconciliacion

Las fotos renombradas como `NOT_MY_AMP_unknown_build_photo_*.jpg` muestran un transformador Hammond `125CSE`, marcado como single-ended 8 W / 60 mA. Eso no coincide con el Hurricane version #6, que usa etapa push-pull con 2 x EL84 y transformador de salida de primario 6-8 k.

Antes de diagnosticar el ampli real hay que confirmar fisicamente:

- Si el montaje real es realmente Hurricane push-pull con 2 x EL84.
- Si hay un transformador de salida push-pull, no un Hammond 125CSE single-ended.
- Si las fotos `NOT_MY_AMP_unknown_build_photo_*.jpg` son de otra fase del proyecto o de un proyecto Harlequin/otro ampli mezclado por error. No usarlas como guia para reparar el Hurricane real.

Hasta resolver esto, no se debe asumir que ningun layout corresponde exactamente al aparato real.

Actualizacion 2026-05-11:

- Las fotos reales muestran un transformador de salida Hammond 1750H, 6600 ohm C.T. / 8 ohm / 20 W, adecuado para push-pull.
- Las fotos reales muestran un transformador de reverb Hammond 1750A, coherente con el driver de reverb.
- Las fotos antiguas `NOT_MY_AMP_unknown_build_photo_*.jpg` quedan definitivamente fuera como referencia del ampli real.
- El transformador de alimentacion real indica 325 V AC / 130 mA, no 295 V AC como el esquema. Esto aumenta la B+ sin carga teorica hasta unos 460 V DC.

## 2. Regla de seguridad

No encender todavia.

Trabajar inicialmente con:

- Ampli desconectado de red.
- Condensadores descargados y verificados con voltimetro DC.
- Una sola mano cuando haya posibilidad de alta tension.
- Puntas con pinzas/cocodrilos siempre que sea posible.
- Multimetro y puntas con categoria/tension adecuadas.
- Sin EL84 instaladas hasta verificar fuente, cableado de zocalos y carga de salida.
- Con EL84 instaladas, nunca sin altavoz o carga ficticia adecuada conectada al secundario correcto del transformador de salida.
- El transformador real fotografiado tiene secundario de 325 V AC. La fuente puede acercarse a 460 V DC sin carga, asi que los condensadores de 450 V quedan especialmente comprometidos durante pruebas sin valvulas o con carga insuficiente.

## 3. Objetivo de la fase 1: identificar que aparato hay realmente

Crear una ficha fisica del ampli real:

- Numero y tipo de zocalos: ECC83/12AX7 y EL84.
- Modelo exacto del transformador de alimentacion.
- Modelo exacto del transformador de salida.
- Colores de cables de primario/secundario de ambos transformadores.
- Impedancias disponibles en salidas de altavoz.
- Presencia real de reverb, tanque, transformador de reverb y footswitch.
- Presencia real de loop send/return.
- Tipo y valor del fusible instalado.
- Tipo de interruptores: power y standby.

Fotos necesarias:

- Vista general interior completa, perpendicular y con buena luz.
- Primer plano fuente/rectificador/filtro.
- Primer plano IEC, fusible, power y standby.
- Primer plano transformador de salida y jacks de altavoz.
- Primer plano de cada zocalo, con pines visibles.
- Primer plano de cada placa/tag board por ambos lados si es accesible.
- Vista del panel de potes y jacks.

## 4. Objetivo de la fase 2: elegir una referencia unica

Referencia provisional:

- Usar `CONFIRMED_Hurricane_Chillidoggy_schematic_v6_2013-05-01.jpg` como esquema electrico base.
- Usar `Hurricane_Chillidoggy_layout_v6_2013-04-26.gif` como layout base.
- Mantener `Hurricane_layout_v2_2013-04-04.jpg` version #2 solo como material historico/comparativo.

Criterio:

- El esquema manda sobre el layout.
- El layout ayuda a ubicar componentes, pero no valida automaticamente el cableado.
- Cualquier diferencia entre montaje real y esquema se anota como desviacion, no se corrige a ciegas.

## 5. Mapa de nodos de fuente esperado en version #6

Segun el esquema Hurricane version #6:

- `A`: primer nodo B+, despues del puente rectificador y primer condensador de 47 uF / 450 V. Alimenta el centro/primario del transformador de salida.
- `B`: despues de resistencia 2k2 / 3 W desde `A`. Alimenta pantallas EL84 y red asociada.
- `C`: despues de resistencia 10k desde `B`. Alimenta inversor de fase / zona previa tardia.
- `D`: despues de resistencia 1k desde `C`. Alimenta etapas de previo/reverb intermedias.
- `E`: despues de resistencia 10k desde `D`. Alimenta primeras etapas de previo.

Condensadores de filtro:

- 47 uF / 450 V de cada nodo `A`, `B`, `C`, `D`, `E` a masa.

Valores a verificar en frio:

- `A-B`: 2k2.
- `B-C`: 10k.
- `C-D`: 1k.
- `D-E`: 10k.
- Positivo de cada condensador a masa: sin corto directo.
- Negativo de cada condensador a chasis/masa: continuidad baja.

## 6. Mediciones en frio, sin valvulas y sin red

### 6.1 Tierra y chasis

- Continuidad tierra IEC a chasis: muy baja resistencia.
- Tierra IEC fijada mecanicamente con punto dedicado, arandela dentada y sin depender de otros tornillos funcionales.
- Neutro/fase no conectados al chasis.
- Masa de circuito conectada al chasis segun el esquema/layout, sin multiples uniones accidentales.

### 6.2 Primario de red

- Continuidad desde IEC/fusible/power/primario del transformador segun interruptores.
- Fusible en fase, no en neutro.
- Power corta fase.
- Standby no debe interrumpir tierra ni neutro.
- Sin continuidad entre primario de red y chasis.
- Sin continuidad entre primario de red y secundarios.

### 6.3 Transformador de alimentacion

Con cables desconectados o al menos interpretando el circuito conectado:

- Resistencia DC del primario.
- Resistencia DC del secundario alta tension.
- Resistencia DC del secundario 6,3 V.
- Aislamiento basico: primario-chasis, primario-secundarios, HT-filamentos.

### 6.4 Rectificador y filtro

- Orientacion de los cuatro 1N4007 del puente.
- Continuidad/caida en modo diodo en cada 1N4007.
- Polaridad de todos los electroliticos.
- Existencia y valor de resistencias de caida entre nodos.
- Si hay resistencias bleeder, anotar valor y ubicacion; si no hay, valorar anadir una solucion segura mas adelante.

### 6.5 Transformador de salida y jacks de altavoz

- Confirmar modelo real: push-pull o single-ended.
- Primario: continuidad placa-placa y placa-centro si es push-pull.
- Secundario: continuidad comun a taps.
- Jacks de altavoz: tip/sleeve correctos, conmutaciones correctas y sin cortos indeseados.
- Confirmar que la carga se conecta al secundario correcto.

### 6.6 Zocalos

Para cada zocalo, dibujar pines vistos desde abajo y comprobar:

- ECC83/12AX7: filamentos pines 4, 5 y 9; placas 1/6; rejas 2/7; catodos 3/8.
- EL84: placa pin 7; pantalla pin 9; reja control pin 2; catodo pin 3; filamentos 4/5.
- Que no haya pines vecinos puenteados por soldadura.
- Que las resistencias de grid stopper esten fisicamente cerca de la reja cuando corresponda.

## 7. Comparacion esquema-layout-montaje

Crear una tabla por bloques:

- Fuente.
- Entrada y primera ganancia.
- Controles gain/volumen.
- Loop send/return.
- Tonestack.
- Master.
- Inversor de fase.
- Etapa 2 x EL84.
- Reverb driver/return.
- Salidas de altavoz.

Para cada componente:

- Referencia si existe.
- Valor en esquema.
- Valor en layout #6.
- Valor montado.
- Punto de inicio y fin real.
- Estado: OK / dudoso / no coincide / falta.

## 8. Primer encendido, solo despues de cerrar fases anteriores

No hacer esta fase hasta que las mediciones en frio no muestren errores graves.

Orden recomendado:

1. Sin valvulas, con limitador de corriente o bombilla en serie si se dispone.
2. Verificar 6,3 V AC de filamentos sin carga.
3. Verificar alta tension AC del secundario.
4. Verificar B+ DC en `A` a `E`, sabiendo que sin carga puede ser alta.
5. Apagar, descargar, verificar descarga.
6. Instalar solo valvulas de previo si procede y repetir mediciones de filamentos/B+.
7. Antes de instalar EL84: conectar altavoz/carga ficticia correcta.
8. Instalar EL84 y medir catodo, pantalla, placa y consumo estimado.

## 9. Calculos pendientes

Cuando el montaje real este identificado:

- Estimar B+ sin carga con el transformador real: 325 V AC * sqrt(2) menos caidas del puente, alrededor de 458-460 V DC.
- Estimar corriente disponible del transformador: 130 mA segun layout Hurricane #6.
- Calcular corriente de reposo de EL84 por caida en resistencia de catodo o metodo seguro equivalente.
- Calcular disipacion de placa aproximada.
- Estimar caidas `A-B-C-D-E` segun corrientes de cada bloque.
- Comparar tensiones de placas/catodos de ECC83 con valores razonables para cada etapa.

## 10. Siguiente accion recomendada

La siguiente sesion deberia centrarse en preparar la reconstruccion fisica con criterio:

1. Decidir la ruta de fuente de alimentacion: PT correcto o rediseño seguro alrededor del PT real.
2. Revisar el esquema contra layout y montaje por bloques.
3. Identificar fisicamente nodos `A`, `B`, `C`, `D`, `E` en la fuente.
4. Anotar resistencias medidas entre nodos de fuente con el ampli descargado.
5. Dibujar o fotografiar los zocalos por debajo y marcar pines.
6. Convertir cada bloque en checklist de reconstruccion/cableado.
