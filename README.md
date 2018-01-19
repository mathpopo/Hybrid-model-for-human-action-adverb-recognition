# Hybrid-model-for-human-action-adverb-recognition
By Bo Pang, Kaiwen Zha, [Cewu Lu](https://cvsjtu.wordpress.com/).

### Introduction

[ADHA](http://mvig.sjtu.edu.cn/publications/adha/adha.html) is the first human action adverb recognition dataset. This hybrid model is the baseline of this dataset.
The model is a fusion of two-stream model, pose-based LSTM model and expression model. The expression information is acting as a feature that combined into the CNN feature of the PBLSTM and Two-Stream model.
The framework of the model is like this:

<p align="center">
<img src="https://github.com/BoPang1996/Hybrid-model-for-human-action-adverb-recognition/blob/master/images/Hybrid_model.jpg" alt="RMPE Framework" width="600px">
</p>


### Usage
1. Get the code.
  ```Shell
  git clone https://github.com/BoPang1996/Hybrid-model-for-human-action-adverb-recognition.git
  cd Hybrid-model-for-human-action-adverb-recognition
  ```
 
2. Get the dataset:
 You can download the ADHA dataset from [here](http://mvig.sjtu.edu.cn/publications/adha/download.html)

3. PBLSTM:
&emsp &emsp 1) Get the pose info using [Open Pose](https://github.com/CMU-Perceptual-Computing-Lab/openpose). The output is skeleton videos.
&emsp &emsp 2) Use ./pose/extract.py to get the input of the PBLSTM model.
&emsp &emsp 3) ./PBLSTM/train.py & ./PBLSTM/test.py to train and output the result of the model.

4. Two-Stream model
    1) Use ./Two_Stream/get_input_data/get_optical_flow    to get the optical flow of the raw video.
    2) Use ./Two_Stream/get_input_data/gettrackingdata.py    to get the input of the two stream video. The output has two folder: "of" and "rgb".("of" folder for motion stream and "rgb" folder for spatial stream)
    3) Use ./Two-Stream/motion/train.py and ./Two-Stream/spatial/train.py to train the model and use ./Two-Stream/Fusion/test.py to output the result.
	
5. Expression
    1) Use [this hybrid model](https://github.com/lidian007/EmotiW2016) to get the expression result of the video. This model is the winner of EmotiW2016. The result is saved as txt file.
    2) To combine the expression feature into the above two models, set the parameter "withexpression" to "True" in the train.py and test.py and set the parameter "expression_path" to the expression result folder.
    3) Retrain the models.

6. Fusion to get the final result
    Run ./Hybrid_Fusion/Fusion.py to get the final reuslt of the hybrid model.


### Citation
Please cite the paper in your publications if it helps your research:    
  
    @inproceedings{fang2017rmpe,
      title={First Step for Human Action Adverb Recognition: ADHA Dataset and A Hybrid Model},
      author={Bo, Pang and Zha, Kaiwen and Lu, Cewu},
      booktitle={ArXiv},
      year={2018}
    }
      
### Acknowledgements

Thanks to [OpenPose](https://github.com/CMU-Perceptual-Computing-Lab/openpose) and [Hybrid expression model](https://github.com/lidian007/EmotiW2016).
