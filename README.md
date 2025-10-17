# 🧭 Diagrama de Flujo — Ciclo de Vida de la Aplicación Qt

Este diagrama muestra las tres fases principales del ciclo de vida de una aplicación Qt:
1. **Fase de Arranque (main.cpp)**  
2. **Fase de Construcción (mainwindow.cpp)**  
3. **Fase de Ejecución (main.cpp)**  

---

```mermaid
graph TD
    subgraph "Fase de Arranque (main.cpp)"
        A(Inicio de la Aplicacion) --> B[Crear objeto QApplication];
        B --> C[Crear objeto MainWindow];
    end

    subgraph "Fase de Construccion (mainwindow.cpp)"
        C --> D{Constructor de MainWindow};
        D --> E[Llamar a setupUI];
        E --> F[Crear widgets: botones, campos de texto, tablas, etc];
        F --> G[Organizar widgets en la ventana con Layouts];
        G --> H[Conectar señales de botones a sus slots correspondientes];
        D --> I[Llamar a loadStyles];
        I --> J[Aplicar hoja de estilos QSS];
    end
    
    subgraph "Fase de Ejecucion (main.cpp)"
        J --> K[Mostrar ventana con w.show];
        K --> L[Iniciar bucle de eventos con a.exec];
        L --> M((Esperando interaccion del usuario));
    end
