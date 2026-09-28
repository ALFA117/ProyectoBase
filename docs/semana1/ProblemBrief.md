# Problem Brief

## Decisión del problema

### Problema elegido

Quien entrega dinero con una condición (un familiar que manda dinero para la despensa, una marca que reparte cupones, un evento que da recompensas) pierde el control y la visibilidad de cómo se usa en cuanto el dinero cambia de manos, y quien lo recibe enfrenta filas, comisiones y cupones duplicados para poder usarlo.

**Propuesto por:** propuesta consolidada del equipo. El núcleo viene de la idea de **Diego Sevilla Díaz** (tarjeta de pago autorizado) y se integró con piezas de las propuestas de **Axel Isaías Rodríguez Frías** (lealtad cultural), **María Fernanda Rivera Islas** (remesas), la idea de cupones que surgió en el debate y la lección de riesgo regulatorio que dejó la propuesta de **Edgar López Baeza** (Coviteni).

### Por qué elegimos este

Al comparar las cinco ideas notamos que tres de ellas (remesas, lealtad y cupones) tenían el mismo problema de fondo: **dinero o valor que se entrega con una condición que hoy nadie puede hacer cumplir ni rastrear**. En lugar de escoger una sola, elegimos el problema común.

Según los criterios de la Sesión 1:

- **Eliminar un intermediario que concentra la confianza:** hoy el emisor tiene que confiar en el beneficiario, en la remesadora o en la plataforma de lealtad; con reglas programadas, la condición se cumple sola.
- **Histórico inalterable:** el emisor necesita un registro de qué se compró, dónde y cuándo, que nadie pueda editar.
- **Partes que no confían entre sí comparten un registro:** emisor, beneficiario y comercio consultan la misma fuente.

Además es la opción con menor riesgo regulatorio: al tratarse de consumo cerrado y condicionado (no transferencia libre de dinero), no requiere licencia de remesadora.

### Propuestas descartadas

Ninguna se descartó por completo; de cada una tomamos una pieza y descartamos el resto:

| Propuesta | Propuso | Qué tomamos | Qué descartamos y por qué |
|-----------|---------|-------------|---------------------------|
| Coviteni (transporte concesionado) | Edgar López Baeza | La lección de diseñar contra el riesgo regulatorio desde el inicio, no después. | El token de participación en utilidades (riesgo LMV/CNBV) y el fondo colectivo de indemnizaciones (riesgo CNSF). Además dependía de un oráculo de datos y de un cobro digital que aún no existe. |
| Tarjeta de pago autorizado (estilo Kura) | Diego Sevilla Díaz | El concepto central: un emisor autoriza un consumo específico y el beneficiario lo cobra con un código de un solo uso. | Nada del núcleo; lo que faltaba era diferenciarnos de Kura, y lo resolvimos haciéndolo multi-caso (remesa, lealtad, cupón). |
| Lealtad cultural (IRL × Stellar) | Axel Isaías Rodríguez Frías | El onboarding "escanea QR → wallet en un clic → reclama" y usar el mismo mecanismo para eventos. | Un producto propio de lealtad: el caso de éxito era prestado y el riesgo Sybil seguía abierto. |
| Remesas con Accesly / Pollar | María Fernanda Rivera Islas | La infraestructura: Accesly para crear wallets sin fricción y Pollar para liquidar en moneda local. | La remesa libre: requiere licencia de remesadora y la economía unitaria no estaba calculada. |
| Cupones verificables | Idea surgida en el debate del equipo | El cupón limitado, no duplicable y con datos de canje en tiempo real, como tercer caso de uso. | Un producto de cupones aislado: poco original por sí solo. |

### Cómo tomamos la decisión

Cada integrante presentó su propuesta y armamos una tabla con la fortaleza y el riesgo principal de cada una. En el debate vimos que las ideas se complementaban: una aportaba el caso de uso, otra el onboarding, otra la infraestructura de pagos y otra la advertencia regulatoria. Llegamos por **consenso tras debate** a consolidarlas en una sola idea, tomando como base la tarjeta de pago autorizado.

---

## Problem Brief

### Encabezado

**Proyecto:** Motor de Autorización Condicionada para Consumo Dirigido en LATAM

**Problema:** quien entrega dinero con una condición (remesa para un gasto específico, cupón, recompensa de evento) no tiene forma de hacer cumplir ni rastrear esa condición.

### Equipo y roles

| Integrante | Apodo | Usuario de GitHub | Rol |
|------------|-------|-------------------|-----|
| Edgar López Baeza | Alfa | _pendiente_ | Diseñador UX/UI |
| Axel Isaías Rodríguez Frías | Morita | _pendiente_ | Project Manager (PM) |
| Diego Sevilla Díaz | Onii | _pendiente_ | Software Engineer |
| María Fernanda Rivera Islas | Fer | _pendiente_ | Speaker (presentación y pitch del proyecto) |

