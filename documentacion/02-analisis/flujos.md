# Flujos de operación

Diagramas Mermaid de comportamiento, sin diseño visual de pantallas. Los pasos técnicos de reserva, oportunidades de llamado y excepción son propuestas de implementación.

## Registro

```mermaid
flowchart TD
    A[Inicio en tablet] --> B[Elegir barbero o Cualquiera]
    B --> C[Seleccionar servicios compatibles]
    C --> D[Escribir nombre y revisar resumen]
    D --> E[Confirmar registro]
    E --> F{Servidor valida jornada, servicios y disponibilidad}
    F -->|No| G[Explicar y actualizar opciones]
    G --> B
    F -->|Sí| H[Crear un turno y prioridad únicos]
    H --> I[Mostrar número y espera aproximada]
    I --> J[Limpiar datos y volver al inicio]
```

## Selección del siguiente

```mermaid
flowchart TD
    A[Barbero solicita siguiente] --> B{Ya tiene llamado o atención}
    B -->|Sí| C[Continuar o resolver turno actual]
    B -->|No| D[Bloquear fila y leer estado vigente]
    D --> E{Acepta turnos}
    E -->|Sí| F[Específicos propios y flexibles compatibles]
    E -->|No| G[Solo específicos propios pendientes]
    F --> H[Excluir reservados, finales y omitidos en esta oportunidad]
    G --> H
    H --> I{Existe candidato}
    I -->|No| J[Informar sin candidato y liberar bloqueo]
    I -->|Sí| K[Elegir por prioridad o excepción válida]
    K --> L[Reservar, guardar llamado y evento]
    L --> M[Confirmar transacción]
    M --> N[Actualizar paneles y anunciar en TV]
```

## Llamado, ausencia y atención

```mermaid
flowchart TD
    A[Turno llamado] --> B{Cliente responde}
    B -->|Sí| C[Barbero inicia atención]
    C --> D[Barbero finaliza atención]
    D --> E[Actualizar reporte y solicitar siguiente]
    B -->|No| F[Barbero marca No responde]
    F --> G[Conservar prioridad y liberar reserva]
    G --> H[Buscar otro en la misma oportunidad]
    G --> I[Ausente vuelve a competir en próxima oportunidad]
    I --> J{Se confirmó que se fue definitivamente}
    J -->|No| I
    J -->|Sí| K[Barbero autorizado retira con motivo]
```

El ciclo del ausente representa espera de una acción humana o liberación de un barbero; no es un proceso que consume turnos automáticamente.

## Cambios de preferencia

```mermaid
flowchart TD
    A[Administrador recibe solicitud] --> B{Turno esperando y destino válido}
    B -->|No| C[No modificar y explicar]
    B -->|Sí| D{Tipo de cambio}
    D -->|Específico a otro específico| E[Nueva prioridad al final]
    D -->|Cualquiera a específico| E
    D -->|Específico a cualquiera| F[Conservar prioridad vigente]
    E --> G[Guardar cambio e historial]
    F --> G
    G --> H[Actualizar carga y estimaciones]
```

## Cerrar recepción de un barbero

```mermaid
flowchart TD
    A[Admin marca No disponible] --> B[Dejar de admitir nuevos específicos]
    B --> C[Excluir al barbero de candidatos flexibles]
    C --> D[Conservar específicos y compromisos activos]
    D --> E{Admin cambia pendientes}
    E -->|Sí| F[Aplicar reglas de cambio a cada turno]
    E -->|No| G[Barbero termina sus específicos]
    F --> H[Sin compromisos pendientes puede retirarse]
    G --> H
```

## Coordinación entre dispositivos

```mermaid
sequenceDiagram
    participant T as Tablet
    participant API as Servidor
    participant DB as Base central
    participant B as Celular barbero
    participant TV as Pantalla
    T->>API: Crear turno con ID de solicitud
    API->>DB: Validar y guardar turno + evento
    DB-->>API: Confirmación
    API-->>T: Comprobante
    B->>API: Solicitar siguiente
    API->>DB: Seleccionar y reservar bajo bloqueo
    DB-->>API: Llamado confirmado
    API-->>B: Turno reservado
    TV->>API: Consultar estado y eventos desde cursor
    API-->>TV: Número, barbero y eventos públicos
    TV->>TV: Mostrar y encolar anuncio
    B->>API: Iniciar y después finalizar
    API->>DB: Persistir cambios e historial
```

El servidor es la autoridad. Ningún celular ni la TV asignan turnos por su cuenta.
