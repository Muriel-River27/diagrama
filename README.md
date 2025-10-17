```mermaid
graph TD
    subgraph "1. Initialization"
        direction LR
        A(Program Start) --> B("MainWindow::MainWindow()")
        B --> C("setupUI(): Create widgets & connect signals")
        C --> D("loadStyles(): Load stylesheets")
        D --> E{Wait for User Interaction}
    end

    subgraph "2. User Interaction (Slots)"
        direction TB
        
        %% Flow 1: Calculate Line
        E --> F_Click("Click 'Calculate Line'")
        F_Click --> F1(on_calculate_line)
        F1 --> F2("Read/Validate P1, P2 from QLineEdits")
        F2 -- Valid --> F3("Calculate & Display Slope")
        F2 -- Invalid --> Err(Show Error)
        F3 --> DDA1("Call dda_algorithm(P1, P2)")
        DDA1 --> F4("populateTable(table_ab, Steps)")
        F4 --> F5("canvas->setLinePoints(Points)")
        F5 --> Render(Trigger Render)

        %% Flow 2: Draw Triangle Outline
        E --> G_Click("Click 'Draw Outline'")
        G_Click --> G1(on_draw_triangle)
        G1 --> G2("Read/Validate Vertices A, B, C")
        G2 -- Valid --> G3("updateSlopeInfoLabel(A, B, C)")
        G2 -- Invalid --> Err
        G3 --> DDA2("Call DDA(A, B)")
        DDA2 --> G4("populateTable(table_ab)")
        G4 --> DDA3("Call DDA(B, C)")
        DDA3 --> G5("populateTable(table_bc)")
        G5 --> DDA4("Call DDA(C, A)")
        DDA4 --> G6("populateTable(table_ca)")
        G6 --> G7("Accumulate Points AB, BC, CA")
        G7 --> G8("canvas->setTriangleOutline(Points)")
        G8 --> Render

        %% Flow 3: Fill Triangle
        E --> H_Click("Click 'Fill'")
        H_Click --> H1(on_fill_triangle)
        H1 --> H2("Read/Validate Vertices A, B, C")
        H2 -- Valid --> H3("Call on_draw_triangle()")
        H2 -- Invalid --> Err
        H3 --> H4("Call DDA(A, B) -> EdgePointsAB")
        H4 --> H5{Loop: For each 'p' in EdgePointsAB}
        H5 -- Iterate --> H6("Call DDA(C, p)")
        H6 --> H7("Accumulate Fill Points")
        H7 --> H5
        H5 -- Loop End --> H8("canvas->setTriangleFill(FillPoints)")
        H8 --> Render

        %% Flow 4: Clear All
        E --> I_Click("Click 'Clear All'")
        I_Click --> I1(on_clear)
        I1 --> I2("Clear QLineEdits & QTableWidgets")
        I2 --> I3("canvas->clear()")
        I3 --> Render

        %% End of flows
        Err --> E
    end

    subgraph "3. Core Components"
        direction TB
        
        %% DDA Algorithm (Logic)
        DDA(dda_algorithm)
        style DDA fill:#D5F5E3,stroke:#2ECC71,stroke-width:2px
        DDA1 --> DDA
        DDA2 --> DDA
        DDA3 --> DDA
        DDA4 --> DDA
        H4 --> DDA
        H6 --> DDA

        %% Rendering (View)
        Paint("DrawingCanvas::paintEvent")
        style Paint fill:#D6EAF8,stroke:#3498DB,stroke-width:2px
        Render --> Paint
        Paint --> E
    end
