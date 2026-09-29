# Problem Brief

## Decisión del problema

### Problema elegido

Un pasajero, un inspector o una aseguradora no pueden saber, en el momento, si el microbús o autobús de transporte concesionado tiene su mantenimiento vigente, y el socio dueño de la unidad no tiene una forma fácil y confiable de demostrar que cumple.

**Propuesto por:** Edgar López Baeza, como evolución de su propuesta original sobre el transporte concesionado (Coviteni).

### Por qué elegimos este

Conserva lo mejor de la propuesta de Coviteni (un problema real, cotidiano y poco explorado en hackathons, dentro del transporte concesionado de la CDMX) pero cambia el enfoque: en lugar de repartir dinero, que nos acercaba a regulación financiera (LMV / CNBV), registramos **evidencia de mantenimiento**, que no es un instrumento financiero.

Frente a los criterios de la Sesión 1:

- **Partes que no confían entre sí comparten un registro:** socio, taller, aseguradora, autoridad y pasajero necesitan ver el mismo expediente de la unidad.
- **Histórico inalterable:** un servicio registrado no puede borrarse ni "maquillarse" después de un accidente.
- **Eliminar un intermediario que concentra la confianza:** hoy la única prueba es un papel o una calcomanía que cualquiera puede copiar.

Además es la opción más fácil de demostrar físicamente: un ESP32 con pantalla que muestra un QR que cambia cada pocos segundos.

### Propuestas descartadas

| Propuesta | Propuso | Motivo del descarte |
|-----------|---------|---------------------|
| Recaudación y reparto transparente en el corredor Coviteni | Edgar López Baeza | No se descartó el sector sino el enfoque: repartir utilidades o crear un fondo colectivo implicaba riesgo LMV / CNBV / CNSF, dependía de un oráculo de datos de recaudación y de un cobro digital que aún no existe. QRuta es su evolución. |
| Tarjeta de pago autorizado (estilo Kura) | Diego Sevilla Díaz | Precedente real e infraestructura disponible, pero no encontramos cómo diferenciarnos de Kura. |
| Lealtad cultural (IRL × Stellar) | Axel Isaías Rodríguez Frías | Fácil de demostrar, pero el caso de éxito era prestado y el abuso con cuentas múltiples (Sybil) quedaba sin resolver. |
| Remesas con Accesly / Pollar | María Fernanda Rivera Islas | Requiere licencia de remesadora, la economía unitaria no estaba calculada y dependía de dos startups tempranas. |
| Cupones verificables | Idea surgida en el debate del equipo | Poco original por sí sola y con el mismo riesgo Sybil. |
| Motor de autorización condicionada (consolidación de las ideas de Diego, Axel, María Fernanda y cupones) | Equipo | Fue nuestra primera elección. La descartamos porque competía directamente con productos que ya existen y el riesgo regulatorio de mover dinero seguía presente. |

### Cómo tomamos la decisión

Cada integrante presentó su propuesta y comparamos fortaleza y riesgo principal de cada una. Primero llegamos a consenso en consolidar cuatro ideas en un motor de autorización condicionada. Al revisarla de nuevo contra los criterios de la Sesión 1, exploramos variantes del transporte concesionado que no movieran dinero y evaluamos cada una con los tres criterios. El QR rotativo con expediente de mantenimiento fue la mejor evaluada y el equipo la eligió por **consenso tras debate**.

---

## Problem Brief

### Encabezado

**Proyecto:** QRuta

**Problema:** nadie puede verificar en el momento si una unidad de transporte concesionado tiene su mantenimiento al día, y el socio no puede demostrar que cumple.

### Equipo y roles

