### Q&A

### Q) Table5 관련 : Dense, Multi-Crop, Crop & Dense

#### A) 원래의 FC layer로만 했다면 fixed size 위한 crop 을 해야하지만, FC를 1x1 conv로 쓰면 FC-layer 앞단의 feature map size를 slide하면서 여러번의 연산으로 조밀하게 갈 수 있음.
- 2014대회의 VGG 팀에서 2013대회의 OverFeat팀에서 한 Dense evaluation 을 multi-crop 이랑 비교한 내용임
- OverFeat 팀의 dense evaluation 은 1데이터 간격으로 각각 non-overlapped pooling (pooling stride) 후 FC classifier로 연결됨. FC layer를 1x1 conv 로 slide하면서 연산을 여러번으로 조밀하게 함. 

[참고]
- [2013 OverFeat 리뷰](https://blog.naver.com/laonple/220752877630) 2013대회에서 OverFeat 팀의 Dense evaluation 은 localization 1위였고, classification, detection 에서도 통합적으로 효과적인 ConvNet 임을 보여줬음. <br><br>


### Q) model training 시에 single-scale, multi-scale 을 하면 input size 는 224 x 224 가 아닌, 256 x 256, 384 x 384, 512 x 512 등이 되나요?
#### A) 아니오. input 과정은 scale 과정으로 확대한 후 224x224로 잘라서 넣어주기 때문에, input size 는 224x224 로 fix 되어 있습니다.
```
논문 2페이지
2.1 ARCHITECTURE
During training, the input to our ConvNets is a fixed-size 224 × 224 RGB image. (...)
```
또한 논문에서는 이미지의 input size 는 224 x 224 로 fix 되어 있어서, scale 조정에 따라 randomly cropped 하여 모델에 넣어준다고 표현하고 있습니다.
여기서 scale 의 개념을 설명하기 위해 논문에서는 train image 의 the smallest side 를 S, test image 의 the smallest side 를 Q 로 정한 후 설명합니다.
S = 224 라면 원본 이미지 전체(whole)를 train image 로 넣어주는 것입니다.
그러나 논문에서와 같이 scale 방법을 쓴다면, S >> 224 를 통해 일부의 이미지를 넣어주게 됩니다.
```
논문 4페이지
To obtain the fixed-size 224×224 ConvNet input images, they were randomly cropped from rescaled training images (...)
for S = 224 the crop will capture whole-image statistics, completely spanning the smallest side of a training image; 
for S ≫ 224 the crop will correspond to a small part of the image, containing a small object or an object part.
```
![image](https://user-images.githubusercontent.com/46803961/109660062-c33b4e80-7bab-11eb-8c07-b53211a8f175.png)<br><br>


### Q) Data augmented 방법 관련 pytorch

- [augmentation의 여러가지 방법](http://incredible.ai/pytorch/2020/04/25/Pytorch-Image-Augmentation/)

- [val set을 나누는 방법-cifar10](https://medium.com/@sergioalves94/deep-learning-in-pytorch-with-cifar-10-dataset-858b504a6b54)
