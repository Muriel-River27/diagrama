graph TD
    A[Usuario hace clic en "Dibujar Contorno"] --> B[Se ejecuta el slot on_draw_triangle];
    B --> C[Llamar a la funcion auxiliar readTriangleVertices];
    
    subgraph Validacion_de_Entradas_readTriangleVertices
        C --> D{Campos de vertices llenos y validos};
        D -- No --> E[Mostrar mensaje de error al usuario];
        E --> F[Fin del proceso];
        D -- Si --> G[Convertir texto a coordenadas numericas QPointF];
    end

    G --> H[Llamar a canvas_setTriangleVertices para guardar coordenadas];
    H --> I[Llamar a updateSlopeInfoLabel para calcular y mostrar pendientes];

    subgraph Procesamiento_de_Lados_del_Triangulo
        I --> J[Limpiar las 3 tablas de datos];
        
        J --> K[Bucle Lado 1 AB: llamar a dda_algorithm A B; llenar tabla Lado AB; guardar puntos del contorno];
        
        K --> L[Bucle Lado 2 BC: llamar a dda_algorithm B C; llenar tabla Lado BC; guardar puntos del contorno];

        L --> M[Bucle Lado 3 CA: llamar a dda_algorithm C A; llenar tabla Lado CA; guardar puntos del contorno];
    end

    subgraph Actualizacion_Visual
        M --> N[Llamar a canvas_setTriangleOutline con todos los puntos del contorno];
        N --> O[Qt llama automaticamente a la funcion paintEvent del lienzo];
        O --> P[El lienzo se redibuja mostrando el triangulo];
    end
