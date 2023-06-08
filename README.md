# FLAVR
## 模型介绍
FLAVR是一种用于视频插值的深度学习模型，可以通过插值技术将低帧率视频转换为高帧率视频。
## 模型结构
3D U-Net结构、encoder部分采用ResNet-3D，decoder部分采用3D TransConv，以及Spatio-Temporal Feature Gating

## 数据集
目前模型在Vimeo-90K 数据集上训练

可以通过[此链接](http://toflow.csail.mit.edu/)进行数据下载

## 训练及推理
### 环境配置
python依赖安装：

    Python==3.7.11
    numpy==1.19.2
    PyTorch ==1.10.0a0+git2040069.dtk2210
### 训练
训练命令：

    python main.py --batch_size 32 \
                   --test_batch_size 32 \
                   --dataset vimeo90K_septuplet \
                   --loss 1*L1 \
                   --max_epoch 200 \
                   --lr 0.0002 \
                   --data_root <dataset_path> \
                   --n_outputs 1

GoPro 数据集上的训练类似，更改`n_outputs`为 7 以进行 8 倍插值。



## 性能和准确率数据
测试数据：[test data](http://toflow.csail.mit.edu/)，使用的加速卡:2张 DCU。


## 源码仓库及问题反馈
* [https://github.com/tarun005/FLAVR](https://github.com/tarun005/FLAVR)
## 参考
* [https://github.com/tarun005/FLAVR](https://github.com/tarun005/FLAVR)
