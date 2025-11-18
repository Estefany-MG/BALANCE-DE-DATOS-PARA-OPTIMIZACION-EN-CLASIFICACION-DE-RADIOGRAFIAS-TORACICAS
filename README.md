# 🤖 TÉCNICAS DE BALANCE DE DATOS PARA OPTIMIZAR EL RENDIMIENTO DE MODELOS DE APRENDIZAJE PROFUNDO EN CLASIFICACIÓN DE RADIOGRAFÍAS TORÁCICAS

## 📜 Resumen del Proyecto

Este repositorio contiene el código fuente completo del proyecto de tesis que aborda el desafío del **desequilibrio de clases** en la clasificación de imágenes médicas.

La investigación evalúa y compara tres estrategias para optimizar el rendimiento del clasificador **ResNet50** en la detección binaria de Neumonía (clase mayoritaria) vs. Normal (clase minoritaria) en radiografías torácicas pediátricas.

| Desafío Principal | Solución Óptima Validada (Escenario 5) | Contribución Clave |
| :--- | :--- | :--- |
| Sesgo del modelo hacia la clase mayoritaria (Neumonía). | Generación de imágenes sintéticas de alta fidelidad mediante **WGAN-GP** (Wasserstein GAN con Penalización de Gradiente). | Se demuestra que la estrategia a nivel de datos (GANs) es superior a las técnicas a nivel de algoritmo (Loss Functions) y a los enfoques híbridos. |

## 🚀 Resultados y Hallazgos Clave

El objetivo principal fue demostrar que las técnicas de balanceo mejoran el rendimiento en al menos un 3%.

| Modelo / Escenario | Estrategia de Balance | Accuracy Global | Especificidad (Clase Normal - Minoría) | ROC-AUC |
| :--- | :--- | :--- | :--- | :--- |
| **Escenario 1 (Línea Base)** | Sin Balance (CCE Estándar) | 91.47% | 84.81% | 0.9635 |
| **Escenario 5 (Óptimo)** | **WGAN-GP + CCE** | **94.37%** | **91.77%** | **0.9837** |
| **Escenario 6 (Híbrido)** | WGAN-GP + Focal Loss | 93.17% | **93.67%** | 0.9813 |

### Conclusiones Principales

  * **Validación de Hipótesis:** La Hipótesis General (H1) fue validada con un **incremento del 3.17% en Accuracy** y un drástico **8.2% de mejora en la Especificidad** (detección de pacientes sanos).
  * **Superioridad del Balanceo de Datos:** El **Escenario 5 (WGAN-GP)** fue identificado como el modelo óptimo, ofreciendo el mejor equilibrio general y capacidad de generalización ($\text{AUC} = 0.9837$).
  * **Refutación del Enfoque Híbrido:** Se demostró que la combinación de GANs con funciones de pérdida (Focal Loss) es redundante en un dataset ya perfectamente balanceado, resultando en una ligera degradación del rendimiento global.
  * **Aporte de la WGAN-GP:** La WGAN-GP fue altamente efectiva, generando imágenes con una calidad excepcional (FID Score $\approx 48.95$).

## ⚙️ Estructura del Repositorio

El proyecto está organizado para reflejar las fases de la metodología de la tesis:

| Archivo / Carpeta | Descripción | Tesis (Capítulo) |
| :--- | :--- | :--- |
| `notebooks/` | Contiene el código fuente por etapas (ver abajo). | IV. Metodología |
| `checkpoints/` | Almacenamiento de los pesos intermedios y el mejor modelo resnet50\_Base\_GAN\_FINETUNED\_best.h5. | V. Resultados |
| `generated_data/` | Imágenes sintéticas generadas por WGAN-GP para el balanceo. | V. Resultados |
| `results/` | Matrices de confusión, curvas ROC/PR, y gráficos de entrenamiento finales. | V. Resultados |
| `TESIS_ANEXO_CODIGO_BASE.py` | Script consolidado y limpio que reproduce todo el pipeline. | Anexo de Código |

## 🛠️ Reproducibilidad y Ejecución

El proyecto se puede ejecutar en Google Colab o cualquier entorno con GPU (NVIDIA).

### Requisitos

1.  **Entorno:** Python 3.8+, TensorFlow 2.x (con GPU), PyTorch 2.x (para GANs).
2.  **Librerías:** Las dependencias se instalan en la primera celda del notebook:
    ```bash
    pip install tensorflow keras scikit-learn matplotlib numpy opencv-python kaggle torch torchvision seaborn tqdm
    ```
3.  **Datos:** Los datos se descargan automáticamente desde la API de Kaggle.

### Pasos de Reproducción

1.  **Configurar Kaggle:** Sube tu archivo kaggle.json para autenticar la descarga del dataset.
2.  **Ejecutar TESIS\_ANEXO\_CODIGO\_BASE.py:** Ejecuta el script o el notebook asociado siguiendo la secuencia lógica:
      * **Fase 1:** Preprocesamiento y Carga de Datos (implementa CLAHE/Recorte).
      * **Fase 2:** Entrenamiento de WGAN-GP (Generación del dataset sintético).
      * **Fase 3:** Entrenamiento de ResNet50 para los 6 Escenarios (incluyendo el Fine-Tuning del Escenario 5 y 6).
      * **Fase 4:** Evaluación de Métricas y Generación de Tablas Comparativas.

## 👥 Contacto y Autoría

| Elemento | Detalle |
| :--- | :--- |
| **Autor** | Estefany Paola Mamani Gutierrez |
| **Tesis** | Universidad Nacional de Moquegua (UNAM) |
| **Asesor** | Mgr. Clares Perca Juan Carlos |
| **Repositorio** | [https://github.com/Estefany-MG/BALANCE-DE-DATOS-PARA-OPTIMIZACION-EN-CLASIFICACION-DE-RADIOGRAFIAS-TORACICAS](https://www.google.com/search?q=https://github.com/Estefany-MG/BALANCE-DE-DATOS-PARA-OPTIMIZACION-EN-CLASIFICACION-DE-RADIOGRAFIAS-TORACICAS) |
