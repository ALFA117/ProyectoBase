# Funcionamiento del Frontend de QRuta

## 1. Objetivo

El frontend de QRuta es la capa de presentación e interacción de la plataforma. Su función es permitir que los diferentes usuarios registren servicios de mantenimiento, consulten expedientes digitales y verifiquen el estado de las unidades de transporte público mediante interfaces sencillas y accesibles.

El sistema contempla interfaces diferenciadas según las necesidades de los talleres mecánicos, socios propietarios, inspectores de SEMOVI y pasajeros.

## 2. Interfaces del sistema

### 2.1. Aplicación web del taller

Permite a los talleres autorizados registrar los servicios de mantenimiento de cada unidad. El formulario contempla información como identificación de la unidad, fecha, tipo de servicio, kilometraje y evidencias del mantenimiento realizado.

Una vez capturada la información, el sistema envía los datos al backend para validar la autorización del taller, procesar el registro y ejecutar las operaciones de firma digital y anclaje de la huella criptográfica en Stellar.

La interfaz está diseñada para facilitar el registro desde un dispositivo móvil, sin exigir que el taller gestione directamente llaves privadas, frases semilla o XLM.

### 2.2. Panel del socio propietario

Permite al socio propietario consultar el expediente digital de cada unidad, revisar el historial de mantenimiento y conocer el estado de vigencia de los servicios registrados.

También contempla la consulta de próximos vencimientos, la recepción de alertas y la exportación del expediente para presentarlo ante una aseguradora cuando sea necesario demostrar el mantenimiento de la unidad.

### 2.3. Página de verificación mediante QR

Es una página web accesible desde el navegador de cualquier teléfono celular, sin necesidad de instalar una aplicación ni crear una cuenta para realizar una consulta pública.

Cuando un inspector de SEMOVI o un pasajero escanea el código QR de una unidad, accede a una página que permite consultar el estado de verificación y la fecha del último mantenimiento, de acuerdo con los permisos y la información pública definida por la plataforma.

El backend comprueba la vigencia del código y recupera la información correspondiente antes de mostrar el resultado.

### 2.4. Pantalla de la unidad

La arquitectura contempla una pantalla instalada dentro de la unidad de transporte que muestra un código QR dinámico. Este código se renueva cada 10–15 segundos para reducir el riesgo de reutilización de fotografías antiguas.

La pantalla funciona como punto de acceso a la página de verificación. La autenticidad del código no depende únicamente de su renovación visual, sino también de los mecanismos de generación, vigencia y validación implementados en el backend.

## 3. Comunicación entre el frontend y el backend

El frontend se comunica con el backend mediante una API, que procesa las solicitudes y devuelve los resultados correspondientes.

El flujo general de una operación es el siguiente:

1. El usuario realiza una acción desde la interfaz.
2. El frontend verifica que los campos obligatorios estén completos y que los datos tengan el formato esperado.
3. La interfaz envía una solicitud al backend mediante la API.
4. El backend aplica las reglas de negocio, comprueba permisos y procesa la solicitud.
5. Cuando corresponde, el backend interactúa con la base de datos y con la red Stellar.
6. El backend devuelve el resultado de la operación.
7. El frontend presenta al usuario un mensaje de éxito, error o estado pendiente de confirmación.

La validación realizada en el frontend mejora la experiencia de uso, pero no sustituye las comprobaciones de seguridad que deben ejecutarse en el backend.

## 4. Principios de diseño

El frontend de QRuta se orienta por los siguientes principios:

* **Simplicidad:** reducir los pasos necesarios para registrar y consultar información.
* **Accesibilidad:** permitir el acceso desde navegadores web y dispositivos móviles.
* **Separación por roles:** ofrecer funciones de acuerdo con las responsabilidades de cada usuario.
* **Claridad:** comunicar los estados de los registros y las operaciones pendientes de forma comprensible.
* **Seguridad:** evitar la exposición de información sensible y de llaves privadas en el navegador.
* **Verificabilidad:** mostrar resultados respaldados por las validaciones realizadas en el backend.

