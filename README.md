# VehicleReID

## Experiment Results

```
# code: /home/lmb/proj/vehicle-reid
# experiment: /media/disk1/lmb/EXP
# resnet50_fc256 pretrain model: /media/disk1/lmb/EXP/exp-vehicle-reid/train-ve1m+veid+veri/model_59.pt
```

### Train in VehicleID (13.164k)

```bash
# /home/lmb/proj/vehicle-reid/train_id.sh
python train_xent_tri.py \
-s vehicleid \  # 训练集名称
-t vehicleid \  # 测试集名称
--height 128 \
--width 256 \
--optim amsgrad \
--lr 0.0003 \
--max-epoch 60 \
--stepsize 20 40 \
--train-batch-size 512 \
--test-batch-size 100 \
-a resnet50 \  # resnet50模型的特征维度2048
--save-dir /media/disk1/lmb/log/exp \
--gpu-devices "0, 1, 2, 3" \
--use-avai-gpus \
--test-size 800 \  # 测试集大小
--workers 4

# /home/lmb/proj/vehicle-reid/test_id.sh
python train_xent_tri.py \
-s vehicleid \  # 训练集名称
-t vehicleid \  # 测试集名称
--height 128 \
--width 256 \
--test-size 800 \
--train-batch-size 1 \
--test-batch-size 512 \
--evaluate \ 
-a resnet50 \ # resnet50模型的特征维度2048
--load-weights /media/disk1/lmb/EXP/exp-vehicle-reid/train-1m/model_best.pth \
--save-dir /media/disk1/lmb/EXP/exp-vehicle-reid/test-1m-id \
--root /media/disk1/lmb/DATASET/ \
--gpu-devices "0, 1, 2, 3" \
--use-avai-gpus
```



| **train (size)** | **test (size)**     | **h w** | **mAP** | **Rank-1** | **Rank-5** | **Rank-10** | **Rank-20** |
| ---------------- | ------------------- | ------- | ------- | ---------- | ---------- | ----------- | ----------- |
| VehicleID (13k)  | VehicleID (0.8k)    | 128 256 | 81.8    | 74.6       | 91.1       | 95.0        | 97.2        |
| VehicleID (13k)  | VehicleID (1.6k)    | 128 256 | 77.5    | 70.3       | 86.3       | 91.3        | 94.6        |
| VehicleID (13k)  | VehicleID (2.4k)    | 128 256 | 74.8    | 67.5       | 83.8       | 89.1        | 92.7        |
| VehicleID (13k)  | VehicleID (3.2k)    | 128 256 | 72.2    | 64.9       | 80.6       | 86.4        | 91.2        |
| VehicleID (13k)  | VehicleID (6.0k)    | 128 256 | 66.7    | 59.3       | 74.8       | 80.9        | 86.7        |
| VehicleID (13k)  | VehicleID (13.164k) | 128 256 | 61.6    | 54.2       | 69.6       | 75.2        | 80.9        |

| **train (size)**    | **test (size)**     | **h w**  | **mAP** | **Rank-1** | **Rank-5** | **Rank-10** | **Rank-20** |
| ------------------- | ------------------- | -------- | ------- | ---------- | ---------- | ----------- | ----------- |
| VehicleID (13k)     | Vehicle-1M (1k)     | 128 256  | 70.3    | 62.8       | 78.8       | 83.6        | 88.1        |
| VehicleID (13k)     | Vehicle-1M (2k)     | 128 256  | 63.4    | 54.9       | 73.2       | 78.8        | 83.9        |
| VehicleID (13k)     | Vehicle-1M (3k)     | 128 256  | 60.4    | 51.5       | 70.8       | 76.7        | 81.9        |
| VehicleID (13k)     | Vehicle-1M (5.527k) | 128 256  | 55.1    | 46.3       | 65.3       | 71.5        | 77.0        |



### Train in Vehicle-1M (930k)

