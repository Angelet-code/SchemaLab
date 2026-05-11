# Transcripcion completa del esquema - Cornford Hurricane / Chillidoggy v6

Referencia:

- `Hurricane/CONFIRMED_Hurricane_Chillidoggy_schematic_v6_2013-05-01.jpg`

Fecha de transcripcion inicial: 2026-05-10

## 0. Alcance y criterio

Este documento transcribe el esquema por bloques y por nodos. No es todavia una verificacion del montaje real.

Reglas usadas:

- El esquema confirmado es la fuente principal.
- El layout v6 se usa solo para ayudar a interpretar zonas densas.
- Cuando una conexion no se lee con total claridad, se marca como `CONFIRMAR`.
- Los nombres de valvulas son nombres de trabajo, no necesariamente los nombres fisicos del chasis.
- No se propone encender el ampli a partir de este documento.

## 1. Nodos globales

| Nodo | Funcion | Procedencia | Destinos principales |
|---|---|---|---|
| `GND` | Masa de circuito | Linea inferior del esquema | Entradas, catodos, filtros, jacks y retornos |
| `A` | Primer B+ filtrado | Salida positiva del puente rectificador | Centro del primario del transformador de salida |
| `B` | B+ despues de `A` | `A` mediante 2k2 / 3 W | Pantallas EL84 y transformador driver de reverb |
| `C` | B+ inversor | `B` mediante 10k | Placas del inversor de fase |
| `D` | B+ previo medio/reverb | `C` mediante 1k | Tercera/cuarta etapa de previo y recovery de reverb |
| `E` | B+ primeras etapas | `D` mediante 10k | Primeras dos etapas de previo |
| `HT_AC_1`, `HT_AC_2` | Alta tension AC | Secundario 295 VAC | Entradas AC del puente rectificador |
| `HEAT_6V3` | Filamentos | Secundario 6,3 VAC / 3 A | Filamentos de valvulas, no detallados en el esquema |

## 2. Valvulas y nombres de trabajo

| Nombre | Tipo | Pines dibujados | Funcion |
|---|---|---|---|
| `V1A_input` | ECC83 / 12AX7 | 6, 7, 8 | Primera etapa de previo |
| `V1B_gain` | ECC83 / 12AX7 | 1, 2, 3 | Segunda etapa de previo |
| `V2A_gain` | ECC83 / 12AX7 | 6, 7, 8 | Tercera etapa de previo antes del loop |
| `V2B_tone_driver` | ECC83 / 12AX7 | 1, 2, 3 | Etapa que ataca tonestack |
| `V3A_PI` | ECC83 / 12AX7 | marcado V9 | Mitad superior del inversor de fase |
| `V3B_PI` | ECC83 / 12AX7 | marcado V10 | Mitad inferior del inversor de fase |
| `V4_reverb_driver` | ECC83 / 12AX7 | sin pines legibles | Driver del transformador de reverb |
| `V5_reverb_recovery` | ECC83 / 12AX7 | sin pines legibles | Recuperador de reverb |
| `V6_EL84_top` | EL84 | simbolo superior | Potencia push-pull |
| `V7_EL84_bottom` | EL84 | simbolo inferior | Potencia push-pull |

## 3. Fuente de alimentacion

### 3.1 Transformador de alimentacion

Texto del esquema:

- Power transformer: `TECM 323 A`.
- Primario: `115 + 115 V AC`.
- Secundario alta tension: `295 V AC / 130 mA`.
- Secundario filamentos: `6,3 V AC / 3 A`.

### 3.2 Rectificador

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| `Br1` | `HT_AC_1`, `HT_AC_2` | `A`, `GND` | Puente rectificador |
| Diodos puente | Dentro de `Br1` | Dentro de `Br1` | 4 x 1N4007 |
| `C42` | Rama del puente | Rama del puente | Valor `???`, condensador antiparasitario |
| `C43` | Rama del puente | Rama del puente | Valor `???`, condensador antiparasitario |
| `C44` | Rama del puente | Rama del puente | Valor `???`, condensador antiparasitario |
| `C45` | Rama del puente | Rama del puente | Valor `???`, condensador antiparasitario |

