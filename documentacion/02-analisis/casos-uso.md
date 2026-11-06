# Casos de uso

Estos casos describen el producto previsto. Los detalles marcados como propuestos se revisan en [decisiones](../05-planificacion/decisiones-pendientes.md).

## CU-01 — Registrar un turno

**Actor:** cliente o administrador en registro asistido. **Requisitos:** RF-01 a RF-06. **Precondición:** jornada abierta y dispositivo autorizado.

1. Elegir un barbero o “Cualquiera”.
2. Seleccionar uno o varios servicios compatibles y escribir nombre.
3. Revisar servicios, valor, preferencia y carácter aproximado de la espera.
4. Confirmar una sola solicitud, aunque se repita el toque.
5. El servidor revalida servicios/disponibilidad, asigna número y prioridad y guarda las líneas con sus importes y duraciones.
6. Mostrar comprobante y volver al inicio eliminando los datos del cliente anterior.

**Alternativas:** sin combinación válida, pedir corregir selección; si cambió la disponibilidad, actualizar opciones sin crear el turno. Si la respuesta se pierde, consultar/reintentar con el mismo identificador, sin crear otro turno.

**Resultado:** una persona registrada y sin asignación anticipada si eligió “Cualquiera”. Cada familiar repite el proceso. Registro telefónico conserva el mismo procedimiento; no crea una reserva por hora.

## CU-02 — Llamar al siguiente

**Actor:** barbero. **Requisitos:** RF-08/09/17. **Precondición:** sesión propia, jornada abierta y sin llamado/atención activos.

1. Pulsar “Llamar siguiente”.
2. El servidor valida rol, disponibilidad y candidatos bajo bloqueo compartido por las mutaciones de fila.
3. Elegir el más antiguo compatible; si no acepta turnos, solo se consideran sus específicos pendientes.
4. Reservar el turno para ese barbero y registrar un evento de llamado.
5. Actualizar paneles y pantalla pública, que muestra número/barbero y solicita el anuncio de voz.

**Alternativas:** no hay candidato: informar sin cambiar estado; conflicto de versión: recargar; falla de voz: mantener anuncio visual. Un reintento devuelve el mismo llamado confirmado.

**Resultado:** un solo turno `LLAMADO`, reservado para un solo barbero.

## CU-03 — Atender y finalizar

**Actor:** barbero que tiene el llamado. **Requisito:** RF-10.

1. Verificar que el cliente corresponde al turno.
2. Pulsar “Iniciar”; guardar barbero real e instante de inicio.
3. Realizar los servicios; el paso del tiempo por sí solo no finaliza la atención.
4. Pulsar “Finalizar”; guardar fin y estado final una sola vez.
5. Actualizar carga, estimaciones y reporte; el barbero puede llamar al siguiente.

**Alternativas:** si detecta servicios equivocados antes de iniciar, solicitar corrección al administrador según DP-05. Una atención en curso no se reasigna ni se retira como si fuera un pendiente.

**Resultado:** un turno finalizado, una persona atendida y sus servicios contabilizados; no se registra un pago.

## CU-04 — Pasar un cliente que no responde

**Actor:** barbero sobre su llamado. **Requisito:** RF-11.

1. Verificar presencialmente que el cliente no está respondiendo.
2. Pulsar “No responde / siguiente”.
3. Registrar intento sin respuesta; liberar la reserva y conservar la prioridad.
4. Buscar otro candidato omitiendo en esa oportunidad al ausente.
5. Cuando ocurra otra oportunidad compatible, el ausente puede ser llamado nuevamente.

**Alternativas:** si no hay otro candidato, permanecer libre y volver a llamar mediante acción explícita cuando corresponda. La ausencia no elimina al cliente automáticamente y no tiene contador máximo.

**Resultado:** se avanza sin perder la antigüedad del ausente ni interrumpir otra atención cuando regrese.

## CU-05 — Retirar un turno pendiente

**Actor:** barbero; alcance propio propuesto DP-01. **Requisito:** RF-12.

1. Elegir un pendiente que esté autorizado a gestionar.
2. Indicar motivo: por ejemplo, el cliente se retiró definitivamente.
3. Confirmar retiro.
4. El servidor valida permiso, estado y versión; marca `RETIRADO` y registra autor/motivo.

**Alternativas:** administrador o cliente intenta retirar: denegar. Si otro barbero ya lo llamó o inició, rechazar la modificación desactualizada. Atención en curso: no aplicar retiro de fila.

**Resultado:** deja de ser candidato, conserva historial y no suma atención ni valor realizado. No se reutiliza su número.

## CU-06 — Cambiar preferencia

**Actor:** administrador. **Requisito:** RF-13. **Precondición propuesta:** turno `ESPERANDO`.

