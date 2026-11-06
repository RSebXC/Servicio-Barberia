# Visión y alcance

## Problema

La barbería necesita registrar llegadas, respetar preferencias de barbero y coordinar la atención desde recepción, celulares y una pantalla pública. La fila debe seguir siendo comprensible cuando un cliente acepta a cualquiera, no responde al llamado o cambia de preferencia.

## Producto previsto

Una aplicación web con cuatro áreas: registro en tablet, panel del barbero, administración y pantalla de llamados. Todos los dispositivos comparten una fila central; cada uno ve únicamente la información y acciones correspondientes a su función.

El cliente registra su nombre, preferencia y uno o varios servicios. Obtiene un número de turno y una estimación de espera. No crea cuenta ni puede modificar su registro. Cada familiar se registra por separado. El personal puede registrar a alguien que llama por teléfono, respetando el mismo orden de ingreso.

## Contexto confirmado

- Una barbería; se contemplan cinco barberos, sin fijar ese número en el software.
- El administrador configura servicios, precios, duraciones y capacidades de cada barbero.
- Se entiende que tres de los cinco realizan todos los servicios; la matriz real debe entregarla la barbería.
- Atención por orden de registro y compatibilidad; no se agenda una hora.
- Llamados visibles y audibles con número de turno y barbero.
- Solo el administrador cambia disponibilidad, preferencias y datos del registro.
- Solo el barbero retira clientes de la fila.

## Primera versión operativa propuesta

Incluye registro, validación de servicios, gestión de fila, lista pública de espera en recepción, llamados, inicio/fin de atención, ausencias, retiro, cambios por administrador, disponibilidad, pantalla pública, historial y reportes diarios básicos. Incluye autenticación del personal y protección de los dispositivos públicos.

Los reportes mostrarán atenciones por día/barbero/servicio y valor de servicios finalizados. **Ese valor no demuestra cobro ni ganancia.** Caja, gastos y comisiones requieren otro alcance.

## Fuera del alcance inicial

- Citas, reservas por horario y pagos anticipados.
- Pagos, facturación, caja, cálculo de utilidad, inventario y nómina.
- Correo de turno, recordatorios, SMS, WhatsApp y llamadas telefónicas automáticas.
- Aplicaciones nativas separadas para Android/iOS.
- Varias sucursales, fidelización y perfiles de clientes.
- Operación digital sin internet con sincronización posterior.
- Impresora de tickets, integración con un POS existente y reproducción de publicidad.

## Demo y operación

La demo futura usará datos ficticios y demostrará recorridos completos. Un prototipo local no demuestra sincronización entre equipos; si se presenta ese comportamiento, deberá usar un servidor compartido o identificarse expresamente como simulación.

La versión operativa necesita además persistencia, permisos reales, pruebas de concurrencia, respaldo, capacitación y validación del equipo de la barbería. Ver [entregas](05-planificacion/demo-y-entregas.md).

## Indicadores de éxito propuestos

| Indicador | Cómo observarlo |
| --- | --- |
| Respeto de prioridad | Ejecutar escenarios EA de antigüedad, cambios y ausencias |
| Coordinación | Un llamado aparece en TV y paneles dentro del objetivo RNF-02 |
| Facilidad de registro | Un cliente nuevo completa el flujo sin crear cuenta |
| Integridad | Un turno nunca está en atención con dos barberos |
| Visibilidad del dueño | Reporte coincide con las atenciones finalizadas de la jornada |

No hay presupuesto, plazo ni precio comercial aprobados. Se estimarán después de validar alcance y condiciones de instalación.
