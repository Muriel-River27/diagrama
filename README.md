```mermaid
objectDiagram
    %% Instancia de Usuario (Clase: usuarios)
    object "usuario: SaraiMuriel" {
        id = "550e8400-e29b-41d4-a716-446655440000"
        nombre_completo = "Sarai Muriel Rivera"
        email = "sarai.muriel@unach.mx"
        activo = true
    }

    %% Instancia de la Dependencia (Clase: dependencias)
    object "dependencia: Personal_DPA" {
        id = "dep-123"
        nombre = "Dirección de Personal Administrativo"
    }

    %% Instancia de Ubicación Física (Clase: ubicaciones)
    object "ubicacion: Estante_A1" {
        codigo_unico = "DPA-EST-A1"
        descripcion = "Archivo de Trámite - Sección A"
    }

    %% Instancia de Expediente (Clase: expedientes)
    object "expediente: EXP_2026_001" {
        codigo_unico = "EXP-SMR-2026"
        nombre = "Expediente de Personal - Sarai Rivera"
        fecha_apertura = "2026-03-12"
    }

    %% Instancia de Documento (Clase: documentos)
    object "documento: Nombramiento_Digital" {
        titulo = "Nombramiento Oficial"
        fecha_emision = "2026-03-12"
        estado = "Activo"
    }

    %% Relaciones de los objetos
    "usuario: SaraiMuriel" -- "dependencia: Personal_DPA" : pertenece a
    "expediente: EXP_2026_001" -- "ubicacion: Estante_A1" : ubicado en
    "expediente: EXP_2026_001" -- "usuario: SaraiMuriel" : responsable
    "documento: Nombramiento_Digital" -- "expediente: EXP_2026_001" : contenido en
