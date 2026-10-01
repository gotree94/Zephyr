# Zephyr RTOS 및 AWS IoT Core 연동 실무 과정 커리큘럼

---

## 1. 교육 개요

* **과정명**: Zephyr RTOS 기반 임베디드 시스템 개발 및 AWS IoT 클라우드 연동 실무
* **교육 기간**: 2주 (총 10일, 하루 7시간 / 총 70시간)
* **일일 일정**: 10:00 ~ 18:00 (점심시간 13:00 ~ 14:00)
* **교육 대상**: Zephyr RTOS 및 IoT Cloud 애플리케이션 개발 기술을 습득하고자 하는 임베디드 개발자 및 관련 분야 학습자
* **교육 목표**:
  1. Zephyr RTOS의 빌드 시스템(CMake, Devicetree, Kconfig) 및 nRF Connect SDK 환경을 체계적으로 이해하고 구축할 수 있다.
  2. GPIO, UART, I2C, SPI 등 핵심 주변장치 드라이버 API를 제어하고 센서 데이터를 수집할 수 있다.
  3. 스레드, 세마포어, 뮤텍스, 메시지 큐 등 RTOS 멀티태스킹 커널 메커니즘을 이해하고 동기화 프로그램을 작성할 수 있다.
  4. BLE 및 Wi-Fi/Ethernet 기반의 네트워크 연결 디바이스를 제어하고 MQTT 프로토콜로 AWS IoT Core와 통신할 수 있다.
  5. 수집된 센서 데이터를 클라우드로 전송하고, 반대로 클라우드 명령으로 디바이스를 제어하는 엔드투엔드(End-to-End) IoT 프로젝트를 완성할 수 있다.

---

## 2. 주차별 상세 커리큘럼

### [1주차] Zephyr RTOS 기초 및 임베디드 시스템 프로그래밍

#### **1일차: Zephyr RTOS 개요 및 개발 환경 구축**
* **학습 목표**: nRF Connect SDK 기반의 Zephyr RTOS 개발 환경을 구축하고, 빌드 구조 및 로깅 시스템을 이해한다.
* **오전 (10:00 ~ 13:00)**
  * Zephyr RTOS 소개 및 Bare-metal 대비 특징/장점
  * nRF Connect SDK (NCS) 구조 및 West 빌드 도구 이해
  * Configuration files (`prj.conf`), Devicetree Overlay (`.overlay`), CMake, Multi-image build
* **오후 (14:00 ~ 18:00)**
  * 개발 환경 설치 (VS Code, nRF Connect Extension, Toolchain)
  * Zephyr 콘솔 메시지 출력 및 로깅 시스템 (`printk()`, Logger module) 활용 실습
  * 디버깅 기초 및 빌드 타깃 설정

#### **2일차: 기본 주변장치(Peripheral) 제어 (GPIO & UART)**
* **학습 목표**: Devicetree 노드를 조작하여 GPIO 및 UART 프로토콜 기반 주변장치를 제어한다.
* **오전 (10:00 ~ 13:00)**
  * Zephyr Devicetree API 및 GPIO API 구조
  * Blinky 샘플 코드 분석 및 LED/버튼 제어 실습
  * GPIO Interrupt(인터럽트) 및 Callback 처리
* **오후 (14:00 ~ 18:00)**
  * UART Protocol 및 Zephyr UART Driver API
  * Async UART / Interrupt-driven UART 처리
  * 시리얼 통신 기반 CLI(Command Line Interface) 응용 구현

#### **3일차: 직렬 통신 프로토콜 (I2C & SPI) 및 센서 인터페이스**
* **학습 목표**: I2C 및 SPI 드라이버를 활용하여 온습도/조도 센서 및 외장 디스플레이를 제어한다.
* **오전 (10:00 ~ 13:00)**
  * I2C Protocol 및 Zephyr I2C Driver API
  * I2C 온습도 센서(예: SHT3x, BME280 등) 데이터 읽기 실습
