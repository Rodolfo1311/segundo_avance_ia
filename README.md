# reconocimiento de vehiculos con tensorflow
## primer entregable
Para este proyecto se utilizara un modelo preentrenado de Tensorflow el cual se llama: faster_rcnn_resnet101_coco

# como ejecutar este proyecto 

## lo necesairo

### 1. clonar este repositorio

### 2. completar el modelo 
###### para esto es necesario descargar las carpetas ["modelo y modelo congelado"](https://drive.google.com/drive/folders/1M6EKf0mCCvixNh2GyP9xtc0HU4oF5FW9?usp=sharing) y pegarlas dentro de deteccion_objetos

### 3. tener instalado [Anaconda](https://www.anaconda.com/products/individual) 
Anaconda es un programa el cual nos sirve para crear distintos entornos en nuestra computadora para la instalacion de librerias

### 4. [crear un entorno virtual en anaconda](https://riptutorial.com/es/python/example/10797/realizacion-de-entornos-virtuales-utilizando-anaconda-)

### 5. instalar en anaconda las siguientes librerias desde el promt de anaconda
#### 1. [tensorflow](https://www.tensorflow.org/install/pip) version 1.14
se debe instalar la version 1.14 porque sobre esta version de tensorflow corre este proyecto
#### 2. [numpy](https://pypi.org/project/numpy/1.16.4/) version 1.16.4
se debe instalar esta version de numpy porque es la que es compatible con tensorflow 1.14
#### 3. [matplotlib](https://anaconda.org/conda-forge/matplotlib)
#### 4. [pandas](https://anaconda.org/anaconda/pandas)
#### 5. [Pillow](https://anaconda.org/anaconda/pillow)
#### 6. [pycocotools](https://anaconda.org/conda-forge/pycocotools)

### 6. descargar la ultima version de [labelimg]() 
este programa nos sirve para etiquetar las imagenes y da como salida un archivo .xml 

### 7. copiar carpetas
adentro de deteccion_objetos>slim copiar las carpetas "development" y "nets" y pegar estas dos carpetas dentro de las carpetas "library" y "lib" que se encuentran en el direcctorio en donde se esta instalado anaconda navigator 

### 8. descargar imagenes
se deben descargar como minimo 100 imagenes del objeto que se desea reconocer y guardarlas adentro de la carpeta
deteccion_objetos>images 

### 9. etiquetar las imagenes
se deben etiquetar las imagenes con el programa labelimg 

### 10. creacion de archivos .CSV y .Record
###### en el promt de anaconda utilizar los comandos:
###### 1. python xml_a_csv.py --inputs=img_test --output=test
###### 2. python xml_a_csv.py --inputs=img_entrenamiento --output=entrenamiento
###### 3. python csv_a_tf.py --csv_input=CSV/test.csv --output_path=TFRecords/test.record --images=images
###### 4. python csv_a_tf.py --csv_input=CSV/entrenamiento.csv --output_path=TFRecords/entrenamiento.record --images=images

### 11. iniciar el entrenamiento 
###### en el promt utilizar el siguiente comando
###### python object_detection/train.py --logtostderr --train_dir=train --pipeline_config_path=modelo/faster_rcnn_resnet101_coco.config
permitimos que el modelo entrene hasta que llegue a tener una perdida maxima del 0.9 para poder tener un modelo con una buena exactitud
a mayor entrenamiento mayor sera la exactitud del model para detener el entrenamiento usar ctrl+C

### 12. crear el modelo congelado 
###### en el promt utilizar el siguiente comando:
###### python object_detection/export_inference_graph.py --input_type image_tensor --pipeline_config_path modelo/faster_rcnn_resnet101_coco.config  --trained_checkpoint_prefix train/model.ckpt-684 --output_directory modelo_congelado

### 13. probar el modelo 
###### 1. para probar el modelo debemos pegar las imagenes en las que querramos reconocer objetos en la carpeta deteccion_objetos>imp_pruebas
###### 2. en el promt utilizar el siguiente comando: python object_detection/object_detection_runner.py
###### 3. el resultado de la prediccion se encontrara en la carpeta deteccion_objetos>output>imp_pruebas

