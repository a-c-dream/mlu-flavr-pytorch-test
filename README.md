# FLAVR

## 论文

` FLAVR: Flow-Agnostic Video Representations for Fast Frame Interpolation `

- https://arxiv.org/pdf/2012.08512.pdf

## 模型结构
 FLAVR模型是一个3D U-Net模型，通过拓展2D U-Net，将2D卷积替换为3D卷积而得到的。该模型能够更准确地对输入帧之间的时间动态进行建模，从而获得更好的插值质量。 

![](https://developer.hpccube.com/codes/modelzoo/flavr_pytorch/-/raw/master/doc/arch_dia.png)

## 算法原理

  3D U-Net结构、encoder部分采用ResNet-3D，decoder部分采用3D TransConv，以及Spatio-Temporal Feature Gating ![](https://developer.hpccube.com/codes/modelzoo/flavr_pytorch/-/raw/master/doc/%E5%8E%9F%E7%90%86.png)

## 环境配置

### Docker（方法一）

此处提供[光源](https://www.sourcefind.cn/#/service-details)拉取docker镜像

```
docker pull image.sourcefind.cn:5000/dcu/admin/base/pytorch:1.10.0-centos7.6-dtk-22.10-py37-latest
docker run -it --network=host --name=flavr --privileged --device=/dev/kfd --device=/dev/dri --ipc=host --shm-size=32G  --group-add video --cap-add=SYS_PTRACE --security-opt seccomp=unconfined -u root --ulimit stack=-1:-1 --ulimit memlock=-1:-1 image.sourcefind.cn:5000/dcu/admin/base/pytorch:1.10.0-centos7.6-dtk-22.10-py37-latest
pip install -r requirements.txt
```

### Dockerfile（方法二）

dockerfile使用方法

```
docker build --no-cache -t flavr:latest .
docker run -dit --network=host --name=flavr --privileged --device=/dev/kfd --device=/dev/dri --ipc=host --shm-size=16G  --group-add video --cap-add=SYS_PTRACE --security-opt seccomp=unconfined -u root --ulimit stack=-1:-1 --ulimit memlock=-1:-1 flavr:latest
docker exec -it flavr /bin/bash
```

### Anaconda（方法三）

关于本项目DCU显卡所需的特殊深度学习库可从[光合](https://developer.hpccube.com/tool/)开发者社区下载安装。

```
DTK驱动：dtk22.10
python：python3.7
torch==1.10.0a0+git2040069.dtk2210
torchvision==0.10.0a0+e04d001.dtk2210
```

`Tips：以上dtk驱动、python等DCU相关工具版本需要严格一一对应`

其它非深度学习库参照requirements.txt安装：

```
pip install -r requirements.txt
pip install tensorboard setuptools==57.5.0 six
```

## 数据集

`模型使用数据为 Vimeo-90K `

-  http://toflow.csail.mit.edu/

项目中已提供用于试验训练的迷你数据集，训练数据目录结构如下，用于正常训练的完整数据集请按此目录结构进行制备：

```
 ── datasets
   │   ├── readme.txt
   │   ├── sep_testlist.txt 
   │   ├── sep_trainlist.txt 
   │   ├── sequences
          │    ├── xx/xx/xxx.png
          │    ├── xx/xx/xxx.png
```




## 训练
### 单机单卡

```
python main.py --batch_size 32 --test_batch_size 32 --dataset vimeo90K_septuplet --loss 1*L1 --max_epoch 200 --lr 0.0002 --data_root datasets --n_outputs 1 --num_gpu 1
```

### 单机多卡

```
python main.py --batch_size 32 --test_batch_size 32 --dataset vimeo90K_septuplet --loss 1*L1 --max_epoch 200 --lr 0.0002 --data_root datasets --n_outputs 1 --num_gpu 4
```

## 推理

    python test.py --dataset vimeo90K_septuplet --data_root <data_path> --load_from <saved_model> --n_outputs 1

## result

测试图

![](https://developer.hpccube.com/codes/modelzoo/flavr_pytorch/-/raw/master/doc/sprite.gif)

### 精度

测试数据：http://toflow.csail.mit.edu/，使用的加速卡:Z100L。

根据测试结果情况填写表格：

|  FLAVR   |   PSNR    | SSIM     |
| :------: | :-------: | -------- |
| vimeo-90 | 18.511020 | 0.702564 |

## 应用场景

### 算法类别

`图像超分`

### 热点应用行业

`设计`,`制造`,`其它`

## 源码仓库及问题反馈

*   https://developer.hpccube.com/codes/modelzoo/flavr_pytorch 
## 参考资料
*  https://github.com/tarun005/FLAVR 

