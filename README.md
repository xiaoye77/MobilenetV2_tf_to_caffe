# MobilenetV2_tf_to_caffe
convert tensorflow mobilenet-v2 checkpoint to caffemodel


Requirements:
1. pycaffe
2. tensorflow >= 1.5
Clone https://github.com/tensorflow/models, and put 'models' folder in this repository


To convert tf mobilenet_v2 to caffe model:

1. Prepare checkpoints of mobilenet_v2:
$ sh download.sh mobilenet_v2_1.0_224

See: https://github.com/tensorflow/models/tree/master/research/slim/nets/mobilenet


2. Restore tensorflow graph from checkpoint and revise protxt:
$ python generate_prototxt.py --factor 1.0 --image_scale 224 

(for mobilenet_v2_1.0_224)

revised prototxt will be generated in prototxt_mobilenet_v2/ directory.


3. Convert variables to caffe parameters:
$ python convert_v2.py --factor 1.0 --image_scale 224

caffemodel will be generated in caffemodel_fromckpt/ directory.


Note:
1. Fix padding problem by using pad=2 and slicing layers.
2. Set epsilon to 1e-3 in batch_norm layer which is equal to tensorflow.
3. ReLU6 not solved, but result is OK.
