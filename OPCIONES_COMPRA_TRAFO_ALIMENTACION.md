# Opciones de compra - transformador de alimentacion para Hurricane

Fecha: 2026-05-11

Objetivo:

- Sustituir el transformador real de 325 V AC por una opcion mas segura/cercana al esquema.
- Comprar preferiblemente en Europa, idealmente en Espana.

## 1. Especificacion objetivo

El esquema Hurricane / Chillidoggy v6 indica:

- Secundario HT: 295 V AC / 130 mA.
- Rectificacion: puente de 4 diodos 1N4007.
- Filamentos: 6,3 V AC / 3 A en el esquema.

El ampli real parece tener:

- 2 x EL84.
- Varias ECC83/12AX7.
- Reverb.
- Loop.
- Transformador de salida Hammond 1750H.
- Transformador de reverb Hammond 1750A.

Para comprar con margen razonable:

- Primario: 230 V o 240 V, 50 Hz.
- HT ideal si se mantiene puente: secundario simple 0-290/300 V AC, 150 mA o mas.
- HT ideal si se cambia a rectificador con toma central: 290-0-290 V AC, 140 mA o mas.
- Filamentos: 6,3 V AC con al menos 3,5-4 A utiles.
- Mejor si tiene pantalla electrostatica, toma de 240 V o fabricacion CE/EN.

## 2. Advertencia sobre 290-0-290 V

Muchos transformadores tipo Marshall 18W son `290-0-290 V`, no `0-290 V`.

No se deben conectar los extremos de un `290-0-290 V` directamente al puente del esquema como si fueran un secundario de 290 V, porque entre extremos hay 580 V AC.

Opciones correctas:

- Convertir la fuente a rectificacion de onda completa con toma central.
- O usar un transformador con secundario simple 0-290/300 V AC pensado para puente.
- No usar medio secundario de un `290-0-290 V` en puente sin aprobacion del fabricante.

## 3. Opciones recomendadas

### Opcion 1 - Hammond 290PAZ

Vendedores encontrados:

- Arteaudio, Espana: `https://arteaudio.es/hammond-290paz-transformador-para-marshall-18w/`
- Mouser Espana: `https://www.mouser.es/ProductDetail/Hammond-Manufacturing/290PAZ`
- Tube-Town, Alemania: `https://www.tubetown.net/ttstore/en/hammond-290paz-power-transformer-for-marshall-1974x-18w.html`
- Hammond ficha fabricante: `https://www.hammfg.com/part/290PAZ`

Datos:

- Primario: 120/240 V AC.
- HT: 290-0-290 V @ 140 mA.
- Filamentos: 3,15-0-3,15 V @ 3 A.
- Winding adicional: 5 V / 6,3 V @ 2 A segun vendedor.
- Modelo para Marshall 18 Watt Combo / 1974X.

Ventajas:

- Buena marca, facil de comprar.
- Disponible en Espana en Arteaudio.
- Muy cercano a la tension objetivo si se usa con rectificacion con toma central.
- Corriente HT suficiente frente a los 130 mA del esquema.
- Puede alimentar filamentos con margen si se reparte carga entre bobinados adecuados.

Inconvenientes:

- No es secundario simple 295 V: hay que adaptar rectificacion.
- Primario 120/240 V, no 230 V exacto; en red europea de 230 V usando 240 V puede dar algo menos de HT, lo cual puede ser favorable.
- Hay que verificar montaje mecanico.

Valoracion:

- Mejor opcion si quieres comprar en Espana y aceptar adaptar la rectificacion a toma central.

### Opcion 2 - TAD MJTM18WP / Marshall 18W Plexi

Vendedor:

- Tube Amp Doctor, Alemania: `https://www.tubeampdoctor.com/en/mains-transf.-for-marshall-18w-plexi/tad-amp-kit`

Datos:

- Hecho en Europa segun TAD.
- Para 2 x EL84 y hasta 6 x ECC83.
- Primarios: 120 V, 230 V, 240 V.
- HT: 290-0-290 V @ 200 mA.
- Filamentos: 3,15-0-3,15 V @ 4 A.
- Bobinados extra para rectificadora: 5 V @ 4 A y 6,3 V @ 4 A segun ficha.

