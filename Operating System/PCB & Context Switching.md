# PCB & Context Switching

### PCB(Process Control Block)

  * PCB란?

    OS가 프로세스를 제어하기 위한 정보를 저장해 두는 곳으로, 프로세스의 상태 정보를 저장하는 자료구조\
    프로세스의 메타데이터가 PCB에 저장됨
    
    연결 리스트 형태로 관리되며 프로세스가 생성될 때마다 고유의 PCB가 생성되고 프로세스가 완료되면 PCB도 함께 제거됨
    
    PCB는 프로세스의 상태 관리와 문맥 교환(Context Switching)을 위해 필요함
    
  * PCB에 저장되어 있는 정보
  
    * 포인터 : 프로세스의 현재 위치를 저장하는 포인터 정보
    * 프로세스 식별자 : 프로세스를 식별하는 PID
    * 프로세스 상태 : 프로세스의 각 상태 생성(New), 준비(Ready), 실행(Running), 대기(Waiting), 종료(Terminated)
    * 프로그램 카운터 : 프로세스가 다음에 실행할 명령어의 주소
    * 레지스터 : CPU레지스터 및 일반 레지스터 정보
    * CPU 스케줄링 정보 : 우선 순위, 최종 실행시각, CPU 점유 시간 등
    * 메모리 관리 정보 : 해당 프로세스의 주소 공간 등
    * 프로세스 계정 정보 : 페이지 테이블, 스케줄링 큐 포인터, 소유자, 부모 등
    * 입출력 상태 정보 : 프로세스에 할당된 입출력장치 목록, 열린 파일 목록 등
    * 포인터 : 부모/자식 프로세스에 대한 포인터, 프로세스가 위치한 메모리 주소에 대한 포인터, 할당 자원에 대한 포인터
    * 열린 파일 리스트 : 프로세스를 위해 열려있는 파일 리스트
    
  * PCB의 필요성

    CPU에서는 프로세스의 상태에 따라 교체작업이 이루어짐\
    (= interrupt가 발생해 할당받은 프로세스를 waiting 상태로, 다른 프로세스를 running 상태로 바꾸는 것)
    
    이때, 앞으로 다시 수행하게 될 waiting 상태의 프로세스에 대한 정보를 PCB에 저장하게 됨
    
### Context Switching

  * Context Switching이란?

    CPU가 이전의 프로세스 상태를 PCB에 보관하고 또 다른 프로세스의 정보를 PCB에서 읽어와 레지스터에 적재하는 과정\
    인터럽트 발생, 실행 중인 CPU 사용 허가 시간 만료, 입출력 작업으로 인한 대기 시 발생\
    (= Ready -> Running, Running -> Ready, Running -> Waiting 과 같은 상태 변경 시 발생)
    
  * Context Switching OverHead

    Context Switching때 CPU는 아무 일을 할 수 없음\
    따라서 Context Switching이 잦으면 오히려 오버헤드가 밸생해 효율이 떨어지게 됨
