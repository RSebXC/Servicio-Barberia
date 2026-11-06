# Manual de usuario previsto

**Versión documental 1.0.** La aplicación todavía no está implementada. Los nombres entre comillas representan acciones previstas y se actualizarán con la interfaz final; no son botones existentes ni hay capturas de una demo.

## Cliente — Registrar mi turno

1. En la tablet, elige tu barbero o “Cualquiera”.
2. Marca los servicios que necesitas. Si eliges barbero, solo aparecen los que él realiza.
3. Escribe tu nombre y revisa la selección.
4. Confirma una vez y espera el comprobante.
5. Conserva tu número de turno. La espera es aproximada y puede cambiar.
6. Atiende al llamado en la pantalla y dirígete al barbero indicado.

Cada persona de una familia debe registrarse por separado. “Cualquiera” respeta tu llegada, pero solo te puede atender quien realice todos tus servicios. No significa pasar inmediatamente.

En recepción podrás consultar la lista pública por número y preferencia. No representa una única secuencia rígida de llamados: un cliente puede esperar un barbero específico mientras otro pasa con un barbero distinto.

Si te equivocaste o quieres cambiar de barbero, solicita ayuda al administrador. No vuelvas a anotarte para corregirlo: crearías otro turno. No necesitas cuenta, correo ni contraseña.

Si aparece un error de conexión, solicita ayuda antes de confirmar otra vez como un registro nuevo. El personal verificará si la primera solicitud se guardó.

## Administrador — Preparar el día

1. Inicia sesión en tu equipo privado.
2. Revisa la jornada, servicios, precios y minutos estimados.
3. Comprueba las capacidades de cada barbero y quién recibirá turnos.
4. Abre la jornada y la recepción general según la configuración final.
5. Confirma que tablet y TV estén autorizadas y conectadas.
6. Haz la prueba de sonido y revisa que no queden datos de prueba en producción.

No dejes tu sesión administrativa abierta en la tablet de autoservicio.

### Configurar servicios y capacidades

1. Entra a servicios y crea o edita nombre, precio y duración estimada.
2. Asigna qué barberos realizan ese servicio.
3. Guarda y revisa las opciones que ve un cliente.

El precio nuevo aplica a registros nuevos; no cambia automáticamente turnos existentes. Si quitar una capacidad deja un pendiente sin atención posible, resuelve primero ese compromiso.

### Marcar que un barbero no recibe más turnos

1. Busca al barbero y revisa su fila.
2. Marca “No disponible / no recibe nuevos turnos”.
3. Sus específicos pendientes se conservan y podrá terminarlos.
4. Los clientes de “Cualquiera” esperarán otro barbero compatible, aunque se anotaran antes.
5. Cuando deba volver a recibir, marca disponible nuevamente.

Marcar no disponible no termina una atención ni retira sus pendientes. Solo tú cambias esta disponibilidad.

### Cambiar preferencia de un cliente

1. Busca su número y verifica el nombre.
2. Selecciona una preferencia válida y revisa el efecto sobre su posición.
3. Explica la regla antes de confirmar:

| Cambio | Resultado |
| --- | --- |
| Un específico a otro específico | Al final de la fila del nuevo |
| Específico a cualquiera | Conserva antigüedad vigente |
| Cualquiera a específico | Al final de la fila del elegido |

El número de turno no cambia. Un barbero que no recibe turnos no puede ser el destino de una incorporación normal.

### Corregir un registro

Busca el turno pendiente, corrige nombre o servicios y guarda. El sistema comprueba compatibilidad. Si necesita otro barbero, aplica el cambio de preferencia y su efecto de fila. El flujo normal no modifica atenciones ya iniciadas/finalizadas.

### Registrar a alguien que llama por teléfono

Usa el registro asistido, escribe su nombre y selección y confirma igual que en la tablet. Comunica el número y que no se reserva una hora. Si no está al llamado, aplica el mismo procedimiento de ausencia que a cualquier persona.

### Solicitar una excepción de orden

Habla primero con la persona que tiene prioridad. Solo con su acuerdo registra la excepción, motivo y turno beneficiado. El barbero hará el llamado autorizado. No uses este mecanismo para corregir servicios incompatibles o evitar restricciones de disponibilidad. Su detalle de interfaz se validará en DP-04.