Nota: los cuatro condensadores alrededor del puente aparecen con valor `???`. En el layout v6 se ven como condensadores ceramicos de alta tension, pero el valor exacto debe confirmarse.

### 3.3 Cadena de filtros B+

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Filtro `A` | `A` | `GND` | 47 uF / 450 V |
| `R1` | `A` | `B` | 2k2 / 3 W |
| Filtro `B` | `B` | `GND` | 47 uF / 450 V |
| `R2` fuente | `B` | `C` | 10k |
| Filtro `C` | `C` | `GND` | 47 uF / 450 V |
| `R3` fuente 1 | `C` | `D` | 1k |
| Filtro `D` | `D` | `GND` | 47 uF / 450 V |
| `R3` fuente 2 | `D` | `E` | 10k |
| Filtro `E` | `E` | `GND` | 47 uF / 450 V |

Nota: el esquema reutiliza `R3` para dos resistencias de la fuente. Conviene renombrarlas internamente como `Rdrop_C_D` y `Rdrop_D_E` en cualquier documento futuro.

Fallo de montaje detectado:

- Montado actualmente: `A -> 4k7 -> B -> 68k -> C -> 1k -> D -> 10k -> E`.
- Debe corregirse a la cadena indicada en esta tabla antes de alimentar.

## 4. Entrada y primera etapa de previo

### 4.1 Jacks de entrada

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Jack entrada alta/baja | Tip/switch | Red de entrada | Dos jacks con conmutacion a masa |
| Resistencia serie entrada 1 | Jack superior | Nodo entrada comun | 68k |
| Resistencia serie entrada 2 | Nodo entrada comun | Reja `V1A_input` | 68k |
| Resistencia vertical entrada | Nodo entrada comun | Nodo jack inferior / referencia | 68k |
| Resistencia referencia entrada | Nodo jack inferior / entrada | `GND` | 1M |

Lectura: es una red de entrada tipo hi/lo con jacks conmutados. La funcion es clara; el cableado exacto de contactos de jack debe verificarse fisicamente.

### 4.2 `V1A_input`

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Reja `V1A_input` | Pin 7 | Red de entrada | Tras 68k |
| Placa `V1A_input` | Pin 6 | `E` | 100k |
| Condensador placa `V1A_input` | Placa pin 6 | `E` | Aproximadamente 220p, en paralelo con carga de placa |
| Catodo `V1A_input` | Pin 8 | `GND` | 1k5 |
| Bypass catodo | Pin 8 | `GND` | 2,2 uF / 100 V, positivo al catodo |
| Acoplo salida | Placa pin 6 | Control `Volume_R2` | 33n seguido de 100k serie |

## 5. Primer control de volumen y segunda etapa

### 5.1 `Volume_R2`

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| `Volume_R2` extremo alto | Salida de `V1A_input` tras 33n + 100k | Pista pot | 100k Log, mitad `1/1` |
| `Volume_R2` extremo bajo | Pista pot | `GND` | Segun esquema |
| `Volume_R2` cursor | Potenciometro | `R11` | Hacia reja de segunda etapa |

### 5.2 `V1B_gain`

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| `R11` | Cursor `Volume_R2` | Reja pin 2 de `V1B_gain` | 68k |
| Placa `V1B_gain` | Pin 1 | `E` | 100k |
| Catodo `V1B_gain` | Pin 3 | `GND` | 1k5 |
| Acoplo salida | Placa pin 1 | Siguiente control `R16` | 4n7 ceramic disk |

## 6. Segundo control de volumen/gain y tercera etapa

### 6.1 `R16`

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| `R16` extremo alto | Salida de `V1B_gain` por 4n7 | Potenciometro | 100k Log, mitad `1/2` |
| `R16` extremo bajo | Potenciometro | `GND` | Segun esquema |
| `R16` cursor | Potenciometro | Reja `V2A_gain` | Mediante 68k |

### 6.2 Red adicional alrededor de `R16`

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Resistencia a masa 1 | Nodo salida 4n7 / entrada control | `GND` | 100k |
| Resistencia a masa 2 | Nodo salida/control asociado | `GND` | 100k |

Nota: estas dos resistencias aparecen alrededor del control de 100k log. La lectura de sus nodos concretos debe confirmarse con el layout antes de modificar cableado real.

