---

```mermaid
graph TB

%% ========================
%% 1. INICIALIZACION
%% ========================
subgraph "1. Inicializacion"
    direction TB
    A([Inicio del Programa]) --> B[MainWindow::MainWindow];
    B --> C[setupUI: crear widgets y conectar senales];
    C --> D[loadStyles: aplicar estilos CSS];
    D --> E{Esperar interaccion del usuario};
end
style A fill:#ABEBC6,stroke:#1E8449,stroke-width:2px

%% ========================
%% 2. FLUJOS DE INTERACCION
%% ========================
subgraph "2. Flujos de Interaccion (Slots)"
    direction TB

    %% ---- Flujo 1: Calcular Linea ----
    E --> F[Click Calcular Linea];
    F --> F1[on_calculate_line];
    F1 --> F2[Leer y validar P1,P2];
    F2 -- Valido --> F3[Calcular y mostrar pendiente];
    F2 -- Invalido --> Err[Mostrar mensaje de error];
    F3 --> DDA1[Llamar dda_algorithm P1,P2];
    DDA1 --> F4[populateTable AB];
    F4 --> F5[canvas_setLinePoints];
    F5 --> Render[Disparar renderizado];

    %% ---- Flujo 2: Dibujar Contorno ----
    E --> G[Click Dibujar Contorno];
    G --> G1[on_draw_triangle];
    G1 --> G2[Leer y validar vertices A,B,C];
    G2 -- Valido --> G3[updateSlopeInfoLabel];
    G2 -- Invalido --> Err;
    G3 --> DDA2[DDA A,B];
    DDA2 --> G4[populateTable AB];
    G4 --> DDA3[DDA B,C];
    DDA3 --> G5[populateTable BC];
    G5 --> DDA4[DDA C,A];
    DDA4 --> G6[populateTable CA];
    G6 --> G7[Acumular puntos AB,BC,CA];
    G7 --> G8[canvas_setTriangleOutline];
    G8 --> Render;

    %% ---- Flujo 3: Rellenar Triangulo ----
    E --> H[Click Rellenar];
    H --> H1[on_fill_triangle];
    H1 --> H2[Leer y validar vertices A,B,C];
    H2 -- Valido --> H3[Llamar on_draw_triangle];
    H2 -- Invalido --> Err;
    H3 --> H4[DDA A,B -> puntos AB];
    H4 --> H5{Iterar puntos AB};
    H5 -- Iterar --> H6[DDA C,p -> rellenar];
    H6 --> H7[Acumular puntos de relleno];
    H7 --> H5;
    H5 -- Fin --> H8[canvas_setTriangleFill];
    H8 --> Render;

    %% ---- Flujo 4: Limpiar Todo ----
    E --> I[Click Limpiar Todo];
    I --> I1[on_clear];
    I1 --> I2[Limpiar campos y tablas];
    I2 --> I3[canvas_clear];
    I3 --> Render;

    %% ---- Fin ----
    Err --> E;
end
style F,G,H,I fill:#FDEBD0,stroke:#B9770E,stroke-width:1px

%% ========================
%% 3. COMPONENTES REUTILIZABLES
%% ========================
subgraph "3. Componentes Reutilizables"
    direction TB
    DDA[dda_algorithm];
    style DDA fill:#D5F5E3,stroke:#27AE60,stroke-width:2px

    Paint[DrawingCanvas::paintEvent];
    style Paint fill:#D6EAF8,stroke:#2980B9,stroke-width:2px

    DDA1 --> DDA;
    DDA2 --> DDA;
    DDA3 --> DDA;
    DDA4 --> DDA;
    H4 --> DDA;
    H6 --> DDA;

    Render --> Paint;
    Paint --> E;
end

