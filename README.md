# Paper reviews (Language: Korean)

---

### Disentangled representation learning GAN for pose-invariant face recognition
- Review date: 2019/02/11
- Conference: CVPR2017
- Area: Face recognition
- Objective: 얼굴인식 분야에서 정면-정면 인식 성능에 비해 정면-옆면 성능이 떨어짐. 즉, 포즈에 강인한 얼굴인식(PIFR)이 필요
- Related work(PIFR): 두 갈래로 나뉨 
  - 정면의 얼굴로 변환하는 것 (정면-정면 인식 성능이 좋기 때문에)
  - 비 정면 얼굴 영상으로부터 특징적인/포즈에 강인한 특징 추출
- Contribution: 4가지
  - 어떤 임의의 방향에서도 얼굴을 돌리거나/정면화 할 수 있는 인코더-디코더 구조의 generator 제안
  - 표현 학습(representation learning)에 있어서 G에서의 포즈 코드와 D에서의 포즈 추정을 통해 포즈에 대한 정보를 분해(얽힌것을 푼다, disentangle)
  - 계수를 학습하는 과정을 통해 여러 장의 얼굴 영상이 입력되어도 하나의 표현으로 융합
  - SOTA on Multi-PIE, CFP, IJB-A
- Method(briefly): 
  - Generator
    - 인코더-디코더 구조
    - 인코더
      - 인코더는 임의의 포즈의 얼굴 영상을 부호화(320-dim)하며, 인식에 방해가 되는 변화들(pose)과 얽힌 것을 푼다. (discriminative representation)
      - 인코더 아키텍처: 영상 -> conv unit(conv+BN+ELU) -> avgpool -> feature (320 dim)
    - 디코더
      - 디코더는 인코더에 의해 부호화된 코드(pose-invariant), 포즈정보(p, side information, one-hot vector, random index), 노이즈(z, pose & identity 제외한 appearance variation)를 이용해서 얼굴에 다양한 표현을 합성한다. 이 때, D가 입력 영상과 동일한 신원으로 판단하도록(fake임을 인지하지 못하도록) 합성한다. (generative representation)
      - 디코더 아키텍처: feature (320+N^p+N^z dim) -> Fconv unit(fractionally-strided conv)
    - Loss: 생성된 영상이 D를 속일 확률 최대화 (true identity & pose)
  - Discriminator
    - 임의의 포즈에 대한 얼굴의 신원 예측 (N^d+1 identification, 1은 fake)
    - 포즈를 구분 (N^p)
    - Loss: 입력된 영상이 true identity & pose[실제 label]를 갖을 확률 최대화 / 생성된 영상이 fake로 분류될 확률 최대화
    - 아키텍처: 영상 -> conv unit(conv+BN+ELU) -> avgpool -> feature (320 dim) -> fc (N^d+N^p+1, for CE)
  - Learning strategy
    - G 20번 backprop(합성된 영상으로만 학습)한 뒤에 D를 backprop(원본에 대한 pose, idenity 학습 및 G 견제)
 
