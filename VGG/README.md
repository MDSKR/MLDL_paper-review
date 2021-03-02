### Q&A

Q> Table5 관련 : Dense, Multi-Crop, Crop & Dense

A> 원래의 FC layer로만 했다면 fixed size 위한 crop 을 해야하지만, FC를 1x1 conv로 쓰면 FC-layer 앞단의 feature map size를 slide하면서 여러번의 연산으로 조밀하게 갈 수 있음.
- 2014대회의 VGG 팀에서 2013대회의 OverFeat팀에서 한 Dense evaluation 을 multi-crop 이랑 비교한 내용임
- OverFeat 팀의 dense evaluation 은 1데이터 간격으로 각각 non-overlapped pooling (pooling stride) 후 FC classifier로 연결됨. FC layer를 1x1 conv 로 slide하면서 연산을 여러번으로 조밀하게 함. 

참고: 2013 OverFeat 리뷰(https://blog.naver.com/laonple/220752877630) 2013대회에서 OverFeat 팀의 Dense evaluation 은 localization 1위였고, classification, detection 에서도 통합적으로 효과적인 ConvNet 임을 보여줬음. 