```bash
# /home/lmb/proj/vehicle-reid/train_1m.sh
python train_xent_tri.py \
-s vehicle1m \  # 训练集名称
-t vehicle1m \  # 测试集名称
--height 128 \
--width 256 \
--optim amsgrad \
--lr 0.0003 \
--max-epoch 60 \
--stepsize 20 40 \
--train-batch-size 256 \
--test-batch-size 100 \
-a resnet50 \ # resnet50模型的特征维度2048
--save-dir /media/disk1/lmb/EXP/exp-vehicle-reid/train-1m \
--gpu-devices "0, 1, 2, 3" \
--use-avai-gpus \
--test-size 1000 \  # 测试集大小
--workers 32 \
--root /media/disk1/lmb/DATASET/ \
--resume /media/disk1/lmb/EXP/exp-vehicle-reid/train-1m/model_9.pt

# /home/lmb/proj/vehicle-reid/test_1m.sh
python train_xent_tri.py \
-s vehicle1m \  # 训练集名称
-t vehicle1m \  # 测试集名称
--height 128 \
--width 256 \
--test-size 5527 \  # 测试集大小
--train-batch-size 1 \ # 不起作用
--test-batch-size 512 \
--evaluate \
-a resnet50 \
--load-weights /media/disk1/lmb/EXP/exp-vehicle-reid/train-1m/model_best.pth \
--save-dir /media/disk1/lmb/EXP/exp-vehicle-reid/test-1m \
--root /media/disk1/lmb/DATASET/ \
--gpu-devices "0, 1, 2, 3" \
--use-avai-gpus
```



| **train (size)**  | **test (size)**     | **h w**  | **mAP** | **Rank-1** | **Rank-5** | **Rank-10** | **Rank-20** |
| ----------------- | ------------------- | -------- | ------- | ---------- | ---------- | ----------- | ----------- |
| Vehicle-1M (930k) | VehicleID (0.8k)    | 128  256 | 66.8    | 60.8       | 73.4       | 78.2        | 82.9        |
| Vehicle-1M (930k) | VehicleID (1.6k)    | 128 256  | 65.6    | 59.6       | 72.3       | 77.0        | 80.4        |
| Vehicle-1M (930k) | VehicleID (2.4k)    | 128 256  | 62.2    | 56.0       | 69.2       | 73.7        | 77.9        |
| Vehicle-1M (930k) | VehicleID (3.2k)    | 128 256  | 59.4    | 53.3       | 66.0       | 70.2        | 74.7        |
| Vehicle-1M (930k) | VehicleID (6.0k)    | 128 256  | 55.7    | 49.5       | 62.4       | 66.5        | 70.6        |
| Vehicle-1M (930k) | VehicleID (13.164k) | 128 256  | 51.0    | 44.7       | 58.1       | 62.7        | 66.9        |

| **train (size)**    | **test (size)**     | **h w**  | **mAP** | **Rank-1** | **Rank-5** | **Rank-10** | **Rank-20** |
| ------------------- | ------------------- | -------- | ------- | ---------- | ---------- | ----------- | ----------- |
| Vehicle-1M (930k)   | Vehicle-1M (1k)     | 128 256  | 96.7    | 95.0       | 98.8       | 99.1        | 99.3        |
| Vehicle-1M (930k)   | Vehicle-1M (2k)     | 128 256  | 92.6    | 90.7       | 94.9       | 95.6        | 96.3        |
| Vehicle-1M (930k)   | Vehicle-1M (3k)     | 128 256  | 92.1    | 89.2       | 95.7       | 96.8        | 97.6        |
| Vehicle-1M (930k)   | Vehicle-1M (5.527k) | 128 256  | 90.6    | 86.7       | 95.4       | 96.9        | 97.7        |



### Train in Vehicle-1M、VehicleID、VeRi (990k)

