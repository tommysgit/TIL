# Interrupt & System Call

## Interrupt

- 직역 하자면 ‘끼어들다’, ‘중단시키다’의 뜻으로 다양한 종류의 이벤트 혹은 이벤트를 알리는 메커니즘이다. 시스템관점에서 보자면 값이 비싼 CPU를 효과적으로 사용하기 위한 방법이다. 인터럽트가 발생하면 CPU는 실행중인 프로세스를 멈추고 원인에 따라 정해진 코드를 수행한다.

### 동작순서

<img src = "https://velog.velcdn.com/images%2Fgrighth12%2Fpost%2F91795fb0-71ad-41d4-89d5-1ad2598105f7%2Fvelog%20%ED%8F%AC%EC%8A%A4%ED%8C%85%EC%9A%A9%20-%20Database%20ER%20diagram%20(crow's%20foot)%20(1).png"/>

1. 인터럽트 발생으로 인한 요청
2. 실행중인 프로세스 중단
3. 프로세스 상태 저장 (PCB, PC)
4. 인터럽트 코드 실행을 위해 CPU에 기존에 할당된 작업과 인터럽트 처리할 작업을 교환 (Context Switching)
5. ISR 실행
    1. 커널의 인터럽트 핸들러가 발생원인 파악
    2. 원인에 따라 인터럽트 벡터에서 알맞은 ISR주소를 가져와 실행
6. 이전에 실행한 프로세스를 복구 (Context Restore)

### 종류

- 외부 인터럽트
    - 전원 이상 인터럽트
    - 기계착오 인터럽트
    - 외부 신호 인터럽트
        - Timer : CPU의 할당된 시간이 끝난 경우
        - 외부장치 : 마우스, 키보드 등등..
    - 입출력 인터럽트
        - I/O요청을 하거나 작업이 끝나 다음 작업이 요구되는 경우
- 내부 인터럽트
    - 잘못된 명령호출 또는 메모리 접근
    - 프로그램 검사 인터럽트
        - 0으로 나눴을 때
        - 각종 예외처리
        - 오버플로우, 언더플로우
- 소프트웨어 인터럽트 (Trap)
    - 프로그램이 커널 코드 호출 (System Call)

### 우선순위

여러 장치에서 동시에 인터럽트 요청이 오거나 이미 인터럽트 작업을 수행중에 요청이 발생한 경우 우선순위 판별이 필요하다. 일반적으로 외부 인터럽트, 내부 인터럽트, 소프트웨어 인터럽트 순이다.

1. 전원이상
2. 기계착오
3. 외부신호
4. 입출력 (I/O)
5. 잘못된 명령어
6. 프로그램 검사
7. SVC (SuperViser Call)

### 용어 정리

- PCB ( Process Control Block ) : Proccess Id, PC, SP등 프로세스가 실행중이던 정보를 저장하는 곳
- PC ( Program Counter ) : CPU가 다음에 실행할 프로세스의 주소를 저장하는 곳으로 레지스터의 한 종류
- Context Switching : 프로세스가 점유중인 CPU를 다른 프로세스에게 넘길 때 이전의 프로세스의 상태(Context)를 보관하고 새로운 프로세스의 상태를 적재하는 작업이다. Context는 PCB에 저장된다.
- ISR ( Interrupt Service Routine ) : 인터럽트 핸들러라고도 불리우며 인터럽트에 대응하는 특정 기능을 처리하는 기계어 코드 루틴이다. 인터럽트 원인에 따라 각각 존재하고 처리하는 시간도 다르다. 일종의 인터럽트에 매칭하는 솔루션(?)
- IV ( Interrupt Vector ) : 여러 종류의 인터럽트에 대한 ISR의 시작주소

## System Call

- 프로그램이 유저 모드에서 커널 모드에서 작업해야하는 일이 발생하였을 때 커널 함수를 호출하는 것

### 종류


<img src = "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FcA9in9%2Fbtqw9OAIYdZ%2FkKNVkBl0y9k9R3EjTNyNI0%2Fimg.png"/>

- 프로레스, 스레드 제어
- 파일 조작
- 장치 관리
- 정보 유지
- 통신 관련

### 유저모드 커널모드

해킹이나 사용자의 부주의한 조작으로 부터 시스템을 보호하기 위해 유저 모드와 커널모드로 나누어 작업을 한다.

<img src = "https://velog.velcdn.com/images%2F0mi%2Fpost%2F41d1c0b6-d718-46d4-bd4c-f65c03e7ef5e%2Fimage.png"/>
- User Mode : 일반적으로 프로그램을 실행하면 유저 모드에서 작동한다.
- Kernel Mode : 인터럽트나 시스템 콜이 발생하면 커널 모드로 변경되어 필요한 작업을 직접 실행한다.

### 유저모드와 커널모드의 흐름

프로세스는 생성되고 종료 하기까지 유저모드와 커널모드를 오가며 작업을 반복하고 ready, waitting, running상태를 오간다.



<img src = "https://t1.daumcdn.net/cfile/tistory/221F5B3F595BA50D07"/>

- **유저모드 → 커널모드 :** 프로그램 실행중에 인터럽트가 발생하거나 시스템 콜을 호출할 때 커널모드로 전환
- **커널모드** : 프로그램의 현재 CPU상태를 저장한다. → 인터럽트 혹은 시스템 콜을 직접 처리 → 중단되었던 프로그램의 CPU상태를 복원한다.
- **커널모드 → 유저모드** : 통제권을 프로그램에게 반환
- **유저모드** : 프로그램이 이어서 작업을 한다.

## 질문

인터럽트와 컨텍스트 스위칭의 차이?

시스템 콜도 인터럽트의 일부인데 중요한 이유?

모든 인터럽트 발생으로 인한 작업은 커널 모드에서 실행되는가?

스케줄링도 인터럽트로 봐야하는가?