**Responsable de las entregas:** Axel Isaías Rodríguez Frías (PM).

**Canal de coordinación interna:** grupo de WhatsApp del equipo.

### Problema y evidencia

**Enunciado:** quien entrega dinero para un uso específico pierde el control y la visibilidad de cómo se gasta en cuanto lo entrega.

**Contexto.** En LATAM una gran cantidad de dinero se mueve como "dinero de confianza". México es uno de los mayores receptores de remesas del mundo, y una parte de esos envíos se manda con un propósito concreto: despensa, medicinas, colegiatura. Al mismo tiempo, marcas y organizadores de eventos reparten cupones y puntos esperando generar lealtad real. En los tres casos el patrón es el mismo: quien entrega el valor espera que se use de cierta forma, pero no tiene herramientas para condicionarlo ni para verificarlo.

**Frecuencia y alcance.** Ocurre cada vez que se envía una remesa con un fin específico, se emite un cupón o se entrega una recompensa. Afecta a familias con migrantes, a pequeños comercios y a organizadores de eventos en toda la región.

**Evidencia.**

- Existe un precedente en producción: Kura ya ofrece pagos autorizados para consumo específico en Centroamérica y el Caribe, lo que muestra que el problema es real y que hay usuarios dispuestos a usar una solución.
- Los cupones de papel o compartidos por redes sociales se pueden copiar con facilidad, y el comercio que los acepta no obtiene datos de quién los canjea.
- Cobrar una remesa en efectivo implica ir a una sucursal o tienda, hacer fila y mostrar identificación.

_(Pendiente para la semana 2: agregar cifras oficiales de remesas de Banxico con enlace y documentar al menos dos conversaciones con posibles usuarios.)_

### Usuario y actores

**Usuario principal: el emisor.** Es quien entrega el valor con una condición: un familiar (a menudo en el extranjero) que manda dinero para la despensa de sus padres, una marca que reparte cupones o un organizador que premia a los asistentes de un evento. Necesita definir cuánto, dónde y por cuánto tiempo se puede usar ese valor, y ver después en qué se gastó.

Hoy lo resuelve mandando dinero libre y pidiendo fotos de tickets, prestando su tarjeta, usando tarjetas de sellos en papel o pagando a plataformas de lealtad. Le cuesta **dinero** (comisiones de remesadoras y plataformas, cupones duplicados), **tiempo** (verificar gastos a mano) y **confianza** (no sabe si el dinero se usó como esperaba).

**Otros actores:**

- **Beneficiario:** recibe el valor. Necesita usarlo fácil, sin filas ni traslados, y sin tener que entender tecnología.
- **Comercio:** acepta el pago. Necesita recibir su dinero en pesos, rápido, sin manejar criptomonedas, y (en el caso de cupones) saber quién canjea.
- **Remesadora / banco (hoy):** mueve el dinero y cobra comisión y margen en el tipo de cambio.
- **Plataforma de lealtad o cupones (hoy):** administra los puntos y se queda con los datos del cliente.
- **Proveedores de infraestructura (propuesta):** Accesly (creación de wallets con login social) y Pollar (conversión a moneda local).

### Flujo actual de valor

Tomamos el caso principal, la remesa familiar para un gasto específico:

1. **Emisor → remesadora.** El familiar en Estados Unidos paga el envío en una sucursal o app. Paga comisión fija más el margen del tipo de cambio. *(Obligación normativa: identificación del remitente y reportes de prevención de lavado de dinero.)*
2. **Remesadora → corresponsal en México.** La remesadora transfiere a través de bancos o redes corresponsales.
3. **Corresponsal → beneficiario.** El beneficiario va a un banco o tienda de conveniencia a cobrar en efectivo, o lo recibe en cuenta. *(Obligación normativa: identificación del beneficiario.)*
4. **Beneficiario → comercio.** El beneficiario gasta el dinero donde decida, en efectivo o con tarjeta.
5. **Beneficiario → emisor (verificación informal).** El beneficiario manda fotos de tickets por WhatsApp si el emisor las pide.

En cupones y lealtad el flujo equivalente es: marca o evento emite el cupón (papel, código o app) → el cliente lo presenta → el comercio lo acepta y lo marca manualmente → la marca recibe (o no) un reporte del comercio.

**Intermediarios explícitos:** remesadora, corresponsal bancario, punto de pago en efectivo, y en lealtad la plataforma que administra los puntos.

### Fricciones identificadas

