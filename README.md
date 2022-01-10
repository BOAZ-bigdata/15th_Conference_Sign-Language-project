# Sign-Langugage-project

## Contributors

<table>
  <tr>
      <td align="center"><a href="https://github.com/winston1214"><img src="https://avatars.githubusercontent.com/u/47775179?v=4" width="100" height="100"><br /><sub><b>김영민</b></sub></td>
      <td align="center"><a href="https://github.com/dbxminz"><img src="https://avatars.githubusercontent.com/u/75927569?v=4" width="100" height="100"><br /><sub><b>곽민지</b></sub></td>
      <td align="center"><a href="https://github.com/manypeople-AI"><img src="https://avatars.githubusercontent.com/u/76834485?v=4" width="100" height="100"><br /><sub><b>이다인</b></sub></td>
      <td align="center"><a href="https://github.com/yyeongeun"><img src="https://avatars.githubusercontent.com/u/70632327?v=4" width="100" height="100"><br /><sub><b>김영은</b></sub></td> 
     </tr>
</table>

## Survey

- STMC-Transformer : <a href='https://bigdata-analyst.tistory.com/284'>Paper Review(KYM)</a>, <a href='https://di-bigdata-study.tistory.com/14'>Paper Review(LDI)</a>, <a href='https://rladuddms.tistory.com/85'>Paper Review(KYE)</a>
- STMC : <a href='https://bigdata-analyst.tistory.com/289?category=883085'>Paper Review(KYM)</a>, <a href='https://rladuddms.tistory.com/88'>Paper Review(KYE)</a>
- NSLT : <a href='https://di-bigdata-study.tistory.com/17'>Paper Review(LDI)</a>, <a href='https://rladuddms.tistory.com/94'>Paper Review(KYE)</a>, <a href='https://bigdata-analyst.tistory.com/295'>Paper Review(KYM)</a>, <a href='https://dbxminz.tistory.com/92'>Paper Review(KMJ)</a>

## Environment

- OS : Ubuntu 18.04.5(Docker) LTS or Colab
- Cuda : 10.0
- GPU : Tesla V100-32GB


## Data

<a href='https://aihub.or.kr/opendata/keti-data/recognition-laguage/KETI-02-003'>DataSet Download</a>

<img src='https://github.com/winston1214/Sign-Langugage-project/blob/master/picture/sample_data.gif?raw=true'></img>

## Install Module
```
$ pip install pyyaml==5.2
$ pip install scipy==1.1.0
$ pip install pillow==6.2.2
$ pip install torch==1.2.0 torchvision==0.4.0
$ python -m pip install cython
$ sudo apt-get install libyaml-dev
```

## Setting(Alphapose)
```
$ git clone https://github.com/winston1214/Sign-Langugage-project.git && cd Sign-Langugage-project
$ cd Alphapose-json
$ python setup.py build develop
```

If you don't run in the COLAB environment or the **cuda version is 10.0**, refer to <a href='https://bigdata-analyst.tistory.com/328?category=908124'>this link</a>.

## PreProcessing

**1. Split frame(Colab)**
```
$ python frame_split_colab.py --source ${video_path} --output ${save_img_path}
```
**2. Extract KeyPoint(OpenPose)**
```
$ cd pytorch-openpose
$ python demo_new_open_json_new.py --source %{input_path} --save_dir ${save path}
```

## Train

```
$ python train.py --X_path ${X_train.pickle path} --save_path ${model save directory} \
--pt_name ${save pt model name} --model ${LSTM or GRU} --batch ${BATCH SIZE}

## Example

$ python train.py --X_path /sign_data/ --save_path pt_file/ \
--pt_name model1.pt --model GRU --batch 128 --epochs 100 --dropout 0.5
```
- X_train.pickle : For convenience, we stored and used the values extracted from the keypoint in **pickle file format**.
  - (shape : [video_len, max_frame_len, keypoint_len] # [7129, 376, 246] )


## Extract KeyPoint
<img src='https://github.com/winston1214/Sign-Langugage-project/blob/master/picture/OpenPose_sample.gif?raw=true'></img>
