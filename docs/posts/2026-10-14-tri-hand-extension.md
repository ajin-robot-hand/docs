---
title: "로봇손 파지 프로젝트의 확장: 시뮬레이션, 실시간 비전 조작, 오디오 동기화 안무"
description: "로봇손 프로젝트를 확장하여 가상 시뮬레이션, 실시간 비전 텔레옵, 음악 동기화 안무까지 구현한 tri_hand 개발기"
date: 2026-10-14
categories:
  - yeonjunky
  - carryplz
  - erdoslibrary
authors:
  - yeonjunky
  - carryplz
  - erdoslibrary
---

<div class="nerfies-wrapper" markdown="1">

<!-- ========================================== -->
<!-- HERO HEADER                                -->
<!-- ========================================== -->
<div class="nerfies-hero">
  <h1 class="nerfies-title">
    로봇손 파지 프로젝트의 확장:<br>시뮬레이션, 실시간 비전 조작, 오디오 동기화 안무
  </h1>
  <p class="nerfies-subtitle">
    기본 물체 파지를 넘어, MuJoCo 시뮬레이션 환경 구축부터 웹캠 원격 제어와 음악 비트 안무까지 확장한 3지 7자유도 로봇손 프로젝트입니다.
  </p>

  <div class="nerfies-authors">
    <span class="nerfies-author"><a href="https://github.com/yeonjunky" target="_blank">Yeonjun Kim</a><sup>1</sup></span>
    <span class="nerfies-author"><a href="https://github.com/carryplz" target="_blank">Carryplz</a><sup>1</sup></span>
    <span class="nerfies-author"><a href="https://github.com/erdoslibrary" target="_blank">Erdoslibrary</a><sup>1</sup></span>
  </div>
  <div class="nerfies-affiliations">
    <span><sup>1</sup>Robot Hand Team / ajin-robot-hand Research Group</span>
  </div>

  <div class="nerfies-btn-group" style="display: flex; justify-content: center; flex-wrap: wrap; gap: 0.75rem; margin-bottom: 2rem;">
    <a href="https://github.com/ajin-robot-hand/padak-tri" class="nerfies-btn" target="_blank" style="display: inline-flex; align-items: center; gap: 0.5rem; padding: 0.55rem 1.25rem; border-radius: 9999px; background-color: #1e293b; color: #ffffff !important; font-size: 0.92rem; font-weight: 600; text-decoration: none;">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
      Code: padak-tri (Choreography)
    </a>
    <a href="https://github.com/ajin-robot-hand/tri_hand" class="nerfies-btn secondary" target="_blank" style="display: inline-flex; align-items: center; gap: 0.5rem; padding: 0.55rem 1.25rem; border-radius: 9999px; font-size: 0.92rem; font-weight: 600; text-decoration: none;">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
      Code: tri_hand (Teleop &amp; Sim)
    </a>
  </div>
</div>

<!-- ========================================== -->
<!-- TEASER MEDIA: HERO DEMO VIDEO              -->
<!-- ========================================== -->
<div class="nerfies-teaser" style="margin: 1.5rem 0 2.5rem 0; background-color: #0f172a; border-radius: 16px; padding: 1rem; box-shadow: 0 12px 30px rgba(0,0,0,0.15); overflow: hidden;">
  <div class="nerfies-video-responsive" style="position: relative; padding-bottom: 56.25%; height: 0; overflow: hidden; border-radius: 10px;">
    <iframe 
      src="https://www.youtube.com/embed/2_KnKuTeGbY?rel=0&modestbranding=1" 
      title="tri_hand Music-Synchronized Choreography Demo" 
      style="position: absolute; top: 0; left: 0; width: 100%; height: 100%; border: 0; border-radius: 10px;"
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
      referrerpolicy="strict-origin-when-cross-origin" 
      allowfullscreen>
    </iframe>
  </div>
  <p class="nerfies-caption" style="margin-top: 1rem; font-size: 0.92rem; color: #cbd5e1; text-align: center;">
    <strong>Teaser: Music-Synchronized Choreography (135 BPM):</strong> 오디오 DAC 클럭을 기준으로 삼아 0.2ms 이하의 오차로 음악에 맞춰 움직이는 로봇손 안무 영상입니다. (<a href="https://youtu.be/2_KnKuTeGbY" target="_blank" style="color: #60a5fa; text-decoration: underline;">YouTube에서 보기</a>)
  </p>
</div>

<!-- more -->

<!-- ========================================== -->
<!-- SECTION 1: ABSTRACT & CONTRIBUTIONS        -->
<!-- ========================================== -->
<div class="nerfies-section" markdown="1">
  <h2 class="nerfies-sec-title">Abstract &amp; Key Contributions</h2>
  <div class="nerfies-content" markdown="1">

