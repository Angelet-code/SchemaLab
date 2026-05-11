# Analisis del transformador de alimentacion real de 325 V AC

Fecha: 2026-05-11

Referencia:

- Foto real: `Fotos Reales Implementacion/trafo (1).jpeg`
- Lectura completa: `TRANSFORMADORES_REALES.md`
- Esquema base: `Hurricane/CONFIRMED_Hurricane_Chillidoggy_schematic_v6_2013-05-01.jpg`

## 1. Problema detectado

El esquema Hurricane / Chillidoggy v6 indica:

- Secundario alta tension: 295 V AC / 130 mA.
- Filamentos: 6,3 V AC / 3 A.

El transformador real fotografiado indica:

- Secundario alta tension: 325 V AC / 130 mA.
- Filamentos: 6,3 V AC C.T. / 3,5 A.

La corriente disponible de alta tension es la misma, pero la tension es aproximadamente un 10,2% superior:

```text
325 / 295 = 1,102
```

Esto no es un detalle menor: afecta a la tension maxima de los condensadores, al B+ real, al bias por catodo de las EL84 y a la disipacion.

## 2. Tension DC sin carga

La fuente es rectificacion por puente con filtro capacitivo.

Estimacion ideal:

```text
B+ sin carga ~= Vac * sqrt(2) - caidas de diodos
```

| Secundario | Pico teorico | B+ aproximado sin carga |
|---:|---:|---:|
| 295 V AC esquema | 417 V | 415 V DC |
| 325 V AC real | 460 V | 458 V DC |

Implicacion:

- Con el transformador real, el primer nodo `A` puede acercarse a 460 V DC sin valvulas.
- Los electroliticos del esquema son de 47 uF / 450 V.
- Por tanto, una prueba sin valvulas puede poner los condensadores justo en el limite o por encima.

## 3. Efecto de la red electrica

Si la red real esta por encima de 230 V, el problema empeora.

Ejemplos aproximados:

| Red real | Secundario equivalente | Pico teorico |
|---:|---:|---:|
| 220 V | 311 V AC | 440 V DC |
| 230 V | 325 V AC | 460 V DC |
| 240 V | 339 V AC | 479 V DC |
| 250 V | 353 V AC | 499 V DC |

Conclusion:

- Con una red alta, condensadores de 450 V quedan claramente insuficientes para pruebas sin carga.
- Antes de alimentar, interesa medir la tension real de red en el taller.

## 4. Efecto con valvulas instaladas

Con carga real, el B+ bajara respecto al valor sin carga por:

- Resistencia interna del transformador.
- Caida en diodos.
- Corriente de las EL84.
- Corriente de pantallas, previo y reverb.
- Caidas en la cadena `A-B-C-D-E`.

Pero hay dos problemas:

1. No sabemos todavia cuanto bajara.
2. El primer encendido seguro suele hacerse sin valvulas o con carga parcial, justo cuando el B+ sube mas.

Ademas, con mas B+:

- Las EL84 pueden disipar mas potencia.
- La resistencia de catodo comun de 220 ohm puede no dejar el punto de reposo donde interesa.
- Las pantallas de las EL84 tambien pueden quedar mas exigidas.
- El ampli puede sonar y comportarse distinto al Hurricane esperado.

## 5. Opciones tecnicas

### Opcion A - Sustituir el transformador de alimentacion por uno mas cercano al esquema

Buscar un transformador con:

- Primario 230 V AC.
- Secundario HT alrededor de 290-0 / 295 V AC, adecuado para puente rectificador segun el esquema.
- Corriente HT en torno a 130 mA o superior razonable.
- Filamentos 6,3 V con corriente suficiente para 2 x EL84 + ECC83 + margen.

Ventajas:

- Es la solucion mas limpia.
- Mantiene el diseno cerca del esquema original.
- Reduce el problema de sobretension sin carga.
- Simplifica calculos y diagnostico.

Inconvenientes:

- Coste.
- Trabajo mecanico si no encaja en el chasis.
- Hay que verificar dimensiones, fijacion y cableado.

Valoracion:

- Es la opcion preferente si quieres un Hurricane fiel, estable y diagnosticable.

### Opcion B - Mantener el transformador real y redisenar la fuente para soportar la tension

Medidas minimas:

- Cambiar electroliticos B+ de 450 V por margen superior real.
- Usar condensadores de 500 V, 550 V o parejas en serie con resistencias de equilibrado, segun espacio y disponibilidad.
- Anadir resistencias bleeder adecuadas.
- Revisar tension nominal de todos los condensadores conectados a B+.
- Recalcular caidas `A-B-C-D-E`.
- Medir corriente y disipacion de EL84 antes de dar por valido el bias.

