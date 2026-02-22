# Embeddings y procesamiento de texto para LLMs

## Contexto

Los LLMs no deberian tratarse como cajas negras. En este proyecto exploro como se procesan textos y se generan embeddings siguiendo el Capitulo 2 de *"Build a Large Language Model (From Scratch)"* de Sebastian Raschka. La idea es entender el flujo real que usan los modelos de lenguaje modernos, desmenuzando cada parte con ejemplos claros y explicaciones en espanol.

---

## Dataset: The Verdict

Se utiliza `the-verdict.txt`, un cuento corto de dominio publico que sirve como corpus de prueba para todo el pipeline.

Es un texto apropiado porque tiene vocabulario variado, es manejable en tamano y no tiene restricciones de uso, lo que lo hace ideal para exploracion educativa.

---

## Lo que desarrolle en el cuadernillo

### 1. Tokenizacion paso a paso

Empece explorando como los LLMs procesan texto: no como palabras completas, sino como tokens. El paso mas importante fue entender que la tokenizacion no es trivial — espacios, puntuacion y mayusculas afectan el resultado.

Implemente dos tokenizadores manuales como referencia: **SimpleTokenizerV1** con vocabulario fijo, y **SimpleTokenizerV2** que agrega tokens especiales `<|unk|>` y `<|endoftext|>` para manejar palabras fuera del vocabulario y separar documentos. La limitacion principal: el vocabulario es cerrado, si aparece una palabra nueva el modelo no puede procesarla.

### 2. BPE con tiktoken

Para resolver eso, use **Byte Pair Encoding (BPE)** con `tiktoken` — el mismo tokenizador que usa GPT-4. La ventaja clave es que nunca produce tokens desconocidos: cualquier texto puede ser codificado descomponiendolo en subpalabras.

### 3. Division en fragmentos (sliding window)

Los LLMs trabajan con ventanas de contexto fijas, no procesan texto completo de una sola vez. Implemente la division con solapamiento usando `max_length` y `stride`. Con stride pequeno hay mas contexto compartido entre fragmentos pero se generan mas datos; con `stride=max_length` no hay solapamiento y se pierde continuidad entre fragmentos.

### 4. Construccion de embeddings

El paso final: convertir IDs de tokens en vectores densos. Se combinan **token embeddings** (representacion semantica) con **positional embeddings** (representacion del orden). Los embeddings posicionales son necesarios porque la capa de atencion es invariante al orden por si sola — no distingue si una palabra aparece al principio o al final de la secuencia.

### 5. Experimento: `max_length` y `stride`

Compare distintas combinaciones para ver como el overlap afecta la cantidad de fragmentos generados y la continuidad del contexto. Muestra bien el trade-off entre cobertura y redundancia.

---

## Interpretacion

Los embeddings son la representacion base que usan los LLMs para procesar lenguaje. Todo el pipeline — tokenizacion, fragmentacion y construccion de vectores — define como el modelo recibe la informacion antes de cualquier capa de atencion o transformacion. Entender estos pasos es entender el punto de entrada real del modelo.

---

## Requisitos

```
Python 3.x
torch
tiktoken
requests
```

---

**Autor:** Diego Alejandro Montes Bonilla
**Curso:** Transformacion Digital y Arquitectura Empresarial
**Fecha:** Febrero 2026
**Universidad:** Escuela Colombiana de Ingenieria Julio Garavito