이 프로젝트에서는 3지 7자유도 로봇손을 다룹니다. 음악 비트에 맞춰 안무를 수행하는 **`padak-tri`**를만들었습니다.
`tri_hand`에서 만든 MuJoCo 기구학 모델과 Dynamixel 모터 드라이버를 그대로 가져와, 2PM 노래 "Heartbeat"(135 BPM)에 맞춰 동작하는 안무 제어 엔진(`padak-tri`)으로 확장했습니다.

<hr style="border: 0; border-top: 1px solid #e2e8f0; margin: 1.5rem 0;">

#### 🌟 핵심 엔지니어링 성과

- **시각 메쉬와 충돌체 분리 (Dual-Layer MJCF)**: 눈에 보이는 겉모양 메쉬와 물리 계산용 단순 충돌체(캡슐)를 따로 분리했습니다. 시뮬레이션 연산이 튀는 현상과 손가락끼리 맞물려 끼이는 문제를 막았습니다.
- **기구학 좌표계와 안전 가동 범위(`safe_range`)**: 엄지(Finger A)와 나머지 두 손가락(Finger B, C)이 마주 보는 구조에 맞춰 관절 회전 방향 부호를 정리했습니다. 쥐거나 펼 때 모터가 무리하지 않도록 안전 범위를 따로 잡고 부드러운 제어 게인($k_p=12, k_v=0.5$)을 적용했습니다.
- **웹캠 기반 7자유도 실시간 원격 제어 (`tri_hand`)**: 특수 장갑 없이 웹캠 하나로 손 랜드마크 21개를 읽어 로봇손 관절로 1:1 전달합니다. 손이 화면을 벗어나거나 가려져도 로봇이 튀지 않도록 안전 필터를 넣었습니다.
- **규칙 기반 무누적 시간표와 순수 함수 `choreo(t)` (`padak-tri`)**: 노이즈가 있는 센서 반응 대신 135 BPM 비트 격자 기준의 순수 함수를 만들었습니다. 시간이 지나도 지연이나 오차가 누적되지 않고 항상 0 ms를 유지합니다.
- **PortAudio DAC 클럭 동기화 (`heartbeat/audio.py`)**: 사운드카드 저수준 콜백(`outputBufferDacTime`)으로 스피커에서 소리가 실제로 나오는 순간을 직접 계산해, OS 오디오 버퍼 지연을 상쇄하고 음악 비트에 오차 없이 동작을 맞췄습니다.
- **사전 안전 검증 스크립트 (`heartbeat/validate.py`)**: 모터 속도 상한, 안전 가동 범위, 비트 정렬, 음원 길이를 구동 전에 모두 검사하여, 시뮬레이션과 실물 로봇을 같은 파이프라인으로 안전하게 구동했습니다.

  </div>
</div>

<!-- ========================================== -->
<!-- QUANTITATIVE RESULTS (Stat Badges & KPIs)  -->
<!-- ========================================== -->
<div class="nerfies-section" id="results">
<h2 class="nerfies-sec-title">Key Quantitative Highlights (KPIs)</h2>
<div class="nerfies-metrics-grid">
<div class="nerfies-metric-card">
  <div class="nerfies-metric-val">&lt; 0.2 ms</div>
  <div class="nerfies-metric-label">Audio Clock Drift</div>
  <div class="nerfies-metric-desc">12초 재생 기준 벽시계 편차 (시간이 지나도 누적 오차 0 ms)</div>
</div>
<div class="nerfies-metric-card">
  <div class="nerfies-metric-val">&lt; 2.0 ms</div>
  <div class="nerfies-metric-label">Sim Tracking Latency</div>
  <div class="nerfies-metric-desc">MuJoCo 물리 시뮬레이션 추종 지연 (허용 한계 50 ms 이내 유지)</div>
</div>
<div class="nerfies-metric-card">
  <div class="nerfies-metric-val">50 Hz</div>
  <div class="nerfies-metric-label">Control Loop Rate</div>
  <div class="nerfies-metric-desc">20 ms 정주기 실시간 제어 루프로 통신 및 동작 지연 최소화</div>
</div>
<div class="nerfies-metric-card">
  <div class="nerfies-metric-val">&le; 3.0 rad/s</div>
  <div class="nerfies-metric-label">Max Joint Velocity Guard</div>
  <div class="nerfies-metric-desc">보간 곡선 가속도까지 계산해 순간 최대 각속도 상한 준수</div>
</div>
<div class="nerfies-metric-card">
  <div class="nerfies-metric-val">Zero (0)</div>
  <div class="nerfies-metric-label">Collision &amp; Limit Violation</div>
  <div class="nerfies-metric-desc">자가 충돌(Self-Collision) 및 가동 범위 위반 0건 확인</div>
</div>
<div class="nerfies-metric-card">
  <div class="nerfies-metric-val">64 / 64 (100%)</div>
  <div class="nerfies-metric-label">Unit &amp; Integration Tests</div>
  <div class="nerfies-metric-desc">사전 정적 검증 스크립트 및 테스트 스위트 전수 통과</div>
