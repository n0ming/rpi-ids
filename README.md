# rpi-ids
## [1] 전체 구성도
![image](https://github.com/user-attachments/assets/55e880bf-88b1-463a-9acc-0e80783baea9)
CAN BUS Pentestion Tool은 https://github.com/n0ming/STM32_Pentesting_Tool 참고해주세요.
## [2] IDS 특징
![image](https://github.com/user-attachments/assets/7f1de63b-30a9-4b5b-97e1-8e41e241b8bb)

## [3] 탐지하는 공격 유형 5가지
1. Dos
   - 5ms 이내 비정상적인 송신 속도에 대하여 동일한 Payload가 5회 이상 들어왔는지 확인
   - DBC를 활용하여 ID 유효성, Payload 유효성 여부 확인
2. Fuzzing
   - DBC를 활용하여 Payload 기반 직전 패킷간의 유사도 검사
   - Payload의 정상 범위를 벗어난 경우, 정의된 CAN ID가 없는 경우, DLC가 다른 경우
3. Suspension
   - UDS를 활용하여 특정 ID에 대한 비정상 패킷이 지속적으로 진행된 경우
   - 주기 ECU ID에 대하여 비정상적으로 오랜 기간 통신이 중단된 경우 (패킷 마다 타이머 적용)
4. Masquerade
   - 각 eECU의 고유시계에 따른 오차 값인 시계오차가 급격하게 변한 경우
5. Repaly
   - 특정 ID에 대하여 비정상 주기로 같은 패킷이 지속될 경우

## [4] CAN 실시간 데이터 처리
CAN 패킷이 들어오면 receive_can_frame()함수를 통해 큐에 넣은 뒤 process_can_msg()함수를 통해 IDS 필터링 진행
TMI: 큐 버퍼 크기를 작게 성정하여 초반에 실제 차량을 테스트 했을때 버퍼가 터졌었음

## [5] 성능 평가 대상
![image](https://github.com/user-attachments/assets/2817fa3d-580a-46b7-aef9-7fb2a7236e0c)
