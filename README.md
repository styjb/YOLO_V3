Note
=
I'm solving scale invariant. 
If you have a good paper, 
you can email me by StinkyTofu95@gmail.com. Thanks!<br>

YOLO_v3<br>
=
YOLO_v3 implemented with tensorflow <br>

- [x] data augmentation(release)<br>
- [x] multi-scale training(release)<br>
- [x] Focal loss(increase 2 mAP, release)<br>
- [x] Single-Shot Object Detection with Enriched Semantics(incrase 1 mAP, not release)<br>
- [x] Soft-NMS(drop 0.5 mAP, release)<br>
- [x] Group Normalization(didn't use it in project, release)<br>
- [ ] Deformable convolutional networks<br>
- [ ] Scale-Aware Trident Networks for Object Detection
- [ ] Understanding the Effective Receptive Field in Deep Convolutional Neural Networks<br>

Train
=
1. clone YOLO_v3 repository
``` bash
git clone https://github.com/Stinky-Tofu/YOLO_v3.git
```
2. prepare data<br>
(1)download datasets
Create a new folder named `data` in the directory where the `YOLO_V3` folder 
is located, and then create a new folder named `VOC` in the `data/`.<br>
Download [VOC 2012_trainval](http://host.robots.ox.ac.uk/pascal/VOC/voc2012/VOCtrainval_11-May-2012.tar)
、[VOC 2007_trainval](http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtrainval_06-Nov-2007.tar)
、[VOC 2007_test](http://host.robots.ox.ac.uk/pascal/VOC/voc2007/VOCtest_06-Nov-2007.tar), and put datasets into `data/VOC`,
 name as `2012_trainval`、`2007_trainval`、`2007_test` separately. <br>
 The file structure is as follows:<br>
 --YOLO_V3<br>
 --data<br>
 -->--VOC<br>
 -->-->--2012_trainval<br>
 -->-->--2007_trainval<br>
 -->-->--2007_test<br>
 
(2)convert data format<br>
You should set `DATASET_PATH` in `config.py` to the path of the VOC dataset, for example:<br>
`DATASET_PATH = '/home/xzh/doc/code/python_code/data/VOC'`,and then<br>
 ```bash
 python voc_annotation.py
```
3. prepare initial weights<br>
Download [YOLOv3-608.weights](https://pjreddie.com/media/files/yolov3.weights) firstly, 
put the yolov3.weights into `yolov3_to_tf/`, and then 
```bash
cd yolov3_to_tf
python3 convert_weights.py --weights_file=yolov3.weights --dara_format=NHWC --ckpt_file=./saved_model/yolov3_608_coco_pretrained.ckpt
cd ..
python rename.py
``` 

4. Train<br>
``` bash
python train.py
```
5. Test<br>
Download weight file [yolo_416_87.78%.ckpt](https://drive.google.com/drive/folders/1We_P5L4nlLofR0IJJXzS7EEklZGUb9sz)
``` bash
python test.py
--map_calc, default=False
--weights_file, default=None
--gpu, default=0
```

## mAP
VOC2007(score_threshold=0.01)<br>
If you want to get a higher mAP, you can set the score threshold to 0.01.<br>
If you want to apply it, you can set the score threshold to 0.2.<br>
![mAP](https://github.com/Stinky-Tofu/YOLO_V3/blob/master/mAP/mAP.png)<br>
VOC2012(score_threshold=0.01)<br>
84.3% http://host.robots.ox.ac.uk:8080/leaderboard/displaylb.php?challengeid=11&compid=4#KEY_YOLD<br>



## Reference:<br>
paper: <br>
[YOLOv3: An Incremental Improvement](https://arxiv.org/abs/1804.02767)<br>
[Foca Loss for Dense Object Detection](https://arxiv.org/abs/1708.02002)<br>
[Group Normalization](https://arxiv.org/abs/1803.08494)<br>
[Single-Shot Object Detection with Enriched Semantics](https://arxiv.org/abs/1712.00433)<br>
[An Analysis of Scale Invariance in Object Detection - SNIP](https://arxiv.org/abs/1711.08189)<br>
[Deformable convolutional networks](https://arxiv.org/abs/1811.11168)<br>
[Scale-Aware Trident Networks for Object Detection](https://arxiv.org/abs/1901.01892)<br>
[Understanding the Effective Receptive Field in Deep Convolutional Neural Networks](https://arxiv.org/abs/1701.04128)<br>

mAP calculate: [mean Average Precision](https://github.com/Cartucho/mAP)<br>
 
## Requirements
. Tensorflow <br>
. Opencv <br>
. Python <br>
. Numpy<br>