1. **Paso 1: costo del envío.** Causa: comisión fija más margen escondido en el tipo de cambio. En envíos pequeños el costo pesa proporcionalmente más. Afecta al emisor.
2. **Paso 3: cobro en efectivo.** Causa: el beneficiario tiene que trasladarse a una sucursal, hacer fila y mostrar identificación. Afecta al beneficiario, sobre todo en zonas rurales y semiurbanas.
3. **Paso 4: sin condición.** Causa: una vez entregado, el dinero es libre; no hay forma de limitarlo a un comercio, a un monto o a una fecha. Afecta al emisor, que no puede asegurar que el dinero se use en lo acordado.
4. **Paso 5: verificación manual.** Causa: no existe un registro del gasto; la única prueba son fotos de tickets. Afecta al emisor (tiempo y desconfianza) y al beneficiario (tener que justificar cada gasto).
5. **Cupones: duplicación.** Causa: códigos que se copian o se usan varias veces y validación manual en caja. Afecta a la marca y al comercio.
6. **Lealtad: datos en manos de terceros.** Causa: la plataforma de lealtad se queda con la información y cobra comisión. Afecta a comercios y organizadores de eventos.

### Oportunidad e hipótesis

**Oportunidad priorizada:** las fricciones 3 y 4 (dinero entregado sin condición y verificación manual), extendidas a la 5 (duplicación de cupones).

**Por qué esta:** son el problema común a los tres casos de uso. Las fricciones de costo y cobro (1 y 2) ya las atacan muchas fintech, pero nadie resuelve bien el "dinero con condición". Además, enfocarnos en consumo condicionado y cerrado nos mantiene fuera del modelo de transferencia libre de dinero, que requeriría licencia de remesadora.

**Hipótesis:** si el emisor puede crear una autorización programada (monto, comercios válidos y vigencia) que el beneficiario cobra con un código QR de un solo uso, y el comercio recibe el pago en pesos al instante, entonces:

- el emisor sabrá en tiempo real qué se compró, dónde y cuándo, sin pedir fotos de tickets;
- el beneficiario podrá usar el valor directamente en el comercio, sin ir a cobrar en efectivo;
- el comercio cobrará en su moneda sin tener que tocar criptomonedas;
- los cupones no se podrán duplicar porque cada código se marca como usado en el momento del cobro;
- el emisor podrá cancelar lo no usado y, al vencer, los fondos regresarán solos.

Para el usuario esto se vería como iniciar sesión con Google, sin palabras técnicas ni llaves privadas.

### Criterio de pertinencia

**Por qué no una base de datos tradicional:** una app con base de datos central podría guardar las autorizaciones, pero el emisor, el beneficiario y el comercio tendrían que confiar en que el operador de esa base de datos no modifica saldos, no reutiliza códigos y no cambia el historial. Ese operador se convertiría en un nuevo intermediario que concentra la confianza y probablemente en uno que cobra comisión, que es justo lo que queremos evitar.

**Por qué no una integración entre sistemas existentes:** los bancos, remesadoras y plataformas de lealtad no comparten un mismo registro; integrar sus sistemas requeriría acuerdos entre cada uno y el emisor seguiría viendo solo lo que cada empresa decida reportarle.

El caso se apoya en los tres criterios de la Sesión 1:

1. **Se elimina un intermediario que concentra la confianza.** Las reglas (monto, comercio, vigencia, código de un solo uso) viven en un contrato Soroban en Stellar y se cumplen automáticamente; nadie puede cambiarlas a escondidas.
2. **El histórico no puede alterarse.** Cada autorización, cobro y cancelación queda registrada de forma inmutable y el emisor la puede consultar siempre.
3. **Partes que no confían entre sí comparten un registro.** Emisor, beneficiario y comercio consultan la misma fuente, incluso si el proveedor de wallets o de conversión a pesos falla o se cambia.

### Supuestos y riesgos

**Supuesto 1: el modelo de consumo condicionado y cerrado no requiere licencia de remesadora.** La hipótesis depende de que limitar el uso a comercios específicos y a consumo (no a retiro libre de efectivo) nos mantenga fuera de la regulación de transferencias de dinero. **Lo invalidaría** que la autoridad (CNBV / Banxico) considere que cualquier valor que cruza la frontera es una remesa, aunque tenga condiciones. Es la misma lección que nos dejó la propuesta de Coviteni: cambiarle el nombre a un instrumento no cambia su naturaleza legal.

**Supuesto 2: Accesly y Pollar (u opciones equivalentes) funcionan en México con la calidad necesaria.** Necesitamos crear wallets con login social en segundos, pagar las comisiones de red por el usuario y liquidar en pesos al comercio en pocos segundos. **Lo invalidaría** que estos proveedores, que todavía son empresas tempranas, no tengan cobertura en México o sean demasiado caros. Por eso el contrato se diseña independiente de ellos, para poder cambiarlos.

**Supuesto 3: los comercios aceptarían escanear un QR y cobrar por esta vía.** **Lo invalidaría** que la comisión o la fricción de adopción sea mayor que el beneficio de recibir ventas dirigidas. Otro riesgo abierto es el abuso con cuentas múltiples (Sybil) en los casos de lealtad y cupones, que tendremos que mitigar en el diseño.