</div>
</div>

<p style="text-align: center; color: #64748b; font-size: 0.9rem; margin-top: 1rem; margin-bottom: 0;">
  ⚡ <strong>전구간 벤치마크 및 정량 계측 실행:</strong> <code>python src/heartbeat/play.py --headless</code>
</p>
</div>

<!-- ========================================== -->
<!-- SECTION 2: END-TO-END PIPELINE             -->
<!-- ========================================== -->
<div class="nerfies-section" id="pipeline">
  <h2 class="nerfies-sec-title">End-to-End System Pipeline</h2>
  <p style="text-align: center; color: #64748b; font-size: 0.95rem; margin-top: 0; margin-bottom: 1.5rem;">
    모든 동작 명령은 사전 안전 검사를 거친 뒤 시뮬레이터와 실물 로봇손으로 보냅니다.
  </p>

<div class="nerfies-steps-grid">
<div class="nerfies-step-item">
  <span class="nerfies-step-num">Phase 1</span>
  <div class="nerfies-step-title">Digital Twin (MuJoCo)</div>
  <div class="nerfies-step-body">정밀 외형 메쉬와 단순 충돌체를 분리해 물리 연산 안정성을 챙기고, 7개 관절의 회전 기준을 맞췄습니다.</div>
</div>
<div class="nerfies-step-item">
  <span class="nerfies-step-num">Phase 2</span>
  <div class="nerfies-step-title">Sim-to-Real Calibration</div>
  <div class="nerfies-step-body">손가락끼리 부딪히지 않는 안전 범위를 정하고, 모터에 무리가 가지 않도록 부드러운 제어값을 찾았습니다.</div>
</div>
<div class="nerfies-step-item">
  <span class="nerfies-step-num">Phase 3</span>
  <div class="nerfies-step-title">Vision Teleoperation</div>
  <div class="nerfies-step-body">웹캠으로 손가락 굽힘 정도를 실시간 계산해 전달하고, 손을 놓쳤을 때 오작동을 막는 보호 로직을 넣었습니다.</div>
</div>
<div class="nerfies-step-item">
  <span class="nerfies-step-num">Phase 4</span>
  <div class="nerfies-step-title">Audio Choreography</div>
  <div class="nerfies-step-body">스피커 소리 출력 지연을 자동으로 보정해 비트를 맞추고, 음악 시작 전 부드럽게 기본 자세를 잡도록 했습니다.</div>
</div>
</div>
</div>

<!-- ========================================== -->
<!-- SECTION 3: PHASE 1 DEEP DIVE               -->
<!-- ========================================== -->
<div class="nerfies-section" markdown="1">
  <h2 class="nerfies-sec-title">Phase 1: Digital Twin &amp; MuJoCo Physics</h2>
  <div class="nerfies-content" markdown="1">

### 시각 메쉬(Visual)와 충돌체(Collision) 분리

복잡한 3D CAD 메쉬를 물리 시뮬레이터에 그대로 넣으면 접촉 계산량이 크게 늘어납니다. 게다가 메쉬 표면 틈새가 미세하게 맞물리면서 물리 연산이 튀거나 손가락끼리 끼이는 문제가 생깁니다.

- **외형 렌더링 (Visual Mesh)**: 정밀 STL 메쉬는 화면에 보여주는 용도로만 쓰고(`group="1", contype="0", conaffinity="0"`), 접촉 계산에서는 뺐습니다.
- **물리 연산 (Collision Primitives)**: 모델 내부에 캡슐과 상자 같은 단순한 기본 입체 도형(`group="0", contype="1", conaffinity="1"`)을 충돌체로 넣었습니다. 덕분에 50 Hz 이상의 빠른 제어 주기에서도 물리 연산이 안정적으로 돌아갑니다.

