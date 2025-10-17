graph TD
    A([Inicio]) --> B[Usuario hace clic en "Dibujar Triangulo"];
    B --> C[Se ejecuta el slot on_draw_triangle];
    C --> D[Llamar a funcion auxiliar readTriangleVertices];
    
    subgraph Validacion_de_Entradas
        D --> E{Campos de vertices llenos y validos};
        E -- No --> F[Mostrar mensaje de error];
        F --> G((Fin del proceso));
        E -- Si --> H[Convertir texto a coordenadas QPointF];
    end

    H --> I[Llamar a canvas_setTriangleVertices para guardar coordenadas];
    I --> J[Llamar a updateSlopeInfoLabel para mostrar pendientes];

    subgraph Dibujo_de_Lados_DDA
        J --> K[Limpiar las tablas de datos];
        K --> L[Ejecutar dda_algorithm para lado AB];
        L --> M[Ejecutar dda_algorithm para lado BC];
        M --> N[Ejecutar dda_algorithm para lado CA];
        N --> O[Guardar puntos del contorno del triangulo];
    end

    subgraph Relleno_del_Triangulo
        O --> P[Calcular limites horizontales del triangulo];
        P --> Q[Ejecutar algoritmo de relleno por filas (scanline)];
        Q --> R[Almacenar puntos de relleno en canvas];
    end

    subgraph Actualizacion_Visual
        R --> S[Llamar a canvas_setTriangleOutline con contorno];
        S --> T[Qt llama a paintEvent del lienzo];
        T --> U[/El lienzo se redibuja mostrando triangulo relleno/];
    end

    U --> V([Fin])
