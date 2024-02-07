
# YOLOv5_rotate
YOLOv5 in DOTA_OBB dataset with CSL_label.(Oriented Object Detection)


## Datasets and pretrained checkpoint
* `Datasets` : [DOTA](https://link.zhihu.com/?target=http%3A//captain.whu.edu.cn/DOTAweb/) 
* `Datasets` : [Chips]-`Not public yet `
* `Pretrained Checkpoint or Demo Files` : 
    * `train,detect_and_evaluate_demo_files`:  | [Baidu Drive(6666)](https://pan.baidu.com/s/19BGy_UIdk8N-mSjHBMI0QQ). |  [Google Drive](https://drive.google.com/file/d/1MdKTgXQpHFBk_RN9UDSIB42M5e8zQaTP/view?usp=sharing) |
    * `yolov5x.pt`:  | [Baidu Drive(6666)](https://pan.baidu.com/s/1pH6EGKZiIyGtoqUe3F8eWQ). |  [Google Drive](https://drive.google.com/file/d/1hGPB7iOl3EmB2vfm44xMpHJV8hPufHn2/view?usp=sharing) |
    * `yolov5l.pt`:  | [Baidu Drive(6666)](https://pan.baidu.com/s/16is2mx879jk9_4RHwcIgKw). |  [Google Drive](https://drive.google.com/file/d/12ljwafulmAP1i9XsaeYvEnIUd18agJcT/view?usp=sharing) |
    * `yolov5m.pt`:  | [Baidu Drive(6666)](https://pan.baidu.com/s/1ZQoxEB-1mtBAk3A-Rt85-A). |  [Google Drive](https://drive.google.com/file/d/1VSDegIUgTh-fMDIjuwTSQaZ1w5bVx2Vd/view?usp=sharing) |
    * `yolov5s.pt`:  | [Baidu Drive(6666)](https://pan.baidu.com/s/1jm7ijb0a3LVkg8P2bkmJnw). |  [Google Drive](https://drive.google.com/file/d/1ePo6OM8MbxG8nAkZS_Bt7cmnChSlKBmo/view?usp=sharing) |
* `The latest YOLOV5 model weights ` : (https://github.com/ultralytics/yolov5).
## Fuction
* `train.py`.  Train.

* `detect.py`. Detect and visualize the detection result. Get the detection result txt.

* `val.py`.  Finally evaluate the detector



## Installation  (Linux Recommend, Windows not Recommend)
`1.` Python 3.8 with all requirements.txt dependencies installed, including torch==1.6, opencv-python==4.1.2.30, To install run:
```
$   pip install -r requirements.txt
```
`2.` Install swig
```
$   cd  \.....\yolov5_DOTA_OBB\utils
$   sudo apt-get install swig
```
`3.` Create the c++ extension for python
```
$   swig -c++ -python polyiou.i
$   python setup.py build_ext --inplace
```


## Usage Example
`1.` `'Get Dataset' `
 
* Split the Chips/DOTA image and labels. Trans DOTA format to YOLO longside format.

* You can refer to  [hukaixuan19970627/DOTA_devkit_YOLO](https://github.com/hukaixuan19970627/DOTA_devkit_YOLO).

* The Oriented YOLO Longside Format is:

```
$  classid    x_c   y_c   longside   shortside    Θ    Θ∈[0, 180)


* longside: The longest side of the oriented rectangle.

* shortside: The other side of the oriented rectangle.

* Θ: The angle between the longside and the x-axis(The x-axis rotates clockwise).x轴顺时针旋转遇到最长边所经过的角度
```
`WARNING: IMAGE SIZE MUST MEETS 'HEIGHT = WIDTH'`


`2.` `'train.py'` 

* All same as [ultralytics/yolov5](https://github.com/ultralytics/yolov5).  You better train demo files first before train your custom dataset.
* Single GPU training:
```
$ python train.py  --batch-size 4 --device 0
```
* Multi GPU training:  DistributedDataParallel Mode 
```
python -m torch.distributed.launch --nproc_per_node 4 train.py --sync-bn --device 0,1,2,3
```


`3.` `'detect.py'` 
    
* 运行图像分割代码SplitOnlyImage.py，将原图分割存储到：inference/clip_images.
* 运行检测代码：python detect.py ，将检测结果存储到： inference/detect_images.
* 运行合并代码：python merge.py ,将合并结果保存到： inference/merge_images.


![detection_result_after_merge](./chips_detection.jpg)