<div style="background: var(--md-code-bg-color, #f8fafc); border: 1px solid rgba(148, 163, 184, 0.25); border-radius: 10px; padding: 1.1rem 1.25rem; margin: 1.5rem 0; box-shadow: 0 2px 6px rgba(0,0,0,0.03);">
<div style="display: flex; align-items: center; justify-content: space-between; margin-bottom: 0.85rem; border-bottom: 1px solid rgba(148, 163, 184, 0.2); padding-bottom: 0.5rem;">
<div style="display: flex; align-items: center; gap: 0.5rem; font-weight: 600; font-size: 0.88rem; color: var(--md-typeset-color, #1e293b);">
<span style="display: inline-block; width: 8px; height: 8px; border-radius: 50%; background-color: #3b82f6;"></span>
MuJoCo MJCF 이중 레이어 모델링 (<code>hand.xml</code>)
</div>
<span style="font-size: 0.75rem; font-family: monospace; color: #64748b; background: rgba(148, 163, 184, 0.15); padding: 0.15rem 0.5rem; border-radius: 4px;">XML Snippet</span>
</div>
<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(280px, 1fr)); gap: 0.85rem; font-size: 0.85rem;">
<div style="background: rgba(59, 130, 246, 0.05); border: 1px solid rgba(59, 130, 246, 0.18); border-radius: 6px; padding: 0.85rem;">
<div style="font-weight: 600; color: #2563eb; margin-bottom: 0.4rem; font-size: 0.82rem;">1. Visual Only (외형 렌더링 전용)</div>
<code style="display: block; background: transparent; padding: 0; color: var(--md-code-color, #0f172a); font-family: monospace; font-size: 0.8rem; word-break: break-all; line-height: 1.5;">&lt;geom type="mesh" mesh="finger_vis" group="1" contype="0" conaffinity="0"/&gt;</code>
</div>
<div style="background: rgba(16, 185, 129, 0.05); border: 1px solid rgba(16, 185, 129, 0.18); border-radius: 6px; padding: 0.85rem;">
<div style="font-weight: 600; color: #059669; margin-bottom: 0.4rem; font-size: 0.82rem;">2. Collision Primitive (물리 계산 전용)</div>
<code style="display: block; background: transparent; padding: 0; color: var(--md-code-color, #0f172a); font-family: monospace; font-size: 0.8rem; word-break: break-all; line-height: 1.5;">&lt;geom type="capsule" size="0.012 0.025" group="0" contype="1" conaffinity="1"/&gt;</code>
</div>
</div>
</div>

<hr style="border: 0; border-top: 1px solid #e2e8f0; margin: 1.5rem 0;">

### 기구학 좌표계와 회전 부호 규칙 (Kinematics Conventions)

물리 시뮬레이터와 실제 Dynamixel 서보 모터가 다르게 움직이지 않도록 좌표계와 회전 방향 기준을 맞췄습니다.

- **중력축과 관절 회전축**: 씬 중력 방향은 `-Y` 축(`gravity="0 -9.81 0"`), 관절 굽힘 회전축은 `+X` 축(`axis="1 0 0"`)으로 통일했습니다.
- **오므림(Grasp/Close) 회전 부호 규칙**:
    - **Finger A (상단 3자유도 엄지)**: **음수(-) 방향**으로 회전해야 오므라듭니다.
    - **Finger B, C (하단 2자유도 손가락 2개)**: **양수(+) 방향**으로 회전해야 오므라듭니다.
    - 상단 손가락과 하단 손가락이 마주 보는 구조(Opposable)이므로, 각 관절의 로컬 프레임에 맞춰 회전 부호를 통일했습니다.
- **엄지 대립 운동 (Yaw Rotation)**: 상단 기저 관절(`A_j0`)은 `±1.0472 rad` (`±60°`) 범위로 회전하여 물체 모양에 맞게 3차원 대립 각도를 바꿉니다.
- **모터 정격 토크**: Dynamixel XL430-W250-T 7개를 사용하며, 모터 과부하를 막기 위해 최대 토크를 1.4 N·m(`forcerange="-1.4 1.4"`)로 제한했습니다.

  </div>
</div>

<!-- ========================================== -->
<!-- SECTION 4: PHASE 2 DEEP DIVE               -->
<!-- ========================================== -->
<div class="nerfies-section" markdown="1">
  <h2 class="nerfies-sec-title">Phase 2: Hardware Bring-Up &amp; Sim-to-Real</h2>
  <div class="nerfies-content" markdown="1">

### 물리적 기구 한계를 반영한 비대칭 가동 범위

실제 서보 모터는 시뮬레이션과 달리 연속해서 돌리면 열이 나고, 기어 유격(백래시)과 부품끼리 부딪히는 물리적 한계가 있습니다. 곧게 펴진 조립 상태(0 rad)를 가동 범위의 정중앙(Neutral)으로 두고, 충돌을 막는 비대칭 안전 가동 범위(`safe_range`)를 정했습니다.

- **비대칭 안전 가동 범위**: 손가락을 쥘 때(`Q_CLOSE`)는 안쪽 충돌을 막기 위해 첫째 관절(`j1`)을 0.3 rad까지만 굽히고 끝 관절(`j2`)을 1.2 rad 굽힙니다. 반대로 펼칠 때(`Q_OPEN`)는 기계적 걸림(Hard Stop)을 피하기 위해 `j1`을 1.2 rad, `j2`를 0.3 rad로 다르게 조절했습니다.
- **부드러운 제어 게인**: 모터가 외력에 억지로 버티며 과열되지 않도록 위치 제어기 게인을 **$k_p=12, k_v=0.5$**로 낮춰 부드럽게 움직이도록 맞췄습니다.

<h4 style="margin: 1.8rem 0 0.8rem 0; font-size: 1.05rem; text-align: center; color: var(--md-typeset-color, #1e293b);">비대칭 관절 안전 가동 범위 (safe_range) 및 파라미터</h4>

