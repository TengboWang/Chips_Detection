
## Brief Introduction
Based on [DOTA_devkit](https://github.com/CAPTAIN-WHU/DOTA_devkit).  
Add some modules to trans DOTA annotation format to YOLO annotation format.  
Add some files for every demo.


## Fuction
* `DOTA.py`  Load image, and show the bounding oriented box.

* `ImgSplit.py` Split image and the label.

* `ResultMerge.py` Merge the detection result annotation txt.

* `dota_×_evaluation_task×.py` Evaluate the detection result annotation txt.

* `YOLO_Transformer.py`     Trans DOTA format to YOLO(OBB or HBB) format.

* `Draw_DOTA_YOLO.py` Picture the YOLO_OBB labels(after augmented).

## Installation
Same as [DOTA_devkit](https://github.com/CAPTAIN-WHU/DOTA_devkit).  Then:

```
$  pip install -r requirements.txt
```
