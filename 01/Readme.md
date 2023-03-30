# 왜 컴퓨터 구조를 배워야하나?
성능/용량/비용을 고려하여 개발하기 위해


# 튜링머신

![image](https://user-images.githubusercontent.com/104714337/228242667-80d5ea2b-e5ac-4ef0-b476-296c2da160a3.png)

- 테이프(Tape): 일정한 크기의 셀(Cell)로 나뉘어 있는 종이 테이프
- 헤드(Head): 종이 테이프의 특정 한 셀을 읽을 수 있는 헤드
- 상태 기록기(State register): 현재 튜링 머신의 상태를 기록하고 있는 장치

        개시 상태(Start state)
        종료 상태(Halt state)
- 행동표(Action table, transition table of instructions): 특정 상태에서 특정 기호를 읽었을 때 해야 할 행동을 지시한다

# 폰노이만 구조

![image](https://user-images.githubusercontent.com/104714337/228243422-9169321b-8d04-4d7c-ba14-5df2698243c0.png)

- 입력장치: 어떤 데이터를 CPU가 처리할 수 있도록 디지털 신호로 변환해주는 장치
- 출력장치: 디지털 신호를 출력할수 있게 변환해주는 장치
- 제어장치(Controll Unit): 명령 처리를 담당

        Hardwired(고정 배선제어 방식) : 제어신호가 Hardwired Circuit에 의해 생성 / RISC 시스템에 적용
        Micro Program : 발생 가능한 제어 신호의 조합을 미리 구성하여 ROM에 저장(필요시 신호 발생시킴) / CISC 시스템에 적용
- 산술/논리장치(Arithmetic Logic Unit): 연산을 담당
- 레지스터: CPU 내부의 메모리

        IR(Instruction Register): 현재 수행중인 명령어 부호를 저장하는 레지스터
        PC(Program Counter): 명령이 저장된 메모리의 주소를 가르키는 레지스터
        AC(Accumulator): 연산 결과를 임시로 저장하는 레지스터
        
* CPU 명령어 수행 과정
1. Fetch Instrunction: 메모리에서 명령을 가져옴
2. Decode Instruction: 명령 해석
3. Execute Instruction: 명령 수행
4. Wrte Back: 수행 결과 기록





# 트랜지스터

![image](https://user-images.githubusercontent.com/104714337/228255537-0594bfb9-f961-42b5-b479-1446db4afef0.png)

![image](https://user-images.githubusercontent.com/104714337/228257358-678b6548-c6ba-4602-b294-3f10f6c55b5d.png)

성질이 다른 2가지 실리콘(N형/P형)을 겹쳐 만듬 (NPN/PNP), 가운데 도선에 특정 전압을 주면 전류가 흐르게됨

트랜지스터를 통해 AND,OR,NOT 논리게이트를 만들어 사용


# CPU의 속도
- hz로 표현
- 1hz당 한 사이클 순환
- 한 사이클 = 레지스터의 숫자만큼 bit를 처리

# CPU가 명령을 실행하는 과정
1. 프로그램 로드
2. 데이터 로드 및 캐싱
3. 연산 및 저장
4. 프로그램 종료할때까지 반복

# 컴퓨터 핵심 부품

![image](https://user-images.githubusercontent.com/104714337/228252879-1279cd92-889b-4501-b728-7a27702f5d0e.png)

- 메인보드와 시스템보드

        메인보드: 부품들을 연결하는 역할 내부의 '버스'라는 통로를 통해 각 부품을 연결
        시스템보드: 핵심 부품을 연결하는 버스를 칭함(주소,데이터,제어 버스로 구성)

# 왜 1비트는 8바이트인가?
컴퓨터는 미국에서 만들어졌다, 영문을 표기하기 위해 만든 ASCII 코드가 활성화되며 표준이 잡힌것으로 추정