<table class="nerfies-specs-table">
  <thead>
    <tr>
      <th>구분</th>
      <th>j1 (기저 관절)</th>
      <th>j2 (말단 관절)</th>
      <th>엄지 요 (A_j0)</th>
      <th>기구학적 설계 목적 및 안전 역할</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>Q_CLOSE (파지)</strong></td>
      <td>0.3 rad</td>
      <td>1.2 rad</td>
      <td>&plusmn;1.0472 rad (&plusmn;60&deg;)</td>
      <td>손가락 간 맞물림 및 내부 자가 충돌(Self-Collision) 방지</td>
    </tr>
    <tr>
      <td><strong>중립 자세 (Neutral)</strong></td>
      <td>0.0 rad</td>
      <td>0.0 rad</td>
      <td>0.0 rad (중앙)</td>
      <td>조립 기준 곧게 편 자세 (가동 범위의 정중앙 기준점)</td>
    </tr>
    <tr>
      <td><strong>Q_OPEN (펼침)</strong></td>
      <td>1.2 rad</td>
      <td>0.3 rad</td>
      <td>&plusmn;1.0472 rad (&plusmn;60&deg;)</td>
      <td>프레임 기계적 걸림 방지 및 손바닥쪽 가동성 확보</td>
    </tr>
    <tr>
      <td><strong>제어기 게인 / 속도</strong></td>
      <td colspan="2">kp = 12, kv = 0.5 (위치 제어기)</td>
      <td colspan="2">최대 관절 속도 상한: <strong>&le; 3.0 rad/s</strong> (급가속 방지)</td>
    </tr>
  </tbody>
</table>

<span style="display: block; text-align: center; font-size: 0.85rem; color: #64748b; margin-top: 0.4rem;">
  * 모든 관절 각도는 0 rad을 중심으로 양방향으로 움직입니다.
</span>

  </div>
</div>

<!-- ========================================== -->
<!-- SECTION 6: PHASE 4 DEEP DIVE               -->
<!-- ========================================== -->
<div class="nerfies-section" markdown="1">
  <h2 class="nerfies-sec-title">Phase 4: Music-Synchronized Choreography (padak-tri)</h2>
  <div class="nerfies-content" markdown="1">

### 1. 규칙 기반 무누적 시간표와 순수 함수 `choreo(t)`

카메라 영상이나 오디오 주파수(FFT)를 실시간으로 분석해 반응하게 만들면, 연산 지연과 프레임 드랍 때문에 박자를 밀리초 단위로 정확히 맞추기 어렵습니다. 또한 주기마다 시간을 더해가는 방식($t \mathrel{+}= \Delta t$)은 컴퓨터 처리가 조금만 밀려도 오차가 쌓여 음악과 로봇 박자가 점점 어긋납니다.

`padak-tri`에서는 2PM 노래 "Heartbeat"(135 BPM)의 안무를 `grid.json` 비트 격자(BPM 135, 첫 박 위치, 총 박자 수)에 맞춰 미리 시간표로 계산했습니다.

- **무상태 순수 함수 (Stateless Pure Function)**: 모든 안무는 음원 재생 시각 $t$(초)만 받아서 7개 관절 목표 각도 $\mathbf{q}(t)$를 계산해 돌려줍니다:
  $$\mathbf{q}(t) = \text{choreo}(t)$$
- **누적 오차 0 ms**: 함수 내부에 이전 상태나 루프 카운터를 저장하지 않고 현재 시각 $t$만 바라보므로, 오디오 재생 위치만 맞으면 몇 시간을 연속으로 돌려도 시간 오차가 쌓이지 않습니다.

<hr style="border: 0; border-top: 1px solid #e2e8f0; margin: 1.5rem 0;">

### 2. PortAudio DAC 하드웨어 오디오 클럭 동기화 (`heartbeat/audio.py`)

일반 운영체제(ALSA, PulseAudio 등)는 소리를 출력할 때 오디오 버퍼(보통 50~150 ms)를 거칩니다. 그래서 코드에서 읽은 시스템 시계(`time.time()`)와 스피커에서 실제로 소리가 나오는 시각 사이에 차이가 생깁니다.

- **`outputBufferDacTime` 콜백 활용**: PortAudio 저수준 버퍼 콜백에서 제공하는 `outputBufferDacTime` 값을 읽어, **스피커에서 소리가 실제로 나오는 물리적 시각을 역추산**했습니다.
- **OS 버퍼 지연 자동 보정**: 스피커 출력 지연을 자동으로 빼서 계산하므로, 12초 연속 재생 기준 **벽시계 편차 &lt; 0.2 ms**, **시뮬레이션 추종 지연 &lt; 2.0 ms**(허용 한계 50 ms 이내) 수준으로 박자를 맞췄습니다.

