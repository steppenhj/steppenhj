# 박해진 | Park Haejin

> 경북대학교  
> 임베디드 SW

---

### Featured Projects

#### 🚗 [Neuro-Drive-CPP](https://github.com/steppenhj/Neuro-Drive-CPP) — Distributed UGV Control System
RPi5(Linux) + STM32(FreeRTOS) 이종 프로세서 분산 제어 플랫폼. Ackermann 조향 RC카에서 soft real-time과 hard real-time을 물리적으로 분리하고, 둘 사이의 협력·Fail-Safe를 설계.

- **왜 분산인가** — Phase 1은 RPi5 단독 제어(I2C 모터 드라이버)였으나 제어 주기 편차로 hard real-time 확보가 어려웠고, 이를 계기로 STM32를 분리해 100Hz 모터 제어를 전담시킴
- **Distributed Architecture** — RPi5는 네트워킹·모드 관리, STM32는 100Hz 모터 제어 + 500ms 워치독. 링크가 끊기면 **fail-stop(안전 정지)으로 수렴**하도록 설계
- **FreeRTOS Task Design** — UART ISR → Queue → Motor/Encoder/Safety Task. 상태를 공유·잠그는 대신 **메시지 큐로 전달해 경쟁 자체를 줄이는** 구조
- **OTA Firmware Update** — 커스텀 부트로더, CRC 핸드셰이크, 섹터 단위 Flash 관리
- **Return-to-Home + Watchdog** — RTH 중 명령 공백을 워치독이 통신두절로 오인하는 문제를 Keep-Alive로 해결('명령 없음'과 '링크 두절'을 구분), 8B → 12B 프로토콜 확장
- **Troubleshooting** — MCU 이식 중 서보·모터 드라이버 소손. 코드 내부는 일관돼 있었기에 원인은 **핀·타이머 설정과 코드의 대응 관계**에 있었고, 설정 파일과 커밋 이력을 대조해 출력 타이머가 뒤바뀐 것을 특정
- **MBSE Documentation** — IBM Rhapsody / StarUML로 UseCase·Class·Sequence·Statechart 일관 모델링

`C++17` `C` `FreeRTOS` `STM32` `Raspberry Pi 5` `UART` `UDP` `WebSocket` `I2C`

#### 🔗 [multi-mcu-can](https://github.com/steppenhj/multi-mcu-can) — CAN 2.0 Multi-MCU Communication
Neuro-Drive Phase 6를 독립 레포로 분리해, 액추에이터 계층을 걷어내고 **버스·프로토콜·검증 규율** 자체에 집중한 후속 프로젝트.

- **2-Node CAN 2.0 Bus (검증 완료)** — STM32F446RE(native bxCAN) ↔ STM32F411RE(**bxCAN 미탑재 → MCP2515/SPI**), 500kbps, 120Ω 양단 종단. 양방향 동기 수신·에러 플래그 0 확인
- **CAN ID 우선순위 설계** — Heartbeat(0x010~) / Status(0x100~) / Diagnostic(0x7E0~)으로 대역·진단 분리
- **단계별 검증 방법론** — Phase 0(전원·GND) → Loopback → 2노드 순으로 한 번에 한 층만 올리고, 이전 층이 검증되기 전엔 다음 층을 쌓지 않음
- **Roadmap** — RPi5 게이트웨이 노드(Phase 3, 호환성 이슈로 보류 중), CAN-FD, ISO-TP, UDS 서비스

`C` `STM32 HAL` `bxCAN` `MCP2515` `SPI`

---

### Tech Stack

**Languages**  
![C](https://img.shields.io/badge/C-A8B9CC?style=flat-square&logo=c&logoColor=white) ![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white)

**Embedded & Real-Time**
- **MCU / SBC** — `STM32F411RE` `STM32F446RE` `Raspberry Pi 5`
- **RTOS** — `FreeRTOS` (Task / ISR / Queue)
- **Protocols** — `CAN 2.0` `UART` `SPI` `I2C` `UDP` `WebSocket`
- **OS** — `Linux (Ubuntu)`

**Tools**  
`STM32CubeIDE` · `VS Code` · `Git / GitHub` · `IBM Rhapsody` · `StarUML`

**Certifications**  
`AWS Certified Cloud Practitioner (2024–2026)`

---

📧 **Contact** — [hermann8hesse@gmail.com](mailto:hermann8hesse@gmail.com)
