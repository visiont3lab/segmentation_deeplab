# Green-Screen: Segmentation with Deeplab V3.1+

## Introduction
We applied the deeplabv3 network to segment people inside an image. We extract the generated segmented masks and we replaced the background with a custom image. The effect is similar to a green screen.

## Requirements

* [Install docker](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-18-04)
* [Install nvidia-docker2](https://github.com/NVIDIA/nvidia-docker)

## Setup

```
cd $HOME
git clone https://github.com/visiont3lab/segmentation_deeplab.git
echo "export SEGMENTATION_DEEPLAB=$HOME/segmentation_deeplab" >> $HOME/.bashrc && source $HOME/.bashrc
```

## Run

```
xhost +local:docker && \
    docker run --runtime=nvidia  --rm  \
        -it --name deep_learning_segmentation_deeplab  \
        --env="DISPLAY=$DISPLAY" --env="QT_X11_NO_MITSHM=1" \
        --volume="/tmp/.X11-unix:/tmp/.X11-unix:rw" --device=/dev/video0  \
        -v $SEGMENTATION_DEEPLAB:/root/home/ws \
        visiont3lab/deep-learning:segmentation_deeplab \
        /bin/bash -c "cd /root/home/ws/ && python3 segmentation.py"
```

## References
[DeepLab Paper](https://arxiv.org/pdf/1606.00915) <br>
[DeepLab tensorflow](https://github.com/tensorflow/models/tree/master/research/deeplab) <br>
[Reference Repository](https://github.com/Golbstein/Keras-segmentation-deeplab-v3.1) <br>
[DeepLab Article](https://www.novatec-gmbh.de/blog/semantic-segmentation-part-1-deeplab-v3/)
