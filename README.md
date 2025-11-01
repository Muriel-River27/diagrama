```mermaid
graph TD
    subgraph "Usuario"
        A["Clic en 'Dibujar Círculo'"] --> B
        L["Clic en 'Limpiar'"] --> M
    end

    subgraph "MainWindow (Controlador)"
        B(on_dibujarButton_clicked) --> C{"Lee Xc, Yc, r de SpinBox"}
        C --> D["Llama a canvasWidget.dibujarCirculo()"]
        
        M(on_limpiarButton_clicked) --> N["Llama a canvasWidget.limpiar()"]
        N --> O["Llama a canvasWidget.resetView()"]
        O --> P["Limpia Modelos de Tablas"]
        P --> Q["Resetea SpinBox a 0"]

        I("slot: actualizarTablaPaso") --> J["Actualiza modeloPasos"]
        K("slot: actualizarTablaOctantes") --> K2["Actualiza modeloOctantes"]
    end

    subgraph "CanvasWidget (Motor de Dibujo)"
        D --> E(dibujarCirculo)
        E --> F(calcularPuntosCirculo)
        F -- "Bucle" --> G(emit nuevoPasoAlgoritmo)
        F -- "Bucle" --> H(emit nuevoPuntoOctantes)
        E --> R["Auto-Zoom y Paneo"]
        R --> S(update)
        
        N --> T(limpiar)
        T --> S
        
        S --> U(paintEvent)
        U --> V["Dibuja Plano Cartesiano Detallado"]
        U --> W["Dibuja Círculo/Relleno"]
    end

    G -.->|"Señal"| I
    H -.->|"Señal"| K
