# 박해진 | Park Haejin

> 경북대학교  
> 임베디드 SW

📧 [hermann8hesse@gmail.com](mailto:hermann8hesse@gmail.com)

---

### Featured Projects

#### 🚗 [Neuro-Drive-CPP](https://github.com/steppenhj/Neuro-Drive-CPP) — Distributed UGV Control System
RPi5(Linux) + STM32(FreeRTOS) 이종 프로세서 분산 제어 플랫폼. Ackermann 조향 RC카에서 soft real-time과 hard real-time을 물리적으로 분리하고, 둘 사이의 협력·Fail-Safe를 설계.

- **Distributed Architecture** — RPi5는 네트워킹·모드 관리, STM32는 100Hz 모터 제어. 책임 분리로 어느 한쪽이 실패해도 시스템이 무너지지 않음
- **FreeRTOS Task Design** — UART ISR + Queue, Motor/Encoder/Safety Task, mutex 보호 공유 상태
- **OTA Firmware Update** — 커스텀 부트로더, CRC 핸드셰이크, 섹터 단위 Flash 관리
- **Return-to-Home + Watchdog** — Keep-Alive 패턴으로 워치독과 자율주행의 충돌 해결, 8B → 12B 프로토콜 확장
- **MBSE Documentation** — IBM Rhapsody / StarUML로 UseCase·Class·Sequence·Statechart 일관 모델링

`C++17` `C` `FreeRTOS` `STM32` `Raspberry Pi 5` `UART` `UDP` `WebSocket`

#### 🔗 [multi-mcu-can](https://github.com/steppenhj/multi-mcu-can) — CAN 2.0 Multi-MCU Communication
Neuro-Drive Phase 6를 독립 레포로 분리해, 액추에이터 계층을 걷어내고 **버스·프로토콜·검증 규율** 자체에 집중한 후속 프로젝트.

- **3-Node CAN 2.0 Bus** — STM32F446RE(bxCAN) + STM32F411RE(bxCAN) + RPi5(MCP2515/SPI), 500kbps, 120Ω 양단 종단
- **UDS / ISO-15765 스타일 ID 할당** — Heartbeat(0x010~), Status(0x100~), Diagnostic(0x7E0~)으로 우선순위·진단 분리
- **단계별 검증 방법론** — Phase 0(전원·GND) → Loopback → 2노드 → 3노드 → 스케줄링 → Bus-off 복구. 각 Phase가 독립 빌드·회귀 테스트 가능
- **Roadmap** — CAN-FD, ISO-TP, UDS 서비스 구현

`C` `STM32 HAL` `bxCAN` `MCP2515` `SocketCAN` `Python`

---

### Tech Stack

**Languages**  
![C](https://img.shields.io/badge/C-A8B9CC?style=flat-square&logo=c&logoColor=white) ![C++](https://img.shields.io/badge/C++-00599C?style=flat-square&logo=cplusplus&logoColor=white)

**Embedded & Real-Time**
- **MCU / SBC** — `STM32F411RE` `STM32F446RE` `Raspberry Pi 5`
- **RTOS** — `FreeRTOS` (Task / ISR / Queue / Mutex)
- **Protocols** — `CAN 2.0` `UART` `SPI` `I2C` `UDP` `WebSocket`
- **OS** — `Linux (Ubuntu)` `Embedded Linux` `SocketCAN`

**Tools**  
`STM32CubeIDE` · `VS Code` · `Git / GitHub` · `IBM Rhapsody` · `StarUML`

**Certifications**  
`AWS Certified Cloud Practitioner`

---

📧 **Contact** — [hermann8hesse@gmail.com](mailto:hermann8hesse@gmail.com)
