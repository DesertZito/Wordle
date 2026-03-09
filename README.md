sequenceDiagram
    participant C as Cliente/Test
    participant S as ServicioPrestamo (Aplicación)
    participant RU as RepoUsuarios (Infraestructura)
    participant RE as RepoEjemplares (Infraestructura)
    participant U as Usuario (Dominio)
    participant E as Ejemplar (Dominio)
    participant P as Prestamo (Dominio)

    C->>S: prestar(usuario_id, ejemplar_id)
    S->>RU: obtener_por_id(usuario_id)
    RU-->>S: objeto Usuario
    S->>RE: obtener_por_id(ejemplar_id)
    RE-->>S: objeto Ejemplar
    
    S->>U: solicitar_prestamo(ejemplar)
    Note over U,E: Lógica de Negocio (Dominio)
    U->>E: prestar()
    E-->>U: estado actualizado
    U->>P: <<create>> Prestamo(ejemplar, usuario)
    U-->>S: objeto Prestamo
    S-->>C: Confirmación Prestamo
