---
date: 2026-08-26
categories:
  - yeonjunky
authors:
  - yeonjunky
---

# 지난 2주: 실제 Dynamixel 제어 기반과 하드웨어 없는 테스트 환경 만들기

지난 2주(8월 12일~26일)에 [util-scripts](https://github.com/ajin-robot-hand/util-scripts)와 [MockPortHandler](https://github.com/ajin-robot-hand/MockPortHandler)에 다음 작업을 반영했습니다.

<!-- more -->

## 한눈에 보기

| 저장소 | 주요 변경 |
| --- | --- |
| `util-scripts` | 장치 탐색·상태 조회 스크립트, XL430 제어 테이블, 하드웨어 안전 가이드 |
| `MockPortHandler` | Protocol 2.0/XL430 mock, 포트 API, 단위 테스트, 한·영 README |

## `util-scripts`

### 브로드캐스트 탐색과 상태 스캔

먼저 DynamixelSDK를 프로젝트에 연결하고, 두 가지 진단 스크립트를 추가했습니다.

- `broadcast_ping.py`는 Protocol 2.0의 broadcast ping으로 연결된 Dynamixel의 ID, 모델·펌웨어 버전을 주기적으로 보여 줍니다.
- `scan_servo.py`는 여러 baud rate와 ID 범위를 순회하며 장치를 찾고, 발견한 장치의 위치·속도·전압·온도·이동 상태·하드웨어 오류 상태를 읽습니다.

### 명령줄 인자와 WSL 환경 설정

스크립트에 Windows·macOS·Linux/WSL별 기본 시리얼 포트 선택과 `--port`, `--baudrate`, `--max-id` 인자를 추가했습니다.

WSL 환경을 고려해 의존성과 `.gitignore`도 정리했습니다.

### XL430 제어 테이블 정의

제어 테이블 주소와 데이터 길이를 `IntEnum`으로 정의했습니다. `PRESENT_POSITION`, `GOAL_POSITION`, `TORQUE_ENABLE` 등의 레지스터 이름을 포함했습니다.

이번에는 기본적인 상태·목표값 레지스터 외에도 다음 튜닝·보호 항목을 주석으로 정리했습니다.

- 위치 P 게인과 향후 PID/피드포워드 튜닝 항목
- 전압·온도 제한 및 하드웨어 오류 시 종료 조건
- 통신 단절 시 토크 차단에 활용할 수 있는 bus watchdog

### 하드웨어 안전 가이드 작성

`dynamixel_hardware_guide.md`에 전원 인가 상태에서 케이블을 만지지 않기, 7개 모터의 전류를 고려한 전원 라인 분산, 대기 중 전원 차단, 토크가 걸린 관절에 외력을 가하지 않기 등의 수칙을 정리했습니다.

**전원 ON → 포트 개방·ping 검증 → 제어 → 토크 해제와 포트 종료 → 전원 OFF** 순서의 제어 루틴을 문서화했습니다. 장치 탐색 스크립트에는 `SIGINT` 처리로 포트를 닫는 정리 경로도 추가했습니다.

## `MockPortHandler`

`MockPortHandler`에서는 DynamixelSDK의 포트 계층을 본뜬 메모리 기반 포트와 XL430 유사 장치를 구현했습니다. 포트를 열면 기본 mock 장치가 생성되고, 패킷을 쓰면 해당 장치가 처리한 Status Packet을 읽을 수 있습니다.

### Protocol 2.0 패킷 처리 구현

- 통신 상수와 CRC-16 계산
- 패킷 파싱·길이 검증·byte stuffing
- Status Packet 생성과 CRC 검증
- `PING`, `READ`, `WRITE`, `REG_WRITE`, `ACTION`, `REBOOT`, `FACTORY_RESET` instruction 처리
- broadcast PING의 응답과 broadcast WRITE/REG_WRITE의 무응답 규칙

`MockXL430`은 모델 번호, 펌웨어 버전, 토크 활성화, 목표 위치 등의 제어 테이블 상태를 메모리에 보관합니다.

### 단위 테스트 추가

패킷 생성과 Status Packet 검증을 위한 테스트 헬퍼를 추가하고, 다음 범위의 단위 테스트 21개를 추가했습니다.

- 포트 열기·닫기, baud rate, 버퍼 비우기, 타임아웃
- ping과 모델/펌웨어 정보 읽기
- 토크와 목표 위치 쓰기 및 읽기
- 잘못된 대상 ID와 잘못된 READ 패킷 처리
- byte stuffing 이후의 CRC 검증
- `REG_WRITE` 후 `ACTION`, `REBOOT`, broadcast 동작
