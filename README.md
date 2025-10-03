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
   - 사용자가 다른 곳으로 이동을 원하는 경우 소리를 내며 목적지로 유도 및 안내
3. 양방향 대화
   - 사용자 발화 의도에 따른 기능 수행 및 양방향 대화
   - Dialogflow API를 이용한 챗봇 기반 대화 구현
   - AI HUB 공개 대화 데이터셋을 이용한 대화 서비스 구현
5. 통합
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

# SLAM & Navigation
Odometry(주행기록계) 데이터를 기반으로 로봇 자세 및 위치를 파악한다. SLAM Gmapping을 이용해 집 내부 지도를 작성한다. 작성된 지도는 목적지로 이동하는데 기본적으로 필요한 정보이다. 
<img width="294" height="205" alt="image" src="https://github.com/user-attachments/assets/5dab2e47-cd93-4db8-ab2e-036be403a77b" />
성된 지도를 바탕으로 costmap, move_base, DWA planner 패키지를 포함한 launch파일을 구성한다. DWA planner에서는 로봇이 전역지도 상에서 목표지점까지의 경로를 나타내는 global path planner와 지역지도 상에서 목표지점까지의 경로를 나타내는 local path planner로 나누어 계획한다. 또한, local path planner가 global path planner에 얼마나 의존할 것인지, 경로를 어느 주기로 갱신할 것인지에 대한 파라미터를 조정할 수 있다. Costmap은 벽 또는 주변 장애물에 대한 Weight를 나타내는 것으로, 로봇 주행에 큰 영향을 미친다. 장애물의 inflation radius와 scaling factor를 조절하여 로봇이 장애물을 얼마나 우회할 것인지가 결정된다. 마지막으로 move_base에서는 위 모든 정보를 종합하여 제한 속도 내(max_vel: 0.3m/s) 각 구간별 주행할 수 있는 속도를 계산한다. 해당 속도를 컨트롤러에게 전달하여 모터출력을 얻는다.
<img width="302" height="278" alt="image" src="https://github.com/user-attachments/assets/72b0fafa-e465-4604-8aa1-b296257ec283" />
<img width="286" height="272" alt="image" src="https://github.com/user-attachments/assets/fa3ceb13-f868-44da-b6e6-9990478ee0c5" />

# 로봇팔 제어
다이나믹셀 모터를 제어할 수 있는 ROS패키지인 ROS Dynamixel Workbench패키지를 이용하여 5축 로봇팔을 제어한다. 필요한 사물의 위치좌표(x,y,z)를 전송받아서 삼각함수를 통해 모터가 가지고 있어야 되는 각도 값을 로봇의 반경을 바탕으로 나머지 모터들의 각도를 몸통길이, 팔 길이, 손목길이는 고정 값으로 하고, 몸통과 팔 쪽에서 그려지는 삼각형을 계산하여 팔각도를 구하여 모터를 제어한다. 물체를 집고 로봇에 싣기 위한 각 로봇팔의 움직임을 하나의 시퀀스로 만들어서 물건을 싣게 되면 사용자에게 이동한다. 손목의 각도는 물체를 집기 유리하게 만들기 위해 지면과 항상 평행을 이루도록 한다.
<img width="337" height="235" alt="image" src="https://github.com/user-attachments/assets/4ac987db-ceb5-45c6-bd1f-4140d6b4f9d1" />
<img width="337" height="120" alt="image" src="https://github.com/user-attachments/assets/104e8598-cbe6-47e7-8e6b-590e028d8950" />
<img width="325" height="342" alt="image" src="https://github.com/user-attachments/assets/df23cc40-8eed-469d-b73a-0dd9cd4af949" />
<img width="295" height="195" alt="image" src="https://github.com/user-attachments/assets/472bc731-e30b-4046-a93b-1928bac65654" /><img width="295" height="196" alt="image" src="https://github.com/user-attachments/assets/2938b4a0-0009-4d69-b709-0ea91f9c2aca" />

# 대화 알고리즘
보담’이라는 말을 인식하기 위해 146번의 녹음을 하였으며, 그 중 50번은 validate samples로 두었다. Hotword가 아닌 단어에 대해서도 359개의 녹음을 진행하였으며, 마찬가지로 144개를 validate samples로 두어 학습을 진행하였다. train samples 와 validate samples 데이터를 5500번의 학습과 확인을 통하여 Hotword 음성모델을 만들었다.
<img width="307" height="177" alt="image" src="https://github.com/user-attachments/assets/fe70f472-554f-4379-a078-bb7a37a5265a" />
전달된 음성은 STT를 통해 텍스트로 변환하여 Dialogflow API에 전달하게 된다. Dialogflow API는 대화 목록에 대해서 학습하여 받아들인 텍스트에서 가장 임계값이 높은 intent로 인식하여 반응을 텍스트로 출력하고, 출력된 텍스트는 Google-text-to-speech API를 사용하여 음성파일을 생성해 출력한다.

# 시행착오
ROS의 로봇팔 패키지를 사용하여 제어하려 했으나 모터와 패키지의 버전 차이로 인해 직접 삼각함수로 계산을 하여 제어하게 되었다. 3개의 관절을 이용해서 거리를 계산을 하면 무수히 많은 로봇팔의 각도가 나와서 어려움을 겪었지만 집게를 지면과 평행을 이루도록 하는 기준을 정함으로써 필요한 각도를 쉽게 구할 수 있었다. 오차 없이 제어하기 위해서 모터 사이의 길이를 고려하여 모터에 의해 만들어지는 팔의 각도와 모터를 고정하는 팔의 각도 사이의 각을 삼각형의 닮음과 삼각함수의 합성을 이용해서 하드웨어적인 오차를 제외하면 소프트웨어적으로 오차 없이 제어할 수 있었다.

# 배운점
ROS를 사용하면서 Linux 환경에서 프로그래밍 능력을 기를 수 있었다. 또한, 시각장애인을 위한 로봇을 제작할 때 시장조사를 한 결과, 취약 계층을 위한 로봇은 생각보다 많지 않다는 것을 알게 되었다. 자율 주행 및 인공지능 기술을 시각장애인 및 노약자를 위한 로봇에 적용할 수 있다는 점에 프로젝트를 진행하는데 동기부여가 되었고, 그들을 위한 로봇을 만드는 것은 자랑스러운 일이라 생각되었다.

# 기대효과
1. 가정 내 안전사고 예방
2. 편의성
3. 심리, 정서적 안정
4. 삶의 질 향상
활용 분야: 물류 로봇(공장 및 스마트 팩토리), 다양한 자율 주행 서비스 로봇(식당, 백화점, 병원, 공항 등) 
