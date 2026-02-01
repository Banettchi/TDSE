# Predicción de Riesgo de Enfermedad Cardíaca: Regresión Logística desde Cero

## Contexto
Las enfermedades cardíacas son la principal causa de muerte a nivel mundial (~18 millones/año según la OMS). Los modelos predictivos permiten identificar pacientes en riesgo mediante el análisis de características clínicas, optimizando así la asignación de recursos médicos y mejorando los resultados del tratamiento.

---

## Dataset
<<<<<<< HEAD
Se utiliza el **Heart Disease Dataset** del repositorio UCI (disponible en Kaggle).
- **Registros**: 303 pacientes
- **Características**: Age, Cholesterol, BP, Max HR, ST depression, Number of vessels fluro
- **Objetivo**: Presencia (1) o Ausencia (0) de enfermedad cardíaca

## Lo que desarrollé en el cuadernillo

### 1. Preparación de Datos
Empecé cargando el dataset y haciendo un análisis exploratorio básico. Un paso que resultó ser vital fue la normalización Min-Max; sin este ajuste, el modelo simplemente no podía converger porque las escalas de las variables eran muy diferentes (edad vs colesterol, por ejemplo).

### 2. Regresión Logística Manual
Aquí programé las funciones clave a mano:
- **Sigmoide**: Para convertir cualquier valor en una probabilidad entre 0 y 1
- **Costo (Binary Cross-Entropy)**: Para medir qué tan lejos están las predicciones de la realidad
- **Gradientes**: Para saber en qué dirección ajustar los pesos

Lo más interesante fue programar el descenso de gradiente y ver cómo el costo iba bajando iteración tras iteración.

### 3. Fronteras de Decisión
Para entender mejor cómo separaba el modelo las clases, grafiqué las fronteras de decisión con diferentes pares de características. Me quedó claro que **ST depression vs Number of vessels** era la combinación con mejor separabilidad, mientras que **Age vs Cholesterol** tenía bastante superposición.

### 4. Regularización L2
También implementé regularización para evitar que los pesos se dispararan. Probé con varios valores de λ:

| Lambda | Accuracy | ‖w‖ |
|--------|----------|-----|
| 0 | 82.4% | 4.21 |
| 0.01 | 82.4% | 3.95 |
| 0.1 | 81.3% | 3.12 |
| 1 | 78.0% | 1.85 |

**λ óptimo**: 0.01-0.1 (balance entre rendimiento y generalización)

## Reflexiones finales
El modelo logró un accuracy del ~82% en el conjunto de prueba, lo cual es razonable considerando que solo usé 6 características. También me quedó claro que las gráficas de frontera de decisión son la mejor forma de saber si el modelo realmente está separando las clases o solo adivinando.

Si tuviera que seguir con esto, me gustaría experimentar con más combinaciones de características y quizás probar con un learning rate adaptativo para acelerar la convergencia.

---
=======
Se utiliza el **Heart Disease Dataset** del repositorio UCI (disponible en [Kaggle](https://www.kaggle.com/datasets/neurocipher/heartdisease)).
>>>>>>> eede5368ccb8219b0aba2d58305ba5bf806879e9

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

<<<<<<< HEAD
---
=======
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
>>>>>>> eede5368ccb8219b0aba2d58305ba5bf806879e9

## Requisitos
```
Python 3.8+
numpy
pandas
matplotlib
scikit-learn (solo para train_test_split)
jupyter
```

<<<<<<< HEAD
---

## Información del Autor
*   **Autor:** Diego Alejandro Montes Bonilla
*   **Curso:** Transformación Digital y Arquitectura Empresarial
*   **Fecha:** Enero 2026
*   **Universidad:** Escuela Colombiana de Ingeniería Julio Garavito
=======
## Cómo Ejecutar
```bash
cd Primer_Corte/Heart_Disease_LR_Homework
pip install numpy pandas matplotlib scikit-learn jupyter
jupyter notebook heart_disease_lr_analysis.ipynb
```

---

## Autor
Desarrollado como tarea del curso de Machine Learning.
>>>>>>> eede5368ccb8219b0aba2d58305ba5bf806879e9
