# Robot_Bodam
보담(보다 더 나은 삶을 살라) - 시각장애인 및 노약자를 위한 자율주행 실내 비서 로봇
2021년 4인 프로젝트(로봇팔 담당)

# 소개
   본 로봇은 시각장애인 및 노약자가 필요로 하는 물건을 직접 가져다준다. 음성인식을 통해 원하는 물건을 인식하고 해당 물건이 있는 위치로 자율 주행을 통해 이동한다. 카메라로 물건을 인식한 뒤 로봇팔로 물건을 스스로 파지하여 사용자에게 전달한다. 사용자가 다른 곳으로 이동하고 싶은 경우에는 소리를 내며 해당 장소까지 유도하며 안내한다. 또한, 사용자와 로봇 간 양방향 대화가 가능하여 말동무 역할을 한다.

# 구성도
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
   -음성 인식: 사용자 음성에서 키워드 인식
   -자율 주행: 집 내부 지도 작성, 물건이 있는 위치로 주행 및 장애물 회피
   -사물 인식: Depth Camera를 통한 물건 인식 및 좌표 추출
   -로봇팔 제어: 다관절 로봇팔을 통한 물건 자율 파지 및 운송
2. 경로 유도 및 안내 주행
   -사용자가 다른 곳으로 이동을 원하는 경우 소리를 내며 목적지로 유도 및 안내
3. 양방향 대화
   -사용자 발화 의도에 따른 기능 수행 및 양방향 대화

# 기대효과
1. 가정 내 안전사고 예방
2. 편의성
3. 심리, 정서적 안정
4. 삶의 질 향상
활용 분야: 물류 로봇(공장 및 스마트 팩토리), 다양한 자율 주행 서비스 로봇(식당, 백화점, 병원, 공항 등) 
