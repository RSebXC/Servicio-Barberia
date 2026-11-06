# Qué necesita la barbería

Lista para levantar información y preparar una instalación. No es una orden de compra ni asume que la barbería carece del equipo.

## Equipo y conexión

| Elemento | Necesidad | Uso y criterio de validación |
| --- | --- | --- |
| Tablet de recepción | Necesario; reutilizable si funciona bien | Navegador actualizado, pantalla táctil legible, Wi-Fi estable; referencia de 10 pulgadas, no mínimo obligatorio |
| Soporte y alimentación de tablet | Necesario | Posición accesible y carga durante la jornada; modo de aplicación fija si el equipo lo permite |
| Un celular por barbero | Necesario durante operación | Navegador actualizado y conexión estable; puede ser equipo existente |
| Equipo de administrador | Necesario | Celular, tablet o computadora con acceso privado; no dejar su sesión abierta en el kiosco |
| TV/monitor visible | Necesario | Ubicación donde se lean números y nombres de barberos desde la espera |
| Reproductor para la TV | Necesario si la TV no pasa validación | Computadora existente o mini PC con navegador, HDMI y audio; validar antes de comprar |
| Bocinas | Solo si audio integrado no basta | Voz comprensible con música, secadoras y ruido de trabajo |
| Router/punto de acceso | Necesario | Cobertura en recepción, estaciones y TV; capacidad para todos los equipos activos |
| Internet | Necesario para arquitectura propuesta | Conexión estable, medida en el local; más importante la continuidad/latencia que un valor aislado de velocidad |
| HDMI, tomas y extensiones seguras | Según instalación | Conectar/alimentar equipos sin depender de batería durante toda la jornada |
| UPS | Recomendado si hay cortes frecuentes | Mantener router y reproductor por un periodo breve; dimensionar según carga real |
| Internet de respaldo | Opcional según continuidad requerida | Puede reducir interrupciones, pero debe probarse el cambio de red |

Una Smart TV con navegador no garantiza compatibilidad de voz o estabilidad. La solución de menor incertidumbre es validar un navegador en reproductor externo con la TV como pantalla. La selección de voz depende del dispositivo según [SpeechSynthesis](https://developer.mozilla.org/en-US/docs/Web/API/SpeechSynthesis); se comprueba en sitio.

## Información que debe entregar el negocio

- Nombre comercial, logotipo si existe y forma de nombrar a cada barbero.
- Lista real de cinco barberos y responsable de cada cuenta; correos de acceso del personal si se usa el proveedor propuesto.
- Catálogo: nombre del servicio, precio, minutos estimados y si es un paquete que sustituye otros servicios.
- Matriz de capacidades: qué barbero realiza cada servicio; confirmar quiénes son los tres que realizan todos.
- Moneda (propuesta GTQ), horario de recepción y responsable de abrir/cerrar jornada.
- Persona administradora y suplencia; quién autoriza cambios y quién atiende solicitudes de soporte.
- Equipo ya disponible, modelos/sistemas/navegadores y ubicación de TV/estaciones.
- Conectividad, cobertura, acceso autorizado al router y frecuencia de cortes.
- Volumen aproximado por día y máximo de personas/dispositivos simultáneos.
- Criterios pendientes DP-01 a DP-10 en [decisiones](../05-planificacion/decisiones-pendientes.md).

No se necesita importar una base histórica de clientes ni pedir correo a cada visitante para la primera versión.

## Plantilla para catálogo y capacidades

| Servicio | Precio | Minutos | Rafael | Fernando | Barbero 3 | Barbero 4 | Barbero 5 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Por completar | — | — | Sí/No | Sí/No | Sí/No | Sí/No | Sí/No |

Esta tabla se completa con el negocio; no copiar a producción los nombres/capacidades/precios ficticios de los escenarios de prueba.

## Servicios digitales y responsables

| Recurso | Decisión necesaria |
| --- | --- |
| Dominio | Titular, renovación y acceso administrativo |
| Hosting | Plan, facturación, región y responsable de renovación |
| Base de datos | Proyecto de producción, respaldo y responsable de recuperación |
| Acceso del personal | Altas/bajas, recuperación y correo de autenticación |
| Soporte | Canal, horario, tiempo de respuesta y qué cambios se cobran aparte |

El desarrollador instala y configura dentro del alcance contratado; la barbería proporciona información correcta, valida reglas y asigna responsables. El detalle comercial se acuerda antes de producción.

## Lista de preparación

- [ ] Registrar y probar el equipo existente antes de cotizar compras.
- [ ] Confirmar catálogo/capacidades y nombres visibles.
- [ ] Medir red y lectura/volumen de TV desde la sala.
- [ ] Acordar propiedad de cuentas y pagos recurrentes.
- [ ] Disponer de lista en papel y responsable para contingencias.
- [ ] Reservar una sesión de capacitación y una jornada piloto.
