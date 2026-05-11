# Analisis del esquema - Cornford Hurricane / Chillidoggy v6

Referencia base confirmada:

- `Hurricane/CONFIRMED_Hurricane_Chillidoggy_schematic_v6_2013-05-01.jpg`

Transcripcion completa v1:

- `TRANSCRIPCION_COMPLETA_ESQUEMA_HURRICANE.md`

Objetivo de este documento:

- Transcribir el esquema electrico a conexiones legibles.
- Separar bloques funcionales.
- Crear una lista de comprobaciones contra el montaje real.
- Calcular tensiones, corrientes y disipaciones esperadas cuando sea posible.
- Marcar explicitamente las zonas ambiguas de la imagen.

## 1. Calidad de lectura del esquema

La imagen es suficientemente legible para:

- Identificar bloques funcionales.
- Leer la mayoria de valores de resistencias y condensadores.
- Seguir los nodos de alimentacion `A`, `B`, `C`, `D`, `E`.
- Entender el recorrido general de senal desde entrada hasta etapa de potencia.
- Preparar mediciones en frio y puntos de verificacion.

La imagen no debe tratarse como infalible para:

- Componentes marcados como `???`.
- Referencias de componentes duplicadas o poco claras.
- Valores pequenos o textos parcialmente borrosos.
- Cableado fisico exacto de zocalos, jacks y masas.

## 2. Metodo de estudio

Orden recomendado:

1. Fuente de alimentacion y nodos `A` a `E`.
2. Etapa de potencia 2 x EL84 y transformador de salida.
3. Inversor de fase con ECC83.
4. Cadena de previo principal.
5. Tonestack, master y loop.
6. Reverb: driver, transformador, tanque y recovery.
7. Masas y retornos.
8. Tabla final de tensiones/corrientes esperadas.

Para cada bloque se documentara:

- Conexiones electricas.
- Funcion del bloque.
- Valores criticos.
- Tensiones DC esperadas.
- Corrientes aproximadas.
- Comprobaciones en frio.
- Comprobaciones con tension, solo cuando sea seguro.
- Posibles errores de montaje que producirian fallo.

## 3. Identificacion de partes del esquema

| Bloque | Zona en el esquema | Funcion | Alimentacion principal | Estado de lectura |
|---|---|---|---|---|
| Entrada | Extremo izquierdo, dos jacks | Entrada alta/baja o entrada con conmutacion, resistencias de entrada y referencia a masa | No aplica | Legible, pero hay que confirmar jacks fisicos |
| Primera etapa ECC83 | Primer triodo de la izquierda, pines dibujados 6/7/8 | Primera ganancia de previo | `E` | Legible |
| Control de volumen/gain inicial | Entre primera y segunda etapa | Atenua senal y fija nivel hacia la segunda etapa | No aplica | Legible |
| Segunda etapa ECC83 | Segundo triodo, pines 1/2/3 | Ganancia adicional | `E` | Legible |
| Control intermedio `R16` | Entre segunda y tercera etapa | Segunda mitad del control de volumen/gain o control doble asociado | No aplica | Legible en valor, revisar cableado en layout |
| Tercera etapa ECC83 | Tercer triodo, pines 6/7/8 | Ganancia previa a loop/tonestack | `D` | Parcialmente legible |
| Loop de efectos | Parte superior central, jacks `Send` y `Return` | Insercion entre previo y tonestack/driver posterior | No aplica | Conexion funcional legible, normalizacion de jack a confirmar |
| Driver de tonestack ECC83 | Triodo central, pines 1/2/3 | Recupera/ataca la red de tono | `D` | Legible |
| Tonestack | Treble/Bass/Middle | Ecualizacion pasiva | No aplica | Legible |
| Master | Potenciometro `Master 220K Log` | Control de nivel hacia inversor | No aplica | Legible |
| Inversor de fase ECC83 | Doble triodo a la derecha, marcado V9/V10 | Genera dos senales opuestas para EL84 | `C` | Legible |
| Etapa de potencia | 2 x EL84 y transformador de salida | Salida push-pull | `A` placas, `B` pantallas | Legible |
| Fuente B+ | Abajo derecha | Rectificacion y filtrado `A-B-C-D-E` | 295 VAC | Legible salvo condensadores `???` del puente |
| Reverb driver | Abajo centro-izquierda, ECC83 y transformador `Tr3` | Excita tanque de reverb | `B` | Legible a nivel de bloque |
| Reverb recovery/mix | Abajo centro, ECC83, `RevRET`, `RevSEND`, `R38` | Recupera senal del tanque y mezcla | `D` | Parcialmente legible |
| Footswitch reverb | Abajo izquierda | Conmuta/anula reverb a masa | No aplica | Legible a nivel funcional |

