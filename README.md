```mermaid
graph TD
    A[Inicio de la Aplicación] --> B{Esperando acción del usuario};
    
    B -- Clic 'Dibujar Línea' --> C[Leer Puntos (X1,Y1,X2,Y2)];
    C --> D[Calcular Puntos de la Línea (Algoritmo DDA)];
    D --> E[Mostrar Puntos en Tabla 'Lado AB'];
    E --> F[Dibujar Línea en el Gráfico];
    F --> B;
    
    B -- Clic 'Dibujar Triángulo' --> I[Leer Vértices (A,B,C)];
    I --> J[Calcular Lados AB, BC, CA (Algoritmo DDA)];
    J --> K[Mostrar Puntos en Tablas 'Lado AB', 'Lado BC', 'Lado CA'];
    K --> L[Dibujar Lados del Triángulo en el Gráfico];
    L --> B;
    
    B -- Clic 'Rellenar Triángulo' --> N[Ejecutar Algoritmo de Relleno sobre el último triángulo];
    N --> B;
    
    B -- Clic 'Limpiar Todo' --> H[Borrar Gráfico y limpiar todas las Tablas];
    H --> B;
```

