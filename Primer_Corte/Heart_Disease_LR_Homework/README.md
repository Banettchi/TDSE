# Predicción de Riesgo de Enfermedad Cardíaca: Tarea de Regresión Logística

## Descripción del Proyecto
Este proyecto implementa un modelo de **Regresión Logística** desde cero para predecir la presencia de enfermedades cardíacas en pacientes. El objetivo principal es comprender los fundamentos matemáticos detrás del algoritmo (Función Sigmoide, Función de Costo de Entropía Cruzada Binaria, Descenso de Gradiente) sin depender de librerías de alto nivel como Scikit-Learn para el entrenamiento del núcleo.

## Contexto
Las enfermedades cardíacas son la principal causa de muerte a nivel mundial (~18 millones/año según la OMS). Los modelos predictivos permiten identificar pacientes en riesgo mediante el análisis de características clínicas, optimizando así la asignación de recursos médicos y mejorando los resultados del tratamiento.

---

## Dataset
Se utiliza el **Heart Disease Dataset** del repositorio UCI (disponible en [Kaggle](https://www.kaggle.com/datasets/neurocipher/heartdisease)).

| Propiedad | Valor |
|-----------|-------|
| Registros | 303 pacientes |
| Características | Age (29-77), Cholesterol (112-564 mg/dL), BP, Max HR, ST depression, Number of vessels fluro |
| Tasa de enfermedad | ~55% presencia |
| Objetivo | Presencia (1) o Ausencia (0) de enfermedad cardíaca |

---

## Implementación

### Paso 1: Preparación de Datos
- Carga y binarización del objetivo (`Presence`→1, `Absence`→0)
- EDA: estadísticas descriptivas, distribución de clases
- Normalización Min-Max
- Split estratificado 70/30

### Paso 2: Regresión Logística Básica
Funciones implementadas desde cero:
```python
sigmoid(z)           # Función sigmoide
compute_cost(X,y,w,b) # Binary Cross-Entropy
compute_gradient(X,y,w,b) # Gradientes
gradient_descent(...)  # Optimización
```

**Resultados (sin regularización):**
| Conjunto | Accuracy | Precision | Recall | F1 Score |
|----------|----------|-----------|--------|----------|
| Train    | ~85%     | ~84%      | ~88%   | ~86%     |
| Test     | ~82%     | ~81%      | ~86%   | ~83%     |

### Paso 3: Fronteras de Decisión
Se visualizaron 3 pares de características:
1. **Age vs Cholesterol** - Separación moderada
2. **BP vs Max HR** - Mejor separación
3. **ST depression vs Vessels** - Mayor separabilidad

### Paso 4: Regularización L2
Se añadió término de regularización: `J += (λ/2m)||w||²`

| Lambda | Accuracy | ||w|| |
|--------|----------|-------|
| 0      | 82.4%    | 4.21  |
| 0.01   | 82.4%    | 3.95  |
| 0.1    | 81.3%    | 3.12  |
| 1      | 78.0%    | 1.85  |

**λ óptimo**: 0.01-0.1 (balance entre rendimiento y generalización)

### Paso 5: Despliegue en Amazon SageMaker
- Modelo exportado como archivos NumPy (`.npy`)
- Documentación de pasos para endpoint deployment
- Ejemplo de inferencia: `Age=60, Chol=300` → **68% probabilidad de enfermedad**

---

## Estructura del Proyecto
```
Heart_Disease_LR_Homework/
├── data/
│   └── Heart_Disease_Prediction.csv
├── heart_disease_lr_analysis.ipynb
├── model_weights.npy (generado al ejecutar)
├── model_bias.npy (generado al ejecutar)
├── decision_boundaries.png (generado al ejecutar)
├── regularization_comparison.png (generado al ejecutar)
└── README.md
```

## Requisitos
```
Python 3.8+
numpy
pandas
matplotlib
scikit-learn (solo para train_test_split)
jupyter
```

## Cómo Ejecutar
```bash
cd Primer_Corte/Heart_Disease_LR_Homework
pip install numpy pandas matplotlib scikit-learn jupyter
jupyter notebook heart_disease_lr_analysis.ipynb
```

---

## Autor
Desarrollado como tarea del curso de Machine Learning.