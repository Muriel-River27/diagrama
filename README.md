objectDiagram
    %% Instancia de Usuario (Clase: usuarios)
    object &quot;usuario: SaraiMuriel&quot; {
        id = &quot;550e8400-e29b-41d4-a716-446655440000&quot; [cite: 3]
        nombre_completo = &quot;Sarai Muriel Rivera&quot; [cite: 43]
        email = &quot;sarai.muriel@unach.mx&quot; [cite: 42]
        activo = true [cite: 47]
    }

    %% Instancia de la Dependencia (Clase: dependencias)
    object &quot;dependencia: Personal_DPA&quot; {
        id = &quot;dep-123&quot; [cite: 16]
        nombre = &quot;Dirección de Personal Administrativo&quot; [cite: 19]
    }

    %% Instancia de Ubicación Física (Clase: ubicaciones)
    object &quot;ubicacion: Estante_A1&quot; {
        codigo_unico = &quot;DPA-EST-A1&quot; [cite: 62]
        descripcion = &quot;Archivo de Trámite - Sección A&quot; [cite: 65]
    }

    %% Instancia de Expediente (Clase: expedientes)
    object &quot;expediente: EXP_2026_001&quot; {
        codigo_unico = &quot;EXP-SMR-2026&quot; [cite: 133]
        nombre = &quot;Expediente de Personal - Sarai Rivera&quot; [cite: 133]
        fecha_apertura = &quot;2026-03-12&quot; [cite: 133, 40]
    }

    %% Instancia de Documento (Clase: documentos)
    object &quot;documento: Nombramiento_Digital&quot; {
        titulo = &quot;Nombramiento Oficial&quot; [cite: 130]
        fecha_emision = &quot;2026-03-12&quot; [cite: 130]
        estado = &quot;Activo&quot; [cite: 130]
    }

    %% Relaciones basadas en la arquitectura del sistema
    &quot;usuario: SaraiMuriel&quot; -- &quot;dependencia: Personal_DPA&quot; : pertenece a [cite: 68]
    &quot;expediente: EXP_2026_001&quot; -- &quot;ubicacion: Estante_A1&quot; : ubicado en [cite: 119]
    &quot;expediente: EXP_2026_001&quot; -- &quot;usuario: SaraiMuriel&quot; : responsable [cite: 133]
    &quot;documento: Nombramiento_Digital&quot; -- &quot;expediente: EXP_2026_001&quot; : contenido en [cite: 130]
