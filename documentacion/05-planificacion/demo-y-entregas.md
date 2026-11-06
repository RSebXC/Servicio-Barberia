# Demo y plan de entregas

Este documento fija objetivos y límites para preparar la siguiente etapa. **No inicia el diseño visual ni la implementación de la demo**, que el propietario del proyecto solicitará después.

## Alcance de la futura demo

Mostrar que el producto coordina una barbería y respeta reglas entendibles. Utilizar cinco perfiles ficticios y un catálogo pequeño, con la matriz de capacidades declarada como ficticia.

| Recorrido | Qué debe demostrar |
| --- | --- |
| Registro | Una persona elige barbero o cualquiera, marca varios servicios y recibe turno |
| Prioridad mixta | Flexible anterior pasa antes que específico posterior si ambos son compatibles |
| Barbero no disponible | Termina específicos y no recibe flexibles ni nuevas incorporaciones |
| Atención | El barbero llama, la TV anuncia y luego se registra inicio/fin |
| Ausencia | Se avanza sin eliminar ni penalizar definitivamente al ausente |
| Cambios | Cada una de las tres transiciones aplica su regla de fila |
| Servicios | No se ofrece una combinación que nadie pueda completar |
| Resumen | Personas y valor realizado coinciden con atenciones finalizadas |

No llenar la presentación con módulos futuros. Correos, caja, citas, inventario y fidelización quedan fuera.

## Modalidad a elegir al iniciar la demo

- **Prototipo local:** valida flujo y presentación con estado simulado. Debe identificarse como simulación; no prueba coordinación real entre equipos, seguridad o persistencia de producción.
- **Demo conectada, recomendada si se quiere mostrar TV y celulares:** usa servidor y datos compartidos de prueba. Permite comprobar el recorrido multidispositivo; aun así requiere endurecimiento y puesta en marcha antes de operar con clientes reales.

La decisión no cambia las reglas de negocio. Si se elige prototipo local, no incorporar datos reales de clientes ni presentarlo como versión operativa.

## Fases propuestas

| Fase | Entregables | Criterio de salida |
| --- | --- | --- |
| 0. Documentación actual | Requisitos, reglas, casos, arquitectura, operación y manual previsto | Paquete coherente y pendientes visibles |
| 1. Diseño de demo, posterior a instrucción del usuario | Identidad visual, navegación y recorrido revisable | Flujos reconocibles y acciones consistentes con permisos |
| 2. Construcción de demo | Recorridos con datos ficticios y reinicio controlado del escenario | Recorridos principales demostrables sin alterar reglas |
| 3. Núcleo operativo | Persistencia, identidad, transacciones, permisos y eventos | Prioridad, concurrencia y permisos verificados |
| 4. Preparación de producción | Configuración real, respaldo, infraestructura y pruebas en local | RNF críticos y recuperación aprobados |
| 5. Piloto y entrega | Capacitación, acompañamiento, manual actualizado y soporte acordado | Barbería completa jornada con seguimiento de incidencias |

No se fijan horas ni fechas sin catálogo final, modalidad de demo, estado del equipo y decisiones pendientes. La demo no obliga a incluir de forma gratuita todas las fases posteriores.

## Criterios mínimos de la demo

- [ ] Registro de específico y flexible con varios servicios.
- [ ] Explicar y demostrar prioridad, no solo mostrar una fila estática.
- [ ] Mostrar que “Cualquiera” no promete un barbero hasta el llamado.
- [ ] Mostrar diferencia entre no disponible y ocupado.
- [ ] Demostrar ausencia, cambios de preferencia y retiro por barbero.
- [ ] Hacer visible el turno/barbero en TV y probar sonido si es parte de la presentación.
- [ ] Usar reportes rotulados como valor de servicios, sin afirmar cobros.
- [ ] Declarar qué está conectado, qué está simulado y qué falta para producción.
- [ ] Poder volver a datos ficticios iniciales sin tocar información de producción.

## Antes de cotizar la versión operativa

Separar desarrollo de instalación, equipo, suscripciones y soporte. Definir entregables, número de revisiones, aceptación, responsabilidades, propiedad de cuentas/código según acuerdo y cómo se cobran nuevas funciones. Los escenarios EA pueden formar parte de la aceptación técnica, una vez validados los DP asociados.

Una estimación debe considerar especialmente motor de prioridad, pruebas concurrentes, integración de TV/audio y contingencia. La cantidad de tablas no mide por sí sola el esfuerzo del proyecto.
