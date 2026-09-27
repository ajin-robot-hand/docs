---
title: "[book] 피지컬 AI 시스템 설계 (1)"
date: 2026-09-27
categories:
  - erdoslibrary
authors:
  - erdoslibrary
---



# about

> 학술적으로 완전히 수렴되거나 고정된 정답이라기보다는, 현재 학계와 산업계의 연구자들이 마주한 다양한 문제들을 어떻게 정의하고 해결해 나가고 있는지를 보여주는 최신 기술 동향에 가깝습니다. 독자 여러분이 이러한 실제 연구 사례와 접근법을 접함으로써 피지컬 AI의 핵심 개념을 빠르게 이해하고, 이를 각자의 실무나 프로젝트에 직접 응용해 볼 수 있도록 내용을 구성했습니다. - p29

<!-- more -->



# 웹과 앱을 넘어 현실로: 피지컬 AI 시대가 온다

### 왜 지금 빅테크는 피지컬 AI에 주목하는가?

생성형 AI의 언어 이해와 추론 능력을 카메라, 센서, 로봇의 움직임, 물리적 환경과 연결하려는 시도

현실 세계에서 무엇을 할 수 있는지를 탐구하는 분야

스스로 물리적 환경을 인지(perception) → 상황을 이해(understanding) → 그에 맞는 행동(action)을 물리적으로 수행할 수 있는 지능령 시스템

#### 1.2 지금 피지컬 AI가 현실적인 기술 흐름이 된 이유

- 개발보다도 더 어려운 건 현장 안정화
- 우리 일상생활은 예측 불가능성
- 거대언어모델(LLM)과 멀티모달(multimodal)기술의 발전 → 스스로 맥락을 유추하여 유연하게 대처할 수 있는 능력
- 최근 주목 받는 시간-언어-행동 모델(Vison-Language-Action Model(VLA))

#### 1.3 로봇 없이는 못하나요? 진입 장벽을 깨는 흔한 오해들

