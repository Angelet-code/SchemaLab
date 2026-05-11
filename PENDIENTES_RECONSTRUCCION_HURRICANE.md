# Pendientes de reconstruccion - Cornford Hurricane

Objetivo:

- Registrar fallos detectados en el montaje actual.
- Separar que hay que comprar, que hay que recablear y que hay que verificar.
- Mantener una lista practica para reconstruir el ampli en la vida real.

## Leyenda de prioridad

| Prioridad | Significado |
|---|---|
| Seguridad | Riesgo de alta tension, red, fuego, descarga, transformadores o carga de salida |
| Funcionamiento | El ampli puede no sonar o funcionar mal |
| Ruido/sonido | Puede sonar, pero con ruido, oscilacion, hum o mala respuesta |
| Calidad | Mejora de fiabilidad, mantenimiento o calidad sonora |
| Estetica/mecanica | Orden, limpieza, sujecion, ergonomia o acabado |

## Pendientes detectados

| ID | Bloque | Fallo detectado | Accion necesaria | Piezas necesarias | Prioridad | Estado | Notas |
|---|---|---|---|---|---|---|---|
| P-001 | Fuente | Transformador de alimentacion real de 325 V AC no coincide con esquema de 295 V AC | Comprar/sustituir por PT mas adecuado al circuito, salvo decision contraria | PT nuevo compatible | Seguridad / calidad | Pendiente compra | El usuario prefiere ahora comprar un trafo nuevo aunque el actual costase bastante |
| P-002 | Fuente B+ | Resistencias de caida A-B-C-D-E montadas con valores incorrectos | Sustituir valores incorrectos y verificar nodos | 2k2 / 3W, 10k, 1k, 10k segun esquema | Seguridad / funcionamiento | Pendiente cambio | Montado actual: A-4k7-B-68k-C-1k-D-10k-E; correcto: A-2k2/3W-B-10k-C-1k-D-10k-E |

## Lista de compra provisional

| ID | Pieza | Especificacion | Cantidad | Motivo | Estado |
|---|---|---:|---:|---|---|
| C-001 | Transformador de alimentacion | Preferido: PT nuevo mas adecuado. Opcion fiel: 0-295 V AC para puente; opcion comercial: 290-0-290 V con fuente adaptada | 1 | Resolver problema de B+ excesiva del PT actual de 325 V AC | Pendiente compra |
| C-002 | Resistencia caida fuente A-B | 2k2 / 3W, margen de tension adecuado | 1 | Reemplazar 4k7 montada entre A y B | Pendiente compra/verificacion |
| C-003 | Resistencia caida fuente B-C | 10k, potencia a confirmar segun caida/corriente; usar margen generoso | 1 | Reemplazar 68k montada entre B y C | Pendiente compra/verificacion |
| C-004 | Resistencia caida fuente C-D | 1k, potencia a confirmar; ya coincide segun usuario | 1 | Verificar valor montado y potencia | Pendiente verificar |
| C-005 | Resistencia caida fuente D-E | 10k, potencia a confirmar; ya coincide segun usuario | 1 | Verificar valor montado y potencia | Pendiente verificar |

## Cambios de montaje pendientes

| ID | Bloque | Cambio | Dependencia | Estado |
|---|---|---|---|---|
| M-001 | Fuente | Revisar arquitectura de rectificacion/filtro segun PT elegido | Decision PT | Pendiente |
| M-002 | Fuente B+ | Cambiar cadena de resistencias a `A -> 2k2/3W -> B -> 10k -> C -> 1k -> D -> 10k -> E` | Compra/verificacion resistencias | Pendiente |

## Verificaciones pendientes

| ID | Verificacion | Metodo | Resultado esperado | Estado |
|---|---|---|---|---|
| V-001 | Tension nominal real de electroliticos B+ | Lectura visual y/o ficha | Margen suficiente para B+ maxima | Pendiente |
| V-002 | Continuidad PT real | Multimetro en frio | Primario, HT, filamentos y C.T. identificados | Pendiente |
| V-003 | Continuidad OT Hammond 1750H | Multimetro en frio | Primario C.T. y secundario 8 ohm correctos | Pendiente |
| V-004 | Cadena resistiva fuente A-B-C-D-E | Medir resistencia entre nodos con ampli descargado | A-B 2k2; B-C 10k; C-D 1k; D-E 10k | Pendiente tras cambio |
