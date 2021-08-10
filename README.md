## CenterNet2 - MMDetection
This repository is the reproduced implemention of [Probabilistic two-stage detection](https://arxiv.org/pdf/2103.07461.pdf), and submitted for [OpenMMLab Algorithm Ecological Challenge](https://openmmlab.com/competitions/algorithm-2021).

You can also refer to our [repo](https://github.com/Jacky-gsq/Centernet2-mmdet) fork by mmdetection. 

### Result and model details

basic settings：
backbone：
neck：
rpn_head:
roi_head:

parameters and resluts:


### How To Use？
1. Our project is based on [mmdetecion](https://github.com/open-mmlab/mmdetection), please refer [get_started.md](https://github.com/open-mmlab/mmdetection/blob/master/docs/get_started.md) for the env installation and basic usage of MMDetection.

2. **clone our repo to your workstation**

```
git clone https://github.com/Jacky-gsq/Centernet2-mmdet
```

3. **copy follwing files to the directory of mmdetection project** 
or 

```bash
cd CenterNet2-MMDetection
mv ./configs/centernet2 ${your path to mmdetection}/configs/
mv ./configs/centernet2_cascade_r50_fpn.py ${your path to mmdetection}/configs/_base_/models/

mv ./models/detectors/centernet2.py ${your path to mmdetection}/mmdet/models/detectors/
mv ./models/dense_heads/custom_centernet_head.py ${your path to mmdetection}/mmdet/models/dense_heads/
mv ./models/roi_heads/custom_cascade_roi_head.py ${your path to mmdetection}/mmdet/models/roi_heads/
```


3. **register and import module in  `__init__.py`**

*mmdetection/models/detectors/__init__.py*


```python
...
from .centernet2 import CenterNet2

__all__ = [
    ..., 'CenterNet2'
]
```


*mmdetection/models/dense_heads/__init__.py*

```python
...
from .custom_centernet_head import CustomCenterNetHead

__all__ = [
    ..., 'CustomCenterNetHead'
]
```
*mmdetection/models/roi_heads/__init__.py*

```python
...
from .custom_cascade_roi_head import CustomCascadeRoIHead

__all__ = [
    ..., 'CustomCascadeRoIHead'
]
```

## Train and Test
- **train**

```bash
# single-gpu
cd ${mmdetection}
python tools/train.py  ../configs/centernet2/centernet2_cascade_res50_fpn_1x_coco.py [optional arguments]
# multi-gpu
.tools/dist_train.sh ../configs/centernet2/centernet2_cascade_res50_fpn_1x_coco.py ${GPU_NUM} [optional arguments]
```

- **test**
```bash
# single-gpu
cd ${mmdetection}
python tools/test.py  ../configs/centernet2/centernet2_cascade_res50_fpn_1x_coco.py ${CHECKPOINT_FILE} [optional arguments]
# multi-gpu
tools/dist_test.sh ../configs/centernet2/centernet2_cascade_res50_fpn_1x_coco.py ${CHECKPOINT_FILE} ${GPU_NUM} --out ${RESULT_FILE} [optional arguments]
```




## Model zoo
pre-trained model in Baidunetdisk


 
| name | bbox_map |download|
|--|--|--|
| CenterNet2 | 40.4 |model |



## License

This project is released under the [Apache 2.0 license](LICENSE).

## Citation

If you use this toolbox or benchmark in your research, please cite this project.

```
@article{mmdetection,
  title   = {{MMDetection}: Open MMLab Detection Toolbox and Benchmark},
  author  = {Chen, Kai and Wang, Jiaqi and Pang, Jiangmiao and Cao, Yuhang and
             Xiong, Yu and Li, Xiaoxiao and Sun, Shuyang and Feng, Wansen and
             Liu, Ziwei and Xu, Jiarui and Zhang, Zheng and Cheng, Dazhi and
             Zhu, Chenchen and Cheng, Tianheng and Zhao, Qijie and Li, Buyu and
             Lu, Xin and Zhu, Rui and Wu, Yue and Dai, Jifeng and Wang, Jingdong
             and Shi, Jianping and Ouyang, Wanli and Loy, Chen Change and Lin, Dahua},
  journal= {arXiv preprint arXiv:1906.07155},
  year={2019}
}
```
