
# :warning:*Update about results and evaluation metric* [08/07/2022]

A problem arises because no prior human pose forecasting work has explicitly written the test MPJPE metric. [Mao et al., 2020, Mao et al., 2019] have specified the MPJPE for the learning loss, and they have referred to the (same) MPJPE for testing, which is however different.

In [Mao et al., 2020], Eq. (6), they define MPJPE as 

$$MPJPE = \frac{1}{J(M+T)}\sum_{t=1}^{M+T} \sum_{j=1}^J ||\hat{\textbf{p}}_{t,j} - \textbf{p}_{t,j} ||^2,$$

which sums up all errors at all frames up to the prediction T.

Also in [Ionescu et al., 2014], Eq. (8), they define the MPJPE as:

$$MPJPE(t) = \frac{1}{J} \sum_{j=1}^J ||\hat{\textbf{p}_{t,j} }- \textbf{p}_{t,j} ||^2,$$

and they state: "For a set of frames the error is the average over the MPJPEs of all frames."

We have therefore interpreted the test MPJPE to be:

$$MPJPE = \frac{1}{J T}\sum_{t=M+1}^{M+T} \sum_{j=1}^J ||\hat{\textbf{p}}_{t,j} - \textbf{p}_{t,j} ||^2,$$

which is implemented in our testing code. Note: coding has been done in good faith, and in good faith we have open-sourced the project here.

As noted in this thread, the code provided by [Mao et al., 2020] actually considers only the target temporal horizon, not the average up to that time.

Running the test code of [Mao et al., 2020], short-term (400ms) and long-term (1000ms) errors for the Human3.6M dataset for STS-GCN are:




--------


 ### Install dependencies:
```
 $ pip install -r requirements.txt
```
 
 ### Get the data

[Human3.6m](http://vision.imar.ro/human3.6m/description.php) in exponential map can be downloaded from [here](http://www.cs.stanford.edu/people/ashesh/h3.6m.zip).
 
Directory structure: 
```shell script
H3.6m
|-- S1
|-- S5
|-- S6
|-- ...
`-- S11
```



### Train
 
```bash
 python main_h36_3d.py --input_n 10 --output_n 25 --skip_rate 1 --joints_to_consider 22 
 ```
```bash
 python main_h36_ang.py --input_n 10 --output_n 25 --skip_rate 1 --joints_to_consider 16 

 
 ### Test
 To test on the pretrained model, we have used the following commands:
 ```bash
 python main_h36_3d.py --input_n 10 --output_n 25 --skip_rate 1 --joints_to_consider 22 --mode test --model_path ./checkpoints/CKPT_3D_H36M
  ```
  ```bash
  python main_h36_ang.py --input_n 10 --output_n 25 --skip_rate 1 --joints_to_consider 16 --mode test --model_path ./checkpoints/CKPT_ANG_H36M
  ```
 
### Visualization
 For visualizing from a pretrained model, we have used the following commands:
 ```bash
  python main_h36_3d.py --input_n 10 --output_n 25 --skip_rate 1 --joints_to_consider 22 --mode viz --model_path ./checkpoints/CKPT_3D_H36M --n_viz 5
 ```
 ```bash
  python main_h36_ang.py --input_n 10 --output_n 25 --skip_rate 1 --joints_to_consider 16 --mode viz --model_path ./checkpoints/CKPT_ANG_H36M --n_viz 5
 ```
 


 
 ### Acknowledgments
 
 Some of our code was adapted from [HisRepsItself](https://github.com/wei-mao-2019/HisRepItself) by [Wei Mao](https://github.com/wei-mao-2019).
 
 The authors wish to acknowledge Panasonic for partially supporting this work and the project of the Italian Ministry of Education, Universities and Research (MIUR) “Dipartimenti di Eccellenza 2018-2022”.

 

### Citation
If you find this project useful in your research, please consider cite:
@article{xxxxx,
  title={Enhanced Human Motion Prediction via Multi-Scale Space-Time Graph Convolutional Network},
  author={Jing Wang,Yuying Li,Jiaxing Xue,Junlin Meng,Wanying Song},
  journal={The Visual Computer},
  volume={xx},
  number={xx},
  pages={xx},
  year={2025},
  publisher={Springer}
}