## 5. Relación con la blockchain

El frontend no necesita interactuar directamente con Stellar para mostrar los expedientes o generar la interfaz de verificación. La comunicación con la blockchain se centraliza en el backend.

Cuando se registra un servicio, el backend procesa la información, calcula la huella digital correspondiente y solicita su anclaje en Stellar. Posteriormente, la plataforma puede consultar la evidencia para verificar la integridad del registro.

Esta separación permite que las interfaces sigan una lógica de funcionamiento independiente de los detalles internos de las transacciones blockchain.

## 6. Alcance del frontend en el MVP

El alcance propuesto contempla:

* Interfaz de registro de servicios para talleres autorizados.
* Panel del socio propietario para consultar expedientes.
* Página de verificación pública mediante QR.
* Visualización del código QR dinámico en la unidad.
* Consulta de estados y resultados devueltos por el backend.
* Acceso a la información necesaria para exportar el expediente.

Las funciones descritas corresponden al diseño propuesto para el MVP. Su disponibilidad efectiva debe comprobarse en el código y en las pruebas del repositorio.

## 7. Consideraciones de seguridad

El frontend no determina por sí solo la autenticidad de un servicio ni garantiza que una unidad tenga mantenimiento vigente. Estas conclusiones dependen de las validaciones del backend, la autorización del taller, la integridad del expediente y la verificación de la evidencia criptográfica correspondiente.

Asimismo, los registros cuyo anclaje todavía no haya sido confirmado en Stellar deben distinguirse de aquellos que ya cuentan con evidencia de confirmación.

El objetivo es ofrecer una interfaz sencilla para el usuario sin comprometer la confiabilidad de la información presentada.

# Decisiones Técnicas de QRuta

## 1. Objetivo

Este documento describe las decisiones técnicas propuestas para el desarrollo del MVP de QRuta y explica cómo contribuyen a resolver el problema de la falta de registros de mantenimiento verificables en el transporte público concesionado.

La arquitectura busca que los servicios registrados por talleres autorizados puedan consultarse y verificarse por propietarios, aseguradoras y autoridades, reduciendo la dependencia de documentos físicos y registros que pueden perderse o modificarse.

## 2. Arquitectura general

La arquitectura propuesta se divide en tres capas principales:

### 2.1. Capa de presentación: frontend

Contiene las interfaces web para talleres, socios propietarios, inspectores y pasajeros, así como la interfaz destinada a mostrar el código QR en la unidad.

Su responsabilidad es recibir las acciones del usuario, presentar información y comunicarse con el backend mediante una API.

### 2.2. Capa de lógica: backend y base de datos

El backend centraliza las reglas de negocio y coordina el registro de los servicios de mantenimiento.

Sus responsabilidades incluyen:

* Validar la autorización de los talleres.
* Procesar los datos de los servicios.
* Gestionar los expedientes digitales.
* Calcular las huellas criptográficas mediante SHA-256.
* Coordinar las operaciones de firma y anclaje.
* Generar y validar los códigos QR dinámicos.
* Consultar la red Stellar para comprobar las evidencias.
* Controlar los permisos de acceso a la información.
* Gestionar los estados de las operaciones y los registros pendientes de confirmación.

La base de datos conserva los expedientes completos y la información necesaria para el funcionamiento de la plataforma fuera de la blockchain.

### 2.3. Capa de integridad: Stellar

Stellar se utiliza para anclar las huellas criptográficas de los registros de mantenimiento mediante transacciones verificables.

La red permite consultar la evidencia del anclaje y comprobar si la huella de un expediente coincide con la que quedó registrada.

La blockchain no almacena necesariamente el expediente completo ni demuestra por sí sola que el mantenimiento haya ocurrido. Su función es proporcionar evidencia verificable de la huella registrada.

## 3. Justificación de las tecnologías

### 3.1. SHA-256

SHA-256 es una función criptográfica que permite calcular una huella digital a partir del contenido de un registro.