### 6.3 `V2A_gain`

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Entrada `V2A_gain` | Cursor `R16` | Reja pin 7 | 68k |
| Placa `V2A_gain` | Pin 6 | `D` | 220k |
| Acoplo salida | Placa pin 6 | Nodo loop/send | 22n |
| Realimentacion local | Nodo despues de 22n | Catodo pin 8 | 470k |
| Catodo `V2A_gain` | Pin 8 | `GND` | 4k7 |

Nota: aqui la imagen se lee mejor con zoom: la resistencia de 470k parece ir desde el nodo posterior al condensador de 22n hacia el catodo; el catodo baja a masa por 4k7. Confirmar en layout/montaje.

## 7. Loop de efectos

### 7.1 Send / Return

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| `Send` | Nodo despues del acoplo 22n de `V2A_gain` | Jack Send | Salida de previo hacia loop |
| Normalizacion loop | `Send` | `Return` | Contactos conmutados en jacks |
| `Return` | Jack Return | Nodo retorno | Entrada de retorno del loop |
| Pull-down retorno | Nodo `Return` | `GND` | 1M |

Lectura: el loop parece pasivo/serie. Si no hay plug, la normalizacion de los jacks deberia llevar la senal de Send a Return. Esta zona es critica en el montaje real porque un jack mal cableado puede dejar el ampli mudo.

### 7.2 Divisor hacia etapa siguiente

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Resistencia superior divisor | Nodo retorno | Nodo intermedio | 100k |
| Resistencia inferior divisor | Nodo intermedio | `GND` | 100k |
| Resistencia serie grid | Nodo intermedio | Reja pin 2 de `V2B_tone_driver` | 68k |

## 8. Etapa driver de tonestack

### 8.1 `V2B_tone_driver`

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Reja `V2B_tone_driver` | Pin 2 | Divisor del loop | Mediante 68k |
| Placa `V2B_tone_driver` | Pin 1 | `D` | 220k |
| Condensador placa | Placa pin 1 | `D` | 470p, en paralelo con carga de placa |
| Catodo `V2B_tone_driver` | Pin 3 | `GND` | 1k5 |
| Salida placa | Placa pin 1 | Tonestack | Nodo principal de tono |

### 8.2 Red de tono asociada a la placa/catodo

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Resistencia tono | Nodo placa/salida | Nodo bajo de red tono | 68k |
| Condensador `C15` | Nodo bajo de red tono | Rama Bass/Middle | 100n |
| Condensador tono inferior | Nodo bajo de red tono | Rama Middle / masa | 33n |

Nota: esta parte forma la entrada al tonestack y debe leerse junto con los potes Treble, Bass y Middle.

## 9. Tonestack

### 9.1 Treble

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Condensador treble 1 | Nodo placa/salida `V2B_tone_driver` | Parte alta Treble | 470p |
| Condensador treble 2 | Nodo placa/salida `V2B_tone_driver` | Parte alta Treble | 220p |
| Pot `Treble` | Red de tono | Salida hacia Master | 220k Lin |
| Resistencia salida Treble | Cursor/salida Treble | Entrada Master | 22k |

### 9.2 Bass

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Pot `Bass` | Red de tono | Rama intermedia | 220k Log |
| Condensador asociado Bass/Master | Nodo salida tono | Rama Bass/Master | 470p |

### 9.3 Middle

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Pot `Middle` | Rama inferior de tonestack | `GND` | 22k Lin |
| Conexion inferior tonestack | Middle / red inferior | `GND` | Segun esquema |

Nota: el tonestack se lee como una red pasiva entre la placa de `V2B_tone_driver` y el Master. La funcion de cada pote es clara, pero para reconstruir fisicamente cada terminal del pote conviene usar layout y continuidad con multimetro.

## 10. Master y mezcla hacia inversor

### 10.1 Master

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Entrada Master | Salida tonestack tras 22k | Pot `Master` | 220k Log |
| Pot `Master` extremo bajo | Pot | `GND` | Segun esquema |
| Salida Master | Cursor | Condensador hacia inversor | 22n |

### 10.2 Acoplo hacia inversor

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Condensador entrada PI | Cursor Master | Reja/entrada PI | 22n |
| Resistencia referencia entrada PI | Nodo entrada PI | Nodo referencia PI | 1M |

