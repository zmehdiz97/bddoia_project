Explainable Object-induced Action Decision for Autonomous Vehicles
===================

The repo for our cvpr 2020 [paper](https://arxiv.org/pdf/2003.09405.pdf). We used [maskrcnn
benchmark](https://github.com/facebookresearch/maskrcnn-benchmark) for bounding
box extraction. The project page is also available [here](https://twizwei.github.io/bddoia_project/).
<p align="center">
	<img src="./images/net.png" alt="net"  width="900">
	<p align="center">
		<em>Proposed architecture.</em>
	</p>
</p>
 

Installation
------------
### Step 1

Clone this repo.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
git clone https://github.com/Twizwei/bddoia_project
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~



### Step 2

Install maskrcnn benchmark. Follow the instructions
[here](https://github.com/facebookresearch/maskrcnn-benchmark/blob/master/INSTALL.md)
to install maskrcnn benchmark.
 

Dataset
-------

Download the our dataset [BDD-OIA](https://drive.google.com/open?id=1NzF-UKaakHRNcyghtaWDmc-Vpem7lyQ6) and then extract it.

To run our model for last frames, it is better to establish symbolic link.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
cd ./maskrcnn/maskrcnn-benchmark
mkdir datasets
ln -s dir_to_lastframe datasets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

BDD-OIA also contains data for videos.

 

Training and evaluation
-----------------------
First we need to train Faster RCNN on BDD100K. The pretrained Faster RCNN is available [here](https://drive.google.com/drive/folders/1OCiWD9q-9ZzxKS45yqA4Tgg_KCt-nD6g?usp=sharing)

To train the model, run

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
python ./maskrcnn/maskrcnn-benchmark/action_prediction/train.py --batch size 2 --num_epoch 50 --initLR 0.001 --gtroot "root-to-action-gt" --reasonroot "root-to-explanation-gt" MODEL.SIDE True MODEL.ROI_HEADS.SCORE_THRESH 0.4 MODEL.PREDICTOR_NUM 1 OUTPUT_DIR "output-directory" MODEL.META_ARCHITECTURE "Baseline1"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Training configurations can be found in `train.py` and
`maskrcnn/maskrcnn-benchmark/maskrcnn_benchmark/config/defaults/py` .

 

To evaluate the model, run

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
python ./maskrcnn/maskrcnn-benchmark/action_prediction/test.py --batch size 2 --gtroot "root-to-action-gt" --reasonroot "root-to-explanation-gt" WEIGHT "weights-dir" MODEL.SIDE True MODEL.ROI_HEADS.SCORE_THRESH 0.4 MODEL.PREDICTOR_NUM 1 OUTPUT_DIR "output-directory" MODEL.META_ARCHITECTURE "Baseline1"
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

A pretrained model `net_Final.pth` is also available [here](https://drive.google.com/drive/folders/1OCiWD9q-9ZzxKS45yqA4Tgg_KCt-nD6g?usp=sharing). 

Acknowledgement
-----------------------
 [Mask R-CNN Benchmark](https://github.com/facebookresearch/maskrcnn-benchmark)
