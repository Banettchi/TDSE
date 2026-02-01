# Predicción de Riesgo de Enfermedad Cardíaca: Regresión Logística desde Cero

## Contexto
Las enfermedades cardíacas son la principal causa de muerte a nivel mundial. Los modelos predictivos permiten identificar pacientes en riesgo mediante el análisis de características clínicas como edad, colesterol y presión arterial, optimizando así la asignación de recursos médicos y mejorando los resultados del tratamiento.

## Dataset
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

## Requisitos
- Python 3.8+
- NumPy
- Pandas
- Matplotlib
- Jupyter Notebook

---

## Pasos del Proyecto
1.  **Carga y Preparación de Datos**: EDA, limpieza y normalización.
2.  **Implementación de Regresión Logística**: Codificación manual de `sigmoid`, `cost` y `gradient_descent`.
3.  **Visualización de Fronteras**: Gráficos de decisión en 2D.
4.  **Regularización**: Implementación de regularización L2 para evitar sobreajuste.
5.  **Despliegue (Simulado)**: Exploración de despliegue en Amazon SageMaker.

---

## Información del Autor
*   **Autor:** Diego Alejandro Montes Bonilla
*   **Curso:** Transformación Digital y Arquitectura Empresarial
*   **Fecha:** Enero 2026
*   **Universidad:** Escuela Colombiana de Ingeniería Julio Garavito