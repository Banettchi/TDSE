# Stellar Luminosity – Regresión lineal y polinomial

## Introducción

Este trabajo lo hice para meterme de lleno y entender bien cómo funcionan los modelos de regresión cuando se aplican a datos reales, en este caso de astrofísica. El objetivo era predecir qué tan luminosa es una estrella basándome en su masa y temperatura. Quise hacerlo todo "a mano" para aprender de verdad, así que no usé librerías automáticas como Scikit-Learn; todo el cálculo matemático y la optimización los hice con **NumPy**, y las gráficas con **Matplotlib**.

Me centré en dos cosas:
*   Que el código se entienda fácil, explicado paso a paso.
*   Que las gráficas cuenten la historia de cómo el modelo va aprendiendo y mejorando en cada iteración.

---

## Qué hay en los Notebooks

### 1. 01_part1_linreg_1feature.ipynb (Masa vs Luminosidad)
*   Armé el modelo lineal básico `L_hat = w·M + b` y la fórmula del error (MSE).
*   Calculé los gradientes a mano (derivadas), probando primero con bucles y luego vectorizado para que fuera más rápido.
*   Entrené el modelo probando varias velocidades de aprendizaje (`alphas`) para ver cuál convergía mejor.
*   Al final, grafiqué la superficie de costo y cómo quedó la línea de regresión sobre los datos.

### 2. 02_part2_polyreg.ipynb (Polinómica + Interacción Masa-Temperatura)
*   Aquí me puse creativo con las características: creé `X = [M, T_scaled, M², M·T_scaled]`. Un detalle importante fue dividir la temperatura por 1000 (`T_scaled`) para que los números no se dispararan.
*   El entrenamiento ya fue 100% vectorizado.
*   Comparé tres versiones del modelo (M1, M2, M3) para ver si valía la pena complicarlo más. La interacción Masa-Temperatura resultó clave.
*   Hice una prueba final prediciendo valores nuevos para ver qué tal respondía.

---

## Requisitos

*   Python 3.x
*   NumPy (para los números)
*   Matplotlib (para las gráficas)

---

## Cómo lo corrí en mi PC (Windows)

1.  Abrí los archivos `.ipynb` directamente en VS Code (también sirve JupyterLab).
2.  Fui corriendo las celdas en orden.
3.  **Tip**: Si veían que la pérdida no bajaba, ajustaba un poco el `alpha` (haciéndolo más pequeño) o le daba más iteraciones, y listo.

---

## Ejecución en AWS SageMaker

### Subiendo los archivos
Fue rápido:
1.  Entré a **SageMaker Studio**.
2.  Le di a **Upload** y subí los dos notebooks.
3.  Elegí el kernel básico de Python (que ya trae NumPy y Matplotlib) y corrí todo "Run All". Cero problemas.

### Evidencias

#### Parte 1: Regresión Lineal
<!-- [FOTO 1: Vista general del notebook 1 en SageMaker] -->
<!-- [FOTO 2: Gráfica de convergencia renderizada en la nube] -->

#### Parte 2: Regresión Polinomial
<!-- [FOTO 3: Vista general del notebook 2 en SageMaker] -->
<!-- [FOTO 4: Comparación final de modelos] -->

---

## Local vs Nube: ¿Qué noté?

Corrí lo mismo en mi compu y en AWS, y vi esto:
*   **Rapidez**: En local se siente un pelín más instantáneo. En SageMaker, a veces el kernel se toma su tiempo en arrancar o en pensar las operaciones pesadas.
*   **Gráficas 3D**: Las figuras interactivas tardan un poquito más en aparecer en la web de Studio que en mi VS Code local.
*   **Resultados**: Lo importante es que los números (pérdidas y pesos finales) dieron idénticos. El código es totalmente portable.

---

## Conclusiones

*   **¿Mejoró el modelo?**: Sí, bastante. El lineal simple (solo Masa) se quedaba corto. Cuando agregué los términos cuadráticos y mezclé la temperatura, el error bajó muchísimo y se ajustó mejor a la física real de las estrellas.
*   **El truco de la Temperatura**: Si no escalaba la temperatura (dividiéndola), el modelo explotaba. Fue un buen aprendizaje sobre la importancia de tener los datos en la misma escala.
*   **Validación**: Las gráficas de "Predicho vs Real" no mienten. El modelo más completo (M3) es el que mejor se pega a la línea ideal.

### Para el futuro
Si tuviera más tiempo, le agregaría:
*   Una función que normalice todas las variables automáticamente (tipo Z-score).
*   Regularización (L2) hecha a mano para evitar que los pesos crezcan demasiado si agrego más grados al polinomio.

---

## Autor
*   **Nombre**: Diego Alejandro Montes Bonilla
*   **Curso**: Transformación Digital y Arquitectura Empresarial
*   **Fecha**: Enero 2026
*   **Universidad**: Escuela Colombiana de Ingeniería Julio Garavito
