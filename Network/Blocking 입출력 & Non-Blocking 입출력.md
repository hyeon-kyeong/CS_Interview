# Blocking I/O & Non-Blocking I/O

I/O 작업은 Kernel level에서만 수행할 수 있으므로 Process, Thread는 커널에게 I/O를 요청해야함

### Blocking I/O

* Blocking I/O 작업 형태

1. Process(Thread)가 Kernel에 I/O를 요청하는 함수를 호출함

2. Kernel이 작업을 완료하면 작업 결과를 반환받음

* 특징

  * I/O 작업이 진행되는 동안 user Process(Thread)는 자신의 작업을 중단한 채 대기함

  * 자원 낭비가 심함 (I/O 작업은 CPU 작업을 거의 쓰지 않기 때문)
  
### Non-Blocking I/O

* Non-Blocking I/O 작업 형태

1. User Process(Thread)가 recvfrom 함수 호출 (Kernel에 해당 Scoket으로부터 data를 받고싶다고 요청함)

2. Kernel은 해당 요청에 대해 곧바로 recvBuffer를 채워 보낼 수 없으므로 "EWOULDBLOCK"을 반환함

3. recvBuffer에 user가 받을 수 있는 데이터가 있는 경우, Buffer로부터 데이터를 복사해 받음

4. recvfrom 함수는 빠른 속도로 data를 복사한 후, 복사한 data의 길이와 함께 data를 반환함

* 특징

  * Blocking 방식과 달리 I/O 작업이 진행되는 동안 user Process(Thread)는 자신의 작업을 중단하지 않음
