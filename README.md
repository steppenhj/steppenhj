# 박해진 · Park Haejin

경북대학교 응용생물학 · 컴퓨터학부 인공지능컴퓨팅(복수전공) · 2027년 2월 졸업 예정
임베디드 SW를 공부하고 있습니다. MCU 펌웨어와 임베디드 리눅스, 두 프로세서 사이의 통신과 안전 정지를 주로 다룹니다.

## 프로젝트

### [Neuro-Drive](https://github.com/steppenhj/Neuro-Drive) — RPi 5 + STM32 분산 제어 RC카
라즈베리파이 5(Linux)가 웹 조종·네트워크·모드 관리를, STM32(FreeRTOS)가 모터 제어와 안전 정지를 맡는 Ackermann 조향 RC카입니다.

- RPi 5 단독 제어(I2C · PCA9685)로 시작했지만 리눅스 유저 공간에서는 제어 주기를 보장할 수 없어 STM32를 분리했습니다. 모터 태스크는 `osDelayUntil` 로 10ms 주기를 고정했습니다.
- 통신이 500ms 끊기면 정지합니다. 같은 감시를 STM32 태스크와 호스트 C++ 코어 두 층에 뒀습니다.
- Return-to-Home(왔던 길 되돌아오기)을 붙이자, 복귀 중 조종 명령이 없는 구간을 워치독이 통신 두절로 오인했습니다. 복귀 중에는 keep-alive를 보내 '명령 없음'과 '링크 두절'을 갈랐습니다.
- UART로 펌웨어를 바꾸는 부트로더를 직접 짰습니다. CRC를 통과한 이미지에만 유효 표식을 남기고, 부팅 때 표식과 CRC를 다시 확인해 맞을 때만 앱으로 넘어갑니다. 전송을 중간에 끊어도 반쯤 쓴 이미지로 넘어가지 않는 것을 보드에서 확인했습니다. 단일 슬롯이라 롤백은 없습니다.
- F446RE로 옮기다 조향 서보가 탔습니다. 석 달 뒤 커밋 이력을 거슬러 올라가 모터와 서보의 출력 타이머가 뒤바뀐 편집을 찾았고, 분석을 README에 남겼습니다.
- IBM Rhapsody·StarUML로 유스케이스·클래스·시퀀스·상태차트를 그렸습니다.

`C` `C++17` `FreeRTOS` `STM32F411RE` `STM32F446RE` `Raspberry Pi 5` `UART` `UDP` `I2C`

### [rpi5-camera-bsp](https://github.com/steppenhj/rpi5-camera-bsp) — 카메라를 커널 단부터 다시 올리기
라즈베리파이 5 카메라 모듈 3(IMX708)을 자동 인식 없이, 직접 쓴 디바이스 트리 오버레이와 직접 빌드한 센서 드라이버로 다시 올렸습니다. 사진을 찍을 때 일어나는 모드 전환 시간을 재서 줄였습니다.

- 모드 전환 1회 75.1ms → 45.7ms(전원 관리 수정 백포트) → 14.3ms(카메라 I2C 100 → 400kHz)
- 드라이버 안에서 `ktime`으로 쟀고, 단계별로 20 · 10 · 25회 평균입니다.

`C` `Linux kernel module` `Device Tree` `I2C`

### [multi-mcu-can](https://github.com/steppenhj/multi-mcu-can) — STM32 두 노드 CAN 2.0 통신
Neuro-Drive의 CAN 단계를 떼어내 버스와 프로토콜만 다룬 프로젝트입니다.

- F446RE(내장 bxCAN)와 F411RE(bxCAN이 없어 SPI로 MCP2515)를 500kbps 한 버스에 묶어 하트비트를 서로 주고받았습니다. 양 끝 120Ω 종단.
- 500kbps는 자동차에서 흔히 쓰는 속도이면서, 두 보드 클럭(45MHz · 8MHz)에서 모두 오차 없이 나눠떨어져서 골랐습니다.
- 전원·GND → 루프백 → 2노드 순서로, 아래 단계가 확인되기 전엔 다음 단계를 올리지 않았습니다.
- RPi 5를 셋째 노드로 붙이는 단계는 MCP2515 모듈의 5V 출력이 RPi 3.3V GPIO와 맞지 않아 보류 중입니다.

`C` `STM32 HAL` `bxCAN` `MCP2515` `SPI`

## 자격
정보처리기사(2026) · AWS Certified Cloud Practitioner(2025)

## 연락
hermann8hesse@gmail.com