| Integrante | Apodo | Usuario de GitHub | Rol |
|------------|-------|-------------------|-----|
| Edgar López Baeza | Alfa | [ALFA117](https://github.com/ALFA117) | Diseñador UX/UI |
| Axel Isaías Rodríguez Frías | Morita | [Axl5136](https://github.com/Axl5136) | Project Manager (PM) |
| Diego Sevilla Díaz | Onii | [Oni7u7](https://github.com/Oni7u7) | Software Engineer |
| María Fernanda Rivera Islas | Fer | [frislas](https://github.com/frislas) | Speaker (presentación y pitch del proyecto) |

**Responsable de las entregas:** Axel Isaías Rodríguez Frías (PM).

**Canal de coordinación interna:** grupo de WhatsApp del equipo.

### Problema y evidencia

**Enunciado:** no existe una forma rápida y confiable de verificar, dentro de la unidad, si un vehículo de transporte concesionado tiene su mantenimiento vigente.

**Contexto.** En la CDMX el transporte colectivo concesionado (microbuses, vagonetas y autobuses) está obligado a pasar cada año la **Revista Vehicular** de SEMOVI, que incluye una inspección físico-mecánica de frenos, llantas, suspensión, dirección, carrocería, equipo de seguridad y seguro vehicular ([SEMOVI – Revista Vehicular Ruta](https://www.semovi.cdmx.gob.mx/tramites-y-servicios/transporte-de-pasajeros/revista-ruta); [El Universal](https://www.eluniversal.com.mx/metropoli/semovi-anuncia-periodo-para-tramitar-revista-vehicular-de-unidades-de-transporte-publico-colectivo-de-cdmx/)). La propia SEMOVI ha anunciado mecanismos de verificación y seguimiento calendarizado del mantenimiento básico y revisiones especiales a microbuses con más de 10 años de antigüedad ([El Financiero](https://www.elfinanciero.com.mx/cdmx/2023/02/04/adios-a-micros-viejos-de-cdmx-este-es-el-operativo-para-que-continuen-circulando/); [La Crónica](https://www.cronica.com.mx/metropoli/evaluara-semovi-microbuses-10-anos-antigueedad.html)).

**Frecuencia y alcance.** La revisión oficial es anual, pero el desgaste es diario. Entre una revista y otra no hay forma de saber, desde la calle, si la unidad recibió servicio. El problema alcanza a todas las rutas concesionadas y a los millones de viajes diarios que realizan.

**Evidencia.** Las fuentes oficiales anteriores muestran que la autoridad ya considera el mantenimiento un problema a supervisar y que hoy la verificación depende de que la unidad acuda a un módulo físico. _(Pendiente para la semana 2: documentar al menos dos conversaciones con socios, choferes o talleres sobre cómo registran hoy el mantenimiento.)_

### Usuario y actores

**Usuario principal: el socio dueño de la unidad.** Invierte en uno o varios vehículos y es responsable de que estén en condiciones. Necesita **demostrar** que cumple: ante la autoridad en una inspección, ante la aseguradora al contratar o reclamar una póliza y ante los pasajeros. Hoy lo resuelve guardando facturas y notas del taller en papel, mostrando la constancia de la revista anual y acudiendo en persona a trámites. Le cuesta **tiempo** (reunir papeles y trasladar la unidad), **dinero** (la revista cuesta alrededor de $2,133 MXN más los días sin operar) y **credibilidad**: aunque haga todo bien, su palabra vale lo mismo que la de quien no lo hace.

**Otros actores:**

- **Taller mecánico:** realiza el servicio y hoy emite una nota o factura que se puede perder o falsificar.
- **Chofer:** opera la unidad y es el primero afectado si falla.
- **Pasajero:** quiere viajar seguro, pero no tiene información para elegir.
- **Inspector de SEMOVI:** necesita verificar cumplimiento rápido en la calle, no solo en módulos.
- **Aseguradora:** necesita saber el historial real de mantenimiento para calcular riesgo y resolver siniestros.

### Flujo actual de valor

Lo que se mueve aquí es **información de cumplimiento**:

1. **Socio → taller.** El socio lleva la unidad a servicio (frenos, llantas, suspensión).
2. **Taller → socio.** El taller entrega una nota, factura o simplemente de palabra. El registro queda en papel o en el sistema propio del taller.
3. **Socio (archivo).** El socio guarda los comprobantes, si los guarda.
4. **Socio → SEMOVI (una vez al año).** La unidad acude a un módulo para la Revista Vehicular y la inspección físico-mecánica; se paga el derecho y se obtiene la constancia. *(Obligación normativa: Revista Vehicular anual de SEMOVI.)*
5. **Socio → aseguradora.** Se contrata o renueva el seguro con base en lo que el socio declara. *(Obligación normativa: seguro vehicular obligatorio para transporte público.)*
6. **Inspector → unidad (en calle).** Si hay operativo, el inspector revisa documentos físicos en el momento.
7. **Pasajero.** No recibe ninguna información; sube sin saber el estado de la unidad.

**Intermediarios explícitos:** taller (emite la evidencia), módulo de SEMOVI (certifica una vez al año) y los documentos en papel (único soporte de la información).

### Fricciones identificadas

1. **Paso 2: evidencia frágil.** Causa: la nota del taller es papel o un archivo privado que se pierde o se altera. Afecta al socio y a la aseguradora.
2. **Paso 3: sin historial confiable.** Causa: cada socio archiva como puede y el historial se puede reconstruir "a modo" después de un accidente. Afecta a la aseguradora, a la autoridad y a las víctimas de un siniestro.
3. **Paso 4: verificación solo una vez al año.** Causa: la inspección depende de llevar la unidad a un módulo físico. Entre revistas no hay visibilidad. Afecta a pasajeros y autoridad.
4. **Pasos 4 y 6: documentos copiables.** Causa: constancias, engomados y calcomanías se pueden fotocopiar o pasar de una unidad a otra. Afecta a la autoridad y a los socios que sí cumplen.
5. **Paso 6: inspección lenta.** Causa: el inspector revisa papeles a mano. Afecta al chofer (tiempo detenido) y al inspector.
6. **Paso 7: pasajero sin información.** Causa: no existe ningún indicador visible y verificable en la unidad. Afecta al pasajero.

### Oportunidad e hipótesis

**Oportunidad priorizada:** fricciones 2 y 4 — el historial de mantenimiento no es confiable y las pruebas de cumplimiento se pueden copiar.

**Por qué esta:** son las que hacen que cumplir no valga la pena. Si cualquiera puede fotocopiar una constancia, el socio que sí invierte en mantenimiento no tiene cómo distinguirse. Resolverlas también mejora la inspección en calle (fricción 5) y le da información al pasajero (fricción 6).

**Hipótesis:** si cada servicio queda registrado por un taller autorizado en un expediente que nadie puede borrar, y cada unidad lleva un dispositivo ESP32 con pantalla que muestra un **QR firmado que cambia cada 30 segundos**, entonces:

- el inspector o la aseguradora escanean y en segundos ven si la unidad está **vigente**, qué taller hizo el último servicio y cuándo vence;
- una foto del QR deja de servir en segundos y no se puede pegar en otra unidad;
- el socio que cumple puede **demostrarlo** sin cargar papeles y eso puede traducirse en mejores condiciones con su aseguradora;
- el pasajero que quiera puede verificar la unidad antes de subir.

Para el usuario esto se ve como escanear un QR con la cámara del celular, sin instalar nada.

### Criterio de pertinencia

**Por qué no una base de datos tradicional:** si el expediente vive en una base de datos del socio, del taller o de una empresa, quien la administra puede editar o borrar registros, justo después de un accidente, que es cuando más importa el historial. La aseguradora y la autoridad tendrían que confiar en esa empresa, que se vuelve un intermediario que concentra la confianza.

**Por qué no una integración entre sistemas existentes:** la mayoría de los talleres que dan servicio a microbuses no tienen sistemas digitales, y SEMOVI, aseguradoras y talleres no comparten un registro común. Integrarlos requeriría acuerdos uno a uno y cada parte seguiría viendo solo su copia.

El caso se apoya en los tres criterios de la Sesión 1:

1. **Varias partes que no confían entre sí comparten un registro.** Socio, taller, aseguradora, autoridad y pasajero tienen incentivos distintos y todos consultan el mismo expediente en Stellar.
2. **El histórico no puede alterarse.** Cada servicio queda firmado por el taller que lo realizó; un error se corrige con un nuevo registro, nunca editando el anterior.
3. **Se elimina un intermediario que concentra la confianza.** La llave pública de cada dispositivo se registra en un contrato Soroban, así que cualquiera puede verificar la firma del QR sin depender de nuestro servidor.

### Supuestos y riesgos

**Supuesto 1: los talleres registrarán servicios reales.** La cadena garantiza que el registro no se borra, pero no que el servicio se haya hecho de verdad. **Lo invalidaría** que los talleres registren servicios falsos a cambio de dinero. Mitigación: solo talleres autorizados pueden registrar, cada registro queda firmado por el taller y se puede adjuntar evidencia (fotos, factura) con su hash en cadena, de modo que un taller tramposo arriesga su reputación de forma permanente.

**Supuesto 2: alguien tiene incentivo para escanear.** El pasajero rara vez va a escanear el QR. **Lo invalidaría** que ni la aseguradora ni la autoridad lo adopten como parte de su proceso. Por eso el cliente principal que buscamos validar es la **aseguradora** (y en segundo lugar SEMOVI), y el socio como quien quiere demostrar cumplimiento.

**Supuesto 3: el dispositivo no se puede clonar ni retransmitir.** El QR rotativo evita fotografías, pero alguien podría transmitir la pantalla en vivo a otra unidad o extraer la llave del ESP32. **Lo invalidaría** que clonarlo sea barato y fácil. Mitigación: cifrado de flash del ESP32 y, en una siguiente versión, incluir ubicación GPS en la firma.