Ventajas:

- Aprovecha el transformador ya montado.
- Puede funcionar si el punto de trabajo queda bajo control.

Inconvenientes:

- Ya no es simplemente "montar el esquema".
- La B+ sera mas alta salvo que se anada caida.
- Requiere mas calculo, medicion y posiblemente modificar resistencias de fuente y catodo.
- Una resistencia serie o zener puede bajar tension bajo carga, pero no siempre protege bien el pico sin carga de todos los nodos si no se disena con cuidado.

Valoracion:

- Viable, pero solo si aceptamos redisenar parte de la fuente y validar el punto de trabajo.

### Opcion C - Bajar tension con zeners, MOSFET capacitance multiplier o regulador pasivo

Posibles enfoques:

- Zeners en el retorno del puente o en la linea B+.
- MOSFET source follower / capacitance multiplier para reducir y suavizar B+.
- Resistencia serie/choke/resistencia de sag antes de la cadena B+.

Ventajas:

- Permite conservar el transformador.
- Puede ajustar B+ hacia valores cercanos al esquema.

Inconvenientes:

- Introduce mas componentes sometidos a alta tension.
- Necesita calculo de disipacion termica.
- Puede cambiar la respuesta dinamica del ampli.
- No elimina por si solo la necesidad de condensadores con margen suficiente.

Valoracion:

- Opcion avanzada. No la elegiria como primera solucion en una reparacion inicial.

### Opcion D - Usar bucking transformer en el primario

Un bucking transformer reduce la tension de red antes del primario del transformador principal.

Ejemplo:

- Si bajas 230 V a unos 210 V, el secundario de 325 V baja proporcionalmente a unos 297 V.

Ventajas:

- Mantiene el transformador actual.
- Reduce tambien filamentos, asi que hay que comprobar que no queden bajos.
- Es reversible y no altera tanto la fuente interna.

Inconvenientes:

- Requiere otro transformador.
- Hay que montarlo de forma segura para red.
- Si se baja demasiado, los filamentos pueden quedar por debajo de rango.
- No arregla el ampli por si mismo: solo adapta la alimentacion.

Valoracion:

- Tecnica interesante para pruebas o para conservar el transformador actual, pero menos limpia que usar un PT correcto.

## 6. Recomendacion

La solucion que mas interesa adoptar, en este proyecto concreto, es:

1. No encender todavia.
2. Medir en frio y documentar el transformador real.
3. Asumir que los condensadores B+ de 450 V no tienen margen suficiente para pruebas sin carga con este PT.
4. Decidir entre dos caminos:

Camino recomendado:

- Sustituir el transformador de alimentacion por uno con HT mas cercana a 295 V AC.
- Mantener el resto del diseno mas fiel al esquema.
- Despues diagnosticar el ampli con menos variables.

Camino alternativo si quieres conservar el PT actual:

- Redisenar la fuente para 325 V AC.
- Cambiar/asegurar electroliticos con margen de tension suficiente.
- Anadir bleeders.
- Recalcular bias de EL84.
- Medir tension real de red.
- Preparar arranque con limitador/variac/carga y procedimiento escrito.

Mi recomendacion practica:

- Para una reparacion ordenada y segura, elegiria cambiar el transformador de alimentacion o usar una reduccion externa bien disenada antes que intentar "absorber" el exceso dentro del circuito original.
- Si el objetivo es aprender y documentar, conservar el PT actual es posible, pero convierte el proyecto en una adaptacion de diseno, no solo en una reparacion del Hurricane.

Actualizacion de decision:

- El usuario indica que la opcion que mas le interesa ahora es comprar un transformador nuevo, aunque el transformador actual costase bastante dinero.
- Mantener el PT actual queda como opcion secundaria, no como ruta principal.

## 7. Datos a medir antes de decidir definitivamente

Con el ampli desenchufado y descargado:

- Resistencia DC del primario azul-azul.
- Resistencia DC del secundario HT rojo-rojo.
- Resistencia DC de filamentos marron-marron.
- Identificar toma central de filamentos.
- Confirmar si la toma central de filamentos esta conectada a masa.
- Leer tension nominal real de cada electrolitico de B+.
- Medir tension real de red del taller.

Sin estas mediciones, la decision ya se puede orientar, pero no cerrar al 100%.
