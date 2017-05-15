# Protobuf-Dreamer
A tiled DeepDream project for creating any size of image, on both CPU and GPU. Tensorflow should be compiled for either the CPU, or GPU depending on what your prefer. The CPU is slower, but this project should allow anyone to create an image of any size. The tiling code is based on [jnordberg](https://github.com/jnordberg)'s [DreamCanvas](https://github.com/jnordberg/dreamcanvas) project.

In order to control the desired output size, resize your image prior to running `pb_dreamer.py`. Any "blurriness" caused by resizing a smaller image to a larger size, should disappear after the DeepDream process. 


### Dependencies: 

`sudo apt-get install python-skimage`

`sudo apt-get install python-pip`

`sudo pip install numpy`

`sudo pip install scipy`

`sudo pip install tensorflow` or `sudo pip install tensorflow-gpu`

Refer to the Tensorflow installation and setup guide for more info: https://www.tensorflow.org/install/

### Setup:

Run the following to download and setup the default model:

`git clone https://github.com/ProGamerGov/Protobuf-Dreamer`

`cd Protobuf-Dreamer` 

`wget https://storage.googleapis.com/download.tensorflow.org/models/inception5h.zip`

`unzip -d model inception5h.zip`

For a full list of layers, see [here](https://github.com/ProGamerGov/Protobuf-Dreamer/blob/master/examples/inception5h/model_info.txt).

### Usage: 

Basic usage: 

```
python pb_dreamer.py --input_image input.png
```

Advanced usage: 

```
python pb_dreamer.py --input_image input.png --output_image output.png --octaves 4 --layer mixed4d_3x3_bottleneck_pre_relu --channel 139 --iter 10 --tile_size 512 --model /home/ubuntu/Protobuf-Dreamer/model/tensorflow_inception_graph.pb
```

### Parameters: 

* `--input_image`: The input image for performing DeepDream on. Ex: `input.png`

* `--output_image`: The name of your output image. Ex: `output.png`

* `--layer`: The target layer. Ex: `mixed4d_3x3_bottleneck_pre_relu`.

* `--channel`: The desired channel of the target layer. Ex: `139`.

* `--tile_size`: The desired size of tiles to use. Ex: `512`.

* `--iter`: The number of iterations. Ex: `10`.

* `--octaves`: The number of octaves. Ex: `4`.

* `--model`: Path to the `.pb` model file. Default is `tensorflow_inception_graph.pb`.


### Channels: 

Using the `--channel` parameter, you can use hundreds of additional "mini layers" inside each main layer: 

Examples: 

* 64 channels (00-63) from the `mixed4c_pool_reduce` layer: https://i.imgur.com/gIJSF17.jpg

* 96 channels (00-95) from the `mixed4a_3x3_bottleneck_pre_relu` layer: https://i.imgur.com/Oglnt4p.jpg

* 100 channels (00-99) from the `mixed5a_1x1` layer: https://i.imgur.com/64BKrJt.jpg

* 101 channels (100-200) from the `mixed5a_1x1` layer: https://i.imgur.com/icJjqm9.jpg

The most interesting layers and channels that I have come across, are [listed here](https://github.com/ProGamerGov/Protobuf-Dreamer/wiki/Interesting-Layers-And-Channels).

A list of all the potential things you can find in the layer channels of the inception5h model, can be [found here](https://github.com/ProGamerGov/Protobuf-Dreamer/blob/master/examples/inception5h/imagenet_comp_graph_label_strings.txt).

### Examples:


<img src="https://raw.githubusercontent.com/ProGamerGov/Protobuf-Dreamer/master/examples/inception5h/mixed5c_pool_reduce_61.jpg" width="720" height="720">

* `--model inception5h.pb`
* `--layer mixed4c_pool_reduce` 
* `--channel 61`

<img src="https://raw.githubusercontent.com/ProGamerGov/Protobuf-Dreamer/master/examples/inception5h/mixed4d_3x3_bottleneck_pre_relu_139.jpg" width="720" height="720">

* `--model inception5h.pb`
* `--layer mixed4d_3x3_bottleneck_pre_relu` 
* `--channel 139`

<img src="https://raw.githubusercontent.com/ProGamerGov/Protobuf-Dreamer/master/examples/inception5h/mixed3a_pool_reduce_13.jpg" width="720" height="720">

* `--model inception5h.pb`
* `--layer mixed3a_pool_reduce` 
* `--channel 13`

<img src="https://github.com/ProGamerGov/Protobuf-Dreamer/raw/master/examples/inception5h/mixed4a_3x3_bottleneck_pre_relu_51.jpg" width="720" height="720">

* `--model inception5h.pb`
* `--layer mixed4a_3x3_bottleneck_pre_relu` 
* `--channel 51`