```bash
# /home/lmb/proj/vehicle-reid/train_ve1m+veid+veri.sh
python train_xent_tri.py \
-s vehicle1m vehicleid veri \  # 训练集名称（多个训练集）
-t vehicle1m vehicleid veri \  # 测试集名称（多个测试集）
--height 128 \
--width 256 \
--optim amsgrad \
--lr 0.0003 \
--max-epoch 60 \
--stepsize 20 40 \
--train-batch-size 256 \
--test-batch-size 100 \
-a resnet50_fc256 \  # 特征维度256
--save-dir /media/disk1/lmb/EXP/exp-vehicle-reid/train-ve1m+veid+veri \
--gpu-devices "0, 1, 2, 3" \
--use-avai-gpus \
--test-size 1000 \  # 测试集大小（多个测试集时，需要在代码里定义不同测试集的默认大小）
--workers 16 \
--root /media/disk1/lmb/DATASET/ \
--label-smooth

# /home/lmb/proj/vehicle-reid/test_ve1m+veid+veri.sh
python train_xent_tri.py \
-s vehicleid \
-t vehicleid \
--height 128 \
--width 256 \
--test-size 800 \
--train-batch-size 1 \
--test-batch-size 512 \
--evaluate \
-a resnet50_fc256 \  # 特征维度256
--load-weights /media/disk1/lmb/EXP/exp-vehicle-reid/train-ve1m+veid+veri/model_59.pt \
--save-dir /media/disk1/lmb/EXP/exp-vehicle-reid/test-ve1m+veid+veid \
--root /media/disk1/lmb/DATASET/ \
--gpu-devices "0, 1, 2, 3" \
--use-avai-gpus
```



| **train (size)**                 | **test (size)**     | **h w**  | **mAP** | **Rank-1** | **Rank-5** | **Rank-10** | **Rank-20** |
| -------------------------------- | ------------------- | -------- | ------- | ---------- | ---------- | ----------- | ----------- |
| Vehicle-1M+VehicleID+VeRi (990k) | VehicleID (0.8k)    | 128  256 | 85.7    | 80.2       | 93.2       | 96.8        | 98.0        |
| Vehicle-1M+VehicleID+VeRi (990k) | VehicleID (1.6k)    | 128 256  | 82.0    | 76.1       | 89.0       | 94.0        | 96.5        |
| Vehicle-1M+VehicleID+VeRi (990k) | VehicleID (2.4k)    | 128 256  | 78.4    | 72.4       | 85.6       | 91.2        | 95.2        |
| Vehicle-1M+VehicleID+VeRi (990k) | VehicleID (3.2k)    | 128 256  | 76.5    | 70.4       | 83.4       | 89.3        | 94.1        |
| Vehicle-1M+VehicleID+VeRi (990k) | VehicleID (6.0k)    | 128 256  | 73.9    | 68.3       | 80.0       | 84.8        | 89.9        |
| Vehicle-1M+VehicleID+VeRi (990k) | VehicleID (13.164k) | 128 256  | 69.6    | 64.4       | 74.7       | 79.3        | 84.4        |

| **train (size)**                 | **test (size)**     | **h w** | **mAP** | **Rank-1** | **Rank-5** | **Rank-10** | **Rank-20** |
| -------------------------------- | ------------------- | ------- | ------- | ---------- | ---------- | ----------- | ----------- |
| Vehicle-1M+VehicleID+VeRi (990k) | Vehicle-1M (1k)     | 128 256 | 96.1    | 93.9       | 98.8       | 99.2        | 99.5        |
| Vehicle-1M+VehicleID+VeRi (990k) | Vehicle-1M (2k)     | 128 256 | 93.7    | 91.9       | 95.8       | 96.3        | 96.6        |
| Vehicle-1M+VehicleID+VeRi (990k) | Vehicle-1M (3k)     | 128 256 | 93.4    | 91.0       | 96.2       | 97.0        | 97.7        |
| Vehicle-1M+VehicleID+VeRi (990k) | Vehicle-1M (5.527k) | 128 256 | 91.5    | 87.9       | 95.9       | 96.9        | 97.6        |



## Time

| Query         | 15123 | 30539 | 45069 | 1       | 1      | 1     | 1     |
| ------------- | ----- | ----- | ----- | ------- | ------ | ----- | ----- |
| Gallery       | 1k    | 2k    | 3k    | 10^6    | 10^7   | 10^8  | 10^9  |
| Distmat Times | 0.8   | 2.98  | 6.32  | 0.04879 | 0.4879 | 4.879 | 48.79 |
