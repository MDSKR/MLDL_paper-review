## DenseNet 참고자료
### DenseBlock
![Concatenation during Forward Propagation
](image/propagation.gif)

### Composition Layer
![Composition Layer gif](image/compositionlayer.gif)


### SubsetRandomSampler가 무엇인가요?
**SubsetRandomSampler(indices)** : 데이터의 인덱스를 입력으로 사용하며, 랜덤하게 index를 뽑아주는 역할을 한다.


사용 방법
1. 인덱스 목록을 만듦
2. 인덱스를 섞음
3. `train set`과 `validation set`을 `validation set` 비율을 기준으로 인덱스 분할
4. `SubsetRandomSampler` 생성
5. `Sampler`를 `DataLoader`에 적용


참고 : [PyTorch [Basics] — Sampling Samplers](https://towardsdatascience.com/pytorch-basics-sampling-samplers-2a0f29f0bf2a)


### Weight 초기화
weight 초기화
- `Xavier`
    - 무작위 초기화가 아닌 입력과 출력의 특성을 고려한 방법으로, 선형인 경우에서만 사용 가능
- `He`
    - `Xavier`에선 입력과 출력 특성 모두를 고려했지만, `He` 초기화는 입력 특성만 고려하며, 비선형일 경우에 사용

참고 : [Delving Deep into Rectifiers Surpassing Human-Level Performance on Imagenet Classification](https://blog.airlab.re.kr/2019/11/He-initialization)

### Data augumentation을 train set에만 진행하는 이유
Data augumentation은 train data set에서만 진행 해야 됨
- validation set과 test set에서 진행하면 안 됨
- why?
    - transformation은 이미지에 변화를 주어서 학습 데이터를 많게 해서 성능을 높이기 위해 하는 것이기 때문에 train set만 해주고, test set에는 해 줄 필요가 없다. 그러나 주의할 것은 Rescale은 train, test 모두 해 주어야 한다

참고 : [3. 데이터 증강기법 (Data Augmentation)](https://libertegrace.tistory.com/entry/3-%EB%8D%B0%EC%9D%B4%ED%84%B0-%EC%A6%9D%EA%B0%95%EA%B8%B0%EB%B2%95-Data-Augmentation)

### torch.optim.lr_scheduler.MultiStepLR 함수
torch.optim.lr_scheduler.MultiStepLR(optimizer, milestones, gamma=0.1, last_epoch=-1, verbose=False)
- epochs가 milestones에 나와있는 값에 도달했을 때 gamma 배 만큼 곱해 lr를 조절

참고 : [TORCH.OPTIM](https://pytorch.org/docs/stable/optim.html)

### Reference
- [Review: DenseNet — Dense Convolutional Network (Image Classification)](https://towardsdatascience.com/review-densenet-image-classification-b6631a8ef803)
