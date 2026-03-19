``` mermaid
classDiagram
    %% OBJETOS DE SEGURIDAD Y ACCESO
    class `adminRole:cat_roles` {
        id = "550e8400-e29b-41d4-a716-446655440000"
        nombre = "Administrador de Archivo"
        descripcion = "Acceso total al acervo documental"
    }

    class `permisoEscritura:cat_permisos` {
        id = "721e8400-e29b-41d4-a716-446655440001"
        nombre = "ESCRITURA_EXP"
        descripcion = "Permite crear y editar expedientes"
    }

    class `user01:usuarios` {
        id = "a1b2c3d4-e5f6-7g8h-i9j0-k1l2m3n4o5p6"
        e_mail = "juan.perez@unach.mx"
        nombre_completo = "Juan Pérez López"
        dep_unid = "Dirección de Personal"
        activo = true
        ultimo_acceso = "2026-03-18 09:00:00"
    }

    %% INFRAESTRUCTURA FÍSICA
    class `edificioA:cat_tipos_nivel` {
        id = "f47ac10b-58cc-4372-a567-0e02b2c3d479"
        nombre = "Edificio"
        nivel = 1
        puede_tener_hijos = true
    }

    class `estante01:ubicaciones` {
        id = "b1c2d3e4-f5g6-7h8i-9j0k-l1m2n3o4p5q6"
        codigo_unico = "EST-01-SEC-A"
        nombre = "Estante Principal"
        descripcion = "Ubicado en el ala norte del archivo central"
        activo = true
    }

    %% ESTRUCTURA DOCUMENTAL
    class `depRRHH:dependencias` {
        id = "d1e2f3g4-h5i6-7j8k-9l0m-n1o2p3q4r5s6"
        nombre = "Recursos Humanos"
        descripcion = "Departamento de Personal Administrativo"
    }

    class `tipoContrato:cat_tipos_documento` {
        id = "e1f2g3h4-i5j6-k7l8-m9n0-o1p2q3r4s5t6"
        nombre = "Contrato Individual"
        descripcion = "Documentos de contratación laboral"
        es_critico = true
    }

    %% EXPEDIENTES Y DOCUMENTOS
    class `expPerez:expedientes` {
        id = "990e8400-e29b-41d4-a716-446655440002"
        codigo_unico = "EXP-2026-JP-001"
        nombre = "Expediente Personal - Juan Pérez"
        fecha_apertura = "2026-01-15"
    }

    class `metaPerez:expedientes_personal` {
        id = "880e8400-e29b-41d4-a716-446655440003"
        nombre_completo = "Juan Pérez López"
        curp = "PERJ850101HCS"
        tipo_contratacion = "Base"
        fecha_alta = "2026-01-15"
    }

    class `docContrato:documentos` {
        id = "770e8400-e29b-41d4-a716-446655440004"
        numero_oficio = "UNACH-RH-2026-045"
        titulo = "Contrato de Prestación de Servicios"
        fecha_emision = "2026-01-10"
        estado = "VIGENTE"
    }

    %% ARCHIVOS Y VERSIONES
    class `filePDF:archivos_adjuntos` {
        id = "660e8400-e29b-41d4-a716-446655440005"
        nombre_archivo = "contrato_jp_firmado.pdf"
        ruta_archivo = "/nas/docs/2026/01/contrato_jp.pdf"
        mime_type = "application/pdf"
        tamano = 2048576
    }

    class `v1:versiones_documento` {
        id = "550e8400-e29b-41d4-a716-446655440006"
        version_no = 1
        motivo_cambio = "Carga inicial de documento escaneado"
    }

    %% FLUJO Y SEGUIMIENTO
    class `mov01:movimientos` {
        id = "440e8400-e29b-41d4-a716-446655440007"
        fecha_salida = "2026-03-18 10:00:00"
        fecha_estimada_retorno = "2026-03-25"
        motivo = "Auditoría Interna"
    }

    class `log01:logs_auditoria` {
        id = "330e8400-e29b-41d4-a716-446655440008"
        operacion = "CONSULTA"
        fecha_hora = "2026-03-18 11:20:00"
        direccion_ip = "10.0.1.55"
    }

    class `alert01:alertas_generadas` {
        id = "220e8400-e29b-41d4-a716-446655440009"
        tipo_alerta = "VENCIMIENTO"
        mensaje = "El contrato EXP-2026-JP-001 vence en 30 días"
        leida = false
    }

    %% RELACIONES (ASOCIACIONES)
    `adminRole:cat_roles` --> `permisoEscritura:cat_permisos` : posee
    `user01:usuarios` --> `adminRole:cat_roles` : asignado_a
    `estante01:ubicaciones` --> `edificioA:cat_tipos_nivel` : nivel_pertenencia
    `expPerez:expedientes` --> `estante01:ubicaciones` : guardado_en
    `expPerez:expedientes` --> `depRRHH:dependencias` : pertenece_a
    `expPerez:expedientes` --> `metaPerez:expedientes_personal` : metadatos_empleado
    `docContrato:documentos` --> `expPerez:expedientes` : contenido_en
    `docContrato:documentos` --> `tipoContrato:cat_tipos_documento` : es_un
    `filePDF:archivos_adjuntos` --> `docContrato:documentos` : adjunto_a
    `v1:versiones_documento` --> `docContrato:documentos` : version_de
    `v1:versiones_documento` --> `filePDF:archivos_adjuntos` : referencia_a
    `mov01:movimientos` --> `expPerez:expedientes` : afecta_a
    `mov01:movimientos` --> `user01:usuarios` : responsable_entrega
    `log01:logs_auditoria` --> `user01:usuarios` : ejecutado_por
    `alert01:alertas_generadas` --> `user01:usuarios` : notificar_a
