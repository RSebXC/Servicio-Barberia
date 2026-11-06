# Integración y puesta en marcha

Procedimiento propuesto para pasar de una aplicación construida a una operación real. No se han ejecutado estas etapas.

## Cómo se integrará físicamente

1. La tablet abre el registro en una URL HTTPS y queda autorizada como dispositivo de recepción.
2. Cada barbero abre su panel web en el celular e inicia sesión con su cuenta. Puede añadirse un acceso directo; eso no implica funcionamiento offline ni notificaciones con la pantalla bloqueada.
3. El administrador entra a su área privada desde un equipo propio.
4. El reproductor conectado a la TV abre la vista pública, se autoriza como pantalla y activa el sonido.
5. Todos consultan el mismo servidor/base central. No hay una base distinta en cada celular.

No hace falta integrar hardware especializado ni instalar una aplicación nativa. No se conecta automáticamente a un sistema de caja existente; si lo hay, sigue siendo independiente en esta versión.

## Etapa 1 — Levantamiento del local

- Completar [necesidades](necesidades-barberia.md), catálogo y matriz de capacidades.
- Probar cobertura Wi-Fi y acceso al servicio desde todas las estaciones.
- Verificar resolución, lectura a distancia, salida HDMI, volumen y voz española.
- Acordar horario, responsable de jornada, permisos de retiro pendientes y contingencia.

**Salida:** ficha del local completa y equipo apto o compras concretas identificadas.

## Etapa 2 — Preparación técnica

- Crear entornos separados y cuenta/proyecto de producción bajo titularidad acordada.
- Elegir región/plan tras revisar latencia y costos; si se adopta Neon Auth, comprobar compatibilidad del proyecto antes de habilitarlo.
- Configurar dominio HTTPS, secretos del servidor y acceso de base de datos.
- Aplicar migraciones probadas en un entorno aislado y verificar restricciones de integridad.
- Configurar identidad del personal, membresías y recuperación de acceso.
- Si se utiliza Managed Better Auth, configurar dominio/correo conforme a su [guía de producción](https://neon.com/docs/auth/production-checklist).
- Configurar respaldo, observabilidad y alertas; ensayar restauración sin sobrescribir producción.

**Salida:** entorno accesible, sin datos ficticios mezclados con operación real y con recuperación verificada.

## Etapa 3 — Configuración del negocio

- Dar de alta servicios, minutos, precios y capacidades reales.
- Crear administrador y cuentas de barberos; probar qué no puede hacer cada uno.
- Autorizar tablet y TV con credenciales limitadas; no compartir contraseña administrativa.
- Abrir jornada de prueba y revisar número de turno, moneda y zona horaria.
- Comprobar que no hay una recepción de turnos abierta por error para barberos ausentes.

**Salida:** configuración revisada por el responsable del negocio.

## Etapa 4 — Prueba integrada y capacitación

Ejecutar con datos identificados como prueba: registro → llamado → TV → inicio → finalización → reporte. Después probar prioridad flexible/específica, cambio de preferencia, ausencia, retiro, cierre de recepción de un barbero y conexión interrumpida.

Realizar solicitudes concurrentes y verificar que un turno no se duplica ni es consumido por dos barberos. Usar [escenarios EA](../02-analisis/escenarios-aceptacion.md), con evidencia de resultado y cualquier pendiente.

Capacitar a cada rol con el [manual](manual-usuario.md). Cada barbero debe practicar la diferencia entre “no responde”, “retirar” y “finalizar”. El administrador debe practicar que no disponible termina la fila específica y deja de recibir flexibles.

**Salida:** escenarios críticos aprobados, personal capaz de completar su recorrido y registro de pendientes aceptables.

## Etapa 5 — Piloto y arranque

1. Programar piloto de bajo riesgo con acompañamiento.
2. Designar una única fila oficial; no mantener una fila digital y otra manual compitiendo.
3. Registrar tiempos reales y ajustar duraciones del catálogo para futuros turnos.
4. Revisar llamados, ausencias, cambios, estabilidad y reporte al final.
5. Resolver fallos críticos antes de usarlo sin acompañamiento.
6. Entregar accesos, procedimientos de respaldo, manual y canal de soporte acordado.

## Contingencia por caída de internet o servicio

1. El administrador comunica el cambio a operación manual y detiene nuevos registros digitales.
2. Usar la última vista disponible solo como referencia desactualizada; confirmar físicamente con barberos los llamados y atenciones activos.
3. Mantener una sola lista en papel con orden, nombre, preferencia, servicios y estado. Usar una serie distinta para registros nuevos, por ejemplo `M-001`, para evitar confusión con números digitales.
4. No seguir pulsando “registrar” ni abrir un segundo sistema independiente. Un timeout puede haber guardado una operación.
5. Al volver la conexión, el administrador recupera primero el estado confirmado; los barberos verifican sus atenciones. Mantener registro digital cerrado mientras se reconcilia.
6. Si todavía no existe herramienta de conciliación, terminar la fila afectada manualmente y reabrir digital cuando no queden pendientes de ese periodo. Conservar el registro de atenciones manuales separado: el reporte digital de ese día será incompleto.
7. No inventar atenciones finalizadas ni reingresar una lista completa para “arreglar” reportes. La carga histórica/conciliación avanzada sería un alcance adicional.

Esta contingencia permite continuar atendiendo, pero **no es operación digital offline**. Si el negocio necesita reportes completos durante caídas, se debe incorporar y cotizar una herramienta de conciliación antes de producción.

## Recuperación y soporte

- Ante fallo de TV, seguir llamados humanos mientras el panel del barbero funciona.
- Ante pérdida de un celular, revocar su sesión; no cambiar la fila desde un equipo sin autorización.
- Ante pérdida/corrupción de datos, detener escrituras y recuperar en entorno aislado con el responsable técnico; reconciliar el periodo afectado antes de volver a abrir.
- Mantener copia de configuración, catálogo y contactos de soporte; no guardar contraseñas en este repositorio.
- Acordar qué incluye garantía, qué es soporte recurrente y qué constituye una funcionalidad nueva.

## Criterios para puesta en producción

- [ ] No existen fallos de prioridad, permisos, duplicación ni pérdida de turnos en escenarios críticos.
- [ ] Sonido/lectura y conectividad funcionan en el equipo del local.
- [ ] Respaldo y restauración ensayados; responsables y costos recurrentes identificados.
- [ ] No quedan propuestas DP que afecten operación sin resolver o limitar explícitamente.
- [ ] Personal capacitado y contingencia practicada.
- [ ] Titularidad, soporte y alcance comercial acordados.
