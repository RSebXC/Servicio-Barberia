# Contratos de API propuestos

Especificación de análisis, no endpoints implementados ni un contrato OpenAPI validado. Prefijo orientativo `/api/v1`. Fechas ISO 8601 UTC, IDs opacos y precios decimales enviados como cadenas; interfaz en español.

## Convenciones

- Toda mutación exige ID de solicitud (`Idempotency-Key`) y autenticación de personal/dispositivo según operación.
- Mutaciones sobre registros existentes incluyen `expectedVersion`; conflicto si cambió desde que se leyó.
- La respuesta contiene `requestId`, versión y estado confirmado. Un timeout no prueba que no se haya guardado: reintentar con el mismo ID y contenido.
- Servidor deduce barbería, rol y barbero de la autorización, no de campos arbitrarios del navegador.
- Estado operativo y eventos: respuesta sin caché compartida y con `Cache-Control: no-store`.
- TV y tablet usan respuestas específicas, no el objeto interno completo con campos ocultos por CSS.

## Operaciones

| Método y ruta | Actor | Entrada principal | Resultado |
| --- | --- | --- | --- |
| `GET /registration/catalog` | Tablet autorizada / admin | Ninguna | Barberos visibles, recepción de turnos, servicios/capacidades |
| `GET /registration/waiting-list` | Tablet autorizada / admin | Jornada | Números, preferencias y estado de espera; sin nombres/contactos |
| `POST /tickets` | Tablet / admin asistido | Nombre, preferencia, servicios, clave de solicitud | Comprobante de un turno nuevo |
| `GET /requests/{requestKey}` | Mismo actor/dispositivo que la creó | Clave | Resultado propio confirmado, sin listado público |
| `GET /admin/queue` | Admin | Jornada | Fila completa y versiones |
| `GET /barber/queue` | Barbero | Jornada | Específicos propios y flexibles compatibles etiquetados |
| `POST /barber/call-next` | Barbero | Clave de solicitud | Reserva del siguiente o sin candidato |
| `POST /tickets/{id}/no-response` | Barbero del llamado | Versión | Devuelve a espera y busca otro en la oportunidad |
| `POST /tickets/{id}/start` | Barbero del llamado | Versión | Atención iniciada |
| `POST /tickets/{id}/finish` | Barbero de la atención | Versión | Atención finalizada una sola vez |
| `POST /tickets/{id}/withdraw` | Barbero autorizado | Versión, motivo | Turno retirado; admin denegado |
| `POST /tickets/{id}/repeat-announcement` | Barbero responsable | Versión | Evento de anuncio nuevo; no otro llamado/reserva |
| `PATCH /tickets/{id}/preference` | Admin | Preferencia, destino, versión, motivo | Prioridad conservada o renovada según RN |
| `PATCH /tickets/{id}/details` | Admin | Nombre/servicios, versión, motivo | Datos corregidos y compatibilidad validada |
| `PATCH /barbers/{id}/availability` | Admin | `acceptsNewTickets`, versión | Estado de recepción actualizado |
| `GET/POST/PATCH /admin/services` | Admin | Filtros o valores de catálogo | Servicios actuales; usar ID en edición |
| `GET/POST/PATCH /admin/barbers` | Admin | Perfil, capacidades, versión | Perfiles/capacidades; usar ID en edición |
| `POST /admin/priority-exceptions` | Admin | Turno, barbero, afectado, motivo, constancia de acuerdo | Autorización puntual propuesta |
| `GET /display/state` | TV autorizada | Jornada | Llamados/atenciones públicos y cursor |
| `GET /display/events?after={cursor}` | TV autorizada | Cursor, límite | Eventos sanitizados posteriores |
| `GET /admin/reports/daily` | Admin | Jornada | Personas, servicios y valor realizado |
| `POST /admin/business-days/open` | Admin | Fecha operativa | Jornada única abierta |
| `POST /admin/business-days/{id}/stop-registration` | Admin | Versión | Cerrar recepción general sin cancelar pendientes |
| `POST /admin/business-days/{id}/close` | Admin | Versión | Jornada cerrada si no quedan compromisos |
| `POST /admin/device-pairings` | Admin | Tipo de dispositivo | Código temporal de alta |
| `POST /devices/pair` | Dispositivo con código válido | Código de un solo uso | Autorización limitada del dispositivo |
| `POST /admin/devices/{id}/revoke` | Admin | Motivo | Autorización revocada |

La gestión de cuentas se integra con el proveedor de identidad elegido y crea/activa membresías en servidor; no se publica un endpoint que permita al cliente asignarse un rol. La API exacta de identidad se documentará con la versión del SDK en la implementación.

## Ejemplo de registro

```json
{
  "customerName": "Ana",
  "preference": "ANY",
  "preferredBarberId": null,
  "serviceIds": ["svc_corte", "svc_barba"]
}
```

Respuesta orientativa:

```json
{
  "requestId": "req_ejemplo",
  "ticketId": "turno_ejemplo",
  "businessDay": "2026-11-06",
  "number": "A-023",
  "state": "ESPERANDO",
  "preference": "ANY",
  "assignedBarberId": null,
  "serviceValue": "65.00",
  "currency": "GTQ",
  "estimatedWaitMinutes": 25,
  "estimateIsApproximate": true,
  "version": 1
}
```

Los valores son ficticios. Si no se puede estimar, `estimatedWaitMinutes` es `null` junto a una razón legible; no sustituirlo por cero. Nunca aceptar precio/prioridad/estado de atención del cuerpo de creación.

## Errores y conflictos

| HTTP / código | Caso | Acción de interfaz |
| --- | --- | --- |
| `400 INVALID_INPUT` | Nombre/forma de petición inválidos | Señalar campos |
| `401 SESSION_REQUIRED` | Falta sesión o autorización de dispositivo | Pedir acceso o alta del dispositivo |
| `403 FORBIDDEN` | Rol equivocado, retiro por admin o acceso cruzado | Explicar que no tiene permiso |
| `404 NOT_FOUND` | Turno inexistente o fuera del ámbito autorizado | No revelar datos externos |
| `409 STALE_VERSION` | Cambio concurrente | Recargar y revisar antes de repetir |
| `409 BARBER_NOT_ACCEPTING` | Destino dejó de recibir turnos | Actualizar selección |
| `409 STATE_CONFLICT` | Tiene atención activa, jornada cerrada o turno ya reservado | Mostrar estado vigente |
| `409 IDEMPOTENCY_MISMATCH` | Misma clave con contenido distinto | No procesar; iniciar acción nueva si corresponde |
| `422 NO_COMPATIBLE_BARBER` | Nadie habilitado para toda la combinación | Corregir servicios/preferencia |
| `429 RATE_LIMITED` | Demasiadas solicitudes | Esperar según indicación, sin duplicar confirmación |
| `503 SERVICE_UNAVAILABLE` | Persistencia temporalmente inaccesible | Mantener desconexión; verificar resultado antes de crear otro |

Sin candidato puede devolverse `200` con `ticket: null`, sin tratar una fila vacía como fallo de servidor. Todas las mutaciones importantes guardan auditoría y eventos en la misma transacción que el cambio, conforme a [arquitectura](arquitectura.md).
