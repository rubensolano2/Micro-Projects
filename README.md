# 🚀 Modelo YOLO para Detección de Objetos en Fútbol 🏈

Este repositorio contiene los scripts y las instrucciones para entrenar y utilizar un modelo YOLO (You Only Look Once) para la detección de objetos en videos de fútbol. Incluye procesos para la configuración del entorno, la obtención de datos, el entrenamiento personalizado del modelo y su validación.

## 🛠️ Configuración del Entorno

Primero, debes configurar tu entorno. Este código se ejecuta en Google Colab, por lo que se asume que estás utilizando su entorno.

```python
from google.colab import drive
drive.mount('/content/drive')

import os
HOME = os.getcwd()
print(HOME)

!mkdir {HOME}/datasets

!pip install -U ultralytics opencv-python==4.8.0.74 roboflow --quiet

🔗 Importante: Antes de continuar, asegúrate de tener una cuenta y acceso a los servicios de Roboflow.

📦 Descarga del Dataset Personalizado
Utiliza el siguiente enlace para obtener el dataset necesario: Smart Football Object Detection.
!pip install roboflow

from roboflow import Roboflow
rf = Roboflow(api_key="YOUR_API_KEY")
project = rf.workspace("your_workspace").project("your_project")
dataset = project.version(3).download("yolov8")

🏋️ Entrenamiento del Modelo Personalizado
El entrenamiento del modelo se realiza mediante el siguiente script, que incluye la configuración necesaria para el modelo YOLO:
import yaml
import torch

# Configuración del dataset y entrenamiento
# ...

!yolo task=detect mode=train model=yolov8s.pt data="/content/your_project/data.yaml" epochs=28 imgsz=800 plots=True

📊 Visualización de Resultados de Entrenamiento
Visualiza los resultados del entrenamiento para evaluar el rendimiento del modelo.
!ls {HOME}/runs/detect/train/

# Confusion Matrix y otras métricas
# ...

🧪 Validación del Modelo Personalizado
Valida el modelo con un conjunto de datos de prueba para asegurar su eficacia.
%cd {HOME}
!yolo task=detect mode=val model={HOME}/runs/detect/train/weights/best.pt data={dataset.location}/data.yaml

