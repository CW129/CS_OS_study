# 05. CPU 성능 향상 기법

## 1. 빠른 CPU를 위한 설계 기법
### 클럭
: 클럭 속도가 CPU 속도에 영향을 준다. (CPU 속도 단위로 간주)

* 클럭 속도
  * 단위: 헤르츠(Hz) - 1초에 클럭이 몇 번 반복됐는지 측정
  * 클럭의 속도는 일정하지 않다. 

<br />

### 코어와 멀티코어
: 기술의 발전으로 CPU(명령어를 실행하는 부품)의 내부에 여러 CPU를 만들 수 있게 됐다.
<br />
CPU 내부에 '명령어를 실행하는 부품'의 역할을 하는 CPU를 코어로 명칭한다. <br />
CPU는 코어를 포함한 부품의 개념으로 사용된다.

![IMG_FDFF85A1A7A8-1](https://user-images.githubusercontent.com/76677897/234341237-78e64f84-0167-4c40-bbc6-000db8107d83.jpeg)

* 멀티코어 CPU(멀티코어 프로세서): 코어를 여러개 포함하고 있는 CPU

<br />

### 스레드와 멀티스레스
스레드: 실행 흐름의 단위

![IMG_12022CFF2500-1](https://user-images.githubusercontent.com/76677897/234341885-dd8f688f-2fe9-457a-bad9-3ad289e9e3a8.jpeg)

* 하드웨어적 스레드: 하나의 코어가 동시에 처리하는 명령어 단위
  * 멀티스레드 프로세서(멀티스레드 CPU): 하나의 코어에 여러 명령어를 동시에 처리할 수 있는 CPU
    * 레지스터: 레지스터 세트가 코어에 여러개 있다면 ALU와 제어장치가 레지스터 세트들의 명령어를 해석하고 실행한다면 하나의 코어에서 여러 명령어를 실행시킬 수 있게 된다.
* 소프트웨어적 스레드: 하나의 프로그램에서 독립적으로 실행되는 단위
  * 싱글스레드
  * 멀티스레드

  ![IMG_6546C9C75392-1](https://user-images.githubusercontent.com/76677897/234342145-925b15f8-1020-44d7-8b6e-c6594fcf0dff.jpeg)

<br />
<br />

## 2. 명령어 병렬 처리 기법(Instruction-Level Parallelism, ILP)

### 명령어 파이프라인

> **📌 클럭 단위의 명령어 처리 과정**
>  1. 명령어 인출(Instruction Fetch)
>  2. 명령어 해석(Instruction Decode)
>  3. 명령어 실행(Execute Instruction)
>  4. 결과 저장(Write Back)
>
> ※ 같은 단계가 겹치지 않는다면 CPU는 각 단계를 동시에 실행할 수 있다.

![IMG_AC034E0652AE-1](https://user-images.githubusercontent.com/76677897/234342637-c06f233f-de77-4ee7-b70a-dad6d2225f26.jpeg)

![IMG_EC32D36C48B0-1](https://user-images.githubusercontent.com/76677897/234342892-f3f662b0-e6e7-40df-9d2e-4861c6ce6575.jpeg)

* 명령어 파이프라이닝: 명령어 파이프라인에 넣고 동시에 처리하는 기법
* 파이프라인 위험: 특정 상황에서 성능 향상에 실패하는 경우
  * 데이터 위험: 명령어 간 '데이터 의존성'에 의해 발생
  * 제어 위험: 프로그램 카운터 값에 갑작스러운 변화가 생기면 명령어 파이프라인에 미리 가지고 처리 중이던 명령어는 쓸모 없게 된다.
    * 분기 예측: 프로그램 분기를 예측해 그 주소를 인출하는 기술
  * 구조적 위험: 서로 다른 명령어가 동시에 ALU, 레지스터 등과 같은 CPU 부품을 사용하려 할 때

<br />

### 슈퍼스칼라
: CPU 내부에 여러 개의 명령어 파이프라인을 포함한 구조

* 슈퍼스칼라 프로세서(슈퍼스칼라 CPU): 슈퍼스칼라 구조로 명령어 처리가 가능한 CPU
  * 매 클럭 주기마다 동시에 여러 명령어를 인출, 실행 가능(멀티스레드 프로세서 사용 가능)

<br />

### 비순차적 명령어 처리(Out-of-order execution, OcOF)
: 명령어들을 순차적으로 실행하지 않는 기법(합법적 새치기🏃🏻‍♀️)

![IMG_9C8C6E203951-1](https://user-images.githubusercontent.com/76677897/234343354-8728c7de-9331-419a-b82d-2a8d4ec0e801.jpeg)

* 데이터 의존성을 가지고 있는지, 순서를 바꿔 실행할 수 있는 명령어에는 어떤것이 있는지 판단해야함 

<br />
<br />

## 3. CISC와 RISC

### 명령어 집합 구조(Instruction Set Architecture, ISA)
: CPU가 이해할 수 있는 명령어들의 모음

![IMG_0B34DF040C53-1](https://user-images.githubusercontent.com/76677897/234343575-9b4fddee-ba8b-41d6-bafc-bac11d925962.jpeg)

* CPU마다 ISA가 다를 수 있음
* ISA는 일종의 CPU의 언어

### CISC(Complex Instruction Set Computer)
: 복잡한 명령어 집합을 활용하는 컴퓨터

* 가변 길이 명령어: 다양하고 강력한 기능의 명령어 집합을 사용하여 형태와 크기가 다양함
* 메모리에 접근하는 주소 지정 방식도 다양

### RISC(Reduced Instruction Set Computer)
: 명령어의 종류가 적고 규격화된 명령어를 활용하는 컴퓨터

* 고정 길이 명령어: 명령어가 규격화되어 있고, 하나의 명령어가 1클럭 내외로 실행
* 명령어 파이프라이닝에 최적화
* 메모리 접근을 단순화, 최소화 하는 대신 레지스터를 적극 사용

![IMG_71DB166B67A6-1](https://user-images.githubusercontent.com/76677897/234343776-ea29cf0f-771d-4849-adbb-db75d416f296.jpeg)