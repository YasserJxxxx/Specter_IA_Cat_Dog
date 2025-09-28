# 🐈🐕 Clasificador Binario de Perros y Gatos (Regresión Logística - Baseline)

[![Python 3.8+](https://img.shields.io/badge/Python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![Scikit-learn](https://img.shields.io/badge/Scikit--learn-v1.0+-orange.svg)](https://scikit-learn.org/stable/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

---

## 💡 Descripción General del Proyecto

Este proyecto implementa un clasificador binario de imágenes para la identificación de **perros** y **gatos**. Se utiliza la **Regresión Logística** como modelo de **línea base (baseline)**. El clasificador opera sobre los píxeles de las imágenes pre-procesadas (escaladas a 64x64 y aplanadas), permitiendo una solución eficiente y con alta interpretabilidad.

### 🎯 Objetivos Clave

* Establecer un rendimiento inicial ($\approx 71\%$ de precisión) con un modelo lineal simple.
* Implementar una arquitectura de **persistencia de datos y modelo** en Google Drive para optimizar el tiempo de ejecución en entornos *notebook*.

---

## 🛠️ Stack Tecnológico y Dependencias

| Tecnología | Rol en el Proyecto |
| :--- | :--- |
| **Python 3.x** | Lenguaje de desarrollo. |
| **Scikit-learn** | Implementación del modelo `LogisticRegression` y cálculo de métricas. |
| **OpenCV (`cv2`)** | Pre-procesamiento de imágenes (escala de grises, redimensionamiento). |
| **NumPy / Pandas** | Manejo de arrays de píxeles y formateo de resultados. |
| **Joblib** | Serialización y persistencia del modelo en Drive. |
| **KaggleHub** | Gestión de la descarga del dataset inicial. |

---

## 🚀 Guía de Configuración y Ejecución

El proyecto está optimizado para ser ejecutado en **Google Colab**.

### 1. Preparación del Entorno

1.  Abre el código fuente completo en una nueva sesión de Google Colab.
2.  Ejecuta la primera celda para instalar automáticamente las librerías necesarias (`pip install -q`).
3.  El script solicitará la **autorización para montar Google Drive**. Este paso es crucial para la persistencia.

### 2. Flujo de Persistencia de Datos

El script sigue una estrategia condicional para optimizar el tiempo:

* **Primera Ejecución:**
    1.  Descarga el *dataset* de Kaggle.
    2.  Ejecuta el **Pre-procesamiento** (aplanamiento, normalización).
    3.  Entrena el modelo de Regresión Logística.
    4.  Guarda los arrays de datos (`.npz`) y el modelo entrenado (`.pkl`) en una carpeta de Drive.
* **Ejecuciones Posteriores:**
    1.  El script detecta los archivos persistentes.
    2.  Omite la descarga y el entrenamiento.
    3.  **Carga el modelo y los datos en segundos.**

### 3. Inferencia Interactiva

Una vez finalizado el entrenamiento/carga, el script ejecuta un módulo de prueba que permite:

* Subir una imagen local (Perro o Gato).
* Pre-procesar la imagen de manera idéntica a los datos de entrenamiento.
* Mostrar la predicción del modelo con su **nivel de confianza** (probabilidad).

---

## 📊 Resultados de Evaluación

Los resultados se obtuvieron al evaluar el modelo entrenado sobre el conjunto de prueba (20% de los datos).

### 1. Matriz de Confusión (Valores Típicos)

| | Predicho Gato (0) | Predicho Perro (1) |
| :--- | :--- | :--- |
| **Real Gato (0)** | $\mathbf{150}$ (Verdaderos Negativos) | $\mathbf{50}$ (Falsos Positivos) |
| **Real Perro (1)** | $\mathbf{66}$ (Falsos Negativos) | $\mathbf{134}$ (Verdaderos Positivos) |

### 2. Métricas Detalladas

| Métrica | Gato (0) | Perro (1) |
| :--- | :--- | :--- |
| **Precision** | $\approx 0.69$ | $\approx 0.73$ |
| **Recall** | $\approx 0.75$ | $\approx 0.67$ |
| **F1-Score** | $\approx 0.72$ | $\approx 0.70$ |
| **Accuracy Global** | \multicolumn{2}{|c|}{$\mathbf{0.7100}$ ($\mathbf{71.00\%}$)} |

### 3. Análisis de las Limitaciones

La precisión del $\sim 71\%$ refleja la limitación del modelo:

* **Regresión Logística** crea una **frontera de decisión lineal**.
* Los problemas reales de clasificación de imágenes (variaciones de pose, iluminación) son **no lineales**.
* El modelo pierde información espacial crítica al **aplanar** la imagen a un vector de 4096 píxeles.

---

## ⏭️ Hoja de Ruta y Próximos Pasos

Para superar la barrera de rendimiento del modelo lineal, se plantean las siguientes mejoras:

### A. Mejoras en la Arquitectura

* **Migración a CNN:** Implementar una **Red Neuronal Convolucional** para aprovechar su capacidad de aprender jerarquías de características (bordes, texturas) directamente de la estructura 2D de la imagen.
* **Transfer Learning:** Utilizar un modelo preentrenado (ej. ResNet, MobileNet) para acelerar el entrenamiento y mejorar la precisión aprovechando el conocimiento visual previo.

### B. Mejoras en la Ingeniería de Datos

* **Aumento de Datos:** Aplicar transformaciones aleatorias (*Data Augmentation*) como rotaciones y volteos para aumentar el tamaño efectivo y la diversidad del conjunto de entrenamiento.

---

## 📝 Licencia

Este proyecto está distribuido bajo la **Licencia MIT**. Consulta el archivo `LICENSE` para más detalles.
