---

```mermaid
graph TD
    subgraph "1. Inicialización"
        direction LR
        A(Inicio del Programa) --> B(MainWindow::MainWindow())
        B --> C(setupUI(): Crear widgets y conectar señales)
        C --> D(loadStyles(): Cargar estilos CSS)
        D --> E{Esperar Interacción del Usuario}
    end

    subgraph "2. Flujos de Interacción (Slots de MainWindow)"
        direction TB
        
        %% Flujo 1: Calcular Línea
        E --> F(Click 'Calcular Línea')
        F --> F1(on_calculate_line)
        F1 --> F2(Leer/Validar P1, P2 de QLineEdits)
        F2 -- Válido --> F3(Calcular y mostrar pendiente)
        F2 -- Inválido --> Err(Mostrar Error)
        F3 --> DDA1(Llamar dda_algorithm(P1, P2))
        DDA1 --> F4(populateTable(table_ab, Pasos))
        F4 --> F5(canvas->setLinePoints(Puntos))
        F5 --> Render(Disparar Renderizado)

        %% Flujo 2: Dibujar Contorno
        E --> G(Click 'Dibujar Contorno')
        G --> G1(on_draw_triangle)
        G1 --> G2(Leer/Validar A, B, C)
        G2 -- Válido --> G3(updateSlopeInfoLabel(A, B, C))
        G2 -- Inválido --> Err
        G3 --> DDA2(Llamar DDA(A, B))
        DDA2 --> G4(populateTable(table_ab))
        G4 --> DDA3(Llamar DDA(B, C))
        DDA3 --> G5(populateTable(table_bc))
        G5 --> DDA4(Llamar DDA(C, A))
        DDA4 --> G6(populateTable(table_ca))
        G6 --> G7(Acumular Puntos AB, BC, CA)
        G7 --> G8(canvas->setTriangleOutline(Puntos))
        G8 --> Render

        %% Flujo 3: Rellenar Triángulo
        E --> H(Click 'Rellenar')
        H --> H1(on_fill_triangle)
        H1 --> H2(Leer/Validar A, B, C)
        H2 -- Válido --> H3(Llamar on_draw_triangle())
        H2 -- Inválido --> Err
        H3 --> H4(Llamar DDA(A, B) -> PuntosLadoAB)
        H4 --> H5{Bucle: Para cada 'p' en PuntosLadoAB}
        H5 -- Iterar --> H6(Llamar DDA(C, p))
        H6 --> H7(Acumular Puntos de Relleno)
        H7 --> H5
        H5 -- Fin Bucle --> H8(canvas->setTriangleFill(PuntosRelleno))
        H8 --> Render

        %% Flujo 4: Limpiar
        E --> I(Click 'Limpiar Todo')
        I --> I1(on_clear)
        I1 --> I2(Limpiar QLineEdits y QTableWidgets)
        I2 --> I3(canvas->clear())
        I3 --> Render

        %% Fin de flujos
        Err --> E
    end

    subgraph "3. Componentes Reutilizables"
        direction TB
        
        %% Algoritmo DDA (Lógica)
        DDA(dda_algorithm)
        style DDA fill:#D5F5E3,stroke:#2ECC71,stroke-width:2px
        DDA1 --> DDA
        DDA2 --> DDA
        DDA3 --> DDA
        DDA4 --> DDA
        H4 --> DDA
        H6 --> DDA

        %% Renderizado (Visual)
        Paint(DrawingCanvas::paintEvent)
        style Paint fill:#D6EAF8,stroke:#3498DB,stroke-width:2px
        Render --> Paint
        Paint --> E
    end