<hr style="border: 0; border-top: 1px solid #e2e8f0; margin: 1.5rem 0;">

### 3. 급가속 방지 프리롤(Preroll) 시퀀스

음악이 시작될 때 로봇 손이 갑자기 움직여 모터 기어에 충격이 가지 않도록, 2단계 준비 동작(프리롤)을 거칩니다.

1. **부드러운 자세 이동 (`preroll_seconds: 3.0s`)**: 조립 상태(0 rad)에서 첫 누운 자세(-1.0 rad)까지 `smoothstep` 곡선을 따라 3초 동안 천천히 이동해 속도 상한(3.0 rad/s)을 지킵니다.
2. **자세 안정화 대기 (`preroll_settle_seconds: 1.0s`)**: 목표 자세에 도착한 뒤, 위치 제어기($k_p=12, k_v=0.5$)가 중력 처짐을 잡고 흔들림이 멈출 때까지 1초 동안 기다렸다가 음악 재생과 함께 첫 동작을 시작합니다.

<hr style="border: 0; border-top: 1px solid #e2e8f0; margin: 1.5rem 0;">

### 4. 동기화 및 프리롤 튜닝 파라미터

<table class="nerfies-specs-table">
  <thead>
    <tr>
      <th>구분</th>
      <th>파라미터</th>
      <th>기본값</th>
      <th>설명 및 튜닝 가이드</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><strong>동기화</strong></td>
      <td><code>LEAD</code></td>
      <td>0.050 s</td>
      <td>모터 위치 제어기(kp=12, kv=0.5) 물리 추종 지연 보정 (<code>--lead</code> 옵션)</td>
    </tr>
    <tr>
      <td><strong>동기화</strong></td>
      <td><code>AUDIO_OFFSET</code></td>
      <td>0.0 s</td>
      <td>청각 비트 지연 보정 (손이 늦으면 음수, 빠르면 양수, <code>--offset</code> 옵션)</td>
    </tr>
    <tr>
      <td><strong>동기화</strong></td>
      <td><code>VIDEO_OFFSET</code></td>
      <td>0.966 s</td>
      <td>영상과 음원의 상호상관(Cross-correlation) 측정 기준값</td>
    </tr>
    <tr>
      <td><strong>프리롤</strong></td>
      <td><code>preroll_seconds</code></td>
      <td>3.0 s</td>
      <td>조립 상태(0 rad) &rarr; 첫 누운 자세(-1.0 rad) 이동 시간 (속도 상한 준수)</td>
    </tr>
    <tr>
      <td><strong>프리롤</strong></td>
      <td><code>preroll_settle_seconds</code></td>
      <td>1.0 s</td>
      <td>도착 후 중력 처짐을 제어기가 잡고 안정화되는 대기 시간</td>
    </tr>
  </tbody>
</table>

<span style="display: block; text-align: center; font-size: 0.85rem; color: #64748b; margin-top: 0.4rem;">
  * 순수 함수 <code>choreo(t)</code>와 튜닝 파라미터는 시뮬레이션과 실물 로봇에서 코드 수정 없이 그대로 공유합니다.
</span>

  </div>
</div>

<!-- ========================================== -->
<!-- SECTION 7: SAFETY & VALIDATION             -->
<!-- ========================================== -->
<div class="nerfies-section" markdown="1">
  <h2 class="nerfies-sec-title">Safety Guardrails &amp; Static Verifier (`validate.py`)</h2>
  <div class="nerfies-content" markdown="1">

동작을 만들 때 실수하더라도 무리한 명령이 실제 로봇에 들어가지 않도록, 구동 전에 전체 안무를 미리 검사하는 4단계 안전 검증 스크립트(`heartbeat/validate.py`)를 만들었습니다.

#### 1. 순간 최대 각속도 검사
- 관절 회전 속도가 안전 기준인 **&le; 3.0 rad/s**를 넘지 않는지 전 구간을 검사합니다.
- 단순 직선 보간뿐 아니라 곡선 보간 시 가속도가 붙어 순간 속도가 치솟는 현상까지 미리 계산해 모터 과전류와 기어 충격을 막습니다.

#### 2. 비대칭 안전 가동 범위 검사
- 7개 관절 모두 `safe_range` 범위 안에서만 움직이는지 전수 검사합니다.
- 쥘 때($j_1 \le 0.3, j_2 \le 1.2$)와 펼칠 때($j_1 \le 1.2, j_2 \le 0.3$), 엄지 대립 회전($A_{j0} \in [-1.0472, +1.0472]$) 한계를 꼼꼼히 확인합니다.

#### 3. 8분음표 비트 격자 정렬
- 모든 안무 키프레임이 음악의 8분음표 비트 격자에 딱 맞물려 있는지 확인하고, 전체 음원 길이(12초)를 벗어나는 잘못된 명령이 없는지 걸러냅니다.