Ventajas:

- Muy buen margen de corriente.
- Primario 230/240 V, muy comodo en Europa.
- Pensado para 18W con 2 x EL84 y muchas ECC83.
- Menos justo que el Hammond 290PAZ en filamentos/HT.

Inconvenientes:

- Tambien es `290-0-290 V`, asi que requiere adaptar rectificacion.
- Mas grande/pesado; hay que comprobar hueco y taladros.
- No es compra en Espana, pero si en Alemania/UE.

Valoracion:

- Mi opcion preferida si priorizas margen electrico y no te importa comprar en Alemania.

### Opcion 3 - Transformador a medida europeo

Especificacion para pedir:

```text
Primario:
  0-230-240 V AC, 50 Hz

Secundario HT:
  0-295 V AC @ 150-180 mA
  aislado, para puente de diodos

Filamentos:
  6,3 V AC C.T. @ 4 A minimo
  ideal 4,5-5 A si hay espacio

Extras deseables:
  pantalla electrostatica
  certificacion CE/EN
  baja vibracion mecanica
  formato y taladros compatibles con el chasis
```

Ventajas:

- Es la solucion electricamente mas fiel al esquema.
- Permite mantener el puente de diodos original.
- Puedes pedir exactamente 295 V y margen de filamentos.

Inconvenientes:

- Plazo y coste.
- Hay que tratar bien con el fabricante.
- Necesita confirmar dimensiones mecanicas.

Valoracion:

- La mejor solucion tecnica si quieres respetar el esquema sin redisenar la fuente.

### Opcion 4 - BTB Elektronik / toroidal universal 200-250-300 V

Vendedor:

- BTB Elektronik, Alemania: `https://btb-elektronik.de/ringkerntrafo-btb2249917-154va-200-250-300v-0-35a-50v-6-3v-7a/RKT2249917-154W`

Datos:

- Primario 230 V.
- Secundario con taps 0-200-250-300 V @ 0,35 A.
- Bias 50 V.
- Filamentos 6,3 V @ 7 A.
- Toroidal 154 VA.

Ventajas:

- Mucho margen.
- Secundario simple/tap, compatible conceptualmente con puente.
- Puedes elegir tap 250 V o 300 V segun B+ objetivo.
- Filamentos sobradisimos.

Inconvenientes:

- Toroidal: montaje mecanico distinto.
- Mas universal que especifico de ampli de guitarra.
- Puede tener menos "sag" que un EI tradicional.
- 300 V es un poco mas alto que 295 V; 250 V puede quedar bajo.

Valoracion:

- Buena opcion tecnica si aceptas toroidal y adaptar mecanica. No seria mi primera si buscas sabor/classicidad de ampli de guitarra.

## 4. Ranking recomendado

1. TAD MJTM18WP si aceptas adaptar rectificacion y quieres margen premium.
2. Hammond 290PAZ comprado en Arteaudio si quieres comprar en Espana y mantener calidad reconocida.
3. Transformador a medida 0-295 V para puente si quieres la solucion mas fiel al esquema.
4. BTB toroidal universal si priorizas margen y disponibilidad antes que formato clasico.

## 5. Mi recomendacion practica

Para este proyecto elegiria una de estas dos rutas:

Ruta conservadora/fiel:

- Encargar o comprar un transformador con secundario simple 0-295 V AC @ 150-180 mA y 6,3 V @ 4 A o mas.
- Mantener puente de diodos.
- Es la ruta mas limpia electricamente.

Ruta compra facil/premium:

- Comprar Hammond 290PAZ en Arteaudio o TAD MJTM18WP en Tube Amp Doctor.
- Modificar la fuente a rectificacion con toma central.
- Mantener electroliticos con margen revisado y bleeders.

No compraria:

- Otro transformador de 320-325 V AC para puente.
- Un secundario de filamentos justo de 3 A si finalmente hay 5 ECC83 + 2 EL84.
- Un `290-0-290 V` para conectarlo al puente usando los extremos completos.

