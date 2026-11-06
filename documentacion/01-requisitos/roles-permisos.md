# Roles y permisos

## Actores

| Actor | Acceso previsto | Responsabilidad |
| --- | --- | --- |
| Cliente | Tablet de registro, sin cuenta | Registrar su propio turno |
| Administrador | Cuenta individual | Configurar y supervisar la operación |
| Barbero | Cuenta individual vinculada a su perfil | Gestionar sus llamados y atenciones |
| Pantalla pública | Dispositivo autorizado de lectura | Mostrar y anunciar llamados |
| Personal que registra por teléfono | Registro asistido por administrador, propuesta | Crear un turno sin adelantarlo |

No se agrega un rol independiente de recepcionista en esta versión. Si se necesita que alguien registre por teléfono sin acceso administrativo, se deberá definir ese permiso antes de producción.

## Matriz normativa

**C:** confirmado. **P:** restricción o capacidad técnica propuesta.

| Acción | Cliente | Administrador | Barbero | Pantalla | Base |
| --- | --- | --- | --- | --- | --- |
| Crear turno por persona | Sí | Sí, asistido | No | No | C/P: acceso asistido propuesto |
| Ver comprobante de su registro | Sí, temporal | Sí | Según su operación | No | P |
| Ver fila operativa completa | No | Sí | Solo vista operativa necesaria | No | P |
| Ver lista pública de espera con números/preferencias | Sí, en recepción | Sí | Sí | Opcional | C/P |
| Ver fila específica propia y candidatos compatibles | No | Sí | Sí | No | C |
| Configurar servicios, precios y duraciones | No | Sí | No | No | C |
| Asignar servicios a barberos | No | Sí | No | No | C |
| Marcar barbero disponible/no disponible | No | Sí | No | No | C |
| Consultar disponibilidad propia | No | Sí | Sí | No | C |
| Cambiar preferencia o barbero de un turno | No | Sí | No | No | C |
| Corregir nombre o servicios pendientes | No | Sí | No | No | C |
| Autorizar excepción de orden con acuerdo presencial | No | Sí | No | No | C |
| Llamar siguiente/iniciar/finalizar | No | No | Sí, en su propia estación | No | C/P: alcance propio propuesto |
| Marcar ausencia y pasar al siguiente | No | No | Sí, sobre su llamado | No | C |
| Retirar/cancelar un turno pendiente | No | **No** | **Sí** | No | C |
| Leer reportes monetarios e historial completo | No | Sí | No | No | P |
| Mostrar número y barbero de llamados | No | Sí | Sí | Sí, lectura | C |
| Gestionar cuentas del personal y dispositivos | No | Sí | No | No | P |

## Alcance propuesto para retirar turnos

El usuario confirmó que solo el barbero puede retirar; no definió si puede hacerlo sobre cualquier fila. Para evitar interferencias, se propone:

1. Puede retirar un turno específico de su fila.
2. Puede retirar un turno de “cualquiera” que él ya haya llamado y marcado ausente, siempre que no esté reservado o atendido por otro.
3. No puede retirar un turno específico de otro barbero ni un turno flexible sobre el que nunca haya intervenido.
4. El retiro pide motivo y confirmación, conserva historial y no borra físicamente el registro.

Este límite es **propuesto** y está registrado como DP-01. Hasta validarlo no se ampliarán permisos por conveniencia. El administrador tampoco obtiene permiso de retiro por ser administrador.

## Identidad y dispositivos

- El rol se valida en el servidor para cada operación, no solo ocultando botones.
- Cada barbero usa su cuenta; no se acepta un `barber_id` del navegador como prueba de identidad.
- Registrar un usuario de autenticación no le da acceso al personal: necesita una membresía activa autorizada por el administrador.
- Tablet y TV usan autorizaciones de dispositivo separadas de la cuenta administrativa.
- La tablet solo puede consultar catálogo, proyección pública de espera y crear turnos; no descargar listados de nombres, contactos ni reportes.
- La TV recibe número, barbero y estado público. No recibe teléfono, correo ni datos internos.
- No se heredan permisos entre roles. Si una persona es administrador y barbero, los permisos adicionales requieren una vinculación explícita y auditable.
