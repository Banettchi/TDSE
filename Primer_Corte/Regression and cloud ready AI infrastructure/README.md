# Stellar Luminosity – Regresión lineal y polinomial

## Introducción

El propósito de este proyecto es explorar, de manera práctica y fundamental, el ajuste de modelos de regresión aplicados a datos astrofísicos. El objetivo central es predecir la luminosidad de una estrella a partir de su masa y temperatura. Para garantizar una comprensión profunda, se ha evitado el uso de bibliotecas de alto nivel como Scikit-Learn; todo el cálculo matricial y la optimización se realizan exclusivamente con **NumPy**, y la visualización con **Matplotlib**.

El enfoque principal ha sido:
*   Mencionar la claridad expositiva del código.
*   Lograr que los resultados gráficos narren la evolución del modelo durante el entrenamiento.

---

## Contenido de los Notebooks

### 1. 01_part1_linreg_1feature.ipynb (Masa vs Luminosidad)
*   Implementación del modelo lineal `L_hat = w·M + b` y cálculo del error (MSE).
*   Desarrollo de gradientes manuales, tanto en bucles como vectorizados.
*   Optimización mediante descenso de gradiente probando diversas tasas de aprendizaje (`alphas`).
*   Visualización de la superficie de costo y el ajuste final sobre los datos observados.

### 2. 02_part2_polyreg.ipynb (Polinómica + Interacción Masa-Temperatura)
*   Creación de nuevas características: `X = [M, T_scaled, M², M·T_scaled]`, normalizando la temperatura (`T/1000`) para evitar desbordes numéricos.
*   Entrenamiento completamente vectorizado.
*   Evaluación comparativa de tres arquitecturas (M1, M2, M3) y análisis del impacto del término de interacción.
*   Prueba de inferencia con valores no vistos.

---

## Requisitos Técnicos

*   Python 3.x
*   NumPy (Cálculo numérico)
*   Matplotlib (Gráficas)

---

## Ejecución Local (Windows)

1.  Se abrieron los archivos `.ipynb` utilizando un editor compatible con Jupyter (VS Code o JupyterLab).
2.  Se ejecutaron las celdas secuencialmente.
3.  **Nota**: Si la convergencia no era óptima, se ajustó el parámetro `alpha` (reduciéndolo) y se incrementaron las iteraciones.

---

## Ejecución en AWS SageMaker

### Proceso de Carga
Brevemente:
1.  Ingresé a **SageMaker Studio**.
2.  Utilicé la opción de **Upload** para cargar ambos notebooks.
3.  Seleccioné el kernel estándar de Python (con soporte para NumPy y Matplotlib) y ejecuté todo el flujo de trabajo sin errores.

### Galería de Evidencias

#### Parte 1: Regresión Lineal
<!-- [FOTO 1: Vista general del notebook 1 en SageMaker] -->
<!-- [FOTO 2: Gráfica de convergencia renderizada en la nube] -->

#### Parte 2: Regresión Polinomial
<!-- [FOTO 3: Vista general del notebook 2 en SageMaker] -->
<!-- [FOTO 4: Comparación final de modelos] -->

---

## Comparativa: Entorno Local vs Nube

Al correr los mismos scripts en ambos entornos, noté lo siguiente:
*   **Velocidad**: La ejecución local se sintió ligeramente más ágil e inmediata. En SageMaker, el kernel tomaba unos instantes extra en iniciar operaciones pesadas.
*   **Gráficos 3D**: Las visualizaciones interactivas o complejas tardaron un poco más en renderizar en la interfaz web de Studio.
*   **Estabilidad**: Los resultados numéricos (pérdidas finales y pesos optimizados) fueron idénticos, validando la portabilidad del código NumPy.

---

## Conclusiones y Aprendizajes

*   **Evolución del Modelo**: El modelo lineal simple (solo Masa) captura la tendencia general, pero es insuficiente. Al introducir términos cuadráticos y la interacción con la temperatura, el error disminuye drásticamente, modelando mejor la física estelar subyacente.
*   **Estabilidad Numérica**: Fue crucial escalar la temperatura (dividiendo por 1000). Sin esto, los gradientes explotaban.
*   **Validación**: Las gráficas de "Predicho vs Real" mostraron claramente que el modelo más completo (M3) se ajusta mejor a la diagonal ideal.

### Próximos Pasos
Para mejorar este proyecto en el futuro, se podría:
*   Implementar normalización automática (Z-score) para todas las variables.
*   Añadir regularización (L2) manual para controlar los pesos en polinomios de mayor grado.

---

## Información del Autor
*   **Nombre**: [Tu Nombre]
*   **Curso**: Transformación Digital y Arquitectura Empresarial
*   **Fecha**: Enero 2026
