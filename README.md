classDiagram
    %% Representación de objetos del Sistema ARCSYS
    class SaraiMuriel {
        id: "550e8400-e29b-41d4-a716-446655440000"
        nombre: "Sarai Muriel Rivera"
        email: "sarai.muriel@unach.mx"
        activo: true
    }

    class Personal_DPA {
        id: "dep-123"
        nombre: "Dirección de Personal Administrativo"
    }

    class Estante_A1 {
        codigo: "DPA-EST-A1"
        descripcion: "Archivo de Trámite - Sección A"
    }

    class EXP_2026_001 {
        codigo: "EXP-SMR-2026"
        nombre: "Expediente de Personal - Sarai Rivera"
        apertura: "2026-03-12"
    }

    class Nombramiento_Digital {
        titulo: "Nombramiento Oficial"
        emision: "2026-03-12"
        estado: "Activo"
    }

    %% Relaciones funcionales
    SaraiMuriel -- Personal_DPA : pertenece a
    EXP_2026_001 -- Estante_A1 : ubicado en
    EXP_2026_001 -- SaraiMuriel : responsable
    Nombramiento_Digital -- EXP_2026_001 : contenido en