## 4. Convenciones para la transcripcion

Para evitar confusiones, cada valvula se nombra por funcion y por posicion aproximada en el esquema:

| Nombre de trabajo | Tipo | Ubicacion | Funcion |
|---|---|---|---|
| `V1A_input` | ECC83 triodo | Izquierda, pines 6/7/8 | Primera etapa de previo |
| `V1B_gain` | ECC83 triodo | Izquierda-centro, pines 1/2/3 | Segunda etapa de previo |
| `V2A_gain` | ECC83 triodo | Centro, pines 6/7/8 | Tercera etapa de previo |
| `V2B_tone_driver` | ECC83 triodo | Centro-derecha, pines 1/2/3 | Driver antes de tonestack |
| `V3_phase_inverter` | ECC83 doble | Derecha, V9/V10 | Inversor de fase |
| `V4_reverb_driver` | ECC83 triodo | Abajo izquierda-centro | Driver del transformador de reverb |
| `V5_reverb_recovery` | ECC83 triodo | Abajo centro | Recuperador de reverb |
| `V6_power_top` | EL84 | Arriba derecha | Valvula de potencia superior |
| `V7_power_bottom` | EL84 | Abajo derecha | Valvula de potencia inferior |

Estos nombres son temporales. Cuando se compare con el layout y el ampli real, conviene sustituirlos por las designaciones fisicas de zocalo.

## 5. Transcripcion - fuente de alimentacion

Transformador de alimentacion indicado en el esquema:

- Modelo: TECM 323 A.
- Primario: 115 + 115 V AC.
- Secundario alta tension: 295 V AC, 130 mA.
- Secundario filamentos: 6,3 V AC, 3 A.

Rectificador:

- Puente con cuatro diodos 1N4007.
- Hay condensadores pequenos alrededor del puente marcados como `???` en la imagen; quedan pendientes de confirmar.

Filtro y cadena B+:

- `A`: primer nodo despues del rectificador.
- `A` a masa: 47 uF / 450 V.
- `A` a `B`: 2k2 / 3 W.
- `B` a masa: 47 uF / 450 V.
- `B` a `C`: 10k.
- `C` a masa: 47 uF / 450 V.
- `C` a `D`: 1k.
- `D` a masa: 47 uF / 450 V.
- `D` a `E`: 10k.
- `E` a masa: 47 uF / 450 V.

Calculo inicial sin carga:

- 295 V AC * sqrt(2) = 417 V pico aproximadamente.
- Restando dos caidas de diodo en puente, `A` podria estar alrededor de 415 V DC sin carga.
- Con valvulas y consumo real, `A` deberia caer de forma apreciable; el valor exacto depende del transformador real, consumo de EL84 y resistencia de devanado.

Comprobaciones en frio:

- `A-B`: aproximadamente 2,2 kOhm.
- `B-C`: aproximadamente 10 kOhm.
- `C-D`: aproximadamente 1 kOhm.
- `D-E`: aproximadamente 10 kOhm.
- Positivo de cada electrolitico a masa: sin corto directo.
- Negativo de cada electrolitico a masa/chasis: continuidad segun el esquema de masas real.

Fallo detectado en el montaje real:

- Correcto segun esquema: `A -> 2k2 / 3W -> B -> 10k -> C -> 1k -> D -> 10k -> E`.
- Montado actualmente segun el usuario: `A -> 4k7 -> B -> 68k -> C -> 1k -> D -> 10k -> E`.
- Consecuencia probable: caidas de tension excesivas hacia `C`, `D` y `E`, especialmente por los 68k entre `B` y `C`; el inversor y previo podrian quedar con tensiones demasiado bajas o comportarse de forma anomala.
- Accion: corregir antes de cualquier prueba con tension.

