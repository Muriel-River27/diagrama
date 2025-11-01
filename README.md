```mermaid
graph TD
    A("Inicio de la Aplicación") --> B["Inicializar UI: MainWindow y CanvasWidget"]
    B --> C{"Esperar Interacción del Usuario"}

    C -- "Clic en 'Dibujar Círculo'" --> D(on_dibujarButton_clicked)
    D --> E{"Leer Xc, Yc, r, Relleno"}
    E --> F{"¿Radio > 0?"}
    F -- No --> C
    F -- "Sí" --> G["Limpiar lienzo y tablas"]
    G --> H["Calcular Puntos (Algoritmo)"]
    H --> I["Mostrar Pasos en Tabla (N, Pk...)"]
    I --> J["Mostrar 8 Puntos en Tabla"]
    J --> K["Aplicar Auto-Zoom y Centrado"]
    K --> L["Llamar a update() para redibujar"]
    L --> M(paintEvent)
    M --> N{"¿Requiere Rellenar?"}
    N -- "Sí" --> O["Dibujar Relleno"]
    N -- "No" --> P["Dibujar Borde"]
    O --> C
    P --> C

    C -- "Clic en 'Limpiar'" --> Q(on_limpiarButton_clicked)
    Q --> R["Limpiar lienzo (limpiar() y resetView())"]
    R --> S["Limpiar modelos de Tablas"]
    S --> T["Resetear SpinBox y CheckBox"]
    T --> U["Llamar a update() para redibujar"]
    U --> V(paintEvent)
    V --> W["Dibuja Plano Cartesiano Vacío"]
    W --> C
    
    C -- "Clic en 'Cerrar' (X)" --> Z(Fin)
