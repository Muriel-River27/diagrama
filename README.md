objectDiagram
    %% Instancia de Usuario (Clase: usuarios)
    object "usuario: SaraiMuriel" {
        id = "550e8400-e29b-41d4-a716-446655440000" [cite: 3]
        nombre_completo = "Sarai Muriel Rivera" [cite: 43]
        email = "sarai.muriel@unach.mx" [cite: 42]
        activo = true [cite: 47]
    }

    %% Instancia de la Dependencia (Clase: dependencias)
    object "dependencia: Personal_DPA" {
        id = "dep-123" [cite: 16]
        nombre = "Dirección de Personal Administrativo" [cite: 19]
    }

    %% Instancia de Ubicación Física (Clase: ubicaciones)
    object "ubicacion: Estante_A1" {
        codigo_unico = "DPA-EST-A1" [cite: 62]
        descripcion = "Archivo de Trámite - Sección A" [cite: 65]
    }

    %% Instancia de Expediente (Clase: expedientes)
    object "expediente: EXP_2026_001" {
        codigo_unico = "EXP-SMR-2026" [cite: 133]
        nombre = "Expediente de Personal - Sarai Rivera" [cite: 133]
        fecha_apertura = "2026-03-12" [cite: 40, 133]
    }

    %% Instancia de Documento (Clase: documentos)
    object "documento: Nombramiento_Digital" {
        titulo = "Nombramiento Oficial" [cite: 130]
        fecha_emision = "2026-03-12" [cite: 130]
        estado = "Activo" [cite: 130]
    }

    %% Relaciones de los objetos
    "usuario: SaraiMuriel" -- "dependencia: Personal_DPA" : pertenece a
    "expediente: EXP_2026_001" -- "ubicacion: Estante_A1" : ubicado en
    "expediente: EXP_2026_001" -- "usuario: SaraiMuriel" : responsable
    "documento: Nombramiento_Digital" -- "expediente: EXP_2026_001" : contenido en