## 6. Transcripcion - etapa de potencia 2 x EL84

Etapa:

- 2 x EL84 en push-pull.
- Transformador de salida con primario para push-pull.
- Nodo `A` alimenta el centro del primario del transformador de salida.
- Placas de las EL84 conectadas a los extremos del primario.
- Nodo `B` alimenta pantallas/rejillas pantalla a traves de resistencias de 220 Ohm.
- Catodos de ambas EL84 unidos con resistencia comun de 220 Ohm a masa.
- Condensador de bypass de catodo: 100 uF.
- Cada reja de control recibe senal desde inversor a traves de resistencia serie 4k7.

Comprobaciones criticas:

- Confirmar que el transformador de salida real es push-pull, no single-ended.
- Confirmar continuidad placa-placa y placa-centro en primario.
- Confirmar que la carga de altavoz esta conectada antes de instalar EL84.
- Confirmar resistencia catodo comun: 220 Ohm.
- Confirmar polaridad del condensador de 100 uF de catodo.

Conexiones de trabajo:

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Primario OT, centro | Nodo `A` | Centro del primario del transformador de salida | B+ principal |
| Primario OT, extremo 1 | Placa de `V6_power_top` | Transformador de salida | Placa EL84 superior |
| Primario OT, extremo 2 | Placa de `V7_power_bottom` | Transformador de salida | Placa EL84 inferior |
| Pantalla `V6_power_top` | Nodo `B` | Pantalla EL84 superior | A traves de 220 Ohm |
| Pantalla `V7_power_bottom` | Nodo `B` | Pantalla EL84 inferior | A traves de 220 Ohm |
| Reja control `V6_power_top` | Salida alta del inversor | Reja EL84 superior | Serie 4k7 |
| Reja control `V7_power_bottom` | Salida baja del inversor | Reja EL84 inferior | Serie 4k7 |
| Retorno de rejas | Rejas EL84 | Masa / referencia bias | Dos resistencias de 220k segun esquema |
| Catodos EL84 | Catodos comunes | Masa | 220 Ohm compartidos |
| Bypass catodo EL84 | Catodos comunes | Masa | 100 uF, polaridad positiva al catodo |

Notas:

- La etapa parece con polarizacion por catodo comun, no fixed bias.
- La corriente total de ambas EL84 se podra estimar midiendo la tension DC sobre la resistencia comun de 220 Ohm.
- Esa medicion incluye corriente de placa y pantalla de ambas EL84.

## 7. Transcripcion - inversor de fase

Lectura funcional:

- Doble triodo ECC83 marcado en el esquema como V9/V10.
- Alimentado desde nodo `C`.
- Las dos placas van a `C` mediante resistencias de 100k.
- Las salidas hacia las EL84 salen de las placas mediante condensadores de 33n.
- Cada salida acopla a una EL84 mediante resistencia serie 4k7.
- Hay dos resistencias de 220k asociadas a las rejas de las EL84 como referencias a masa/bias.
- Entrada al inversor desde `Master` mediante condensador de 22n.
- En la entrada hay una resistencia de 1M a masa.
- Aparece una red con 47k, 1M, 1k5 y 100n entre la entrada, catodos y masa; corresponde al circuito de polarizacion/realimentacion local del inversor.

Conexiones de trabajo:

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Alimentacion placas PI | Nodo `C` | Placas de ambos triodos ECC83 | Cada rama con 100k |
| Acoplo salida PI superior | Placa triodo superior | Reja `V6_power_top` | 33n seguido de 4k7 |
| Acoplo salida PI inferior | Placa triodo inferior | Reja `V7_power_bottom` | 33n seguido de 4k7 |
| Referencia reja EL84 superior | Reja `V6_power_top` | Masa/referencia bias | 220k |
| Referencia reja EL84 inferior | Reja `V7_power_bottom` | Masa/referencia bias | 220k |
| Entrada PI | Salida de master via 22n | Reja de entrada del inversor | Con 1M a masa |
| Red catodica PI | Catodos / nodo comun | Masa | 1k5 y red asociada; revisar contra layout |
| Condensador PI | Red catodica/entrada | Masa o nodo asociado | 100n; conexion exacta a confirmar al comparar layout |

