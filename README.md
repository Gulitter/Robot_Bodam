# Robot_Bodam
보담(보다 더 나은 삶을 살라) - 시각장애인 및 노약자를 위한 자율주행 실내 비서 로봇
2021년 4인 프로젝트(로봇팔 담당)

# 소개
   본 로봇은 시각장애인 및 노약자가 필요로 하는 물건을 직접 가져다준다. 음성인식을 통해 원하는 물건을 인식하고 해당 물건이 있는 위치로 자율 주행을 통해 이동한다. 카메라로 물건을 인식한 뒤 로봇팔로 물건을 스스로 파지하여 사용자에게 전달한다. 사용자가 다른 곳으로 이동하고 싶은 경우에는 소리를 내며 해당 장소까지 유도하며 안내한다. 또한, 사용자와 로봇 간 양방향 대화가 가능하여 말동무 역할을 한다.

# 구성도
**회로 구성**    

- 로봇 전원부와 모터 제어 회로 구성 및 납땜
- 모터 제어 전원과 메인 보드 전원 분리

**로봇 본체**

- Solidworks 기반 로봇 내, 외부 설계
- 설계 부품 자리 배치 및 조립
- 배터리 및 센서(IMU, Lidar, Encoder, speaker, Camera)   구성
- 상단부에 로봇팔 및 카메라, 중앙에는 라이다 센서, 하단부에는 제어 회로로 구성
<img width="156" height="156" alt="image" src="https://github.com/user-attachments/assets/46daa55b-9f33-4114-9304-bcee7a3bff4f" />
<img width="308" height="160" alt="image" src="https://github.com/user-attachments/assets/777b3797-3531-4637-8bff-c10abc6108aa" />
<img width="576" height="326" alt="image" src="https://github.com/user-attachments/assets/0e9b0e37-e3bf-4d62-abe0-ec39bc7ffcad" />
<img width="645" height="440" alt="image" src="https://github.com/user-attachments/assets/5580a505-e718-451a-b594-e0d68f0ce86c" />
<img width="513" height="327" alt="image" src="https://github.com/user-attachments/assets/51e5e4b8-a108-4d73-9633-2a466e7c36fa" />


# 특징
■ 자율 물건 파지 및 이송 : 사람의 개입 없이 사용자의 음성만으로 로봇이 스스로 물건이 있는 위치로 이동하고, 물건을 파지하여 사용자에게 가져다줌
■ 이동성: 기존 인공지능 스피커와 달리 이동성이 있어 사용자의 위치와 관계없이 사용 가능
■ 사용자와의 양방향 대화: 단방향 대화가 아닌 양방향 대화를 통해 정서적 교감 가능

# 기능
1. 물건 자율 이송
   **음성 인식**: 사용자 음성에서 키워드 인식
      - 음성모델을 수집, 학습하여 Hotword Detection을 구현
      - Wit.AI API를 이용한 STT(Speech To Text)
      - 텍스트에 따른 명령 수행
   **자율 주행**: 집 내부 지도 작성, 물건이 있는 위치로 주행 및 장애물 회피
      - 주변 환경 인지 및 지도 작성
      - Ubuntu, ROS melodic환경에서 SLAM기반 자율주행 구현
      - 주행 안정화를 위한 파라미터 수정 
   **사물 인식**: Depth Camera를 통한 물건 인식 및 좌표 추출
      - YOLO Mark를 이용하여 타겟 데이터를 labeling하여 이미지를 학습
      - Depth카메라를 이용한 물건 탐색 학습한 데이터를 사용한 물건 구분
      - 사물의 위치 좌표(x,y,z)를 로봇팔 제어부로 전송
   **로봇팔 제어**: 다관절 로봇팔을 통한 물건 자율 파지 및 운송
      - Dynamixel Workbech 패키지 기반 dynamixel 서보 모터 5개로 각 관절 제어
      - 물품 파지 및 이송 자세 제어
2. 경로 유도 및 안내 주행
   -사용자가 다른 곳으로 이동을 원하는 경우 소리를 내며 목적지로 유도 및 안내
3. 양방향 대화
   -사용자 발화 의도에 따른 기능 수행 및 양방향 대화
   - Dialogflow API를 이용한 챗봇 기반 대화 구현
   - AI HUB 공개 대화 데이터셋을 이용한 대화 서비스 구현
4. 통합
   - S/W를 통합하기 위한 ROS custom msg파일 생성
   - ROS topic 통신을 이용한 모든 S/W 통합(음성 인식, 자율 주행, 사물 인식, 로봇팔 제어, 대화)
   - 시나리오 구현

# 개발환경

**OS**
Linux(Ubuntu 18.04), ROS Melodic

**개발환경(IDE)**
Vim, VScode, Arduino IDE

**개발도구**
Jetson Nano, Arduino Mega

**개발언어**
C, C++, Python

**디바이스**
- RX-64, RX-28(Dynamixel Servo Motor)
- IG-32GM(DC motor)
- TB6612(Motor Driver)

**센서**
음성 인식
 - 마이크, 스피커
   
사물 인식
 - Realsense D435i(Depth camera)
   
자율주행 
 - A1M8 RPLIDAR(Lidar sensor)
 - myAHRS+(IMU sensor)

   
**통신**
U2D2-RS485 통신, Serial 통신

**언어**
C, C++, Python


# 기대효과
1. 가정 내 안전사고 예방
2. 편의성
3. 심리, 정서적 안정
4. 삶의 질 향상
활용 분야: 물류 로봇(공장 및 스마트 팩토리), 다양한 자율 주행 서비스 로봇(식당, 백화점, 병원, 공항 등) 