### Retirar clientes

**El administrador no tiene permiso de retiro.** Si alguien se fue definitivamente, comunícalo al barbero autorizado para que él lo retire. No simules una finalización para sacarlo de la fila.

### Revisar el reporte y cerrar jornada

Consulta personas atendidas, servicios realizados, barberos y valor de servicios. Pendientes y retirados no son atenciones. El valor mostrado no acredita que el cliente pagó ni representa ganancia neta.

Al cerrar recepción general deja que se resuelvan los compromisos. No cierres una jornada cancelando automáticamente pendientes. El flujo final de jornada se confirmará en DP-07.

## Barbero — Atender desde mi celular

1. Inicia sesión con tu cuenta y revisa tu nombre y disponibilidad.
2. Consulta tus específicos y los flexibles compatibles, que aparecen diferenciados.
3. Cuando estés libre, pulsa “Llamar siguiente”. El sistema decide por prioridad.
4. Verifica que el cliente corresponda al turno y pulsa “Iniciar atención”.
5. Al terminar, pulsa “Finalizar atención”. Después puedes llamar de nuevo.

No necesitas esperar a que se cumplan los minutos estimados; marca el fin real. El sistema tampoco terminará por ti cuando pase ese tiempo.

### Si el cliente no responde

1. Comprueba que no esté respondiendo.
2. Pulsa “No responde / siguiente”.
3. Atiende al siguiente llamado; el ausente mantiene su prioridad para otra oportunidad.

No uses “Retirar” si solamente llegará más tarde. Si regresa mientras estás atendiendo, esperará a que termines. Si eligió “Cualquiera”, otro barbero compatible podría llamarlo antes.

### Si se fue definitivamente

Sobre un turno que estés autorizado a gestionar, selecciona “Retirar”, escribe el motivo y confirma. El turno conserva historial, pero ya no se llama. El límite exacto de filas sobre las que puedes retirar está propuesto en DP-01; no se permitirá retirar una atención activa de otro barbero.

### Si necesitas dejar de recibir turnos

Solicita al administrador que te marque no disponible. Verás el estado en tu perfil, pero no podrás cambiarlo. Termina tus específicos pendientes; desde ese momento no se incorporan flexibles. Un llamado ya confirmado se resuelve antes de retirarte.

### Si hay un error de servicios o conexión

Pide al administrador corregir servicios antes de iniciar, siguiendo el flujo final validado. Si la aplicación pierde red, no asumas que una acción se guardó: al reconectar recupera el estado antes de repetir. Para llamados que no se escucharon, repetir el anuncio no debe crear otra reserva.

## Personal — Encender la pantalla de llamados

1. Enciende TV, reproductor y audio; selecciona la entrada correcta.
2. Abre la vista pública autorizada.
3. Activa y prueba el sonido mediante la acción inicial.
4. Comprueba que se lean los turnos desde la zona de espera.
5. Durante la jornada revisa el indicador de conexión.

La pantalla anuncia número y barbero. Si la voz falla, mantén la pantalla y realiza llamados humanos mientras se resuelve. Si está desconectada, no consideres actualizado el último llamado visible.

## Problemas frecuentes

| Situación | Qué hacer |
| --- | --- |
| No aparece el barbero elegido como seleccionable | Puede no recibir turnos; consultar al administrador |
| No aparece un servicio | No lo realiza el elegido o la combinación no tiene un barbero compatible |
| La espera aumentó | Es aproximada; puede haber atenciones más largas, ausentes que vuelven o cambios |
| El cliente cree que pasó alguien después | Revisar compatibilidad/preferencia y cambios de prioridad en historial |
| El número figura dos veces visualmente | Revisar el ID y jornada antes de crear o retirar nada; reportar posible fallo |
| No hay internet | Administrador activa la contingencia manual; no mantener dos filas paralelas |
| No puedo entrar | Solicitar recuperación de acceso; no usar la cuenta de otro compañero |

Para la caída prolongada seguir el procedimiento de [integración y contingencia](integracion-puesta-marcha.md). El sistema no procesa cobros ni envía mensajes/llamadas automáticas al cliente en esta versión.
