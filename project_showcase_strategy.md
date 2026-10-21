# tri_hand 프로젝트 쇼케이스 웹페이지 작성 전략 보고서

본 문서는 `tri_hand`(3지 다관절 로봇 손)의 4단계 연구·개발 결과물을 [SayCan](https://say-can.github.io/) 및 [Nerfies](https://nerfies.github.io/) 스타일의 **대중적 로보틱스 학술 프로젝트 웹사이트(Academic Project Page)** 형태로 효과적으로 정리·전시하기 위한 종합 전략 가이드입니다.

---

## 📌 1. 핵심 방향성 및 타깃 독자 정의

- **목표**: 
  - 단순 기능 나열을 넘어 **"가상 시뮬레이션(Digital Twin) ➡️ 실물 하드웨어 배포(Sim-to-Real) ➡️ 실시간 비전 조작(Teleoperation) ➡️ 오디오 정밀 동기화 제어(Choreography)"**로 이어지는 탄탄한 엔드투엔드 로보틱스 엔지니어링 역량을 시각적으로 증명합니다.
- **타깃 독자**: 로보틱스/AI 연구원, 엔지니어, 기술 채용 담당자, 오픈소스 커뮤니티
- **표현 원칙**:
  - **3초 원칙**: 페이지 접속 직후 상단 히어로(Hero) 티저 비디오로 결과물을 한눈에 각인.
  - **1분 원칙**: 파이프라인 다이어그램과 요약(Abstract)으로 전체 아키텍처 이해.
  - **5분 원칙**: 각 단계별 정량적 데이터(오차 0.2ms, 속도 3.0 rad/s 상한 등)와 안전성 설계로 엔지니어링 신뢰성 확보.

---

## 🏛 2. 웹사이트 전체 목차 구성 (Site Architecture)

SayCan 스타일의 1-Page 반응형 웹사이트 섹션 구조입니다.

```
[Hero Header]
  ├── Title, Subtitle, Author / Affiliations
  ├── Quick Action Buttons (Paper/Doc, Code, Video, Dashboard)
  └── Teaser Media (실물 로봇 ↔ MuJoCo 동시 구동 2분할 클립)

[Section 1] Abstract & Key Contributions
  └── 프로젝트 요약 및 핵심 엔지니어링 기여도 3~4가지 불릿 포인트

[Section 2] End-to-End Pipeline Overview
  └── 4단계 워크플로우 한눈에 보기 (인터랙티브/다이어그램)

[Section 3] Phase 1: Digital Twin & MuJoCo Simulation
  └── 정밀 기구학 모델링, 시각 메쉬 ↔ 충돌체 분리, 사전 물리 검증

[Section 4] Phase 2: Hardware Bring-Up & Sim-to-Real Calibration
  └── Dynamixel 제어, safe_range 정의, 비대칭 관절 한계(Q_CLOSE vs Q_OPEN)

[Section 5] Phase 3: Vision-Based Teleoperation
  └── MediaPipe 21 랜드마크 추출, 7-DoF 리타겟팅 수식, Fail-safe 방어 로직

[Section 6] Phase 4: Music-Synchronized Choreography ("Heartbeat")
  └── 오디오 DAC 클럭 동기화, 순수 함수 choreo(t), 프리롤(Preroll) 안착

[Section 7] Safety Guardrails & Quantitative Results
  └── 정밀도(0.2ms), 속도 제한(3.0 rad/s), 정적 검증기(validate.py)

[Section 8] Video Gallery & Comparative Showcase
  └── 상황별(비트 연출, 웹캠 조종, 관절 궤적) 쇼케이스 비디오 그리드

[Section 9] Hardware Specs & Resources
  └── BOM(부품 구성), 오픈소스 코드 링크, 실행 가이드 링크
```

---

## ⚖️ 3. 섹션별 강약 조절 전략 (강조할 것 vs 살짝만 언급할 것)

웹페이지가 지루한 매뉴얼이 되지 않도록, **엔지니어링 의사결정의 이유와 안전성 검증**은 강력히 강조하고, **단순 설치법 및 환경 트러블슈팅**은 최소화합니다.

| 구분 | 🔥 강력하게 강조할 항목 (Deep-Dive & Highlight) | 💧 살짝만 언급할 항목 (Brief / Minimal Note) |
|---|---|---|
| **Phase 1: 가상 모델링 (MuJoCo)** | • **시각 메쉬(Visual)와 충돌체(Collision) 분리 설계**<br>• 복잡한 STL 메쉬 대신 Primitive 박스/실린더를 사용하여 시뮬레이션 안정성 확보 및 초기 자가 충돌(Self-Collision) 원천 차단<br>• 7-DoF 관절 회전축 및 비대칭 부호 규칙(A vs B·C) | • `hand.xml`의 단순 태그 문법 나열<br>• MuJoCo 패키지 설치 명령어(`pip install mujoco`)<br>• 씬 조명/바닥 텍스처 등 렌더링 부가 설정 |
| **Phase 2: 실물 모터 연동 (Sim-to-Real)** | • **기구적 간섭을 반영한 비대칭 안전 가동 범위(`safe_range`)**<br>  - `Q_CLOSE`: 손가락 간 충돌 방지 (`j1` 0.3 rad, `j2` 1.2 rad)<br>  - `Q_OPEN`: 기구 정지점 반영 (`j1` 1.2 rad, `j2` 0.3 rad)<br>• 0 rad(곧게 편 자세)이 범위의 끝이 아닌 중심이라는 물리적 제약 모델링<br>• 모터 정격 토크(1.4 N·m) 한계와 과열/탈조 방지 게인 설계 | • U2D2 통신 패킷 구조 및 Dynamixel Protocol 2.0 세부 스펙<br>• 1,000,000 bps 보드레이트 등 기본 통신 설정<br>• 단순 USB 시리얼 포트 번호 찾는 방법 |
| **Phase 3: 비전 텔레옵 (Teleoperation)** | • **인간 손 ↔ 3지 로봇 손 기구학적 리타겟팅 매핑**<br>  - 검지·중지·약지 ➡️ Finger A·B·C<br>  - 손허리(MCP) ➡️ `j1`, 손가락 끝 마디 합(PIP+DIP) ➡️ `j2`<br>  - 엄지 벌림 ➡️ 대립 요 관절(`A_j0`)<br>• **Fail-safe 안전 제어**: 손 이탈 시 급격한 튐 없이 직전 자세 유지 및 지수 평활(Exponential Smoothing) 필터 | • MediaPipe 라이브러리 내부 딥러닝 아키텍처 설명<br>• OpenCV 웹캠 캡처 루프 코드(`cv2.VideoCapture`)<br>• 단순 카메라 해상도/FPS 세부사항 |
| **Phase 4: 비트 안무 (Heartbeat)** | • **PortAudio DAC 시간 기반 마스터 클럭 동기화**<br>  - 스피커 출력 지연 자동 보정으로 **오차 0.2ms** 달성<br>• **순수 함수 `choreo(t)` 기반 무상태(Stateless) 제어**<br>  - 시간에 따른 누적 드리프트(Drift) 원천 차단<br>• **프리롤(Preroll) 메커니즘**: 음원 시작 전 급가속 방지를 위해 비트 격자 밖에서 누운 자세로 서서히 안착하는 안전 시퀀스 | • 2PM 곡의 예술적/음악적 배경이나 가사 내용<br>• 안무의 각 초(sec)별 정성적 주관적 묘사<br>• 오디오 파일 코덱 변환 과정 |
| **운영 및 인프라** | • **자동 정적 검증 파이프라인 (`validate.py`)**<br>  - 곡 시작 전 관절 속도 상한(3.0 rad/s), 격자 정렬, 가동 범위 위반 여부를 사전 검증해 실물 파손 방지 | • Windows vs WSL2 환경 차이 및 문제 해결기<br>• `usbipd` 명령어 옵션 및 가상환경 설정법<br>*(상세 내용은 GitHub 문서 링크로 유도)* |

---

## 🎨 4. 상세 섹션별 스토리텔링 및 시각 자료(Media) 배치

### 1) Hero Section (첫인상 극대화)
- **비주얼 구성**: 
  - 화면 중앙 상단에 **MuJoCo 시뮬레이션과 실물 로봇 손이 음악에 맞춰 정확히 동일한 궤적으로 춤추는 좌우 2분할(Split) 동영상** 배치.
- **카피라이트 제안**:
  > **로봇손 파지 프로젝트의 확장: 시뮬레이션, 실시간 비전 조작, 오디오 동기화 안무**  
  > *기본 물체 파지에서 더 나아가, MuJoCo 물리 시뮬레이션부터 실시간 웹캠 원격 제어와 음악 비트 안무까지 구현한 3지 다관절 로봇손(tri_hand) 프로젝트*
- **퀵 버튼**: `[Code (GitHub)]`, `[System Demo]`, `[Execution Guide]`, `[Technical Docs]`

### 2) Section 1: Abstract & Section 2: Pipeline
- **핵심 메시지**:
  - "시뮬레이션에서 검증되지 않은 코드는 실물에 넣지 않는다"는 원칙 하에, 가상 공간 모델링에서 실물 조작, 비전 인터페이스, 정밀 오디오 제어까지 하나의 일관된 소프트웨어 스택으로 구축함.
- **다이어그램**:
  - 웹캠 영상 ➡️ MediaPipe ➡️ 리타겟팅 ➡️ `choreo(t)` / `motors.py` ➡️ 실물 로봇 & MuJoCo 뷰어가 대칭으로 연결된 인포그래픽.

### 3) Phase 1: Digital Twin & MuJoCo Simulation
- **스토리텔링**:
  - CAD 모델 메쉬를 MuJoCo로 반입할 때 발생할 수 있는 불안정성을 제거하기 위해, 외형은 고정밀 STL을 사용하되 물리 연산은 경량 프리미티브 박스로 분리.
  - Finger A(상단 3-DoF)와 Finger B, C(하단 2-DoF)의 서로 다른 회전 방향(부호 규칙)을 기구학적으로 표준화.
- **미디어**:
  - 와이어프레임 렌더링 샷 (Visual 메쉬 껍질 안에 단순 Collision 박스가 들어있는 투시 렌더링).

### 4) Phase 2: Hardware Bring-Up & Sim-to-Real Calibration
- **스토리텔링**:
  - 단순 가상 모델을 넘어 실제 로보티즈 Dynamixel 모터(XL430, 1.4 N·m)의 기구적 정지점과 물리적 한계를 정밀 계측.
  - 오므림(`Q_CLOSE`)과 눕힘(`Q_OPEN`)의 관절 배분이 서로 다른 비대칭 안전 가동 영역을 수립하여 모터 부하와 손가락 간 충돌을 방지.
- **미디어**:
  - `motors.py calibrate` 과정을 보여주는 사진 또는 짧은 GIF.
  - 관절 각도 0 rad(중립) 기준으로 양방향 가동 범위를 나타낸 인포그래픽 차트.

### 5) Phase 3: Vision-Based Teleoperation
- **스토리텔링**:
  - 전용 센서 글러브 없이 일반 컴퓨터 내장 웹캠만으로 21개 3D 관절 랜드마크를 추출하고, 사람 손의 굽힘량을 로봇 관절 각도로 실시간 매핑.
  - 통신 지연이나 노이즈로 인한 모터 급발진을 막기 위해 지수 평활 및 손 검출 실패 시 안전 정지(Fail-safe) 레이어 구현.
- **미디어**:
  - 사용자 손(MediaPipe 스켈레톤 오버레이)과 로봇 손이 실시간으로 쥐고 펴는 1:1 비교 영상.

### 6) Phase 4: Music-Synchronized Choreography ("Heartbeat")
- **스토리텔링**:
  - 딥러닝 추론이나 실시간 비전의 지연(Jitter) 문제를 극복하기 위해, 오디오 재생 샘플 수와 DAC 시각을 마스터 클럭으로 삼는 **규칙 기반(Rule-based) 시간표 파이프라인** 구축.
  - 상태가 누적되지 않는 순수 함수 `choreo(t)`를 통해 장시간 재생에도 시간 드리프트 제로 달성.
  - 조립 상태에서 시작 자세로 부드럽게 전환하는 **프리롤(Preroll)**을 도입하여 모터 충격 방지.
- **미디어**:
  - 135 BPM 음악 파형과 관절 목표 각도 곡선이 비트 라인에 정확히 칼박자로 일치하는 타임라인 그래프.
  - 프리롤 구간 동안 손이 서서히 자리를 잡은 뒤 음악과 함께 안무가 시작되는 클립.

### 7) Section 7: Quantitative Results (엔지니어링 완성도)
- **정량적 지표 카드 3선**:
  1. **Clock Drift: < 0.2 ms** (12초 재생 동안 벽시계 대비 편차, 시뮬레이션 어긋남 최대 2 ms)
  2. **Max Joint Speed: ≤ 3.0 rad/s** (가속도 및 피크 속도 상한 엄격 준수)
  3. **Zero Self-Collision** (전구간 헤드리스 시뮬레이션을 통한 바닥 외 접촉 0건 검증)

---

## 🛠 5. 구현 템플릿 및 기술 스택 권장안

SayCan과 동일한 수준의 미려한 웹페이지를 빠르고 완성도 높게 제작하기 위한 권장 기술입니다.

1. **템플릿 베이스**:
   - **[Nerfies Academic Project Template](https://github.com/nerfies/nerfies.github.io)** (HTML / Bulma CSS)
   - 별도의 무거운 프레임워크(React, Next.js) 없이 순수 HTML/CSS 기반으로 가볍고 로딩이 빠르며, GitHub Pages로 즉시 호스팅 가능.
2. **미디어 포맷 최적화**:
   - GIF 대신 **WebM / MP4 루프 비디오** 사용:
     ```html
     <video autoplay loop muted playsinline width="100%">
       <source src="static/videos/demo.mp4" type="video/mp4">
     </video>
     ```
   - 페이지 로딩 속도를 극대화하고 모바일 브라우저에서도 부드럽게 재생되도록 압축.
3. **인터랙티브 요소**:
   - 슬라이더 또는 토글 버튼을 이용해 `[Simulation View]` ↔ `[Real Robot View]`를 겹쳐서 비교해볼 수 있는 이미지/비디오 비교 슬라이더(JuxtaposeJS 등) 적용 고려.

---

## 📋 6. 제작 단계별 체크리스트 (Action Plan)

- [x] **미디어 에셋 준비**:
  - [x] 웹캠 텔레옵 실시간 구동 영상: [YouTube (c8-295kr47s)](https://youtu.be/c8-295kr47s)
  - [x] MuJoCo / 실물 로봇 안무 재생 영상: [YouTube (2_KnKuTeGbY)](https://youtu.be/2_KnKuTeGbY)
  - [x] 2분할(Split) / 비디오 갤러리 쇼케이스 구성 완료
  - [x] CAD 메쉬 ↔ 충돌체 분리 기구학 도식화 완료
- [x] **웹 템플릿 구축**:
  - [x] MkDocs Material 호환 Scoped Nerfies 스타일시트 구성 (`extra.css`)
  - [x] 쇼케이스 포스트 원고 작성 (`docs/posts/2026-10-14-tri-hand-extension.md`)
  - [x] End-to-End Mermaid 파이프라인 및 가동 범위 표 구현
- [x] **배포 및 검증**:
  - [x] GitHub Pages 배포 연동 (`.github/workflows/deploy.yml` + `extra_css`)
  - [x] 모바일 16:9 반응형 비디오 컨테이너 (`.nerfies-video-responsive`) 적용
  - [x] YouTube 임베드 기반 플레이어 최적화