Nota: la mezcla de reverb parece entrar cerca de esta zona mediante `R38`, pero el dibujo de los terminales del potenciometro de reverb no es completamente explicito. Ver seccion Reverb.

## 11. Inversor de fase

El inversor usa una ECC83 doble marcada como V9/V10 en el esquema.

### 11.1 Alimentacion y placas

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Placa `V3A_PI` | Placa mitad superior | `C` | 100k |
| Placa `V3B_PI` | Placa mitad inferior | `C` | 100k |
| Nodo `C` | Fuente B+ | Placas PI | Tambien filtro 47 uF a masa |

### 11.2 Entrada y red de polarizacion

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Entrada PI | Condensador 22n desde Master | Reja `V3A_PI` | Entrada de senal |
| Resistencia grid/reference superior | Reja `V3A_PI` | Nodo referencia PI | 1M |
| Resistencia grid/reference inferior | Nodo referencia PI | Reja/referencia `V3B_PI` | 1M |
| Resistencia referencia | Nodo referencia PI | Nodo a masa/retorno | 47k |
| Condensador referencia | Reja/referencia `V3B_PI` | Nodo a masa/retorno | 100n |
| Resistencia catodica/intermedia | Nodo referencia PI | Catodos PI | 1k5 |

Nota: la topologia exacta se lee como inversor diferencial/long-tail con red de referencia local. La conexion precisa de cada pin debe confirmarse contra layout antes de diagnosticar el zocalo.

### 11.3 Salidas del inversor

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Acoplo salida superior | Placa `V3A_PI` | Reja `V6_EL84_top` | 33n seguido de 4k7 |
| Acoplo salida inferior | Placa `V3B_PI` | Reja `V7_EL84_bottom` | 33n seguido de 4k7 |
| Referencia reja EL84 superior | Reja `V6_EL84_top` | Nodo bias/catodo/masa segun esquema | 220k |
| Referencia reja EL84 inferior | Reja `V7_EL84_bottom` | Nodo bias/catodo/masa segun esquema | 220k |

## 12. Etapa de potencia 2 x EL84

### 12.1 Placas y transformador de salida

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Primario OT centro | Nodo `A` | Centro primario OT | B+ principal |
| Primario OT extremo superior | Placa `V6_EL84_top` | OT | Salida push-pull |
| Primario OT extremo inferior | Placa `V7_EL84_bottom` | OT | Salida push-pull |
| Secundario OT | Altavoz / jacks | Carga | En esquema solo se dibuja el transformador, no los jacks |

### 12.2 Pantallas, rejas y catodos

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Pantalla `V6_EL84_top` | Nodo `B` | Pantalla EL84 superior | 220 Ohm serie |
| Pantalla `V7_EL84_bottom` | Nodo `B` | Pantalla EL84 inferior | 220 Ohm serie |
| Grid stopper superior | Salida PI superior | Reja `V6_EL84_top` | 4k7 |
| Grid stopper inferior | Salida PI inferior | Reja `V7_EL84_bottom` | 4k7 |
| Grid leak superior | Reja `V6_EL84_top` | Nodo referencia | 220k |
| Grid leak inferior | Reja `V7_EL84_bottom` | Nodo referencia | 220k |
| Catodos EL84 | Catodos comunes | `GND` | 220 Ohm |
| Bypass catodos EL84 | Catodos comunes | `GND` | 100 uF, positivo al catodo |

Nota de seguridad: con EL84 instaladas, el ampli no debe alimentarse sin altavoz o carga ficticia adecuada.

## 13. Reverb

### 13.1 Toma de senal hacia reverb driver

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Toma reverb | Bus de senal despues de primeras etapas | `R12` | Rama seca hacia driver de reverb |
| `R12` | Bus de senal | Reja `V4_reverb_driver` | Aproximadamente 68k |

Nota: la toma se dibuja bajando desde la zona de previo anterior al loop/tonestack. Confirmar el punto exacto contra layout si hay problemas de nivel de reverb.

