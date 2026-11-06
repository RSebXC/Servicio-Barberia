# Documentación del sistema de turnos

Versión documental: **1.0 — 6 de noviembre de 2026**. Zona horaria de operación propuesta: `America/Guatemala`.

Este paquete describe el producto por construir. No certifica funciones implementadas, pruebas ejecutadas ni infraestructura instalada. Los manuales describen el comportamiento previsto; sus nombres de botones deberán ajustarse a la interfaz final.

## Cómo leer esta documentación

1. Para entender y presentar el producto: visión, reglas de negocio y flujos.
2. Para desarrollar: requisitos, permisos, casos de uso, arquitectura, datos y contratos.
3. Para preparar la barbería: necesidades, integración y manual de usuario.
4. Para preparar la siguiente etapa: demo, escenarios de aceptación y decisiones pendientes.

| Documento | Contenido |
| --- | --- |
| [Visión y alcance](00-vision-alcance.md) | Problema, solución, límites y métricas |
| [Requisitos funcionales](01-requisitos/funcionales.md) | Capacidades identificadas con RF |
| [Requisitos no funcionales](01-requisitos/no-funcionales.md) | Calidad, continuidad y objetivos verificables |
| [Roles y permisos](01-requisitos/roles-permisos.md) | Qué puede hacer cada actor |
| [Reglas de negocio](01-requisitos/reglas-negocio.md) | Prioridad, disponibilidad, cambios y ausencias |
| [Casos de uso](02-analisis/casos-uso.md) | Actor, condiciones, pasos y excepciones |
| [Escenarios de aceptación](02-analisis/escenarios-aceptacion.md) | Ejemplos para verificar el producto futuro |
| [Flujos](02-analisis/flujos.md) | Diagramas de registro, atención y cambios |
| [Arquitectura](03-tecnico/arquitectura.md) | Componentes, sincronización, concurrencia y despliegue |
| [Tecnologías](03-tecnico/tecnologias.md) | Propuesta técnica, motivos y alternativas |
| [Modelo de datos](03-tecnico/modelo-datos.md) | Entidades, estados, restricciones y reportes |
| [Contratos de API](03-tecnico/contratos-api.md) | Operaciones, permisos, entradas y errores |
| [Necesidades de la barbería](04-operacion/necesidades-barberia.md) | Equipo, conexión, datos y responsables |
| [Integración y puesta en marcha](04-operacion/integracion-puesta-marcha.md) | Configuración, pruebas, capacitación y contingencia |
| [Manual de usuario](04-operacion/manual-usuario.md) | Instrucciones previstas por rol |
| [Demo y entregas](05-planificacion/demo-y-entregas.md) | Alcance comercial, fases y criterios de salida |
| [Decisiones y pendientes](05-planificacion/decisiones-pendientes.md) | Confirmaciones, propuestas y datos por levantar |
| [Fuentes técnicas](fuentes.md) | Documentación oficial consultada |

## Convenciones

- **Confirmado:** acordado por el propietario del proyecto en la conversación.
- **Propuesto:** decisión de diseño o implementación recomendada; no constituye un acuerdo comercial ni una regla aprobada por la barbería.
- **Pendiente:** dato o comportamiento que falta validar; no impide documentar el resto.
- **Futuro:** ampliación fuera de la primera versión.

Los identificadores permiten relacionar reglas `RN`, requisitos `RF/RNF`, casos `CU` y escenarios `EA`. La fuente normativa del orden de la fila es [Reglas de negocio](01-requisitos/reglas-negocio.md); la de permisos es [Roles y permisos](01-requisitos/roles-permisos.md).

## Cambios que sustituyen el contexto original

- “Cualquiera” permanece sin asignación mientras espera; no se asigna al registrarse al barbero con menos personas.
- La prioridad combina antigüedad, preferencia y capacidad de realizar todos los servicios.
- Solo el administrador modifica la disponibilidad.
- Solo el barbero retira turnos de la fila. La última aclaración sustituye el permiso inicial del administrador para cancelar o quitar clientes.
- Un barbero no disponible termina su fila específica; deja de recibir turnos de “cualquiera”.
- No hay citas ni cuentas de clientes. Correos y avisos anticipados quedan para una ampliación.

## Historial

| Versión | Fecha | Cambio |
| --- | --- | --- |
| 1.0 | 2026-11-06 | Documentación inicial basada en contexto y aclaraciones; sin implementación |
