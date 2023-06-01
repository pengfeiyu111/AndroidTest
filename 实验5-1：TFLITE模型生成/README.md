```python
import os
```


```python
import numpy as np
```


```python
import tensorflow as tf
```


```python
assert tf.__version__.startswith('2')
```


```python
from tflite_model_maker import model_spec
```


```python
from tflite_model_maker import image_classifier
```


```python
from tflite_model_maker.config import ExportFormat
```


```python
from tflite_model_maker.config import QuantizationConfig
```


```python
from tflite_model_maker.image_classifier import DataLoader
```


```python
import matplotlib.pyplot as plt
```


```python
image_path = tf.keras.utils.get_file(
      'flower_photos.tgz',
      'https://storage.googleapis.com/download.tensorflow.org/example_images/flower_photos.tgz',
      extract=True)
image_path = os.path.join(os.path.dirname(image_path), 'flower_photos')

```


```python
data = DataLoader.from_folder(image_path)
train_data, test_data = data.split(0.9)

```

    INFO:tensorflow:Load image with size: 3670, num_label: 5, labels: daisy, dandelion, roses, sunflowers, tulips.
    

    INFO:tensorflow:Load image with size: 3670, num_label: 5, labels: daisy, dandelion, roses, sunflowers, tulips.
    


```python
model = image_classifier.create(train_data)

```

    INFO:tensorflow:Retraining the models...
    

    INFO:tensorflow:Retraining the models...
    

    Model: "sequential"
    _________________________________________________________________
     Layer (type)                Output Shape              Param #   
    =================================================================
     hub_keras_layer_v1v2 (HubKe  (None, 1280)             3413024   
     rasLayerV1V2)                                                   
                                                                     
     dropout (Dropout)           (None, 1280)              0         
                                                                     
     dense (Dense)               (None, 5)                 6405      
                                                                     
    =================================================================
    Total params: 3,419,429
    Trainable params: 6,405
    Non-trainable params: 3,413,024
    _________________________________________________________________
    None
    Epoch 1/5
    

    2023-06-01 01:24:07.092395: W tensorflow/core/framework/cpu_allocator_impl.cc:82] Allocation of 19267584 exceeds 10% of free system memory.
    2023-06-01 01:24:07.143428: W tensorflow/core/framework/cpu_allocator_impl.cc:82] Allocation of 19267584 exceeds 10% of free system memory.
    2023-06-01 01:24:07.169141: W tensorflow/core/framework/cpu_allocator_impl.cc:82] Allocation of 51380224 exceeds 10% of free system memory.
    2023-06-01 01:24:07.209881: W tensorflow/core/framework/cpu_allocator_impl.cc:82] Allocation of 19267584 exceeds 10% of free system memory.
    2023-06-01 01:24:07.279806: W tensorflow/core/framework/cpu_allocator_impl.cc:82] Allocation of 19267584 exceeds 10% of free system memory.
    

    103/103 [==============================] - 58s 542ms/step - loss: 0.8513 - accuracy: 0.7840
    Epoch 2/5
    103/103 [==============================] - 55s 532ms/step - loss: 0.6543 - accuracy: 0.8908
    Epoch 3/5
    103/103 [==============================] - 54s 524ms/step - loss: 0.6156 - accuracy: 0.9187
    Epoch 4/5
    103/103 [==============================] - 54s 525ms/step - loss: 0.5957 - accuracy: 0.9290
    Epoch 5/5
    103/103 [==============================] - 54s 519ms/step - loss: 0.5811 - accuracy: 0.9381
    


```python
loss, accuracy = model.evaluate(test_data)
```

    12/12 [==============================] - 8s 493ms/step - loss: 0.6331 - accuracy: 0.8937
    


```python
model.export(export_dir='.')

```

    2023-06-01 01:28:50.470787: W tensorflow/python/util/util.cc:368] Sets are not currently considered sequences, but this may change in the future, so consider avoiding using them.
    

    INFO:tensorflow:Assets written to: /tmp/tmpcd41z7xz/assets
    

    INFO:tensorflow:Assets written to: /tmp/tmpcd41z7xz/assets
    2023-06-01 01:28:55.242636: I tensorflow/core/grappler/devices.cc:66] Number of eligible GPUs (core count >= 8, compute capability >= 0.0): 0
    2023-06-01 01:28:55.242816: I tensorflow/core/grappler/clusters/single_machine.cc:358] Starting new session
    2023-06-01 01:28:55.321843: I tensorflow/core/grappler/optimizers/meta_optimizer.cc:1164] Optimization results for grappler item: graph_to_optimize
      function_optimizer: Graph size after: 913 nodes (656), 923 edges (664), time = 23.46ms.
      function_optimizer: function_optimizer did nothing. time = 0.015ms.
    
    /opt/conda/envs/tf/lib/python3.8/site-packages/tensorflow/lite/python/convert.py:746: UserWarning: Statistics for quantized inputs were expected, but not specified; continuing anyway.
      warnings.warn("Statistics for quantized inputs were expected, but not "
    2023-06-01 01:28:56.145905: W tensorflow/compiler/mlir/lite/python/tf_tfl_flatbuffer_helpers.cc:357] Ignored output_format.
    2023-06-01 01:28:56.145963: W tensorflow/compiler/mlir/lite/python/tf_tfl_flatbuffer_helpers.cc:360] Ignored drop_control_dependency.
    

    INFO:tensorflow:Label file is inside the TFLite model with metadata.
    

    fully_quantize: 0, inference_type: 6, input_inference_type: 3, output_inference_type: 3
    INFO:tensorflow:Label file is inside the TFLite model with metadata.
    

    INFO:tensorflow:Saving labels in /tmp/tmpbomj3vnc/labels.txt
    

    INFO:tensorflow:Saving labels in /tmp/tmpbomj3vnc/labels.txt
    

    INFO:tensorflow:TensorFlow Lite model exported successfully: ./model.tflite
    

    INFO:tensorflow:TensorFlow Lite model exported successfully: ./model.tflite
    