* **오후 (14:00 ~ 18:00)**
  * SPI Protocol 및 Zephyr SPI Driver API
  * SPI 센서 또는 Display(OLED) 인터페이스 제어
  * Zephyr Sensor Subsystem API를 활용한 센서 드라이버 추상화 이해

#### **4일차: Zephyr RTOS 멀티 스레드 프로그래밍**
* **학습 목표**: RTOS 스레드 생명주기와 스케줄링 개념을 이해하고 멀티 스레드 애플리케이션을 구현한다.
* **오전 (10:00 ~ 13:00)**
  * Bare-metal 구조와 RTOS 멀티태스킹 비교
  * Zephyr RTOS Thread 개념, 생명주기(Creation, Termination, Sleep), 우선순위(Priority)
  * 정적(Static) 및 동적(Dynamic) 스레드 생성 실습
* **오후 (14:00 ~ 18:00)**
  * Cooperative vs Preemptive 스케줄링 분석
  * Workqueue (System Workqueue, Custom Workqueue) 개념 및 활용
  * 인터럽트 하반부(Bottom-half) 처리를 위한 Workqueue 실습

#### **5일차: 스레드 동기화 및 IPC (Inter-Process Communication)**
* **학습 목표**: 세마포어, 뮤텍스, 메시지 큐를 활용하여 동기화 이슈 및 데이터 공유 문제를 해결한다.
* **오전 (10:00 ~ 13:00)**
  * 공유 자원 경쟁 상태(Race Condition)와 상호 배제
  * Semaphores(세마포어) 및 Mutex(뮤텍스) API 활용 실습
  * 교착 상태(Deadlock) 및 우선순위 역전(Priority Inversion) 방지
* **오후 (14:00 ~ 18:00)**
  * Message Queues 및 Mailboxes를 이용한 스레드 간 데이터 전달
  * Event Flags 및 Atomic Operations
  * 센서 수집 스레드 - 데이터 처리 스레드 간 IPC 실습

---

### [2주차] 네트워크, AWS IoT Cloud 연동 및 미니 프로젝트

#### **6일차: 무선 네트워크 기초 (BLE / Wi-Fi)**
* **학습 목표**: Zephyr의 네트워크 스택 및 BLE/Wi-Fi Subsystem을 이해하고 통신 환경을 구축한다.
* **오전 (10:00 ~ 13:00)**
  * Zephyr Network Stack 구조 이해
  * Bluetooth Low Energy (BLE) 개요 및 GATT/GAP 개념
  * BLE Peripheral / Central 기본 샘플 동작 실습
* **오후 (14:00 ~ 18:00)**
  * Wi-Fi 또는 Ethernet 소켓 프로그래밍 API
  * IP 스택(IPv4/IPv6), DHCP, DNS 설정
  * TCP/UDP 소켓 통신 예제 실습

#### **7일차: AWS IoT Core 및 MQTT 프로토콜 이해**
* **학습 목표**: AWS IoT 구성요소를 이해하고 계정을 설정하여 MQTT 통신 환경을 준비한다.
* **오전 (10:00 ~ 13:00)**
  * AWS IoT Core 주요 개념 (Things, Certificates, Policies, Endpoints)
  * AWS 콘솔 기반 IoT 사물(Thing) 등록 및 보안 인증서(Certificate, Key) 발급
* **오후 (14:00 ~ 18:00)**
  * MQTT Protocol 동작 원리 (Publish, Subscribe, Topic, QoS Level)
  * PC 기반 MQTT 클라이언트(MQTT Explorer 등)를 이용한 AWS IoT Core 연동 테스트