1. Buscar turno y verificar identidad con la persona.
2. Elegir nueva preferencia y validar servicios/recepción de turnos del destino.
3. Mostrar antes de confirmar si conserva prioridad o pasa al final.
4. Aplicar RN-10, RN-11 o RN-12, guardar historial y recalcular espera.

**Alternativas:** destino no compatible o no recibe turnos: no confirmar; turno llamado/en atención: bloquear el cambio normal y resolver según DP-05, sin quitar la reserva silenciosamente.

**Resultado:** preferencia actualizada y orden correcto. El número de turno no cambia.

## CU-07 — Cambiar disponibilidad

**Actor:** administrador. **Requisito:** RF-15.

1. Seleccionar barbero y consultar sus pendientes/atención.
2. Marcar que acepta o no nuevos turnos; guardar motivo opcional.
3. Si deja de aceptar, bloquear nuevos específicos y excluirlo de la fila flexible.
4. Conservar sus específicos pendientes y atenciones/llamados ya comprometidos.
5. Si se cambian sus pendientes a otros barberos, aplicar CU-06 uno por uno.

**Resultado:** puede terminar la fila y salir. El barbero ve el estado, pero no lo cambia. No se programan horarios automáticos de almuerzo en la primera versión.

## CU-08 — Corregir datos o servicios

**Actor:** administrador. **Requisito:** RF-14. **Precondición propuesta:** pendiente en espera.

1. Localizar turno y corregir nombre o servicios.
2. Validar combinación completa, precio y duración.
3. Conservar prioridad cuando la preferencia no cambia; si exige cambiar barbero, ejecutar CU-06.
4. Guardar versiones anterior/nueva, motivo y totales recalculados.

**Alternativas:** no existe barbero compatible: rechazar; atención finalizada: no reescribir el historial desde este formulario. Una corrección posterior exige un flujo adicional fuera del alcance inicial.

## CU-09 — Configurar catálogo y personal

**Actor:** administrador. **Requisitos:** RF-16/21/24.

1. Crear/actualizar perfiles de barberos y vincular cuentas autorizadas.
2. Crear servicios activos con precio y duración válidos.
3. Asignar capacidades a cada barbero.
4. Autorizar tablet y pantalla pública por separado.
5. Revisar impacto antes de desactivar servicios/capacidades con turnos pendientes.

**Alternativas:** una edición haría imposible un pendiente específico: bloquearla hasta resolver el pendiente o acordar un cambio. Nunca modificar snapshots históricos ni borrar servicios referenciados.

## CU-10 — Mostrar y anunciar llamados

**Actor:** pantalla pública habilitada por personal. **Requisito:** RF-17/18.

1. Abrir pantalla y activar/probar sonido mediante interacción humana.
2. Obtener estado público y cursor de eventos.
3. Recibir nuevos llamados en orden y mostrar número/barbero.
4. Encolar voz para no superponer llamados simultáneos; registrar eventos ya procesados en la sesión.
5. Tras reconectar, recuperar estado y eventos posteriores al cursor; no narrar todo el historial.

**Resultado:** información visible aunque la voz no funcione. La confirmación de un evento en la TV no demuestra que alguien lo escuchó; puede solicitarse repetir el anuncio sin crear otro turno.

## CU-11 — Consultar resumen diario

**Actor:** administrador. **Requisito:** RF-19.

1. Elegir jornada o rango local.
2. Consultar personas atendidas, servicios, barberos y valor de servicios finalizados.
3. Ver pendientes/retirados por separado y comparar con historial.

**Resultado:** cifras reproducibles por barbero real y precios guardados en cada turno. No se reportan utilidades ni pagos.

## CU-12 — Autorizar una excepción de orden

**Actor:** administrador; llamado ejecutado por barbero. **Requisito:** RF-22.

1. Identificar al cliente con prioridad y obtener su acuerdo presencial para esperar.
2. Seleccionar turno beneficiado y barbero compatible, indicar motivo y registrar la constancia del acuerdo.
3. Crear autorización puntual propuesta en DP-04, sin modificar antigüedad base.
4. El siguiente llamado del barbero consume la autorización una sola vez si sigue siendo válida.

**Alternativas:** no hay acuerdo, cambian condiciones o existe atención activa: no adelantar. La excepción no permite atender servicios incompatibles ni incorporar flexibles a un barbero que no recibe turnos.

## CU-13 — Cerrar y abrir jornada

**Actor:** administrador. **Requisito:** RF-23. **Flujo propuesto DP-07.**

1. Bloquear nuevos registros al terminar el horario de recepción.
2. Resolver llamados y atenciones activas. Los barberos retiran pendientes si corresponde o los atienden.
3. Cerrar jornada cuando no quedan turnos activos; conservar reporte.
4. Abrir la siguiente con numeración nueva y perfiles revisados.

No cancelar pendientes automáticamente a medianoche. Si la jornada cruza de día, mantenerla identificada hasta cerrarla y no mezclar sus números con otra jornada abierta.
