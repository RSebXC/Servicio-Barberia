# Escenarios de aceptación

**Estado: especificados, todavía no ejecutados.** Son la base de las pruebas de negocio y de la demostración futura.

## Datos ficticios de referencia

Para estos ejemplos, Rafael, Fernando y Sofía realizan Corte, Barba y Mascarilla; Diego realiza Corte y Barba; Mateo realiza Corte. Los nombres distintos de los citados por el usuario, sus capacidades y los valores son ficticios.

Duraciones/precios de prueba: Corte 30 min/Q40; Barba 15 min/Q25; Mascarilla 10 min/Q20. La combinación completa suma 55 min/Q85. No son precios sugeridos para la barbería. Todos aceptan turnos salvo que un escenario diga lo contrario. Cada escenario parte de un estado limpio.

## Matriz de escenarios

| ID | Dado / cuando | Resultado esperado | Referencia |
| --- | --- | --- | --- |
| EA-01 | Una familia registra tres personas | Tres turnos distintos; ninguna reserva de grupo | RF-02, RN-01, CU-01 |
| EA-02 | Cliente elige Diego | Solo ve Corte y Barba; API rechaza Mascarilla aunque se manipule la petición | RF-03, RN-07 |
| EA-03 | Flexible pide los tres servicios | Solo Rafael, Fernando o Sofía pueden llamarlo; sigue sin asignación hasta el llamado | RF-03/09, RN-05/07 |
| EA-04 | En una variante solo Rafael hace Mascarilla y el flexible la pide | Solo Rafael puede llamarlo; no se transforma en específico | RN-05/07 |
| EA-05 | Ana flexible ingresa antes que Luis específico Fernando; Fernando se libera | Fernando llama a Ana si es compatible | RF-09, RN-06 |
| EA-06 | Luis específico Fernando ingresa antes que Pedro flexible; Rafael se libera | Rafael llama a Pedro y Luis sigue esperando Fernando | RN-04/06 |
| EA-07 | Ana flexible es anterior a Luis específico Fernando; admin cierra recepción de Fernando | Fernando llama a Luis; Ana espera otro compatible | RF-15, RN-09 |
| EA-08 | Fernando no recibe turnos y alguien intenta elegirlo desde una tablet desactualizada | Servidor rechaza el nuevo ingreso específico y actualiza opciones | RF-01/15, RN-09 |
| EA-09 | Fernando ya tiene un específico y pasa a no disponible | Conserva ese turno y puede terminarlo; no recibe flexibles | RN-09, CU-07 |
| EA-10 | Admin cambia Fernando → Rafael | Turno queda detrás de todos los elegibles que ya esperaban para Rafael; nueva prioridad global | RF-13, RN-10 |
| EA-11 | Admin cambia específico → cualquiera | Conserva prioridad vigente; no queda asignado | RN-11 |
| EA-12 | Admin cambia cualquiera → Fernando | Va al final con nueva prioridad; no adelanta a flexibles previos compatibles | RN-12 |
| EA-13 | Turno hace Fernando → Rafael → cualquiera | Conserva la prioridad posterior al envío al final, no la del ingreso original | RN-10/11 |
| EA-14 | Barbero marca no responde y pulsa siguiente | Llama a otro; el ausente conserva prioridad y no se repite en bucle en esa oportunidad | RF-11, RN-14 |
| EA-15 | Ausente específico Fernando regresa mientras Fernando atiende | Espera; al terminar vuelve a competir primero según su prioridad | RN-04/14/15 |
| EA-16 | Ausente flexible es compatible con Rafael, que se libera después | Rafael puede llamarlo según prioridad; no está reservado al primer barbero | RN-05/14 |
| EA-17 | Se repite ausencia varias veces | Nunca se retira ni penaliza automáticamente por contador | RN-14/16 |
| EA-18 | Administrador, cliente o TV intenta retirar | Denegado, aun enviando la solicitud directamente a API | RF-12/21, RN-16 |
| EA-19 | Barbero retira pendiente propio con motivo | Sale de candidatos, mantiene historial y no suma atención | RF-12, CU-05, DP-01 |
| EA-20 | Barbero intenta cambiar su disponibilidad | Denegado; administrador sí puede cambiarla | RF-15/21, RN-08 |
| EA-21 | Admin corrige nombre pendiente | Cambia nombre y conserva número/prioridad | RF-14, DP-03 |
| EA-22 | Admin modifica servicios a una combinación que su específico no realiza | Rechaza o exige cambio de preferencia con regla de prioridad; nunca guarda incompatibilidad | RF-14, RN-07/13 |
| EA-23 | Dos barberos llaman al mismo tiempo y solo hay un flexible | Solo uno lo reserva; el otro recibe sin candidato o siguiente distinto | RF-09, RNF-01 |
| EA-24 | Cliente confirma dos veces con el mismo ID de solicitud | Un solo turno, número y conjunto de líneas | RF-02, RNF-08 |
| EA-25 | Se reintenta finalizar una atención ya finalizada | No duplica conteo, valor ni eventos de finalización | RF-10/19, RNF-08 |
| EA-26 | Admin cambia precio del Corte después del ingreso | El turno conserva Q40; nuevos turnos usan el nuevo precio | RF-04/16/19 |
| EA-27 | Finaliza un turno con Corte + Barba | Una persona, dos servicios y Q65 de valor realizado; no “Q65 cobrados” | RF-19, CU-11 |
| EA-28 | Tablet/TV consultan endpoints de reportes o contactos | Denegado; respuesta pública no contiene esos datos | RF-21/24, RNF-07 |
| EA-29 | TV pierde conexión y vuelve dentro de la misma sesión | Recupera estado/cursor sin repetir anuncios procesados; mantiene señal de conexión | RF-17/18, RNF-09 |
| EA-30 | Audio no tiene voz en español o está bloqueado | Llamado visual continúa; operador ve fallo y puede llamar presencialmente | RNF-15, CU-10 |
| EA-31 | Se corta internet durante confirmación | No mostrar éxito sin verificar; reintento con mismo ID recupera resultado | RF-18, RNF-08/10 |
| EA-32 | Una atención supera la duración configurada | No finalizar ni liberar automáticamente; advertir estimación incierta | RF-05/10, RN-18 |
| EA-33 | Flexible sin otro compatible espera y Rafael cierra recepción | No llamarlo con Rafael; mostrar espera sin estimación si no hay otro receptor | RN-07/09, DP-06 |
| EA-34 | No existe combinación completa disponible | Impedir nuevo registro y explicar que se necesita asistencia | RF-03, CU-01 |
| EA-35 | Admin crea excepción con acuerdo y barbero llama | Se atiende beneficiado una vez; historial registra motivo/acuerdo; prioridades base se conservan | RF-22, RN-17, DP-04 |
| EA-36 | Admin intenta excepción hacia barbero incompatible o no receptor para flexible | Rechazar; acuerdo no evita validar restricciones | RN-07/09/17 |
| EA-37 | Dos registros se confirman simultáneamente | Números y prioridades únicos; orden determinado por confirmación del servidor | RF-23, RN-03 |
| EA-38 | Admin desactiva capacidad que requiere un específico pendiente | Bloquear cambio hasta resolver compromiso, sin perder turno | RF-16, CU-09 |
| EA-39 | Jornada tiene atenciones o pendientes y se intenta cerrar | No cancelar ni trasladar silenciosamente; exigir resolución | RF-23, DP-07 |
| EA-40 | Barbero inicia llamado ya reservado por otro | Denegado; turno continúa con su propietario legítimo | RF-10/21, RNF-01 |
| EA-41 | Tablet consulta lista pública de espera | Muestra números/preferencias y explicación de prioridad, sin nombres completos, teléfonos ni correos | RF-26, RNF-07 |

## Recorridos mínimos de aceptación

- **Registro y atención:** EA-01/02/05/27, comprobando tablet → celular → TV → reporte.
- **Prioridad y cambios:** EA-05 a EA-17 y EA-33.
- **Permisos:** EA-18/20/28/40, mediante API además de interfaz.
- **Integridad:** EA-23 a EA-26 y EA-37 con solicitudes simultáneas/reintentos reales.
- **Continuidad:** EA-29 a EA-32 sobre equipo y red de destino.

Las pruebas de rendimiento RNF y la restauración de respaldo son adicionales a estos casos. Los escenarios asociados a DP no resueltos deben actualizarse al validar esas decisiones; no se reportarán como aprobados antes de ello.
