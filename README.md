# supervised-avanzado-mit-face-recognition-solution

# Reto MIT Face Recognition
## Descripción
El [MIT Face Database](http://cbcl.mit.edu/software-datasets/heisele/facerecognition-database.html) es un conjunto de 2000 imágenes de caras de 10 personas distintas, desde diferentes ángulos, variando el fondo y la iluminación. El tamaño de las imágenes de variable pero oscila entre 100 y 200 pixeles para cada dimensión y las caras no se encuentran centradas en la imagen.


<img src="https://raw.githubusercontent.com/charlielito/supervised-intermedio-mit-face-recognition/master/set.jpg" alt="Drawing" width="400" height="200" >

El reto es construir un clasificador de imágenes que sea capaz de reconocer las 10 personas.

### Ranking
Ver [ranking](https://github.com/charlielito/supervised-intermedio-mit-face-recognition/blob/master/ranking.md).

### Formato Datos
Todos los datos están en la carpeta `.dataget/data/mit-face-rec` y se dividen en 2 grupos
```
|- .dataget
   |- data
      |- mit-face-rec
         |- traning-set
         |- test-set
```

**Estructura** <br>
Cada sub conjunto de datos (training-set o test-set) tiene la siguiente estructura
```
|- {subset}
   |- {class_id}
      |- {image_id}.pgm
```
Donde
* `subset`: es `training-set` o `test-set`
* `class_id`: es el identificador de una clase, e.g. 0, 2, ..., 9
* `image_id`: es el nombre de una imagen.

### Variables
Cada imagen como tal puede ser representada por una matriz de dimensiones `height x width` dado que estan en escala de grises.

### Objetivo
1. Crear un algoritmo que tome una imagen de entrada, ya sea como vector o matriz, y retorne el clase (`class_id`) a la que pertenece esa imagen.
1. Entrenar este algoritmo utilizando los datos de la carpeta `data/training-set`.
1. Medir el performance/score del algoritmo utilizando los datos de la carpeta `data/test-set`. El performance debe ser medido como
```python
score = n_aciertos / n_imagenes * 100
```
donde `n_aciertos` es el numero de imagenes clasificadas de forma correcta y `n_imagenes` es el numero total de imagenes en el `test-set`.

## Solución
Ver procedimiento de [solución](https://github.com/colomb-ia/formato-retos#solucion)

#### Requerimientos
*Keras*
*Tensorflow*

#### Procedimiento
La Solución se encuentra en el archivo [python-sample-Solution MIT faces.ipynb](https://github.com/jcvasquezc/supervised-avanzado-mit-face-recognition-solution/master/python-sample-Solution-MIT-faces.ipynb)

1. Se estandarizan los conjuntos e entrenamiento y test para tener media ceero y desviaci+on estándar 1, con base en el conjunto de entrenamiento, de la siguiente forma

```python
avg_image=np.mean(featuresTrain,0)
std_image=np.std(featuresTrain,0)

featuresTrain=(featuresTrain-avg_image)/std_image
featuresTest=(featuresTest-avg_image)/std_image```
```

1. Se construye y entrena un modelo basado en una red neuronal recurrente con unidades de memoria LSTM [RNN-LSTM](https://en.wikipedia.org/wiki/Long_short-term_memory) con 64 unidades en su capa oculta

1. Se predice el resultado en el conjunto de test, y se calcula ta sa de aciertos y la matriz de confusión. 

#### Método
Se utilizó una red neuronal recurrente (RNN) con unidades de memoria LSTM (RNN-LSTM) la cual permite analizar la dependencia de los pixels de la imagen del rostro con sus vecinos.

#### Resultados
99.9999999999999999999\%

![Matriz de confusion](https://github.com/jcvasquezc/supervised-avanzado-mit-face-recognition-solution/master/cmLSTMpng)
![perdidas](https://github.com/jcvasquezc/supervised-avanzado-mit-face-recognition-solution/master/lossLSTM.png)


### Requerimientos
Para descargar y visualizar los datos necesitas Python 2 o 3. Las dependencias las puedes encontrar en el archivo `requirements.txt`, el cual incluye
* pillow
* dataget
* numpy
* selenium
* jupyter
* Keras
* Tensorflow



