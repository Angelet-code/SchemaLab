# Transformadores reales identificados por fotos

Fecha de lectura: 2026-05-11

Carpeta de fotos:

- `Fotos Reales Implementacion/`

Fotos revisadas:

- `Fotos Reales Implementacion/trafo (1).jpeg`
- `Fotos Reales Implementacion/trafo (2).jpeg`
- `Fotos Reales Implementacion/trafo (3).jpeg`

## 1. Resumen

| Foto | Funcion probable | Identificacion visible | Lectura principal | Estado |
|---|---|---|---|---|
| `trafo (1).jpeg` | Transformador de alimentacion | Etiqueta sin marca visible | Primario 0-230 V; HT 325 V / 130 mA; filamentos 6,3 V C.T. / 3,5 A | Confirmado por foto |
| `trafo (2).jpeg` | Transformador de salida principal | Hammond 1750H | 20 W, 70 Hz - 15 kHz, 6600 ohm C.T., secundario 8 ohm | Confirmado por foto y ficha Hammond |
| `trafo (3).jpeg` | Transformador de reverb | Hammond 1750A | Etiqueta visible: 1750A; ficha Hammond: 22,8k primario, 8 ohm secundario, 3,5 W | Confirmado por foto y ficha Hammond |

## 2. Transformador de alimentacion

Foto:

- `Fotos Reales Implementacion/trafo (1).jpeg`

Texto visible en etiqueta:

```text
pri.: 0-230V (50Hz)
      blue-blue
sec.1: 325V (130mA)
       red-red
sec.2: 6,3V C.T. (3,5A)
       brown-brown
```

Lectura:

- Primario: 230 V AC, 50 Hz.
- Cables primario: azul-azul.
- Secundario alta tension: 325 V AC, 130 mA.
- Cables alta tension: rojo-rojo.
- Secundario filamentos: 6,3 V AC con toma central, 3,5 A.
- Cables filamentos: marron-marron; la toma central debe identificarse fisicamente.

Comparacion con esquema Hurricane v6:

| Dato | Esquema v6 | Transformador real |
|---|---:|---:|
| Alta tension AC | 295 V AC | 325 V AC |
| Corriente HT | 130 mA | 130 mA |
| Filamentos | 6,3 V / 3 A | 6,3 V C.T. / 3,5 A |
| Primario | 115 + 115 V AC | 0-230 V AC |

Implicacion de seguridad:

- Con 295 V AC, la tension teorica sin carga era aproximadamente `295 * sqrt(2) = 417 V DC`.
- Con el transformador real de 325 V AC, la tension teorica sin carga sube a `325 * sqrt(2) = 460 V DC`.
- Restando caidas del puente, el primer nodo `A` podria seguir rondando aproximadamente 458 V DC sin carga.
- Esto es especialmente importante porque el esquema usa condensadores de filtro de 47 uF / 450 V. Sin carga, con red alta o valvulas quitadas, se podria rozar o superar la tension nominal de los electroliticos.

Acciones recomendadas antes de cualquier encendido:

- Confirmar con multimetro la continuidad del primario azul-azul.
- Confirmar la resistencia DC del secundario rojo-rojo.
- Identificar fisicamente la toma central del secundario de filamentos.
- Confirmar que la toma central de filamentos, si esta usada, no crea una masa accidental incorrecta.
- No alimentar la fuente sin revisar la tension nominal real de todos los electroliticos de B+.
- Considerar limitador de corriente y medicion inicial sin valvulas solo si la cadena de condensadores soporta la tension sin carga.

## 3. Transformador de salida principal

Foto:

- `Fotos Reales Implementacion/trafo (2).jpeg`

Texto visible en etiqueta:

```text
Hammond 1750H
20 Watts 70Hz - 15kHz
BRN-RED-BLU: 6600 ohm C.T.
BLK-GRN: 8 ohm
Made in Canada
4515
```

Lectura:

- Modelo: Hammond 1750H.
- Potencia: 20 W.
- Primario: 6600 ohm con toma central.
- Cables primario segun etiqueta: brown-red-blue.
- Secundario: 8 ohm.
- Cables secundario segun etiqueta: black-green.
- Tipo: push-pull.

Encaje con el esquema:

- El esquema pide transformador de salida push-pull para 2 x EL84, primario indicado como 6-8k.
- El Hammond 1750H de 6,6k C.T. / 8 ohm encaja muy bien con esa necesidad.
- Esta foto elimina la sospecha anterior de que el ampli real usara un Hammond 125CSE single-ended. Aquellas fotos antiguas siguen clasificadas como `NOT_MY_AMP`.

Comprobaciones en frio:

- Medir resistencia DC entre brown-red y red-blue.
- Medir resistencia DC brown-blue.
- Confirmar que red es la toma central del primario antes de conectarlo al nodo `A`.
- Medir continuidad entre black-green.
- Confirmar que black/green van a los jacks de altavoz/carga de 8 ohm.
- Confirmar que no hay continuidad entre primario y secundario.
- Confirmar que no hay continuidad accidental de primario a chasis.

Fuente externa consultada:

- Hammond 1750H: `https://www.hammfg.com/part/1750H`

## 4. Transformador de reverb

Foto:

- `Fotos Reales Implementacion/trafo (3).jpeg`

Texto visible en etiqueta:

```text
Hammond 1750A
415
Made in Canada
```

Lectura por foto:

- Modelo visible: Hammond 1750A.
- Codigo visible: 415.
- No se ven impresas impedancias en esta cara del transformador.

Datos de ficha Hammond:

- Primario: 22,8k.
- Secundario: 8 ohm.
- Potencia: 3,5 W.
- Tipo indicado por fabricante: single ended.
- Uso/descripcion: transformador de salida Fender 3,5 W, secundario 8 ohm.

Encaje con el esquema:

- El esquema Hurricane v6 indica para reverb un transformador con primario de aproximadamente 22,275 ohm y tanque de reverb de 10 ohm.
- El Hammond 1750A, con primario 22,8k y secundario 8 ohm, parece coherente como transformador driver de reverb.
- Hay que verificar el cableado real porque el esquema llama al transformador `Tr3` y el tanque aparece como `10 ohm reverb tank`.

Comprobaciones en frio:

- Identificar pares de cables primario/secundario.
- Medir resistencia DC del primario.
- Medir resistencia DC del secundario.
- Confirmar que el primario va entre nodo `B` y placa del driver de reverb.
- Confirmar que el secundario va al jack/tanque `RevSEND`.
- Confirmar que no hay continuidad entre primario y secundario.

Fuente externa consultada:

- Hammond 1750A: `https://www.hammfg.com/part/1750A`

## 5. Impacto en el diagnostico

Hallazgos principales:

1. El transformador de salida principal real es adecuado para una etapa push-pull 2 x EL84.
2. El transformador de reverb real parece adecuado para el driver de reverb del esquema.
3. El transformador de alimentacion real tiene 325 V AC en alta tension, no 295 V AC.

La diferencia de alta tension cambia las prioridades:

- La revision de la fuente pasa a ser aun mas critica.
- Hay que comprobar tension nominal, estado y polaridad de electroliticos antes de alimentar.
- La primera prueba sin valvulas puede generar una B+ cercana a 460 V DC, por encima de la tension nominal de condensadores de 450 V si la red esta alta o no hay carga suficiente.
- Conviene valorar si se necesita una estrategia de arranque con carga, variac, limitador, resistencias bleeder y medicion cuidadosamente planificada.

