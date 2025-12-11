# Vision-Austral
| **Fase** | **N°** | **Tarea** | **Descripción** | **Herramienta / Comando Clave** | **Resultado Esperado** |
|---------|-------|-----------|------------------|----------------------------------|-------------------------|
| **I. Preparación de Datos y Entorno** | 1.1 | Instalación Base | Instalar la librería de Ultralytics (YOLOv8) y Python. | `pip install ultralytics` | Librería YOLOv8 lista para usarse. |
| | 1.2 | Recolección de Imágenes | Reunir un conjunto de imágenes de anchoas (200–500 mínimo). | Archivos JPG/PNG | Carpeta con imágenes de anchoas. |
| | 1.3 | Etiquetado de Datos | Dibujar bounding boxes de las anchoas. Clase única: **anchovy**. | LabelImg, Roboflow o CVAT | Archivos `.txt` formato YOLO por imagen. |
| | 1.4 | División del Dataset | Separar en train/val/test (80/10/10). | Script Python o herramienta de etiquetado | Carpetas `train`, `val`, `test` organizadas. |
| | 1.5 | Archivo de Configuración | Crear `anchovy.yaml` con rutas y clase. | Archivo YAML | Archivo YAML con `nc: 1` y `names: [anchovy]`. |
| **II. Entrenamiento del Modelo YOLOv8** | 2.1 | Entrenamiento (Fine-Tuning) | Entrenar YOLOv8n preentrenado usando fine-tuning recomendado. | `yolo train model=yolov8n.pt data=anchovy.yaml epochs=100 imgsz=640 batch=8 freeze=10` | Archivo de pesos `best.pt` generado. |
| | 2.2 | Evaluación de Rendimiento | Revisar mAP, F1-Score y métricas. | Logs de YOLOv8 | mAP alto (≥ 80%). |
| **III. Simulación de Medición** | 3.1 | Detección de Coordenadas | Obtener bounding boxes en imágenes de prueba. | `yolo predict model=runs/detect/train/weights/best.pt source=./ruta/a/imagenes/test` | Coordenadas `(xmin, ymin, xmax, ymax)` por detección. |
| | 3.2 | Establecer Patrón de Calibración | Medir un objeto conocido para obtener la proporción mm/píxel. | Regla o software de imagen | Factor de Calibración (mm/píxel). |
| | 3.3 | Cálculo de Longitud (Píxeles) | Calcular longitud en píxeles desde la caja. | Script Python | `Largo_Pixeles = max((x_max - x_min), (y_max - y_min))` |
| | 3.4 | Cálculo de Longitud Real | Convertir la longitud en píxeles a mm. | Script Python | Longitud real = `Largo_Pixeles * Factor_de_Calibración`. |
