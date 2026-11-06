# Registro de decisiones y pendientes

Versión 1.0, 2026-11-06. Este documento diferencia acuerdos de propuestas. No requiere detener la documentación ni contratar servicios; los pendientes se resuelven antes de implementar la función afectada o salir a producción, según corresponda.

## Decisiones confirmadas por el propietario del proyecto

| ID | Decisión | Efecto |
| --- | --- | --- |
| DC-01 | Un turno por persona, varios servicios y sin cuenta de cliente | No hay registros familiares agrupados ni edición pública |
| DC-02 | Solo por orden de registro, incluso inscripción por teléfono | No hay reservas por hora |
| DC-03 | Específicos más flexibles, respetando antigüedad entre compatibles | No asignar flexibles al registrarse |
| DC-04 | Solo administrador marca disponibilidad | Barbero consulta, no modifica |
| DC-05 | No disponible termina específicos pendientes y excluye flexibles | No es una cancelación ni un cierre forzado de atención |
| DC-06 | Específico → otro específico y cualquiera → específico van al final | Renovar prioridad vigente |
| DC-07 | Específico → cualquiera conserva antigüedad | No enviar al final por salir de una fila específica |
| DC-08 | Ausente conserva prioridad, reintentos sin límite y sin interrumpir atención | No hay retiro por contador |
| DC-09 | Solo barbero retira turnos | Sustituye la regla inicial que lo permitía al administrador |
| DC-10 | Administrador corrige registros y cambia barbero/preferencia | Revalidar servicios y orden |
| DC-11 | Servicios ofrecidos según capacidades; combinación completa compatible | No dividir automáticamente una visita entre barberos |
| DC-12 | Excepción presencial acordada y gestionada por administrador | No adelantar automáticamente para optimizar tiempos |

## Propuestas adoptadas como base documental, aún por validar

| ID | Tema | Propuesta actual | Cuándo resolver |
| --- | --- | --- | --- |
| DP-01 | Alcance del retiro por barbero | Solo específicos propios y flexibles que ya llamó, sin invadir reserva/atención de otro | Antes de implementar retiro |
| DP-02 | Ausencias y repetición de llamados | Guardar intentos; omitir ausente en la misma oportunidad, volver a competir en otra; repetición de anuncio separada de nueva reserva | Antes de implementar motor de llamados |
| DP-03 | Servicios, paquetes y correcciones | Sumar minutos/precios; paquetes como servicio propio; conservar prioridad al corregir servicios si no cambia preferencia; editar solo pendientes en espera | Antes de implementar catálogo y corrección |
| DP-04 | Excepción de orden | Autorización de un solo uso con turno/barbero/afectado/motivo/acuerdo; no alterar antigüedad base ni evitar compatibilidad | Antes de implementar excepciones |
| DP-05 | Corrección de un turno ya llamado | Bloquear edición normal; definir liberación coordinada con el barbero antes de corregir, sin simular ausencia ni invadir una atención | Antes de habilitar ese flujo; si no se define, limitar edición a espera |
| DP-06 | Llamado flexible confirmado antes de no disponible | Conservar compromiso ya confirmado; flexibles sin llamado siguen esperando otro | Antes de implementar disponibilidad concurrente |
| DP-07 | Jornada, número y cierre | Jornada explícita, serie A-001 diaria; cerrar recepción y resolver activos antes del cierre; sin cancelación nocturna automática | Antes de operación real |
| DP-08 | Datos, presentación pública y retención | TV con número/barbero; lista pública de espera sin nombres/contactos; 90 días datos operativos y 12 meses de historia minimizada, por acordar | Antes de usar datos reales |
| DP-09 | Stack, identidad y hosting | Next.js/TypeScript, PostgreSQL/Neon, Prisma, Managed Better Auth y consultas cada 3 s; medir costo/latencia | Antes de instalar dependencias o provisionar |
| DP-10 | Condiciones reales del local | Confirmar nombres, matriz, precios/minutos, moneda GTQ, equipo, red, responsables y objetivos RNF | Antes de cotizar instalación y lanzar piloto |

Los periodos de retención son propuestas operativas, no un dictamen legal. La seguridad de cuenta del personal y la autorización de dispositivo son necesarias para no exponer funciones administrativas; el proveedor exacto sigue propuesto.

## Ambigüedades resueltas para esta versión documental

- La frase final “solo el barbero” se aplica al retiro de turnos, por ser la pregunta que estaba respondiendo. No transfiere al barbero permisos para corregir registros ni cambiar disponibilidad.
- “Se sumará a su fila” al existir un único compatible significa que solo podrá atenderlo ese barbero; no cambia un flexible a específico automáticamente. Si el único compatible cierra recepción, el flexible espera según RN-09.
- Conservar antigüedad después de un cambio a cualquiera significa conservar la **vigente**, no recuperar la anterior a un cambio que ya lo mandó al final.
- “No disponible” no es “libre/ocupado”. La primera variable controla recepción; la segunda deriva de llamados y atenciones.
- Valor de servicios realizados no equivale a dinero cobrado. El módulo de caja no se incorpora de forma implícita.

## Registro de riesgos

| Riesgo | Consecuencia | Respuesta prevista |
| --- | --- | --- |
| Subestimar competencia entre flexibles y específicos | Adelantos o espera mal calculada | Motor único y EA-05/07/10/12 |
| Doble solicitud o dos llamados simultáneos | Duplicación/reserva doble | Transacciones, bloqueo e idempotencia |
| Retirar con un rol incorrecto | Violación de acuerdo operativo | Matriz de permisos y pruebas negativas |
| Ausentes indefinidos | Espera incierta y llamados repetidos | Intervención humana y estimación informativa; sin borrado automático |
| Flexible queda sin compatibles que acepten | Espera sin estimación | Mostrar condición al administrador; resolver preferencia sin asignarlo silenciosamente |
| TV o voz incompatibles | No se escucha el llamado | Validación de equipo y respaldo presencial |
| Internet inestable | Operación digital interrumpida | Contingencia de una sola fila manual |
| Operación manual durante caída | Reporte digital incompleto | Mantener registro separado; no inventar conciliación automática |
| Consultas frecuentes y planes insuficientes | Costo o lentitud inesperados | Medir tráfico/latencia y revisar transporte/planes |
| Confundir demo con producto final | Compromisos comerciales incompletos | Entregas y aceptación separadas |

## Cómo mantener la documentación

Al validar un DP, registrar fecha y decisión, modificar la regla normativa, actualizar permisos/casos/API/manual afectados y ajustar escenarios EA. No corregir solo la interfaz dejando otra regla en el servidor. Mantener versiones documentales junto al código cuando empiece la implementación.
