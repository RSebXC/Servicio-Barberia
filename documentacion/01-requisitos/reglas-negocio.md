# Reglas de negocio y orden de la fila

## Vocabulario

- **Turno:** registro de una persona y una combinación de servicios.
- **Específico:** solo puede atenderlo el barbero elegido, salvo cambio administrativo.
- **Cualquiera/flexible:** permanece sin asignación; lo atiende un barbero compatible cuando se llama.
- **Compatible:** puede realizar todos los servicios del turno; no se divide una visita entre barberos en la primera versión propuesta.
- **Antigüedad vigente:** prioridad actual de un turno. Puede cambiar por una modificación de preferencia.
- **Acepta nuevos turnos:** disponibilidad definida por el administrador. Es independiente de estar ocupado o libre.
- **Comprometido:** turno específico pendiente o llamado que ya se reservó para un barbero.

## Reglas confirmadas

| ID | Regla |
| --- | --- |
| RN-01 | Un turno representa una persona. Una familia de tres crea tres turnos. |
| RN-02 | Se permiten varios servicios; el administrador define precio, duración y barberos capaces de realizarlos. |
| RN-03 | Sin citas: el orden nace cuando el servidor acepta el registro. Una llamada telefónica no reserva una hora. |
| RN-04 | El turno específico espera al barbero elegido, aunque otro se desocupe. |
| RN-05 | “Cualquiera” espera sin asignación. Su prioridad compite con la fila específica al liberarse un barbero compatible. |
| RN-06 | Para un barbero que acepta turnos, se llama al más antiguo entre sus específicos y los flexibles compatibles. |
| RN-07 | Se valida la combinación completa de servicios. Si solo un barbero puede realizarla, será su única opción compatible. |
| RN-08 | Solo el administrador modifica la disponibilidad de un barbero. El barbero consulta su estado. |
| RN-09 | No disponible: no recibe nuevos específicos ni flexibles; termina sus específicos pendientes. El administrador puede cambiarlos respetando las reglas de cambio. |
| RN-10 | Específico → otro específico: va al final de la fila del destino. |
| RN-11 | Específico → cualquiera: conserva la antigüedad vigente. |
| RN-12 | Cualquiera → específico: va al final de la fila del destino. |
| RN-13 | Solo el administrador modifica preferencias, servicios y datos del registro. El cliente no tiene perfil de edición. |
| RN-14 | Si no responde, el barbero pasa al siguiente. El ausente conserva prioridad para una próxima oportunidad compatible; no hay límite de intentos. |
| RN-15 | El regreso de un ausente no interrumpe una atención en curso. |
| RN-16 | Solo el barbero retira un turno de la fila. Sustituye la autorización inicial al administrador. |
| RN-17 | El administrador puede habilitar una excepción de orden tras acuerdo presencial con el cliente afectado. El sistema no la decide automáticamente. |
| RN-18 | El tiempo de espera es una estimación, no una garantía de hora de atención. |

## Decisiones de implementación propuestas

### Prioridad y desempate

El servidor asignará una secuencia creciente `priority_order` por jornada a cada ingreso. Para RN-10/RN-12 asignará una nueva secuencia al final y guardará la anterior en historial. RN-11 conserva la secuencia vigente, sin recuperar una secuencia anterior a un cambio que ya envió al cliente al final.

La secuencia es global: evita adelantar a un turno flexible previo cuando el cliente del final de una fila específica cambia después a “cualquiera”. Número de ticket y hora original de creación no cambian. El orden efectivo se decide por `priority_order`, con ID como desempate defensivo.

### Selección del siguiente

Dentro de una transacción exclusiva de la barbería:

1. Validar sesión, jornada y que el barbero no tenga otro llamado o atención activos.
2. Si acepta turnos: reunir sus específicos pendientes y flexibles compatibles.
3. Si no acepta turnos: reunir solo específicos ya comprometidos con él. No incorporar flexibles aunque sean anteriores.
4. Excluir turnos finales, reservados por otro y ausentes omitidos en esta misma oportunidad.
5. Ordenar por antigüedad vigente y reservar un único turno como `LLAMADO`.
6. Registrar evento para la pantalla y auditoría; confirmar antes de responder.