## ejemplo del funcionamiento 
![RAM](https://user-images.githubusercontent.com/64815890/82742358-4c1e8300-9d1a-11ea-9151-e9c665dcf058.jpeg)
![BT](https://user-images.githubusercontent.com/64815890/82742359-4cb71980-9d1a-11ea-88fe-db434d9e42ac.jpeg)
![carro naranja](https://user-images.githubusercontent.com/64815890/82742361-4de84680-9d1a-11ea-8ca2-eb9bdd3b4e3f.jpeg)
![carro rojo](https://user-images.githubusercontent.com/64815890/82742362-4e80dd00-9d1a-11ea-97be-c6718f56f611.jpeg)
![Hilux](https://user-images.githubusercontent.com/64815890/82742363-4fb20a00-9d1a-11ea-95e5-e0bf066678c0.jpeg)
![Ladera](https://user-images.githubusercontent.com/64815890/82742364-50e33700-9d1a-11ea-94d1-c44421fd5ccc.jpeg)


## Segundo entregable 
### 1. obtencion de imagenes
para el segundo entregable lo que se realizo fue conseguir imagenes de todos los tipos de vehiculos solicitados los cuales son:
#### 1.pickup
#### 2.bus
#### 3.camion
#### 4.mototaxi
#### 5.moto
### 2. configuracion de label_map.pbtxt
en este archivo se encuentra en deteccion_objetos>configuracion la siguiente estructura:
###### .item {
######  id: 1
######  name: 'moto'
###### }

este objeto consta de 2 campos los cuales son id y name en los cuales se debe escribir el id y nombre de cada una de las etiequetas
 para declarar una nueva solamente se debe copiar esta estructura y llenarla con el id siguiente y el nombre de la etiqueta 
### 3. configuracion de labels.txt
este archivo se encuentra en deteccion_objetos>configuracion y es un archivo de texto en el cual se debe indicar todas las etiquetas 
que se utilizaran en este caso son 5
###### 0.null
###### 1.pickup
###### 2.bus
###### 3.camion
###### 4.mototaxi
###### 5.moto

la primera linea siempre debe ser null
### 4. configurar numero de clases en el archivo faster_rcnn_resnet101_coco.config
este archivo se encuentra en deteccion_objetos>modelo lo unico que se debe configurar en este archivo es el numero de clases que hace 
referencia a la cantidad de etiquetas que se utilizaran que en este caso seran 5
###### num_classes: 5

### 5. eliminacion de los archivos .CSV y .Record de la primera entrega 
estos archivos se encuentran en deteccion_objetos>CSV y deteccion_objetos>TFRecords es necesario dejar estas dos carpetas vacias para
crear los nuevos archivos .CSV y .Record 

### 6. creacion de archivos .CSV y .Record
###### en el promt de anaconda utilizar los comandos:
###### 1. python xml_a_csv.py --inputs=img_test --output=test
###### 2. python xml_a_csv.py --inputs=img_entrenamiento --output=entrenamiento
###### 3. python csv_a_tf.py --csv_input=CSV/test.csv --output_path=TFRecords/test.record --images=images
###### 4. python csv_a_tf.py --csv_input=CSV/entrenamiento.csv --output_path=TFRecords/entrenamiento.record --images=images

### 7. reentrenamiento del modelo 
###### en el promt utilizar el siguiente comando
###### python object_detection/train.py --logtostderr --train_dir=train --pipeline_config_path=modelo/faster_rcnn_resnet101_coco.config
permitimos que el modelo entrene hasta que llegue a tener una perdida maxima del 0.9 para poder tener un modelo con una buena exactitud
a mayor entrenamiento mayor sera la exactitud del model para detener el entrenamiento usar ctrl+C para este segundo entregable se entreno
el modelo durante 4,633 pasos como podemos ver acontinuacion 

![entrenamiento](https://user-images.githubusercontent.com/64815890/83317194-43312400-a1e8-11ea-96d5-e9115f71556a.jpg)

### 8. congelado del nuevo modelo 
###### en el promt utilizar el siguiente comando:
###### python object_detection/export_inference_graph.py --input_type image_tensor --pipeline_config_path modelo/faster_rcnn_resnet101_coco.config  --trained_checkpoint_prefix train/model.ckpt-684 --output_directory modelo_congelado

### 9. probar el modelo 
###### 1. para probar el modelo debemos pegar las imagenes en las que querramos reconocer objetos en la carpeta deteccion_objetos>imp_pruebas
###### 2. en el promt utilizar el siguiente comando: python object_detection/object_detection_runner.py
###### 3. el resultado de la prediccion se encontrara en la carpeta deteccion_objetos>output>imp_pruebas
#### reconociendo 
![reconociendo](https://user-images.githubusercontent.com/64815890/83317209-4d532280-a1e8-11ea-92a0-52068c3baf1a.jpg)

## RESULTADOS DEL SEGUNDO ENTREGABLE 
![camion2](https://user-images.githubusercontent.com/64815890/83317190-41fff700-a1e8-11ea-91ac-772cf1cdbd0b.jpeg)
![camion3](https://user-images.githubusercontent.com/64815890/83317191-42988d80-a1e8-11ea-9819-f35b0c01347d.jpeg)
![carro naranja](https://user-images.githubusercontent.com/64815890/83317193-42988d80-a1e8-11ea-89fe-ea6727666756.jpeg)
![Hilux](https://user-images.githubusercontent.com/64815890/83317196-462c1480-a1e8-11ea-93b7-199ee109bda6.jpeg)
![moto](https://user-images.githubusercontent.com/64815890/83317199-475d4180-a1e8-11ea-97e8-dffc790e0417.jpeg)
![moto1](https://user-images.githubusercontent.com/64815890/83317200-47f5d800-a1e8-11ea-9bf9-4157a192d735.jpeg)
![moto3](https://user-images.githubusercontent.com/64815890/83317202-488e6e80-a1e8-11ea-9634-78b52bc356a0.jpeg)
![mototaxi](https://user-images.githubusercontent.com/64815890/83317204-49bf9b80-a1e8-11ea-90d2-be43db81a417.jpeg)
![mototaxi1](https://user-images.githubusercontent.com/64815890/83317205-4a583200-a1e8-11ea-92d7-27fa3bae0c46.jpeg)
![mototaxi3](https://user-images.githubusercontent.com/64815890/83317207-4b895f00-a1e8-11ea-8e2f-f2cd15f25b5d.jpeg)
![RAM](https://user-images.githubusercontent.com/64815890/83317208-4c21f580-a1e8-11ea-8f96-29172b2a5c10.jpeg)
![bus](https://user-images.githubusercontent.com/64815890/83317210-4f1ce600-a1e8-11ea-8c37-a6efef6e7256.jpeg)
![bus2](https://user-images.githubusercontent.com/64815890/83317213-504e1300-a1e8-11ea-8d22-13679728d5b2.jpeg)
![bus3](https://user-images.githubusercontent.com/64815890/83317216-517f4000-a1e8-11ea-98dd-2a9b1e8e67d5.jpeg)
![camion](https://user-images.githubusercontent.com/64815890/83317220-52b06d00-a1e8-11ea-9fe3-2f776dee25f6.jpeg)