Si cambia algún dato incluido en el cálculo, como la fecha o el tipo de servicio, la huella resultante debe ser diferente.

Esta característica permite detectar alteraciones cuando se compara la huella recalculada con la que se ancló originalmente en Stellar.

Para que la comparación sea confiable, el sistema debe definir de manera consistente cómo se estructuran y serializan los datos que forman parte del registro.

### 3.2. Stellar

Se elige Stellar para proporcionar un registro compartido y verificable de las huellas criptográficas de los servicios de mantenimiento.

Su utilización responde a la necesidad de que diferentes actores, como talleres, propietarios y aseguradoras, puedan comprobar la integridad de los registros sin depender exclusivamente de la base de datos de una sola organización.

En el MVP se propone utilizar transacciones con datos asociados, mediante mecanismos como `manage_data` o un memo hash, según el diseño final de la transacción.

La implementación debe respetar los límites de tamaño, las reglas de la red y los requisitos de firma correspondientes al mecanismo seleccionado.

### 3.3. Base de datos externa a la blockchain

Los expedientes completos se almacenan fuera de Stellar para mantener la información operativa en una base de datos convencional.

Esta decisión permite conservar datos como kilometraje, tipo de mantenimiento, evidencias y referencias documentales sin publicar todo el contenido en una red pública.

La base de datos facilita las consultas de la aplicación, mientras que Stellar proporciona evidencia criptográfica para comprobar la integridad de los registros.

La solución requiere controles de acceso, respaldos y medidas de protección para evitar pérdidas o accesos no autorizados.

### 3.4. Backend y API

El backend centraliza las reglas de negocio y la comunicación con la base de datos y Stellar.

Esta decisión permite mantener las llaves privadas fuera del frontend, validar las solicitudes en un entorno controlado y evitar que la lógica crítica dependa exclusivamente del navegador del usuario.

La API permite que las distintas interfaces utilicen los mismos servicios de registro, consulta y verificación.

### 3.5. Vercel y Supabase

El Product Blueprint propone Vercel para el alojamiento de la aplicación y Supabase para la base de datos y los servicios asociados.

Estas herramientas se consideran para facilitar el desarrollo inicial y reducir los costos de infraestructura durante la validación del MVP.

Su configuración definitiva debe responder a los requisitos de seguridad, disponibilidad, escalabilidad y presupuesto del proyecto.

### 3.6. QR dinámico

Se propone un código QR que se renueva cada 10–15 segundos para reducir el riesgo de reutilización de fotografías antiguas.

El mecanismo debe incorporar una validación de vigencia y correspondencia con la unidad. El diseño puede utilizar tokens temporales y mecanismos criptográficos de autenticación.

La renovación periódica reduce determinados riesgos, pero no elimina por sí sola la posibilidad de retransmitir un código válido. Por ello, la validación debe realizarse en el backend.

### 3.7. Stellar Testnet

Se propone utilizar la red de pruebas de Stellar durante el desarrollo del MVP.

Esto permite probar la creación y consulta de transacciones antes de evaluar el despliegue en la red principal.

La transición a mainnet deberá considerar la gestión de fondos, la seguridad de las llaves, los costos operativos y las pruebas de funcionamiento.

### 3.8. No utilizar Soroban en la primera versión

El MVP no contempla inicialmente contratos inteligentes de Soroban, porque el objetivo prioritario es registrar huellas criptográficas y verificar su integridad.

Esta decisión busca mantener una arquitectura inicial sencilla y concentrar los esfuerzos en validar el flujo esencial del producto.

La incorporación de contratos inteligentes podrá evaluarse posteriormente si se requieren reglas automatizadas que justifiquen su complejidad adicional.

## 4. Decisiones de seguridad

### 4.1. Gestión de identidades y firmas

Cada taller autorizado debe estar asociado con una identidad verificable y con los mecanismos criptográficos definidos para firmar los registros.

La arquitectura debe distinguir entre la autenticación de un usuario en la aplicación y la firma digital que vincula un registro con una identidad criptográfica.