#### **8일차: Zephyr 기반 AWS IoT MQTT 애플리케이션 개발**
* **학습 목표**: Zephyr 디바이스에서 TLS 인증 기반의 MQTT 클라이언트를 구현하여 AWS IoT Core와 연동한다.
* **오전 (10:00 ~ 13:00)**
  * Zephyr MQTT Helper Library 및 TLS/mTLS 보안 설정
  * 인증서 매핑 (`credentials.c` / Devicetree/Kconfig 연동)
  * AWS IoT Core 연결 및 MQTT Connect/Keep-alive 구현
* **오후 (14:00 ~ 18:00)**
  * 센서 측정 데이터를 JSON 포맷으로 패키징 후 AWS IoT Topic으로 Publish
  * AWS IoT Topic을 Subscribe하여 디바이스 제어 명령(LED, 모터 등) 수신 및 처리
  * 소스 코드 구조 분석 및 예외 처리(재연결 로직 등)

#### **9일차: AWS IoT Advanced (Device Shadow & Rules Engine)**
* **학습 목표**: AWS IoT Device Shadow와 규칙 엔진을 적용하여 고급 Cloud-Edge 연동을 구현한다.
* **오전 (10:00 ~ 13:00)**
  * AWS IoT Device Shadow 개념 (Reported state, Desired state, Delta)
  * Zephyr에서 Device Shadow JSON 상태 업데이트 및 동기화 구현
* **오후 (14:00 ~ 18:00)**
  * AWS IoT Rules Engine 활용 (DynamoDB 데이터 저장, SNS 알림 전송 등)
  * 센서 임계값 초과 시 자동 알림 및 섀도 상태 변경 구현

#### **10일차: 통합 실무 프로젝트 및 최종 평가**
* **학습 목표**: 2주간 배운 내용을 종합하여 지능형 IoT 임베디드 노드를 제작하고 시연한다.
* **오전 (10:00 ~ 13:00)**
  * **종합 미니 프로젝트**: "Zephyr RTOS 기반 멀티스레드 IoT 환경 감시 시스템 구현"
    * Task 1: 센서 데이터 periodic 모니터링 (I2C/SPI + Thread)
    * Task 2: 네트워크 및 MQTT 연동 (AWS IoT Core)
    * Task 3: 클라우드 원격 제어 및 로컬 디스플레이 표시
* **오후 (14:00 ~ 18:00)**
  * 프로젝트 구현 및 디버깅
  * 팀별/개인별 프로젝트 발표 및 동작 시연
  * 교육 내용 종합 정리 및 Q&A

---

## 3. 요약 일별 시간표

| 주차 | 일차 | 주요 교육 항목 | 세부 핵심 주제 |
| :--- | :--- | :--- | :--- |
| **1주차** | **1일차** | Zephyr RTOS 환경 구축 | NCS 구조, West, Devicetree, Kconfig, `printk()`, Logger |
| | **2일차** | 기본 주변장치 (GPIO, UART) | Blinky, Interrupts, Async UART, 시리얼 CLI |
| | **3일차** | 직렬 통신 (I2C, SPI) | I2C/SPI 센서 수집, OLED Display, Sensor Subsystem |
| | **4일차** | 멀티 스레드 프로그래밍 | Thread Lifecycle, Priority, Workqueue |
| | **5일차** | 동기화 & IPC | Semaphores, Mutex, Message Queue |
| **2주차** | **6일차** | 무선 네트워크 (BLE/Wi-Fi) | Zephyr Net Stack, BLE GATT/GAP, Socket API |
| | **7일차** | AWS IoT Core & MQTT | AWS 계정/사물 생성, TLS 인증서, MQTT 개요 |
| | **8일차** | AWS IoT MQTT 연동 | Zephyr MQTT Client, Publish/Subscribe, JSON 파싱 |
| | **9일차** | AWS IoT Shadow & Rules | Device Shadow 상태 동기화, Rules Engine 연동 |
| | **10일차** | 통합 프로젝트 & 평가 | 멀티스레드 기반 IoT 시스템 완성, 시연 및 발표 |