# Exploring Convolutional Layers Through Data and Experiments

## Descripción del Problema

Este proyecto explora las capas convolucionales como componentes arquitectónicos cuyas decisiones de diseño afectan el rendimiento, escalabilidad e interpretabilidad de las redes neuronales. En lugar de tratar las redes neuronales como cajas negras, analizamos cómo el **sesgo inductivo** se introduce a través de las capas convolucionales.

## Dataset: Fashion-MNIST

### Justificación de la Elección
Fashion-MNIST es un dataset apropiado para capas convolucionales porque:
- **Datos estructurados espacialmente**: Las imágenes de 28x28 píxeles tienen relaciones espaciales locales que las convoluciones pueden explotar
- **Complejidad moderada**: 10 clases de prendas de vestir ofrecen un reto real sin requerir recursos computacionales excesivos
- **Patrones visuales**: Bordes, texturas y formas son características que las capas convolucionales detectan eficientemente
- **Benchmark establecido**: Permite comparación con literatura existente

### Características del Dataset
| Propiedad | Valor |
|-----------|-------|
| Imágenes de entrenamiento | 60,000 |
| Imágenes de prueba | 10,000 |
| Dimensiones | 28 x 28 píxeles |
| Canales | 1 (escala de grises) |
| Clases | 10 |

### Clases
0. T-shirt/top
1. Trouser
2. Pullover
3. Dress
4. Coat
5. Sandal
6. Shirt
7. Sneaker
8. Bag
9. Ankle boot

---

## Arquitectura del Proyecto

```
├── README.md
├── cnn_exploration.ipynb      # Notebook principal con todos los experimentos
└── requirements.txt           # Dependencias del proyecto
```

---

## Arquitecturas Implementadas

### Modelo Baseline (Sin Convoluciones)
```
Input (784) → Dense(256, ReLU) → Dropout(0.3) → Dense(128, ReLU) → Dense(10, Softmax)
```
- **Parámetros**: ~235,000
- **Limitación**: No captura relaciones espaciales locales

### Modelo CNN
```
Input (28,28,1) → Conv2D(32, 3x3) → MaxPool(2x2) → Conv2D(64, 3x3) → MaxPool(2x2) → Flatten → Dense(64) → Dense(10)
```

#### Justificación de Decisiones Arquitectónicas:

| Decisión | Valor | Justificación |
|----------|-------|---------------|
| Kernel size | 3x3 | Captura patrones locales eficientemente, estándar en la industria |
| Filtros | 32→64 | Incremento progresivo para detectar características más complejas |
| Pooling | MaxPool 2x2 | Reduce dimensionalidad y proporciona invarianza a traslaciones |
| Stride | 1 | Preserva información espacial máxima en convoluciones |
| Padding | 'same' | Mantiene dimensiones para facilitar cálculos |

---

## Experimento Controlado: Efecto del Tamaño del Kernel

### Configuración
Variable manipulada: **Tamaño del kernel** (3x3 vs 5x5 vs 7x7)

Variables controladas:
- Número de filtros: 32, 64
- Capas convolucionales: 2
- Función de activación: ReLU
- Pooling: MaxPool 2x2
- Epochs: 10
- Batch size: 64

### Resultados Esperados

| Kernel | Parámetros | Accuracy Val | Observaciones |
|--------|------------|--------------|---------------|
| 3x3 | ~XX,XXX | XX.X% | TBD |
| 5x5 | ~XX,XXX | XX.X% | TBD |
| 7x7 | ~XX,XXX | XX.X% | TBD |

---

## Interpretación y Razonamiento Arquitectónico

### ¿Por qué las capas convolucionales superan al baseline?

*(Por completar después de ejecutar experimentos)*

Las CNNs introducen **sesgo inductivo** apropiado para datos de imagen:
1. **Localidad**: Los píxeles cercanos están más relacionados que los lejanos
2. **Invarianza a traslaciones**: Un patrón es el mismo sin importar su posición
3. **Jerarquía composicional**: Características simples se combinan en patrones complejos

### ¿Qué sesgo inductivo introduce la convolución?

- **Conectividad local**: Cada neurona solo ve una región pequeña de la entrada
- **Peso compartido**: Los mismos filtros se aplican en toda la imagen
- **Equivarianza a traslaciones**: Si la entrada se desplaza, la salida también

### ¿Cuándo NO serían apropiadas las convoluciones?

- Datos tabulares sin estructura espacial
- Secuencias donde el orden temporal es más importante que la localidad
- Grafos con conectividad irregular
- Datos donde la posición absoluta importa más que los patrones locales

---

## Despliegue en SageMaker

### Entrenamiento


## Requisitos

---

## Autor

- **Nombre**: Diego Alejandro Montes Bonilla
- **Curso**: Fundamentos de Deep Learning
- **Fecha**: Febrero 2026

---