#### 4. 사전 충돌 검사 및 단위 테스트
- 화면 표시 없이(Headless) 고속 시뮬레이션을 돌려 손가락끼리 부딪히지 않는지 확인합니다(충돌 0건).
- 총 **64개 단위·통합 테스트(100%)**를 모두 통과한 동작 파일만 실물 모터로 보냅니다.

  </div>
</div>

<!-- ========================================== -->
<!-- SECTION 8: VIDEO SHOWCASE GALLERY          -->
<!-- ========================================== -->
<div class="nerfies-section" id="video-gallery" markdown="1">
  <h2 class="nerfies-sec-title">Video Showcase Gallery</h2>
  <p style="text-align: center; color: #64748b; font-size: 0.95rem; margin-top: 0; margin-bottom: 2rem;">
    실시간 웹캠 조작과 음악 동기화 안무의 실제 구동 영상을 확인해 보세요.
  </p>

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(320px, 1fr)); gap: 1.8rem; margin: 1.5rem 0;">
<div style="text-align: center;">
  <div class="nerfies-video-responsive">
    <iframe 
      src="https://www.youtube.com/embed/c8-295kr47s?rel=0&modestbranding=1" 
      title="Webcam Vision Teleoperation Demo" 
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
      referrerpolicy="strict-origin-when-cross-origin" 
      allowfullscreen>
    </iframe>
  </div>
  <p style="margin-top: 0.8rem; font-size: 0.88rem; color: #64748b; line-height: 1.5;">
    <strong style="color: var(--md-typeset-color, #1e293b); font-size: 0.95rem;">1. Real-Time Vision Teleoperation (7-DoF)</strong><br>
    웹캠으로 손 움직임을 실시간 인식해 tri_hand 7개 관절을 원격 조작하고, 손을 놓쳤을 때 튀지 않게 막는 Fail-safe 제어 시연
  </p>
</div>

<div style="text-align: center;">
  <div class="nerfies-video-responsive">
    <iframe 
      src="https://www.youtube.com/embed/2_KnKuTeGbY?rel=0&modestbranding=1" 
      title="Music-Synchronized Choreography Demo" 
      allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" 
      referrerpolicy="strict-origin-when-cross-origin" 
      allowfullscreen>
    </iframe>
  </div>
  <p style="margin-top: 0.8rem; font-size: 0.88rem; color: #64748b; line-height: 1.5;">
    <strong style="color: var(--md-typeset-color, #1e293b); font-size: 0.95rem;">2. Music-Synchronized Choreography (135 BPM)</strong><br>
    오디오 DAC 클럭 동기화로 0.2ms 이하 오차를 유지하며 음악에 맞춰 안무를 수행하는 구동 영상
  </p>
</div>
</div>
</div>