1. 기계 공학, 제어 공학, AI 모델링의 전문가가 되어야만 시작할 수 있다. No.
    - 오픈소스 프레임워크(https://huggingface.co/lerobot)
    - 로봇 전용 미들웨어(ROS2)
2. 값비싼 로봇 하드웨어와 거대한 테스트 인프라가 없으면 불가능하다. No.
    - MuJoCo, Gazebo, Isaac Sim
3. 데이터 확보와 거대 모델 훈련은 빅테크 기업들만의 전유물이다. No.
    - https://robotics-transformer-x.github.io/

#### 2.1 텍스트를 생성하는 LLM과 행동을 만드는 피지컬 AI의 차이

- 생각을 잘하는 만큼이나, 안전하게/정확하게/반복 가능하게 행동하는 것
- 입력과 출력의 형태
    - 입력: 카메라 영상, 깊이 센서, 관절 각도, 속도, 힘/토크, GPS, IMU, 배터리 상태, 주변 객체의 위치 정보
    - 출력: 복합적
---

# 생각에서 행동으로: 피지컬 AI 핵심 아키텍처 이해하기

### LLM플래닝: 사람의 말을 실제 행동으로 바꾸는 첫 번째 방법

#### 3.1 LLM을 이용한 로봇의 행동 계획 세우기
- [SayCan(2022)](https://say-can.github.io/)
![](https://velog.velcdn.com/images/erdosnumber0/post/22829080-8c68-4374-946a-a8658e1391e3/image.gif)

  - LLM: 무엇을 해야 할 것 같은가 제안
  - 로봇의 가치함수: 그 행동이 지금 실제로 가능한가 평가
  - 두 정보를 결합해 다음 행동 선택
  - 의의: 이 역할을 나눔으로써, 로봇이 복잡한 언어 명령어를 더 유연하게 이해할 수 있고, 동시에 실제 환경에서 불가능한 행동을 어느 정도 걸러낼 수 있었다. 미리 준비된 스킬만 있다면, 이 스킬들의 조합으로 더 긴 작업을 수행할 수도 있었다.
  - 한계: 로봇이 사용할 수 있는 행동 단위가 미리 준비되어 있어야 한다. LLM이 아무리 좋은 계획을 세워도 그 계획을 실행할 원시 행동이나 스킬이 없다면 실제 행동으로 이어질 수 없음. 또한, 가치 함수가 정확하지 않으면 실행 가능성 평가도 흔들릴 수 있다.


#### 3.2 계획하는 모델에서 보는 모델로:PaLM-E(2023)

- [PaLM-E(2023): An Embodied Multimodal Language Model](https://palm-e.github.io/)

![](https://velog.velcdn.com/images/erdosnumber0/post/602c53ce-fbb6-4084-8e97-a548b9bdbed9/image.gif)



- 핵심: 로봇이 "보는 것"과 "말하는 것"을 하나의 문장 구조 안으로 연결
- 의의: 웹과 비전 도메인에서 학습된 표현 자체를 체화 모델 안으로 주입하고 그 전이 효과를 실험적으로 보여준 모델 -> VLA 흐름으로 이어지는 다리 역할

#### 3.3 함수 호출과 코드 생성으로 로봇을 움직이는 역할: ChatGPT for Robotics(2023)
- [ChatGPT for Robotics(2023)](https://www.microsoft.com/en-us/research/articles/chatgpt-for-robotics/)

![](https://velog.velcdn.com/images/erdosnumber0/post/88b7e61c-dc37-41f3-8025-cadeae2aa4a0/image.png)

- 핵심 아이디어: 로봇이 사용할 수 있는 고수준 라이브러리 설계
- 이 함수들을 언어 모델이 잘 사용할 수 있도록 프롬프트를 구성하는 프롬프트 엔지니어링

- 사용자가 자연어로 목표를 말하면, 언어 모델이 이를 상위 함수 체인으로 바꾸는 user on the loop 구조 지향. 여기서 ChatGPT는 사람과 로봇 시스템 사이에서 계획과 코드를 다듬는 협업형 상위 계층에 가깝다.

![](https://velog.velcdn.com/images/erdosnumber0/post/80e3cafd-b972-4fea-8e76-f5f32e0f100d/image.jpg)



----
### VLA 모델의 탄생: 판단을 넘어 직접 행동하는 AI로

VLA: Vision-Language-Action

계획만 언어 모델에 맡길 것이 아니라, 로봇의 행동 정책 자체도 대규모 모델로 일반화할 수는 없을까?

#### RT-1: 실제 로봇 제어도 Transformer로 스케일링할 수도 있다(2022)
- [Robotics Transformer for Real World Control at Scale](https://robotics-transformer1.github.io/)

![](https://velog.velcdn.com/images/erdosnumber0/post/6047d02f-c78f-4e4b-9ca1-ff98dfef06d5/image.gif)

- 목적: 많은 로봇 데이터를 모아 하나의 모델을 학습시키면, 로봇 정책(policy)도 새로운 지시문 조합, 새로운 배경, 방해 물체가 많은 장면에서 더 잘 일반화할 수 있는지를 확인

- 의의: (스케일링에 대한 논의 제시). 단순히 데이터 개수만 많은 것보다,  작업 다양성이 일반화에 더 중요하다. 같은 작업을 수천 번 반복해서 찍는 것만으로는 한계가 있고, 서로 다른 물체와 서로 다른 상황, 서로 다른 지시문을 폭넓게 포함하는 데이터셋을 만드는 것이 일반화에 훨씬 도움이 된다. 로봇 정책을 키우려면 단순히 모델만 키워서는 안 된다. 다양한 작업, 다양한 물체, 다양한 환경, 다양한 실패 상황이 포함된 데이터가 필요하다. RT-1은 로봇 제어를 스케일링 가능한 학습 문제로 바라보게 만든 중요한 전환점이었다.

#### 4.3 RoboCat: 여러 로봇 몸체와 작업으로 확장되는 범용 정책(2023)

- [RobotCat](https://deepmind.google/blog/robocat-a-self-improving-robotic-agent/)
- 기존 범용 모델이 새 작업을 조금 배우고, 그걸 바탕으로 더 많은 데이터를 스스로 만든 뒤, 다시 범용성을 넓힌다는 구조를 제시.
- 더 다양한 몸체(embodiment)와 자기 개선(self-improvement) 방향으로 확장한 연구

#### 4.4 RT-2:웹 지식이 로봇 행동으로 전이되다(2023)
- [Vision-Language-Action Models Transfer Web Knowledge to Robotic Control](https://robotics-transformer2.github.io/)
![](https://velog.velcdn.com/images/erdosnumber0/post/87ad3d43-9569-4238-aadb-c2c9c42c597f/image.png)
![](https://velog.velcdn.com/images/erdosnumber0/post/a39090f2-2002-4ca0-93e4-92a2ba6e81ec/image.png)

- 시각, 언어, 행동 모델이 웹에서 배운 지식을 로봇 제어로 옮길 수 있는가
- 의의: 시각, 언어, 행동을 하나의 모델 안에서 연결하고, 웹에서 학습한 일반 지식을 실제 제어로 전이하는 문제로 다시 정의. VLA 흐름을 대표하는 중요한 전환점

![](https://velog.velcdn.com/images/erdosnumber0/post/bc332ab6-8246-4938-afff-da058011658c/image.jpg)

> VLA를 키우려면 어떤 데이터 생태계가 필요할까?

---

### 오픈 로봇 데이터와 범용 모델 생태계

#### 5.2 Open X-Embodiment와 Octo
- [Open X-Embodiment](https://robotics-transformer-x.github.io/)
- [Octo](https://octo-models.github.io/)

![](https://velog.velcdn.com/images/erdosnumber0/post/3fbc6ea0-dbe0-4452-b75c-4ff7d5915025/image.png)


- 의의: 강력한 사전 학습 기반 위에서 각 현장에 맞는 빠른 적응을 가능하게 하는 기반 정책(foundation policy)
- 한계: 단일 로봇팔(single-arm)과 양팔 조작(dual-arm manipulation) 중심으로 학습, 평가되었고 네비게이션이나 사족 보행(quadruped locomotion) 같은 영역까지 직접 다루지는 않음. 또 손목 카메라(wrist camera) 정보 활용이 충분히 강하지 않다는 점, 언어 조건과 목표 이미지 조건 사이에 성능차이가 있다는 점.

#### 5.3 OpenVLA: 오픈소스 생태계가 제어 명령에서 범용 AI로 진화

- [OpenVLA](https://openvla.github.io/)
![](https://velog.velcdn.com/images/erdosnumber0/post/aa442d5c-ddfd-444f-9524-b147f6481477/image.png)

---

### VLA에는 왜 중간 표현과 연속 액션이 필요했을까?
'보고 말귀를 알아듣고 바로 움직이는 모델' -> '행동하기 전에 장면을 해석하고, 목표를 만들고, 그 목표를 실제 움직임으로 바꾸는 모델'

#### 6.2 RT-H: 행동 사이에 언어적 중간 표현을 두는 방법
- [Action Hierarchies Using Language](https://rt-hierarchy.github.io/)
- 고수준 명령과 저수준 제어 사이에 해석 가능하고 수정 가능한 중간층을 둔 연구
- 의의: 이후 명시적 추론, 중간 목표 생성, 듀얼 시스템 로봇 구조로 이어지는 중요한 선행 사례

#### 6.3 π₀와 RDT-1B: 연속 액션을 부드럽게 생성하는 방법
- 로봇의 실제 액션을 어떤 방식으로 생성해야 하는가?
- π₀: flow matching을 이용해 연속 액션 분포를 직접 생성
  - flow matching: 무작위 노이즈에서 시작해 점점 그럴듯한 연속 액션으로 바꿔가는 생성 방식
  - 두뇌는 시각/언어 모델의 힘을 빌리고, 손발은 로봇 물리에 맞게 다시 설계한 구조
- [RDT-1B: a Diffusion Foundation Model for Bimanual Manipulation](https://rdt-robotics.github.io/rdt-robotics/)
![](https://velog.velcdn.com/images/erdosnumber0/post/1b515f86-f419-45b4-9317-1e5688dce519/image.png)
- 의의: 행동도 토큰처럼 생성될 수 있지 않을까의 한계 -> 정밀한 물리 제어에는 한계가 있다. 의미 이해와 계획은 언어 모델의 강점을 빌릴 수 있지만, 실제 손발의 궤적은 텍스트 문법만으로 다루기 어렵다. 그러니 로봇 행동을 언어처럼 다룬다는 발상을 시맨틱 계층에는 남겨두되, 실제 출력 계층은 연속 생성 모델로 분화시키기 시작. 이러한 흐름이 후에 VLA 내부에서 추론 계층(reasoning layer), 액션 전문가(action expert), 하위 제어기가 점점 분리되는 기술적 토대가 됨.

#### 6.4 NaVILA: 이동 로봇에 계층형 구조가 필요한 이유
- [Navila: vision-and-language navigation](https://navila-bot.github.io/)
- 카메라로 본 장면과 자연어 지시를 함께 이해해 이동하는 문제
- 어디로 가야하는지를 해석하는 층 + 그것을 실제로 넘어지지 않고 걷는 동작으로 바꾸는 층을 분리한 모델

---
### 명시적 추론과 듀얼 시스템 설계

#### 7.2 CoT-VLA: 행동 전에 목표 장면을 먼저 추론하는 방법
- [CoT-VLA](https://cot-vla.github.io/)
- 의의: '길게 설명하는 텍스트'에서 '행동에 직접 쓰이는 미래 시각 상태'로 옮겨 놓았다. 


#### 7.4 GROOT N1, π₀.₅: 계층형 시스템 설계가 주목받는 이유
- [GROOT N1](https://wikidocs.net/366379)
- dual-system architecture를 가진 VLA
- 느리지만 신중하게 장면과 지시를 해석하는 계층과, 빠르게 실제 행동을 만들어내는 계층을 나누는 구조


- [π₀.₅: a VLA Model with Open-World](https://wikidocs.net/328763) 
![](https://velog.velcdn.com/images/erdosnumber0/post/133fd006-4a04-4f37-aec0-3d43e35a91be/image.png)

- 오픈 월드 일반화, 즉 훈련 때 보지 못한 새로운 실제 환경에서도 일반화되는 능력을 목표로 잡고 있다.
- 일반화: 학습한 데이터만 잘 외우는 것이 아니라, 처음 보는 집, 물체, 배치에서도 적절히 행동할 수 있는 성질
- 웹 데이터, 객체 검출 데이터, 하위 과업 라벨, 서로 다른 로봇 플랫폼에서 수집한 행동 데이터까지 함께 섞어 학습

> 상위 추론 계층이 장면을 이해한다고 할 때, 그 장면과 지식은 어떤 형태로 표현되어야 할까?
(이미지 픽셀만 보는 것이 아니라, 물체, 공간, 관계, 규칙, 가능 행동을 함께 다뤄야 한다. 온톨로지, 객체 중심 표현, 3D 장면 그래프 같은 구조화된 지식 표현이 다시 중요해지는 이유는?)

---
### 온톨로지와 장면 그래프로 현실 세계 구조화하기
- ontology
- scene graph
- OG-RAG를 통해 온톨로지가 LLM과 RAG에서 어떤 역할을 하는지 
- 3D장면 그래프와 로봇 온톨로지를 결합해 행동 가능한 지식 기반을 만드는 흐름
- 피지컬 AI의 주류 모델을 대체하는 기술이라기보다, 상위 추론 계층을 보강하는 기술.

#### 8.1 온톨로지와 OG-RAG:단순 검색을 넘어 구조화된 지식으로
- [OR-RAG(Ontology-Grounded Retrieval-Augmented Generation For Large Language Models)](https://arxiv.org/abs/2412.15235)
- ontology: 어떤 분야에서 중요한 대상이 무엇이고, 그것들이 서로 어떤 관계를 맺는지를 명확한 형태로 정리해 둔 지식 구조
  - 중요한 이유: 정보가 단순한 문장 조각의 집합으로만 존재하지 않기 때문에. 실제 도메인 지식은 여러 개념과 사실이 함께 묶여야 의미가 분명해진다.
- 기존 RAG처럼 문서를 기계적으로 나누어 검색하는 데서 그치지 않고, 도메인 온톨로지를 활용해 문서 속 정보를 구조화한 뒤 검색에 활용
- 문서를 자르기 전에 해당 도메인의 전문가가 미리 정의해 둔 온톨로지 체계를 기준으로 문서 내의 다양한 사실들을 선별하고 구조화 -> 정리된 지식을 하이퍼그래프(hypergraph)라는 구조로 변환

#### 8.2 공간을 이해하는 AI: 3D 장면 그래프를 활용한 상위 추론 레이어 설계

- 장면 그래프 + 온톨로지 결합으로 단순환 환경 데이터는 로봇이 작업 계획에 활용할 수 있는 행동 가능한 지식(actionable knowledge)으로 바뀐다.