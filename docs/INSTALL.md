## Installation

Use the docker from dev-pops 

### A from-scratch setup script

Here is a full script for setting up SOLO with conda and link the dataset path (supposing that your COCO dataset path is $COCO_ROOT).

```shell


conda install -y cython==0.28.5
git clone https://github.com/WXinlong/SOLO.git
cd SOLO
pip install -r requirements/build.txt
pip install "git+https://github.com/cocodataset/cocoapi.git#subdirectory=PythonAPI"
pip install -v -e .

# download COCo
mkdir data
ln -s $COCO_ROOT data
```


### Prepare datasets

It is recommended to symlink the dataset root to `$SOLO/data`.
If your folder structure is different, you may need to change the corresponding paths in config files.

```
SOLO
├── mmdet
├── tools
├── configs
├── data
│   ├── coco
│   │   ├── annotations
│   │   ├── train2017
│   │   ├── val2017
│   │   ├── test2017
│   ├── cityscapes
│   │   ├── annotations
│   │   ├── train
│   │   ├── val
│   ├── VOCdevkit
│   │   ├── VOC2007
│   │   ├── VOC2012

```
The cityscapes annotations have to be converted into the coco format using the [cityscapesScripts](https://github.com/mcordts/cityscapesScripts) toolbox.
We plan to provide an easy to use conversion script. For the moment we recommend following the instructions provided in the
[maskrcnn-benchmark](https://github.com/facebookresearch/maskrcnn-benchmark/tree/master/maskrcnn_benchmark/data) toolbox. When using this script all images have to be moved into the same folder. On linux systems this can e.g. be done for the train images with:
```shell
cd data/cityscapes/
mv train/*/* train/
```


