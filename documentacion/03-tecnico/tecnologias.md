# Tecnologías y decisiones de implementación

**Propuesta revisada documentalmente el 6 de noviembre de 2026.** No hay paquetes instalados ni versiones seleccionadas. Al implementar, fijar versiones compatibles en el archivo de dependencias y su lockfile; no mezclar ejemplos de versiones distintas.

## Stack recomendado para evaluar

| Capa | Propuesta | Motivo del proyecto | Condición |
| --- | --- | --- | --- |
| Aplicación | Next.js + TypeScript | Compartir proyecto y tipos entre cuatro vistas y servidor | Verificar build, rutas y despliegue con versión elegida |
| Interfaz | React y CSS del proyecto | Tablet táctil, panel móvil y TV con la misma base | Estilo y biblioteca de componentes se decidirán al diseñar la demo |
| API | Route Handlers de Next.js | Concentrar validación y permisos en servidor | Endpoints de turnos dinámicos, sin caché de estado obsoleto |
| Datos | PostgreSQL administrado, candidato Neon | Relaciones claras, persistencia y control concurrente | Validar región, respaldo, límites y costo |
| Acceso a datos | Prisma | Esquema/migraciones y acceso tipado | Revisar API de la versión; SQL cuando se requieran restricciones específicas |
| Identidad del personal | Neon Managed Better Auth, si se adopta Neon | Evitar construir contraseñas y recuperación desde cero | Probar integración, configuración de correo y membresías internas |
| Actualización de vistas | Consultas cada 3 s con versión/cursor | Menos componentes iniciales y eventos recuperables | Medir latencia, consultas y costo antes de producción |
| Anuncio | SpeechSynthesis del navegador y señal de aviso | Anunciar número y barbero desde el reproductor de TV | Probar voz española, sonido y equipo real |
| Verificación | Pruebas de negocio/integración y recorridos de navegador | Comprobar prioridad, permisos y concurrencia | Herramienta concreta se selecciona al implementar |
| Hosting | Candidato Vercel; alternativa servidor Node.js | Despliegue de una sola aplicación | Revisar plan apto para operación comercial y costo total |

Next.js ofrece [manejadores de solicitudes HTTP](https://nextjs.org/docs/app/getting-started/route-handlers) y [opciones de despliegue](https://nextjs.org/docs/app/getting-started/deploying). Esas capacidades respaldan la propuesta; no constituyen una comparación de rendimiento frente a otros frameworks.

[Prisma documenta transacciones](https://www.prisma.io/docs/orm/fundamentals/transactions). Se comprobará su versión concreta antes de implementar el bloqueo del motor y la migración de índices; este documento no copia una API histórica como si fuera vigente.

La opción de [identidad administrada de Neon](https://neon.com/docs/auth/overview) es una propuesta para el personal. No crea cuentas para clientes ni concede el rol de barbero a cualquier persona que se registre. Antes de producción hay que completar la configuración de dominio y correo prevista por el [checklist del proveedor](https://neon.com/docs/auth/production-checklist).

## Alternativas razonables

| Alternativa | Cuándo considerarla | Qué cambia |
| --- | --- | --- |
| Otro hosting Node.js | Mejor costo, latencia o experiencia de mantenimiento | Despliegue y operación; no la fila |
| Otro PostgreSQL administrado | Respaldo/región/precio más conveniente | Conexión, identidad elegida y procedimientos |
| SSE o suscripciones | Actualización por consultas no cumple objetivo o sale costosa | Transporte y gestión de conexiones/eventos |
| Servidor local | La barbería no tiene internet confiable y acepta mantener equipo local | Autenticación, respaldo, soporte y acceso remoto; requiere rediseño de despliegue |

No se recomienda añadir Redis, microservicios, aplicaciones nativas ni un sistema de mensajería para cinco estaciones sin una necesidad medida. La voz no requiere un servicio de IA en la propuesta inicial. La disponibilidad de voces se comprueba según [MDN](https://developer.mozilla.org/en-US/docs/Web/API/SpeechSynthesis).

## Costos a separar en una propuesta comercial

1. Desarrollo, configuración, instalación y capacitación.
2. Hosting de aplicación, base de datos, respaldo y dominio.
3. Correo transaccional del acceso del personal, si lo requiere la configuración final; es distinto de avisos al cliente.
4. Equipo físico, red, reproductor de TV y audio.
5. Soporte, actualizaciones, restauraciones y cambios de alcance.

No se incluyen cifras de suscripción porque no se han elegido planes ni revisado cotizaciones para esta instalación. Verificar precios, condiciones comerciales y renovación cuando se prepare la propuesta; no prometer operación gratuita indefinida.

## Riesgos técnicos concretos

- Consulta frecuente: puede generar mucho tráfico aunque la fila sea pequeña; medir y ajustar transporte.
- Televisor inteligente: su navegador y voces pueden ser insuficientes; validar reproductor externo antes de comprar.
- Estimación de espera: ausencias, regreso de clientes y correcciones la alteran; informar siempre que es aproximada.
- Dependencia de internet: requiere contingencia manual o inversión en un alcance offline distinto.
- Identidad administrada: verificar condiciones y región admitida antes de provisionar; usar el SDK y guía vigentes del proveedor.

Todas las elecciones de stack siguen siendo **propuestas**, registradas en DP-09. Las fuentes adicionales están en [fuentes técnicas](../fuentes.md).
