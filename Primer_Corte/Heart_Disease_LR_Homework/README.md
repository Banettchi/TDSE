# Predicción de Riesgo de Enfermedad Cardíaca: Tarea de Regresión Logística

## Descripción del Proyecto
Este proyecto implementa un modelo de **Regresión Logística** desde cero para predecir la presencia de enfermedades cardíacas en pacientes. El objetivo principal es comprender los fundamentos matemáticos detrás del algoritmo (Función Sigmoide, Función de Costo de Entropía Cruzada Binaria, Descenso de Gradiente) sin depender de librerías de alto nivel como Scikit-Learn para el entrenamiento del núcleo.

## Contexto
Las enfermedades cardíacas son la principal causa de muerte a nivel mundial. Los modelos predictivos permiten identificar pacientes en riesgo mediante el análisis de características clínicas como edad, colesterol y presión arterial, optimizando así la asignación de recursos médicos y mejorando los resultados del tratamiento.

## Dataset
Se utiliza el **Heart Disease Dataset** del repositorio UCI (disponible en Kaggle).
- **Registros**: 303 pacientes.
- **Características**: 13 (incluyendo Edad, Sexo, Colesterol, Presión Arterial, etc.).
- **Objetivo**: Presencia (1) o Ausencia (0) de enfermedad cardíaca.

## Requisitos
- Python 3.8+
- NumPy
- Pandas
- Matplotlib
- Jupyter Notebook

## Estructura del Proyecto
- `data/`: Contiene el archivo del dataset (`Heart_Disease_Prediction.csv`).
- `heart_disease_lr_analysis.ipynb`: Notebook principal con todo el análisis y código.

## Pasos del Proyecto
1.  **Carga y Preparación de Datos**: EDA, limpieza y normalización.
2.  **Implementación de Regresión Logística**: Codificación manual de `sigmoid`, `cost` y `gradient_descent`.
3.  **Visualización de Fronteras**: Gráficos de decisión en 2D.
4.  **Regularización**: Implementación de regularización L2 para evitar sobreajuste.
5.  **Despliegue (Simulado)**: Exploración de despliegue en Amazon SageMaker.

## Cómo Ejecutar
1.  Clonar el repositorio.
2.  Instalar dependencias: `pip install numpy pandas matplotlib jupyter`.
3.  Abrir el notebook: `jupyter notebook heart_disease_lr_analysis.ipynb`.
4.  Ejecutar las celdas secuencialmente.