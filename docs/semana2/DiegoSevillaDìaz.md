# Historias de usuario individuales

**Nombre:** Diego Sevilla Dìaz

**Usuario de GitHub:** Oni7u7

---

## Mis historias de usuario

> Entre 5 y 7 historias en formato "como [rol] quiero [acción] para [beneficio]", pensadas desde distintos roles o necesidades del producto que el equipo está diseñando. Si escribes menos de 7, borra las líneas que no uses (mínimo 5).

1. Como socio dueño de una unidad de transporte concesionado quiero que cada servicio de mantenimiento y antidoping quede registrado con fecha y huella digital inalterable en un expediente digital para poder demostrar ante la aseguradora que mi unidad tenía mantenimiento vigente al momento de un accidente y no perder la cobertura civil.
2. Como taller mecánico autorizado quiero firmar digitalmente cada servicio que realizo y anclarlo al expediente de la unidad para que mi trabajo quede como evidencia verificable y no dependa de notas en papel que después alguien puede cuestionar o perder.
3. Como laboratorio de antidoping quiero registrar únicamente la huella criptográfica del resultado (nunca el dato sensible) y firmarlo como parte independiente para cumplir con mi obligación de certificar sin exponer información médica del chofer ni arriesgar responsabilidad legal por manejo de datos.
4. Como ajustador o aseguradora quiero consultar el expediente verificable de una unidad específica contra lo anclado en Stellar para resolver una disputa de cobertura con evidencia que no puede haber sido alterada por el socio, el taller ni Coviteni después del siniestro.
5. Como inspector de SEMOVI quiero escanear el QR rotativo que muestra la pantalla dentro de la unidad y ver en el momento si su mantenimiento está vigente para verificar cumplimiento sin tener que pedir papeles después ni depender de documentación en la oficina de la ruta.
6. Como chofer de la unidad quiero que el QR cambie cada 10-15 segundos automáticamente en la pantalla para que nadie pueda fotografiar un código viejo y pegarlo en otra unidad para simular cumplimiento que no existe.
7. Como pasajero quiero poder escanear el QR y ver el estado de mantenimiento de la unidad que estoy abordando para tener una señal adicional de confianza sobre las condiciones del vehículo, aunque no sea el usuario principal del sistema.

## La más importante y por qué

> Organiza las historias de mayor a menor importancia: en la primera fila va la más importante. En cada fila indica el número de la historia y por qué la ubicaste en esa posición. Si usaste menos de 7 historias, borra las filas que sobren.

| Orden de importancia | Historia # | Por qué |
| :---: | :---: | --- |
| 1 (la más importante) | #1 | Es el problema original y la razón de ser del producto: el socio se descapitaliza cuando la aseguradora no paga por falta de prueba.  |
| 2 | #2 | Sin la firma del taller no hay dato honesto en el origen. Es la pieza que resuelve "quién certifica que el mantenimiento sí se hizo", el hueco que mata la mayoría de ideas blockchain. |
| 3 | #4 | Es la contraparte directa de #1: si la aseguradora no puede consultar y validar el expediente, el socio sigue perdiendo la disputa aunque el registro exista. |
| 4 | #5 | El QR en vivo es la capa que sirve a autoridad y aseguradora en el momento, no después. |
| 5 | #6 | Sin la rotación del QR, el mecanismo anti-falsificación se cae y el puente físico deja de ser confiable. |
| 6 | #3 | El antidoping es parte del expediente y requiere cuidado especial por datos sensibles, pero es un componente secundario frente al mantenimiento como causa principal de disputa con la aseguradora. |
| 7 (la menos importante) | #7 | El pasajero es beneficiario secundario y así lo reconocemos. |
