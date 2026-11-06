# Requisitos funcionales

**C:** confirmado por conversación. **P:** especificación propuesta para completar la operación. **F:** futuro, excluido de la primera versión.

| ID | Requisito y resultado observable | Base | Regla |
| --- | --- | --- | --- |
| RF-01 | Mostrar tarjetas de barberos con nombre y opción “Cualquiera”; distinguir quién no recibe turnos | C | RN-08/09 |
| RF-02 | Crear un turno por persona con nombre, preferencia y al menos un servicio | C | RN-01/02 |
| RF-03 | Filtrar servicios por barbero o validar la combinación completa para “cualquiera”; rechazar combinaciones imposibles | C | RN-07 |
| RF-04 | Registrar precio y duración de cada servicio elegido y calcular totales en el servidor | P | RN-02 |
| RF-05 | Entregar número de turno, nombre, servicios, preferencia y espera aproximada; no prometer un barbero a los flexibles | C/P | RN-05/18 |
| RF-06 | Permitir registro asistido por teléfono usando el mismo orden de confirmación | C/P | RN-03 |
| RF-07 | Mostrar al administrador fila completa, preferencias, estado, antigüedad y carga por barbero | C | RN-04/06 |
| RF-08 | Mostrar al barbero sus específicos, candidatos flexibles compatibles y disponibilidad, distinguiendo ambos grupos | C/P | RN-05/08 |
| RF-09 | Seleccionar y reservar el siguiente turno mediante las reglas centrales; no permitir elegir otro arbitrariamente | C | RN-06/17 |
| RF-10 | Permitir al barbero confirmar inicio y fin; impedir dos atenciones simultáneas propias | C/P | RN-15 |
| RF-11 | Permitir marcar “no responde” y llamar a otro, manteniendo prioridad y reintentos sin límite | C | RN-14 |
| RF-12 | Permitir retiro por barbero con motivo e historial; denegar retiro al administrador | C/P | RN-16 |
| RF-13 | Cambiar preferencias solo desde administración, aplicando las tres reglas de prioridad | C | RN-10/12/13 |
| RF-14 | Corregir nombre/servicios pendientes solo desde administración, revalidando compatibilidad | C/P | RN-13 |
| RF-15 | Cambiar disponibilidad solo por administrador; al cerrar recepción conservar fila específica y excluir flexibles | C | RN-08/09 |
| RF-16 | Administrar catálogo, precios, duraciones, perfiles y capacidades sin alterar importes de turnos históricos | C/P | RN-02 |
| RF-17 | Mostrar en TV los llamados por número y barbero y anunciarlos en español | C | RN-06 |
| RF-18 | Sincronizar vistas, indicar pérdida de conexión y recuperar estado sin inventar confirmaciones | P | RN-18 |
| RF-19 | Consultar atenciones finalizadas por jornada, barbero y servicio, con valor de servicios realizados | C/P | RN-02 |
| RF-20 | Registrar actor, momento, motivo y cambios de las operaciones importantes | P | RN-13/16/17 |
| RF-21 | Autenticar personal y aplicar la matriz de permisos en servidor | P | RN-08/13/16 |
| RF-22 | Autorizar excepción puntual de orden por administrador, registrando acuerdo; el barbero ejecuta el llamado | C/P | RN-17 |
| RF-23 | Gestionar jornada y numeración diaria sin duplicados y sin trasladar turnos pendientes silenciosamente | P | RN-03 |
| RF-24 | Autorizar y revocar dispositivos de registro y pantalla sin exponer cuentas administrativas | P | RN-13 |
| RF-25 | Enviar correo de turno y avisos anticipados | F | Fuera de alcance |
| RF-26 | Mostrar una lista pública de espera en recepción con números y preferencias, sin contactos ni nombres completos; indicar que el orden de llamado depende de compatibilidad | C/P | RN-04/06 |

## Validaciones del registro propuestas

- Nombre visible obligatorio, de 2 a 80 caracteres tras quitar espacios laterales; admitir tildes y nombres repetidos.
- Uno o varios IDs de servicios activos, sin duplicados; no aceptar precios o minutos definidos por el cliente.
- Preferencia `ANY` sin barbero específico, o `SPECIFIC` con un barbero que acepte turnos y pueda realizar todo.
- Para `ANY`, al menos un barbero compatible que acepte turnos en el momento de confirmar. Si todos cerraron recepción, no crear un turno nuevo imposible de canalizar.
- Revalidar al confirmar: que la tablet haya mostrado un servicio disponible no garantiza que siga disponible.
- Identificador de solicitud para que un doble toque o un reintento no genere dos turnos.
- No exigir correo ni teléfono en la primera versión. El correo del personal para acceso es un dato distinto.

## Reportes

Contar personas por turnos `FINALIZADO`; contar servicios por sus líneas, sin confundir ambos valores. Mostrar barbero que realmente atendió, no el originalmente elegido. Retirados y pendientes no suman valor de servicios realizados. Los precios históricos se conservan aunque cambie el catálogo.

Moneda propuesta: GTQ. No llamar “ganancias”, “ventas cobradas” ni “cierre de caja” a este reporte. Exportación CSV es una mejora propuesta posterior a validar el reporte en pantalla.