Comprobaciones en frio:

- Confirmar dos resistencias de placa de 100k desde nodo `C`.
- Confirmar dos condensadores de acoplo de 33n hacia EL84.
- Confirmar dos resistencias serie 4k7 cerca de rejas EL84.
- Confirmar dos resistencias de referencia de 220k en rejas EL84.
- Confirmar que no hay continuidad DC desde placas del inversor a rejas EL84 a traves de los condensadores.

## 8. Transcripcion - previo principal hasta el tonestack

### 8.1 Entrada y primera etapa `V1A_input`

Lectura funcional:

- Dos jacks de entrada con red de 68k/68k/1M.
- La reja de `V1A_input` entra por pin 7 segun el dibujo.
- Catodo pin 8 con 1k5 a masa y condensador de bypass 2,2 uF / 100 V.
- Placa pin 6 con resistencia de 100k hacia nodo `E`.
- Hay un condensador pequeno de aproximadamente 220p asociado entre la zona de placa/alimentacion y la placa; marcar como red de brillo/estabilidad pendiente de confirmar.
- Salida por condensador de 33n y resistencia serie de 100k hacia el primer control de volumen/gain.

Conexiones de trabajo:

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Resistencia entrada serie 1 | Jack entrada | Nodo entrada | 68k |
| Resistencia entrada serie 2 | Nodo entrada | Reja `V1A_input` | 68k |
| Referencia entrada | Nodo entrada/jack | Masa | 1M y red de jack |
| Placa `V1A_input` | Pin 6 | Nodo `E` | 100k |
| Catodo `V1A_input` | Pin 8 | Masa | 1k5 |
| Bypass catodo | Pin 8 | Masa | 2,2 uF / 100 V |
| Acoplo salida | Placa `V1A_input` | Primer control | 33n + 100k serie |

### 8.2 Segunda etapa `V1B_gain`

Lectura funcional:

- Entrada desde el primer control de volumen/gain mediante resistencia de 68k marcada `R11`.
- Reja por pin 2.
- Placa pin 1 con 100k a nodo `E`.
- Catodo pin 3 con 1k5 a masa.
- Salida desde placa por condensador de 4n7 ceramico hacia el control `R16` de 100k log.

Conexiones de trabajo:

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Entrada `V1B_gain` | Control anterior | Reja pin 2 | 68k `R11` |
| Placa `V1B_gain` | Pin 1 | Nodo `E` | 100k |
| Catodo `V1B_gain` | Pin 3 | Masa | 1k5 |
| Acoplo salida | Placa pin 1 | Control `R16` | 4n7 ceramic disk |
| Control `R16` | Salida etapa 2 | Entrada etapa 3 | 100k Log, mitad indicada como `1/2` |

### 8.3 Tercera etapa `V2A_gain`

Lectura funcional:

- Entrada desde `R16` mediante 68k.
- Reja por pin 7.
- Placa pin 6 con 220k hacia nodo `D`.
- Catodo pin 8 con red de 470k/4k7 dibujada hacia masa; esta zona requiere contraste con layout porque no es una catodo comun tipico simple.
- Salida desde placa por condensador de 22n hacia la zona de loop/driver posterior.

Conexiones de trabajo:

| Elemento | Conexion 1 | Conexion 2 | Valor / nota |
|---|---|---|---|
| Entrada `V2A_gain` | Wiper/control `R16` | Reja pin 7 | 68k |
| Placa `V2A_gain` | Pin 6 | Nodo `D` | 220k |
| Catodo/red local | Pin 8 | Masa / red asociada | 470k y 4k7 visibles; pendiente de confirmar |
| Acoplo salida | Placa pin 6 | Siguiente bloque | 22n |

## 9. Pendientes de transcripcion

Pendiente documentar con detalle:

- Loop send/return.
- Tonestack treble/bass/middle.
- Master.
- Reverb driver/recovery.
- Footswitch reverb.
- Asignacion completa de nodos `A` a `E` a cada triodo.
