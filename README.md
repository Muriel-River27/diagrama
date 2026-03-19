objectDiagram
    %% Instancia de Usuario (Clase: usuarios) 
    object &quot;usuario: SaraiMuriel&quot; {
        id = &quot;550e8400-e29b-41d4-a716-446655440000&quot; 
        nombre_completo = &quot;Sarai Muriel Rivera&quot; 
        email = &quot;sarai.muriel@unach.mx&quot; 
        activo = true 
    }

    %% Instancia de la Dependencia (Clase: dependencias) 
    object &quot;dependencia: Personal_DPA&quot; {
        id = &quot;dep-123&quot; 
        nombre = &quot;Dirección de Personal Administrativo&quot; 
    }

    %% Instancia de Ubicación Física (Clase: ubicaciones) 
    object &quot;ubicacion: Estante_A1&quot; {
        codigo_unico = &quot;DPA-EST-A1&quot; 
        descripcion = &quot;Archivo de Trámite - Sección A&quot; 
    }

    %% Instancia de Expediente (Clase: expedientes) 
    object &quot;expediente: EXP_2026_001&quot; {
        codigo_unico = &quot;EXP-SMR-2026&quot; 
        nombre = &quot;Expediente de Personal - Sarai Rivera&quot; 
        fecha_apertura = &quot;2026-03-12&quot; 
    }

    %% Instancia de Documento (Clase: documentos) 
    object &quot;documento: Nombramiento_Digital&quot; {
        titulo = &quot;Nombramiento Oficial&quot; 
        fecha_emision = &quot;2026-03-12&quot; 
        estado = &quot;Activo&quot; 
    }

    %% Relaciones de los objetos
    &quot;usuario: SaraiMuriel&quot; -- &quot;dependencia: Personal_DPA&quot; : pertenece a
    &quot;expediente: EXP_2026_001&quot; -- &quot;ubicacion: Estante_A1&quot; : ubicado en 
    &quot;expediente: EXP_2026_001&quot; -- &quot;usuario: SaraiMuriel&quot; : responsable 
    &quot;documento: Nombramiento_Digital&quot; -- &quot;expediente: EXP_2026_001&quot; : contenido en 
