# Sistema de Detección de Equipo de Protección Personal (PPE)

## Descripción del Proyecto
Este repositorio contiene la implementación de un sistema de visión por computador diseñado para la detección y monitoreo de Equipo de Protección Personal (PPE) en entornos de obras eléctricas.

El sistema está desarrollado sobre la arquitectura **YOLO26m** (Ultralytics) y ha sido entrenado para identificar tanto la presencia como la ausencia de elementos indispensables de seguridad bajo diversas condiciones de iluminación, ángulo y fondo.

El modelo clasifica y localiza 6 clases:
- **Casco:** `helmet` / `no_helmet`
- **Guantes:** `gloves` / `no_gloves`
- **Chaleco:** `vest` / `no_vest`

Durante la etapa de validación, el modelo alcanzó un **mAP50 general de 0.7690**, integrando además técnicas de interpretabilidad visual (Grad-CAM) para analizar la atención del modelo en cada detección.

---

## Descargas y Recursos

Debido al tamaño de los archivos, los pesos entrenados del modelo y el dataset consolidado se alojan en enlaces externos:

* **Pesos del Modelo Entrenado (`best.pt`):** [Descargar archivo best.pt](ENLACE_AQUI)
* **Dataset Consolidado (`.zip`):** [Descargar dataset .zip](ENLACE_AQUI)

---

## Estructura de Notebooks e Instrucciones de Uso

El flujo de trabajo está modularizado en tres notebooks independientes según la tarea que desees realizar:

### 1. Preparación, Fusión y Corrección de Datos
* **Archivo:** `Object Detection - PPE - Dataset and Labels Correction.ipynb`
* **Propósito:** Documenta el proceso de descarga desde las fuentes públicas originales, la fusión de datos, el filtrado de clases y la rutina de corrección manual de etiquetas/falsos positivos para generar el dataset final.

---

### 2. Pipeline Completo de Machine Learning (Entrenamiento y Evaluación)
* **Archivo:** `Object Detection - PPE (Helmet, Gloves, Vest).ipynb`
* **Propósito:** Contiene todo el ciclo de vida del modelo:
  1. Configuración del entorno e importación de dependencias.
  2. Carga del modelo base.
  3. Carga del dataset:
     - Mediante el archivo comprimido `.zip` descargado previamente.
     - O mediante descarga directa configurando tu propia variable `ROBOFLOW_API_KEY`.
  4. Configuración y ejecución del entrenamiento con hiperparámetros optimizados.
  5. Pruebas, evaluación de métricas (`mAP50`, curvas de pérdida, matriz de confusión) e interpretabilidad con Grad-CAM.
  6. Exportación y guardado de los pesos finales `best.pt`.

---

### 3. Inferencia y Pruebas en Tiempo Real
* **Archivo:** `PPE_Detection_RTCamara.ipynb`
* **Propósito:** Permite ejecutar inferencias en vivo conectando el sistema a la cámara local o integrada del dispositivo.
* **Uso:** 
  1. Descarga el archivo `best.pt` desde la sección de recursos.
  2. Carga el archivo `.pt` dentro del entorno del notebook.
  3. Ejecuta las celdas para inicializar la captura de video y realizar la detección de PPE en tiempo real.
