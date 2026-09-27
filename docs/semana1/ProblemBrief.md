# Problem Brief

## Decisión del problema

### Problema elegido

Los socios y operadores de las rutas de transporte concesionado en la CDMX (como el corredor Coviteni) no tienen una forma confiable y verificable de saber cuánto se recaudó en pasajes y cómo se reparte ese dinero entre ellos.

**Propuesto por:** Edgar López Baeza.

### Por qué elegimos este

Es un problema real, con datos concretos y un nicho que casi no se trabaja en hackathons. Además cumple con claridad dos criterios de la Sesión 1: hay **varias partes que no confían entre sí** (socios, administración, choferes, autoridad) que necesitan **compartir un mismo registro**, y ese registro necesita un **histórico que no se pueda alterar** (los cortes diarios). En las otras propuestas blockchain aportaba, pero el problema de confianza era menos central.

### Propuestas descartadas

| # | Propuesta | Propuso | Motivo del descarte |
|---|-----------|---------|---------------------|
| 2 | Tarjeta de pago autorizado (estilo Kura) | Diego Sevilla Díaz | Tiene un precedente verificable, infraestructura real (Accesly / Pollar) y un contrato Soroban con valor genuino, pero no encontramos un ángulo de diferenciación propio frente a Kura. |
| 3 | Lealtad cultural | Axel Isaías Rodríguez Frías | Es la más fácil de demostrar, pero el caso de éxito es prestado (IRL × Stellar) y el problema de cuentas falsas (Sybil) sigue sin resolver. |
| 4 | Remesas con Accesly / Pollar | Fernanda | La infraestructura existe, pero no tenemos calculada la economía unitaria, requiere licencia regulatoria y depende de dos startups todavía tempranas. |
| 5 | Cupones | Idea surgida en la discusión del equipo | Baja complejidad y demo visual, pero es menos original y comparte el mismo problema de Sybil sin resolver. |

### Cómo tomamos la decisión

Cada integrante presentó su propuesta. Hicimos una tabla comparando la fortaleza y el riesgo principal de cada idea, debatimos contra los criterios de la Sesión 1 y llegamos a consenso tras el debate por la propuesta de Coviteni, aceptando conscientemente sus riesgos (regulación, oráculo de datos y cobro aún no digital) para trabajarlos en las siguientes semanas.

---

## Problem Brief

### Encabezado

**Proyecto:** CorteClaro _(nombre de trabajo)_

**Problema:** en las rutas de transporte concesionado de la CDMX nadie puede verificar cuánto se recaudó en pasajes ni cómo se repartió entre los socios.

### Equipo y roles

| Integrante | Usuario de GitHub | Rol |
|------------|-------------------|-----|
| Edgar López Baeza | _pendiente_ | Producto e investigación del problema |
| Diego Sevilla Díaz | _pendiente_ | Arquitectura técnica |
| Axel Isaías Rodríguez Frías | _pendiente_ | Desarrollo y repositorio |
| Fernanda _(apellidos pendientes)_ | _pendiente_ | Investigación de usuarios y regulación |

**Responsable de las entregas:** _por definir_

**Canal de coordinación interna:** grupo de WhatsApp del equipo.

### Problema y evidencia

**Enunciado:** los socios de las rutas de transporte concesionado no pueden verificar cuánto se recaudó ni cómo se repartió el dinero de los pasajes.

