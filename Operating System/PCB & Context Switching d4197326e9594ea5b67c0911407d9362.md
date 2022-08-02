# PCB & Context Switching

## PCB

프로세스가 생성될 때 마다 프로세스가 가지고 있는 메타 데이터를 저장하는 곳으로 우리가 프로그램을 실행하여 메모리에 적재되면 프로세스가 생성되고, 프로세스 주소공간에 코드, 데이터, 힙, 스택영역이 생성된다. 이후 이 프로세스의 메타정보들이 PCB에 저장된다.

<img src = "https://t1.daumcdn.net/cfile/tistory/2164D3365829BAD527"/>


- Meta Data
    - Process ID : 프로세스 고유 식별번호
    - Program Counter : 다음에 실행될 명령어의 주소를 기억
    - Process Status : 프로세스의 상태 ( ready, waiting, running )
    - CPU Registers : 프로세스의 레지스터 상태를 저장하는 공간
        - CPU 범용 레지스터
        - 데이터 레지스터
        - 세그먼트 레지스터
    - Process Priority : 프로세스의 우선순위 스케줄링관련 정보
    - I/O Imformation : 프로세스 실행 시 필요한 I/O정보 등을 저장

<aside>
💡 PCB의 역할과 관리방법

</aside>

- 각종 인터럽트에 의하여 CPU는 작업중인 프로세스를 끝내지 않고 Context Switching을 하는데 다시 수행해야할 프로세스의 정보를 PCB에 저장해야한다.
- PCB는 Linked List로 관리가 된다.
- PCB List Head에 생성이 될 때마다 PCB가 붙으며, 주소값으로 연결이 이루어져있어 삽입, 삭제에 용이하다.

## Context Switching

문맥 교환이라고도 하며, CPU를 점유중인 프로세스가 인터럽트를 발생시킨 프로세스와 Switching하는 것을 의미한다.

<img src = "https://velog.velcdn.com/images%2Fhaero_kim%2Fpost%2Fbbc56488-d299-4c5d-9f1c-c9808b6f016b%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202020-08-03%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.06.12.png"/>


- 수행과정
    - CPU가 실행중인 프로세스를 중단하고 PCB에 상태를 저장
    - 다음에 실행할 프로세스의 PCB를 읽어 레지스터에 적재
    - 작업 수행
    
- Context Switching Overhead
    - Context Switching이 일어나는 동안 CPU는 아무 일을 할 수 없다.
    - Context Switching에는 다음과 같은 비용이 발생한다.
        - 메모리 접근을 위한 Kernel모드 진입
        - Cache 초기화
        - Memory Mapping 초기화
    - 따라서 잦은 인터럽트로 인한 문맥교환은 성능저하를 야기한다.