Las llaves privadas no deben exponerse en el frontend ni almacenarse en lugares inseguros.

La solución debe establecer cómo se generan, protegen, utilizan y revocan las llaves de los talleres.

### 4.2. Patrocinio de las transacciones

El proyecto propone que la plataforma absorba los costos de las operaciones en Stellar para que los talleres no tengan que gestionar XLM directamente.

La implementación deberá definir el mecanismo de patrocinio compatible con las operaciones utilizadas, así como las responsabilidades de firma y los controles sobre los recursos de la plataforma.

El patrocinio de los costos no elimina la necesidad de utilizar las firmas criptográficas requeridas por la red.

### 4.3. Verificación de integridad

La verificación debe recuperar el expediente correspondiente, recalcular la huella con el mismo procedimiento utilizado originalmente y compararla con la evidencia anclada.

Si las huellas no coinciden, el sistema debe identificar la discrepancia y evitar presentar el registro como íntegro.

### 4.4. Manejo de errores y confirmaciones

El sistema debe distinguir entre un registro capturado, un registro procesado y un registro cuyo anclaje ha sido confirmado en Stellar.

Si una operación falla o queda pendiente, la interfaz debe comunicarlo de forma clara. No debe presentarse como confirmado un anclaje que todavía no ha sido validado.

### 4.5. Protección de la información

La información completa del expediente se conserva fuera de la blockchain. Los accesos a dicha información deben controlarse mediante permisos y mecanismos de autenticación apropiados.

La información mostrada públicamente mediante el QR debe limitarse a los datos necesarios para la verificación y no debe exponer documentación sensible.

## 5. Flujo técnico de un registro

1. El taller autorizado captura los datos del servicio.
2. El backend verifica la autorización y valida la información.
3. El sistema prepara el contenido que formará parte del registro.
4. Se aplica el mecanismo de firma digital definido para vincular el registro con la identidad criptográfica correspondiente.
5. Se calcula la huella SHA-256 del contenido establecido.
6. El backend prepara y envía la transacción de anclaje a Stellar.
7. El sistema registra la referencia de la transacción y su estado de confirmación.
8. El expediente queda disponible para consulta según los permisos definidos.
9. Cuando se solicita una verificación, el sistema recalcula la huella y la compara con la evidencia anclada.

## 6. Alcance del MVP

El MVP prioriza las siguientes funciones:

* Registro de servicios por talleres autorizados.
* Firma de los registros según el mecanismo criptográfico definido.
* Anclaje de huellas SHA-256 en Stellar.
* Expediente digital de mantenimiento por unidad.
* Verificación mediante QR dinámico.
* Consulta de solo lectura para aseguradoras.
* Alertas básicas de vencimiento.
* Validación de la integridad de los registros.

Las funciones adicionales, como el registro de antidoping, las listas de inspección diaria, las órdenes de corrección y el tablero avanzado de flotillas, quedan fuera del alcance inicial definido en el Product Blueprint.

## 7. Limitaciones técnicas

El anclaje de una huella criptográfica permite comprobar si el contenido presentado coincide con el que se registró, pero no garantiza que los datos originales fueran verdaderos.

La confiabilidad del sistema depende también de la verificación de los talleres, la validez de las firmas, la calidad de las evidencias, la seguridad de la base de datos y la correcta implementación de los permisos.

La seguridad del QR depende de su diseño y validación, no únicamente de su renovación periódica.

La disponibilidad y el rendimiento deben comprobarse mediante pruebas antes de considerar validadas las métricas técnicas del proyecto.

## 8. Estado de implementación

Las tecnologías, componentes y mecanismos descritos en este documento representan las decisiones propuestas para la arquitectura del MVP.

Cada componente deberá verificarse contra el código, la configuración y las pruebas del repositorio para determinar si está implementado, en desarrollo o pendiente.

El objetivo de esta documentación es mantener trazabilidad entre el problema de negocio, las decisiones de ingeniería y las funcionalidades efectivamente entregadas.
