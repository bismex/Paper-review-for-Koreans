# Paper reviews (Language: Korean)

---

### Disentangled representation learning GAN for pose-invariant face recognition
- Date: 2019/02/09
- Conference: CVPR2017
- Area: Face recognition
- Objective: 얼굴인식 분야에서 정면-정면 인식 성능에 비해 정면-옆면 성능이 떨어짐. 즉, 포즈에 강인한 얼굴인식(PIFR)이 필요
- Related work: 두 갈래로 나뉨 
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
    - 인코더는 임의의 포즈의 얼굴 영상을 부호화
    - 디코더는 부호화된 코드, 포즈정보, 노이즈를 타겟 포즈로 합성 (포즈정보와 노이즈[for appearance variation]는 피드)
    - 임의의 포즈를 갖은 입력 얼굴 영상과 변환된 얼굴이 D에 의해서 동일한 신원으로 판단되도록 합성하는 것 (D를 속이는 것)
  - Discriminator
    - 실제 vs 합성 이미지 구분
    - 임의의 포즈에 대한 얼굴의 신원 예측
  - 일련의 과정들에 의해서 G는 얼굴을 좀 더 동일한 신원같게 만들고 학습된 표현은 보다 포괄적이고 생산적이다
 
