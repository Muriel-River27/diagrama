# Diagrama de flujo — Ciclo de vida de la aplicación Qt

```mermaid
graph TD
    subgraph "Fase de Arranque (main.cpp)"
        A(Inicio de la Aplicación) --> B[Crear objeto QApplication];
        B --> C[Crear objeto MainWindow];
    end

    subgraph "Fase de Construcción (mainwindow.cpp)"
        C --> D{Constructor de MainWindow};
        D --> E[1. Llamar a setupUI()];
        E --> F[Crear todos los widgets: botones, campos de texto, tablas, etc.];
        F --> G[Organizar widgets en la ventana usando Layouts];
        G --> H[Conectar señales de los botones (ej. 'clicked') a los slots (ej. 'on_draw_triangle')];
        D --> I[2. Llamar a loadStyles()];
        I --> J[Aplicar la hoja de estilos QSS a la interfaz];
    end
    
    subgraph "Fase de Ejecución (main.cpp)"
        J --> K[Mostrar la ventana con w.show()];
        K --> L[Iniciar el bucle de eventos con a.exec()];
        L --> M((Esperando Interacción del Usuario));
    end