Un turno flexible llamado deja de estar sin asignación durante ese llamado/atención. Si no responde, la reserva se libera y vuelve a la espera flexible con su prioridad intacta.

**Cierre de recepción del barbero:** un llamado ya confirmado antes de marcarlo no disponible se conserva, aunque era flexible. La operación administrativa y el llamado usan el mismo bloqueo; el orden de confirmación define cuál ocurrió primero. Este tratamiento del llamado en curso es propuesto (DP-06).

### Ausencia sin bucles

Al pulsar “No responde / siguiente” se registra la ausencia y se busca otro candidato **en la misma oportunidad**, omitiendo al ausente ya probado. El sistema nunca lo vuelve a llamar inmediatamente en un bucle automático.

Una nueva oportunidad ocurre al terminar la siguiente atención o por una nueva acción explícita de llamado cuando el barbero sigue libre. Otro barbero compatible que se libere también puede llamar al ausente. Si no hay otro candidato, el barbero queda sin atención y puede volver a llamar cuando la persona llegue. No hay penalización permanente ni retiro automático. El detalle técnico de oportunidades es propuesto, no un límite de intentos.

### Cambios, servicios y excepciones

- Cambios normales solo mientras está `ESPERANDO`; si está llamado debe deshacerse el llamado mediante un flujo coordinado, pendiente DP-05. No cambiar en plena atención.
- Corregir nombre no altera prioridad. Corregir servicios conserva prioridad si sigue siendo compatible; un cambio de barbero aplica RN-10/RN-12. Regla propuesta DP-03.
- No permitir un cambio normal hacia un barbero no disponible. Sus turnos existentes permanecen; no recibe incorporaciones nuevas.
- Una excepción administrativa será una autorización puntual para un turno y barbero, con motivo, constancia de acuerdo y vigencia hasta el siguiente llamado o cambio relevante. Se consume una sola vez, no modifica la antigüedad base y no evita validar servicios/estado. El barbero ejecuta el llamado. Propuesta DP-04.
- No se borra un turno retirado ni se lo cuenta como atención realizada.

## Ejemplos normativos

| Situación | Resultado |
| --- | --- |
| Ana flexible llegó antes que Luis específico Fernando; Fernando acepta turnos y se libera | Pasa Ana si es compatible |
| Misma situación, Fernando ya está no disponible | Pasa Luis; Ana espera otro compatible |
| Luis espera Fernando y Pedro flexible llegó después; se libera Rafael | Rafael puede llamar a Pedro; Luis mantiene su elección |
| Un flexible solo es compatible con Rafael | Sigue siendo flexible; solo Rafael podrá llamarlo mientras acepte turnos |
| Ese Rafael deja de aceptar nuevos turnos antes de llamarlo | El flexible espera; no se transforma automáticamente en específico |
| Cambio Fernando → Rafael → cualquiera | Va al final al cambiar a Rafael; conserva esa nueva prioridad al pasar a cualquiera |
| Un cliente ausente vuelve mientras el siguiente está en atención | Espera a la próxima oportunidad compatible |

## Estimación de espera propuesta

No sumar simplemente la fila del barbero: también compiten los flexibles anteriores. Simular la liberación de barberos usando las mismas reglas RN-04 a RN-12, duraciones sumadas y remanente de la atención actual. En cada liberación simulada elegir el candidato compatible más antiguo y actualizar la disponibilidad simulada.

Se suma la duración de servicios sin descuentos por combinación; los paquetes que se solapen se configuran como un servicio propio. La barbería validará esta política en DP-03.

Si una atención excede su duración estimada, un remanente calculado en cero no significa que esté libre: mostrar “atención en curso; estimación sujeta a cambio”. Los ausentes preservan prioridad, por lo que su regreso puede alterar el pronóstico. Si no hay un barbero que pueda recibir el turno, mostrar “sin estimación disponible”, nunca cero minutos.

El teléfono al cliente, si ocurre, es una gestión humana fuera del sistema. Guardar su número o automatizar llamadas no forma parte del alcance confirmado.