### 13.2 `V4_reverb_driver` y transformador `Tr3`

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Reja `V4_reverb_driver` | `R12` | Reja ECC83 | Entrada driver |
| Placa `V4_reverb_driver` | ECC83 driver | Primario `Tr3` | Driver del transformador |
| Primario `Tr3` | Nodo `B` | Placa driver | Transformador con primario 22,275 Ohm segun texto |
| Catodo `V4_reverb_driver` | Catodo ECC83 | `GND` | `R35` 1k5 |
| Secundario `Tr3` | Salida reverb | `RevSEND` | Hacia tanque |
| Retorno secundario | Secundario `Tr3` | `GND` | Segun esquema |

### 13.3 Tanque y jacks de reverb

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| `RevSEND` | Secundario `Tr3` | Entrada tanque | Jack send de reverb |
| Tanque reverb | `RevSEND` | `RevRET` | Marcado 10 Ohm reverb tank |
| Retorno tanque | Salida tanque | `RevRET` | Entrada recovery |
| Mallas/retornos | Jacks reverb | `GND` | Segun esquema |

### 13.4 `V5_reverb_recovery`

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Reja recovery | `RevRET` | Reja ECC83 recovery | Entrada de tanque |
| Placa recovery | Placa ECC83 | `D` | `R37` 100k |
| Catodo recovery | Catodo ECC83 | `GND` | `R36` 1k5 |
| Bypass catodo recovery | Catodo recovery | `GND` | `C12` 2,2 uF / 100 V |
| Acoplo recovery | Placa recovery | Control reverb | `C14` 1000p |
| Control reverb | `C14` / mezcla | `GND` | `R38` 22k Lin |

Nota: el potenciometro `R38` actua como nivel/mix de reverb. En la imagen se ve un extremo a masa y el acoplo desde `C14`; el punto exacto de mezcla con la senal seca debe confirmarse con layout o continuidad.

### 13.5 Footswitch reverb

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Jack footswitch | Rama reverb | `GND` | Conmutacion para anular/activar reverb |

Lectura: el footswitch conmuta una rama de reverb a masa. El punto exacto de insercion debe verificarse en el layout/montaje.

## 14. Condensadores, resistencias y notas generales del esquema

Notas impresas en el layout v6 relacionadas con el esquema:

- Condensadores de film: 400 V.
- Condensadores ceramicos: no menos de 1 kV.
- Diodos: 1N4007.
- Resistencias: metal film 0,5 W, tolerancia +/-1% salvo potencia indicada.
- Electroliticos B+: 47 uF / 450 V.
- Electroliticos pequenos: 100 uF / 100 V y 2,2 uF / 63-100 V segun posicion.
- Potenciometros indicados: CTS/OMEG en la nota del layout.
- Tanques reverb sugeridos: Accutronics 8AB2A1B, Ruby RRVL-3AB2C1B, Accutronics 9AB2C1A o similar.

## 15. Zonas ambiguas que no deben corregirse a ciegas

| Zona | Ambiguedad | Accion recomendada |
|---|---|---|
| Condensadores del puente | Valores marcados `???` | Confirmar en layout o componente real |
| Jacks de entrada | Conmutacion fisica hi/lo | Verificar con continuidad del jack real |
| Red alrededor de `R16` | Dos resistencias de 100k a masa y terminales del pote | Comparar con layout antes de tocar |
| `V2A_gain` | Realimentacion 470k desde salida a catodo | Confirmar fisicamente; lectura probable |
| Tonestack | Terminal exacto de cada pote | Usar layout y multimetro |
| Inversor de fase | Red 1M/1M/47k/1k5/100n | Confirmar pin a pin en zocalo |
| `R38` reverb | Punto exacto de mezcla wet/dry | Confirmar con layout/continuidad |
| Footswitch reverb | Punto exacto que conmuta a masa | Confirmar con layout/continuidad |
| Secundario OT / jacks altavoz | No aparece detallado en esquema | Usar layout y transformador real |
| Filamentos | No aparecen cableados en esquema | Verificar en montaje real |

## 16. Orden recomendado para la siguiente revision

1. Revisar esta transcripcion contra `Hurricane_Chillidoggy_layout_v6_2013-04-26.gif`.
2. Crear una tabla de pines fisicos por zocalo.
3. Crear una tabla de mediciones en frio: resistencias entre nodos, cortos, continuidad de trafos y jacks.
4. Solo despues pasar a calculos de tensiones/corrientes esperadas.
