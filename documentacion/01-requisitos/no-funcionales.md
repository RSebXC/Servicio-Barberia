# Requisitos no funcionales

Todos los valores numéricos de este documento son **objetivos propuestos para validar**, no mediciones ni garantías contratadas.

| ID | Objetivo | Verificación futura |
| --- | --- | --- |
| RNF-01 | Una persona por turno y una atención/llamado activos por barbero; nunca asignación doble | Prueba concurrente y restricciones de base de datos |
| RNF-02 | Reflejar un cambio confirmado en otras pantallas en ≤5 s con red estable | Medir desde confirmación del servidor hasta render en tres dispositivos |
| RNF-03 | Operaciones comunes con respuesta p95 ≤2 s en una prueba de 30 min con 10 dispositivos, 500 turnos por jornada y 100 mutaciones | Medir API, sin incluir audio; documentar red, región y arranque en frío |
| RNF-04 | Registro legible en tablet y acciones de barbero utilizables desde celular | Probar 360 px de ancho móvil, tablet de 10 pulgadas y TV 1080p real |
| RNF-05 | Controles táctiles principales ≥44 px, foco visible, etiquetas y estados no basados solo en color | Revisión manual con teclado y tacto |
| RNF-06 | HTTPS y autorización por rol en cada lectura sensible y escritura | Intentos negativos por actor y acceso cruzado entre barberos |
| RNF-07 | TV sin contactos ni datos internos; tablet vuelve al inicio y elimina datos del cliente anterior | Inspeccionar respuestas públicas y reset tras registro/inactividad |
| RNF-08 | Reintentos idempotentes: doble toque no duplica turno, llamado ni finalización | Reenviar la misma solicitud antes/después de un corte de conexión |
| RNF-09 | Tras reconectar, recuperar estado y cursor de eventos; no volver a anunciar un evento ya recibido dentro de la misma sesión | Cortar red, generar eventos y reconectar |
| RNF-10 | No confirmar escrituras sin respuesta del servidor; indicar “sin conexión” y deshabilitar acciones operativas | Simular caída de internet y del backend |
| RNF-11 | Guardar instantes en UTC y presentar jornada en `America/Guatemala`; dinero decimal exacto | Pruebas de cambio de día y sumas monetarias |
| RNF-12 | Auditoría para cambios de prioridad, servicios, disponibilidad, retiros y excepciones | Revisar eventos de un recorrido completo |
| RNF-13 | Separar demo/desarrollo/producción y mantener secretos fuera del navegador y del repositorio | Revisión de configuración y respuestas de API |
| RNF-14 | Objetivo inicial de respaldo diario externo o equivalente verificado; RPO ≤24 h y recuperación RTO ≤4 h | Restauración ensayada en entorno aislado; validar plan contratado |
| RNF-15 | Llamados visuales siguen funcionando si no hay voz; el fallo de audio es visible al operador | Desactivar voz y repetir llamado |
| RNF-16 | Mensajes claros sin trazas técnicas ni contraseñas; registros técnicos con identificador de correlación y sin contactos | Revisar fallos esperados |
| RNF-17 | El motor de fila es independiente de componentes visuales y reutilizable por todas las vistas | Revisión de estructura y escenarios automatizados de negocio |

## Límites y continuidad

La arquitectura propuesta depende de internet. Instalar un acceso directo o permitir caché visual no equivale a operar sin conexión. Sin red no se registran ni llaman turnos digitalmente; se utiliza la contingencia manual descrita en [integración](../04-operacion/integracion-puesta-marcha.md).

El objetivo de actualización de cinco segundos se refiere a vistas activas. Un celular bloqueado o con navegador suspendido puede necesitar recargar; las notificaciones push fuera de la aplicación no se incluyen.

Retención propuesta: 90 días para nombres operativos y 12 meses para auditoría e historial minimizado. Debe acordarse antes de producción (DP-08); no es una exigencia legal afirmada por este documento. Los agregados estadísticos pueden conservarse sin datos identificables si la barbería lo aprueba.
