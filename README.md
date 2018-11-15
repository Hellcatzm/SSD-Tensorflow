# SSD源码详解

这是网上一个经典的SSD_TF版本项目，我对于训练过程给出了较为详细的注释，另外援引了其他人的模型应用于自己的数据的脚本，记录一下对这个开源项目的学习。<br>
[『TensorFlow』SSD源码学习_其一：项目介绍导读](https://www.cnblogs.com/hellcat/p/9248489.html)<br>
[『TensorFlow』SSD源码学习_其二：基于VGG的SSD网络前向架构](https://www.cnblogs.com/hellcat/p/9312881.html)<br>
[『TensorFlow』SSD源码学习_其三：搜索网格生成](https://www.cnblogs.com/hellcat/p/9322279.html)<br>
[『TensorFlow』SSD源码学习_其四：数据介绍及TFR文件生成](https://www.cnblogs.com/hellcat/p/9338093.html)<br>
[『TensorFlow』SSD源码学习_其五：TFR数据读取&数据预处理](https://www.cnblogs.com/hellcat/p/9341921.html)<br>
[『TensorFlow』SSD源码学习_其六：标注格式整理](https://www.cnblogs.com/hellcat/p/9355609.html)<br>
[『TensorFlow』SSD源码学习_其七：损失函数](https://www.cnblogs.com/hellcat/p/9351802.html)<br>
[『TensorFlow』SSD源码学习_其八：网络训练](https://www.cnblogs.com/hellcat/p/9360640.html)<br>
个人复现的SSD:<br>
[SSD_Realization_TensorFlow](https://github.com/Hellcatzm/SSD_Realization_TensorFlow)<br>
[SSD_Realization_MXNet](https://github.com/Hellcatzm/SSD_Realization_MXNet)<br>
还有Mask_RCNN的注释版：<br>
[Mask_RCNN](https://github.com/Hellcatzm/Mask_RCNN)<br>
#### 数据下载：[VOC2012](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar)<br>
#### 二进制数据生成：<br>
注意目录`./VOC2012/`里面就是VOC2012数据解压出来的五个文件夹下面命令才能运行<br>
```bash
DATASET_DIR=./VOC2012/
OUTPUT_DIR=./tfrecords
python tf_convert_data.py \
    --dataset_name=pascalvoc \  # 数据集名称，实际作者就实现了这一个数据集的预处理方法
    --dataset_dir=${DATASET_DIR} \
    --output_name=voc_2012_train  # tfr文件名，为了兼容后面的程序，命名格式较为固定
    --output_dir=${OUTPUT_DIR}
```
#### 训练命令：<br>
```bash
DATASET_DIR=./tfrecords
TRAIN_DIR=./logs/
CHECKPOINT_PATH=./checkpoints/ssd_300_vgg.ckpt
python train_ssd_network.py \
    --train_dir=${TRAIN_DIR} \
    --dataset_dir=${DATASET_DIR} \
    --dataset_name=pascalvoc_2012 \
    --dataset_split_name=train \
    --model_name=ssd_300_vgg \
    --checkpoint_path=${CHECKPOINT_PATH} \
    --save_summaries_secs=60 \
    --save_interval_secs=600 \
    --weight_decay=0.0005 \
    --optimizer=adam \
    --learning_rate=0.001 \
    --batch_size=32
```
