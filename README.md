# Neural Style Transfer - PyTorch Implementation

<div align="center">
 <img src="https://user-images.githubusercontent.com/50144683/235256418-05c08a1b-46b4-4994-a15b-e68def61a259.jpg" width="309px" height="223px">
 <img src="https://user-images.githubusercontent.com/50144683/235256454-f49e4e12-9d4e-4c44-9997-2b8a2ec24b38.jpg" height="223px">
 <img src="https://user-images.githubusercontent.com/50144683/235256661-4e6d3458-f29c-46a6-9853-b1baaf7e3c2f.jpg" width="710px"></br>
An example that maps the artistic style of The Mosaic onto an anime character:
</div>
</br>

This repository contains the Pytorch implementation of the following paper:
>**A Neural Algorithm of Artistic Style**</br>
>Leon A. Gatys, Alexander S. Ecker, Matthias Bethge</br>
>https://arxiv.org/abs/1508.06576
>
>**Abstract:** _In fine art, especially painting, humans have mastered the skill to create unique visual experiences through composing a complex interplay between the content and style of an image. Thus far the algorithmic basis of this process is unknown and there exists no artificial system with similar capabilities. However, in other key areas of visual perception such as object and face recognition near-human performance was recently demonstrated by a class of biologically inspired vision models called Deep Neural Networks. Here we introduce an artificial system based on a Deep Neural Network that creates artistic images of high perceptual quality. The system uses neural representations to separate and recombine content and style of arbitrary images, providing a neural algorithm for the creation of artistic images. Moreover, in light of the striking similarities between performance-optimised artificial neural networks and biological vision, our work offers a path forward to an algorithmic understanding of how humans create and perceive artistic imagery._

## Architecture
<img src="https://user-images.githubusercontent.com/50144683/235258076-9dc4a505-b59c-4206-9bc6-18fefb3510d6.png">
Using a Deep Residual Convolutional Neural Network as an Image Transformation Network (ITN). We train the ITN to transform input images into output images. We use a VGG16 which is pre-trained on ImageNet dataset as Loss Network to define two Perceptual Losses (Feature Reconstruction Loss & Style Reconstruction Loss) that measure perceptual differences in content and style between images.

## Download Dataset
I have download the `Human Faces' dataset from [Kaggle](https://www.kaggle.com/datasets/ashwingupta3012/human-faces).
+ Create a folder `dataset` in the root folder.
  - Extract the zip file and place the folder inside the 'dataset' folder 

## Train
```
python train.py  --dataset_path <path-to-dataset> \
                  --style_image <path-to-style-image> \
                  --epochs 1 \
                  --batch_size 4 \
                  --image_size 256
```
+ We can replace above `<path-to-dataset>` with `dataset/`
+ The `style_image` argument will consider `Mosaic Style` by default in the directlory `images/styles/mosaic.jpg`.


| Mosaic Style | Starry-Night Style | Illusion Style |
| --------------------------------- | --------------------------------- | --------------------------------- |
|<img src="https://user-images.githubusercontent.com/50144683/235258673-9b9a621b-f010-4757-80a8-b98450ae37ca.jpg" >| <img src="https://user-images.githubusercontent.com/50144683/235259271-032e91fb-3977-4fc4-b14d-a121b9949267.jpg"> | <img src="https://user-images.githubusercontent.com/50144683/235259356-e5de0d90-4901-4982-8505-cab909537203.jpg"> |
<p align="center">
    Figure: Training progress over the first 10,000 batches on different styles.
</p>

## Test on Image
The `checkpoints` directory contins models which I have trained on 3 different styles
```
python test_on_image.py  --image_path <path-to-image> \
                          --checkpoint_model <path-to-checkpoint> \
```
+ The Stylized images will be save the directory `images/outputs`

## Test on Video
We need to install FFmpeg to stylize a video.
+ Download FFmpeg from [here](https://ffmpeg.org/download.html)
+ Extract the files and place in the directory `C:\ffmpeg`
+ Add the location of ffmpeg.exe in the PATH variable and restart the system.
```
python test_on_video.py  --video_path <path-to-video> \
                          --checkpoint_model <path-to-checkpoint> \
```
<p align="center">
<video src="https://user-images.githubusercontent.com/50144683/235264892-02fec52f-4340-46f2-accb-5677a44614e2.mp4" width="75px">
</p>