<!-- ========================================== -->
<!-- SECTION 9: HARDWARE SPECS & RESOURCES      -->
<!-- ========================================== -->
<div class="nerfies-section">
  <h2 class="nerfies-sec-title">Hardware &amp; Kinematics Specifications</h2>
  
  <h3 style="margin-top: 0; font-size: 1.15rem; text-align: center;">1. tri_hand Hardware Bill of Materials (BOM)</h3>
  <table class="nerfies-specs-table">
    <thead>
      <tr>
        <th>구분</th>
        <th>부품 및 구성</th>
        <th>세부 사양</th>
        <th>담당 역할</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><strong>Actuator</strong></td>
        <td>ROBOTIS Dynamixel XL430-W250-T (&times;7)</td>
        <td>정격 토크 1.4 N&middot;m, Protocol 2.0</td>
        <td>손가락 A (3관절), 손가락 B (2관절), 손가락 C (2관절) 구동</td>
      </tr>
      <tr>
        <td><strong>Interface</strong></td>
        <td>ROBOTIS U2D2 + Power Hub</td>
        <td>USB to RS485 / TTL, 1 Mbps Baudrate</td>
        <td>PC와 모터 간 고속 제어 신호 통신</td>
      </tr>
      <tr>
        <td><strong>Power</strong></td>
        <td>SMPS DC 12V 5A 전원 공급기</td>
        <td>안정적인 전원 공급</td>
        <td>순간 최대 전류 수용 및 모터 토크 유지</td>
      </tr>
      <tr>
        <td><strong>Kinematics</strong></td>
        <td>3D Printed Modular Frame &amp; Linkage</td>
        <td>PLA+ 고강도 필라멘트 출력</td>
        <td>마주 보는 3개 손가락(Opposable)의 기계 구조 구현</td>
      </tr>
    </tbody>
  </table>

  <h3 style="margin-top: 2rem; font-size: 1.15rem; text-align: center;">2. Kinematics Specs &amp; Coordinate System</h3>
  <table class="nerfies-specs-table">
    <thead>
      <tr>
        <th>항목</th>
        <th>설정값 / 규격</th>
        <th>세부 설명 및 모델링 원칙</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td><strong>좌표계 및 중력축</strong></td>
        <td>중력: -Y 축 (<code>0 -9.81 0</code>)<br>관절축: +X 축 (<code>1 0 0</code>)</td>
        <td>시뮬레이션 환경의 중력 방향과 7개 관절의 회전축을 일치시킴</td>
      </tr>
      <tr>
        <td><strong>오므림(Grasp) 부호</strong></td>
        <td>Finger A: 음수(-) 회전<br>Finger B, C: 양수(+) 회전</td>
        <td>마주 보는 손가락 구조(Opposable)에 맞춰 관절 회전 방향 부호를 통일함</td>
      </tr>
      <tr>
        <td><strong>엄지 대립 운동 (A_j0)</strong></td>
        <td>&plusmn;1.0472 rad (&plusmn;60&deg;)</td>
        <td>엄지 기저부 회전(Yaw)으로 손가락 대립 각도를 조절함</td>
      </tr>
      <tr>
        <td><strong>안전 가동 범위 (safe_range)</strong></td>
        <td>Q_CLOSE: j1 0.3, j2 1.2 rad<br>Q_OPEN: j1 1.2, j2 0.3 rad</td>
        <td>조립 기준(0 rad)을 중심으로 손가락 간 충돌과 프레임 걸림을 막음</td>
      </tr>
      <tr>
        <td><strong>동적 한계치</strong></td>
        <td>토크: 1.4 N&middot;m / 속도: &le; 3.0 rad/s</td>
        <td>토크 제한(1.4 N&middot;m)과 사전 검증 속도 상한으로 모터 과부하를 막음</td>
      </tr>
    </tbody>
  </table>

  <div class="nerfies-btn-group" style="display: flex; justify-content: center; flex-wrap: wrap; gap: 0.75rem; margin-top: 2rem; margin-bottom: 0;">
    <a href="https://github.com/ajin-robot-hand/padak-tri" class="nerfies-btn" target="_blank" style="display: inline-flex; align-items: center; gap: 0.5rem; padding: 0.55rem 1.25rem; border-radius: 9999px; background-color: #1e293b; color: #ffffff !important; font-size: 0.92rem; font-weight: 600; text-decoration: none;">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
      padak-tri Repository
    </a>
    <a href="https://github.com/ajin-robot-hand/tri_hand" class="nerfies-btn secondary" target="_blank" style="display: inline-flex; align-items: center; gap: 0.5rem; padding: 0.55rem 1.25rem; border-radius: 9999px; font-size: 0.92rem; font-weight: 600; text-decoration: none;">
      <svg width="18" height="18" viewBox="0 0 24 24" fill="currentColor"><path d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"/></svg>
      tri_hand Repository
    </a>
  </div>
</div>

<!-- ========================================== -->
<!-- SECTION: LINK TO BASIC PROJECT             -->
<!-- ========================================== -->
<div class="nerfies-section">
  <div style="text-align: center; margin: 3rem 0;">
    <h3 style="margin-top: 0; font-size: 1.25rem; color: var(--md-typeset-color, #1e293b);">
      이전 단계: 3지 다관절 로봇손의 기본 물체 파지
    </h3>
    <p style="max-width: 700px; margin: 0.5rem auto 1.5rem auto; font-size: 0.95rem; color: #64748b;">
      일상 물체 3종(휴지심, 물통, 상자) 대상의 접촉면 설계와 기본 파지 메커니즘을 다룬 선행 프로젝트 글도 함께 확인해 보세요.
    </p>
    <a href="2026-10-14-tri-hand-basic.md" class="nerfies-btn secondary">
      ⬅️ tri-hand-basic 프로젝트 보러가기
    </a>
  </div>
</div>

<!-- ========================================== -->
<!-- SECTION 10: BIBTEX CITATION                -->
<!-- ========================================== -->
<div class="nerfies-section" id="bibtex">
  <h2 class="nerfies-sec-title">BibTeX Citation</h2>
  <p style="text-align: center; color: #64748b; font-size: 0.95rem;">
    본 연구 및 제어 프레임워크를 인용하거나 활용하실 경우 아래 형식을 참조해 주세요.
  </p>
  <pre class="nerfies-bibtex-block"><code>@misc{trihand2026showcase,
  author    = {Yeonjun Kim and Carryplz and Erdoslibrary},
  title     = {로봇손 파지 프로젝트의 확장: 시뮬레이션, 실시간 비전 조작, 오디오 동기화 안무 (tri_hand)},
  year      = {2026},
  publisher = {GitHub},
  howpublished = {\url{https://github.com/ajin-robot-hand/docs}},
  note      = {End-to-End Robotics Showcase: MuJoCo Simulation, Vision Teleoperation, and Audio Synchronization}
}</code></pre>
</div>

</div>

