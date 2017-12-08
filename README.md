# Feature Pyramid Networks for Object Detection
A Tensorflow implementation of FPN detection framework.    
The paper references [Feature Pyramid Networks for Object Detection](https://arxiv.org/abs/1612.03144)    
Rotation detection method baesd on FPN reference [R2CNN](https://github.com/yangxue0827/R2CNN_FPN_Tensorflow) and [R-DFPN](https://github.com/yangxue0827/R-DFPN_FPN_Tensorflow)  
If useful to you, please star to support my work. Thanks.     

# Configuration Environment
ubuntu(Encoding problems may occur on windows) + python2 + tensorflow1.2 + cv2 + cuda8.0 + GeForce GTX 1080      
You can also use docker environment, command: docker push yangxue2docker/tensorflow3_gpu_cv2_sshd:v1.0     

# Make tfrecord   
The image name is best in English.   
The data is VOC format, reference [here](sample.xml)     
data path format  
VOCdevkit  
>VOCdevkit_train  
>>Annotation  
>>JPEGImages   

>VOCdevkit_test   
>>Annotation   
>>JPEGImages   

python ./data/io/convert_data_to_tfrecord.py --VOC_dir='***/VOCdevkit/VOCdevkit_train/' --save_name='train' --img_format='.jpg' --dataset='ship'

# Demo  
1、Unzip the weight ./output/res101_trained_weights/*.rar   
2、put images in ./tools/inference_image  
3、python ./tools/inference.py   

# Train
1、Configure parameters in ./libs/configs/cfgs.py and modify the project's root directory    
2、Modify ./libs/lable_name_dict/***_dict.py, corresponding to the number of categories in the configuration file    
3、download pretrain weight([resnet_v1_101_2016_08_28.tar.gz](http://download.tensorflow.org/models/resnet_v1_101_2016_08_28.tar.gz) or [resnet_v1_50_2016_08_28.tar.gz](http://download.tensorflow.org/models/resnet_v1_50_2016_08_28.tar.gz)) from [here](https://github.com/yangxue0827/models/tree/master/slim), then extract to folder ./data/pretrained_weights    
4、python ./tools/train.py

# Test tfrecord     
mkdir test_result    
python ./tools/test.py  

# eval    
python ./tools/ship_eval.py

# Summary   
tensorboard --logdir=./output/res101_summary/   
![01](output/res101_summary/fast_rcnn_loss.bmp) 
![02](output/res101_summary/rpn_loss.bmp) 
![03](output/res101_summary/total_loss.bmp) 

# Graph
![04](graph.png) 

# Test results    
## airplane
![11](tools/test_result/00_gt.jpg)   
![12](tools/test_result/00_fpn.jpg)  
 
## sar_ship
![13](tools/test_result/01_gt.jpg)   
![14](tools/test_result/01_fpn.jpg)  

## ship
![15](tools/test_result/02_gt.jpg)    
![16](tools/test_result/02_fpn.jpg)      

# Note 
This code works better when detecting single targets, but not suitable for multi-target detection tasks. Hope you can help find bugs, thank you very much.    
    