**Contexto.** Buena parte del transporte público de la CDMX lo operan empresas o agrupaciones concesionarias formadas por muchos socios dueños de unidades. Coviteni (Congreso-Viga-Tepito Nueva Imagen) opera el corredor del Eje 1 y 2 Oriente con autobuses de alta capacidad y, según reportes públicos, transporta alrededor de 40,000 personas al día en 148 paradas ([PortalAutomotriz](https://www.portalautomotriz.com/noticias/transporte/autobuses-panoramicos-de-international-en-el-corredor-del-eje-1-y-2-oriente-del)).

**Frecuencia y alcance.** El problema ocurre todos los días, en cada corte de caja, y se acumula en cada reparto periódico entre socios. Afecta a todos los socios del corredor y se repite en muchas otras rutas concesionadas de la ciudad con el mismo esquema.

**Evidencia.** El dato de afluencia proviene de la fuente citada arriba y de la ruta publicada en [Moovit](https://moovitapp.com/index/es-419/transporte_p%C3%BAblico-line-COVITENI-Ciudad_de_Mexico-822-938755-11593508-1). Como usuarios del transporte concesionado observamos que el pasaje se cobra en efectivo al chofer y que no se entrega comprobante, por lo que el registro del viaje no existe fuera de lo que reporta quien cobra. _(Pendiente para la semana 2: documentar al menos dos conversaciones con socios o choferes de la ruta para confirmar cómo se hacen el corte y el reparto.)_

### Usuario y actores

**Usuario principal: el socio dueño de unidades.** Invierte en uno o varios autobuses y recibe una parte de lo recaudado. Necesita saber, con certeza, cuánto generaron sus unidades y cuánto le corresponde, sin depender solo de la palabra de la administración. Hoy lo resuelve asistiendo a cortes y asambleas, revisando bitácoras en papel y, en muchos casos, cobrando una cuota fija al chofer para no tener que confiar en el conteo. Le cuesta dinero (fugas de efectivo no rastreables), tiempo (conciliaciones y asambleas) y conflicto con los demás socios.

**Otros actores:**

- **Chofer:** cobra el pasaje, maneja el efectivo y entrega la cuenta o cuota al final del turno. Carga con el riesgo de robo y con la sospecha de quedarse con dinero.
- **Administración de la empresa concesionaria:** concentra el efectivo, hace el corte, paga gastos (combustible, mantenimiento, seguros) y reparte el resto. Es el punto donde hoy se concentra la confianza.
- **Pasajero:** paga el pasaje; hoy no recibe comprobante y su viaje no queda registrado.
- **Autoridad (SEMOVI):** otorga la concesión y regula tarifas; necesita datos confiables de afluencia para planear y supervisar el servicio.
- **Proveedor de cobro digital (futuro):** validadores o tarjeta de movilidad integrada, si la ruta migra al cobro electrónico.

### Flujo actual de valor

1. **Pasajero → chofer.** El pasajero paga el pasaje en efectivo al subir. No se emite comprobante. La tarifa está fijada por la autoridad *(obligación normativa: tarifa autorizada por SEMOVI)*.
2. **Chofer (durante el turno).** El chofer acumula el efectivo en la unidad. No hay registro independiente de cuántos pasajeros subieron.
3. **Chofer → administración.** Al final del turno el chofer entrega la cuenta completa o una cuota fija pactada; el excedente, si existe, no queda registrado.
4. **Administración (corte).** La administración cuenta el efectivo, lo anota en bitácoras o en una hoja de cálculo propia y descuenta gastos operativos.
5. **Administración → banco.** El efectivo se deposita en la cuenta de la empresa *(obligaciones fiscales: facturación y declaración de ingresos ante el SAT)*.
6. **Administración → socios.** Periódicamente se reparte el remanente entre socios según las unidades o participaciones de cada uno, con base en el corte que reporta la propia administración.
7. **Socios (verificación).** El socio solo puede revisar el reporte que le entregan; no tiene acceso a una fuente independiente para contrastarlo.

**Intermediarios explícitos:** chofer (custodia del efectivo), administración (corte y reparto) y banco (custodia del depósito). La confianza se concentra en los pasos 3, 4 y 6.

### Fricciones identificadas

1. **Paso 1–2: no hay registro del viaje.** Causa: el pago en efectivo no deja rastro. Afecta al socio (no sabe cuánto generó su unidad) y a la autoridad (no tiene datos reales de afluencia).
2. **Paso 3: cuota fija en lugar de cuenta real.** Causa: como no se puede verificar el conteo, se pacta una cuota. Afecta al socio, que pierde el excedente en días buenos, y al chofer, que absorbe la pérdida en días malos.
3. **Paso 2–3: riesgo de manejar efectivo.** Causa: la unidad carga dinero durante todo el turno. Afecta al chofer (robos y asaltos) y al socio (pérdidas).
4. **Paso 4: el corte lo hace una sola parte.** Causa: la administración cuenta, registra y guarda el registro. Afecta a todos los socios, que no pueden auditarlo.
5. **Paso 6: reparto sin reglas visibles.** Causa: el cálculo depende de hojas de cálculo internas. Genera disputas entre socios, asambleas largas y, en casos extremos, salida de socios o conflictos legales.
6. **Paso 7: el histórico se puede modificar.** Causa: bitácoras en papel o archivos editables. Afecta a cualquier socio que quiera revisar meses anteriores.

### Oportunidad e hipótesis

**Oportunidad priorizada:** fricciones 4, 5 y 6 — el corte y el reparto dependen de una sola parte y el histórico se puede alterar.

**Por qué esta:** es la fricción que genera más conflicto entre socios y la que no se resuelve solo con digitalizar el cobro. Aunque la ruta pase a cobro electrónico, el registro seguiría en manos de la administración o de un proveedor, y los socios seguirían dependiendo de su palabra.

**Hipótesis:** si cada cobro (o cada corte diario, mientras el cobro siga en efectivo) se registra en un libro compartido que ningún actor puede editar por su cuenta, y el reparto entre socios se ejecuta con reglas públicas en un contrato inteligente, entonces:

- el socio podría ver en tiempo real lo que generaron sus unidades, sin esperar la asamblea;
- el reparto se calcularía siempre igual y cualquiera podría comprobarlo;
- las disputas sobre "cuánto entró" pasarían a ser consultas a un mismo registro;
- la autoridad podría recibir datos de afluencia confiables sin depender del reporte de la empresa.

### Criterio de pertinencia

Una base de datos tradicional no resuelve el problema porque **alguien tendría que administrarla**, y ese alguien sería la misma administración (o un proveedor contratado por ella) en la que hoy los socios no confían del todo. Quien controla la base de datos puede corregir, borrar o reescribir registros, que es exactamente la fricción actual.

Una integración entre sistemas existentes tampoco alcanza: hoy no hay sistemas que integrar (el cobro es en efectivo y el corte está en papel u hojas de cálculo) y, aunque los hubiera, cada parte seguiría confiando en su propia copia.

El caso se apoya en dos criterios de la Sesión 1:

1. **Varias partes que no confían entre sí necesitan compartir un mismo registro.** Socios, administración, choferes y autoridad tienen incentivos distintos y todos necesitan ver los mismos números de recaudación.
2. **El histórico no puede alterarse.** Un corte registrado debe quedarse como quedó; si hay un ajuste, debe verse como una nueva transacción, no como una edición del pasado.

Adicionalmente, las reglas de reparto en un contrato inteligente **reducen el papel de la administración como intermediario que concentra la confianza**: sigue operando la ruta, pero ya no es la única fuente de verdad sobre el dinero.

### Supuestos y riesgos

**Supuesto 1: los datos de recaudación pueden entrar al registro de forma confiable (problema del oráculo).** Mientras el cobro sea en efectivo, el registro solo es tan bueno como el dato que alguien captura. Lo invalidaría que no exista una fuente independiente (validador electrónico, contador de pasajeros o tarjeta de movilidad). Mitigación a explorar: empezar registrando cortes firmados por más de una parte (chofer y administración) y avanzar hacia el cobro digital.

**Supuesto 2: los socios y la administración aceptarían la transparencia.** La hipótesis supone que al menos una parte de los socios quiere visibilidad y tiene fuerza para exigirla. Lo invalidaría que la administración o un grupo de socios se beneficie de la opacidad actual y bloquee la adopción.

**Supuesto 3: el modelo cabe dentro del marco legal.** Registrar ingresos y repartirlos no debería requerir autorización especial, pero si el diseño se acerca a representar participaciones de los socios como activos transferibles, podría caer bajo la Ley del Mercado de Valores (LMV). Lo invalidaría que cualquier versión útil del producto requiera una autorización regulatoria que el equipo no puede obtener. Mitigación: limitar el alcance a registro y reparto, sin tokenizar la propiedad de las unidades.
