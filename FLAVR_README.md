# 简介

FLAVR是一种用于视频插值的深度学习模型，可以通过插值技术将低帧率视频转换为高帧率视频。它通过对低帧率视频进行逐帧处理，并使用深度学习网络来推断丢失的帧，以生成更平滑的高帧率视频。相比传统的插值算法，FLAVR能够生成更加自然和逼真的高帧率视频，并且可以处理复杂的场景和动作。 

# 测试流程

## 安装工具包

pytorch1.10版本[1.10.0a0+git2040069-dtk2210]

## 加载环境变量

```
export PATH={PYTHON3_install_dir}/bin:$PATH

export LD_LIBRARY_PATH={PYTHON3_install_dir}/lib:$LD_LIBRARY_PATH
```

## 下载数据集

Vimeo-90K septuplet 数据集

[vimeo_triplet](http://data.csail.mit.edu/tofu/dataset/vimeo_triplet.zip)

# 运行指令

## 在 Vimeo-90K septuplets 上训练模型

要在 Vimeo-90K 数据集上训练您自己的模型，请使用以下命令。[您可以从此链接](http://toflow.csail.mit.edu/)下载数据集(至少需要2个DCU)。

```
python main.py --batch_size 32 --test_batch_size 32 --dataset vimeo90K_septuplet --loss 1*L1 --max_epoch 200 --lr 0.0002 --data_root <dataset_path> --n_outputs 1
```

GoPro 数据集上的训练类似，更改`n_outputs`为 7 以进行 8 倍插值。

## 直接进行模型下载

您可以从以下链接下载预训练的 FLAVR 模型。

| 方法    | 训练好的模型                                                 |
| ------- | ------------------------------------------------------------ |
| **2倍** | [关联](https://drive.google.com/drive/folders/1M6ec7t59exOSlx_Wp6K9_njBlLH2IPBC?usp=sharing) |
| **4倍** | [关联](https://drive.google.com/file/d/1btmNm4LkHVO9gjAaKKN9CXf5vP7h4hCy/view?usp=sharing) |
| **8倍** | [关联](https://drive.google.com/drive/folders/1Gd2l69j7UC1Zua7StbUNcomAAhmE-xFb?usp=sharing) |

### Middleburry 评价

要在 Middleburry 的公共基准上进行评估，请运行以下命令。

```
python Middleburry_Test.py --data_root <data_path> --load_from <model_path> 
```

# 参考

[https://github.com/tarun005/FLAVR](https://github.com/tarun005/FLAVR)