# OS-Scheduler-Project

## 1 스케줄러  
### Short Term Scheduler  
> **어떤 프로세스에 CPU를 할당해 줄 것인가?**
  
ready state의 프로세스 중에서 어떤 프로세스를 running state로 만들 것인지 결정한다.  
실행 속도가 ms단위 이하로 빈번하게 호출되기 때문에 알고리즘의 수행 속도가 빨라야한다.  
  
> Long Term Scheduler : 어떤 프로세스를 ready queue에 넣어줄 것인지 결정한다.  
> Mid Term Scheduler : 메모리에 적재된 프로세스의 개수를 관리한다.  
  
### 선점 / 비선점
- 선점형(Preemptive): 다른 프로세스가 우선순위에 따라 현재 CPU에 할당된 프로세스를 밀어낼 수 있다.  
- 비선점형(non-preemptive): 한 프로세스가 CPU에 할당되면 다른 프로세스는 기다려야 한다.  


## 2 스케줄링의 목표
- CPU Utilization: 전체 시스템 시간 중 CPU가 작업을 처리하는 시간의 비율.  
- Throughput: 단위시간 당 완료된 프로세스의 개수.  
- turnaround time: 프로세스가 시작해서 끝날 때 까지 걸리는 시간이다. 준비큐에서 대기한 시간, CPU에서 실행하는 시간, I/O 시간을 합한 시간이다.  
   `(waiting time + Burst time)`  
- waiting time: 프로세스가 ready queue에서 대기하며 보낸 시간의 합.  
- response time: request를 제출한 후 첫 번째 응답이 나올 때 까지 걸린 시간. (출력하는데 걸리는 시간은 비포함)  
  
> **CPU 이용률과 처리량을 최대화하고 총처리 시간, 대기 시간, 응답 시간을 최소화 하는 것이 바람직하다.**  
  
> ![image](https://user-images.githubusercontent.com/65759076/117789012-e0af2780-b282-11eb-817d-ac923735f034.png)  
  
## 3 스케줄링 알고리즘
### 범용 스케줄링 알고리즘
#### FCFS (First Come First Serve)  
가장 간단한 CPU 스케줄링 알고리즘으로, CPU를 먼저 요청하는 프로세스가 CPU를 먼저 할당받는다. (non-preemptive)  
  
> **예컨대 하나의 긴 프로세스가 CPU를 할당받고 작업을 진행하고 있을 때에, 모든 다른 프로세스들은 긴 시간을 기다려야 하기 때문에**  
> **CPU와 장치 이용률이 저하되는 단점이 있다. `(Convoy effect)`**  
> ![image](https://user-images.githubusercontent.com/65759076/117796352-f7a54800-b289-11eb-91fb-c302cda0c479.png)
  
  
#### SJF (Shortest Job First)  
- non-preemptive:  
가장 짧은 `Burst Time`을 갖는 프로세스에게 우선적으로 CPU를 할당한다.   
만약 `Burst Time`이 동일하다면, `FCFS`방식으로 동작.  
  
- preemptive:  
현재 프로세스의 남은 시간보다 짧은 `Burst Time`을 가진 프로세스가 선점할 수 있다.  
  
> **상대적으로 Burst Time이 긴 프로세스는 무한히 뒤로 밀려 서비스를 받지 못하는 `starvation`이 일어날 수 있다.**  
> **이를 방지하기 위하여 `Aging`기법을 이용하여 오래 기다린 프로세스를 작업할 수 있도록 한다. -> HRRF**  
  
  
#### HRRN (High-Response-Ratio Next)
- SJF + Aging(Non-preemptive)  
- Dynamic Priority가 높은 프로세스 우선 할당
 > **`= (WT+BT)/BT`**  
 > ![image](https://user-images.githubusercontent.com/65759076/117803687-e06a5880-b291-11eb-8eb0-aa7a7935cf3d.png)  
  
  
#### RR (Round Robin)  
`FCFS`알고리즘과 유사하지만, `시간 할당량(Time Quantum)`을 정의하여 preemptive로 동작한다.  
10~100ms 정도의 시간 단위로 프로세스를 할당하고, 할당된 시간이 지나면 ready queue의 맨 끝으로 밀려난다.  
모든 프로세스들이 공평하게 시간을 할당받기 때문에 응답 시간이 적어진다.  
  
> 시간 할당량이 적어지면, `context switching`이 자주 일어나 `overhead`가 커짐.  
> 시간 할당량이 커지면, `FCFS`방식과 점점 비슷해진다.  
> **따라서 최적의 `Time Quantum`을 찾아야 한다.**  
  
  
#### Priority Scheduling (우선순위 스케줄링)
운영체제 혹은 사용자에 의해 프로세스에 우선순위를 부여하고, CPU는 가장 높은 우선순위를 가진 프로세스에 할당된다.
- 선점형: 도착한 프로세스의 우선순위가 현재 실행되는 프로세스보다 높으면 **CPU 선점**.  
- 비선점형: 도착한 프로세스의 우선순위가 현재 실행되는 프로세스보다 높으면 단순히 `ready queue`의 **head**에 넣는다.  
  
> **문제점은 `starvation`인데, `aging`기법을 통해 해결할 수 있다.**
  
  
#### Multilevel Queue Scheduling(다단계 큐 스케줄링)
여러 개의 `ready queue`를 갖는 스케줄링 기법이다. 각 큐마다 다른 스케줄링 알고리즘을 가질 수 있고,  
큐와 큐간의 스케줄링도 존재한다.  

각 큐는 우선순위를 갖고, 우선순위가 높은 큐가 **비어있어야** 그 아래 우선순위의 큐를 실행할 수 있다.  
처리할 프로세스의 큐 간 이동은 허용되지 않기 때문에 스케줄링 부담이 낮은 대신 융통성이 떨어진다.  

> **마찬가지로 `starvation`문제가 있다. 해결 방안으로는 큐들 사이에 시간을 할당하는 방법이 있다.**
  
  
#### Multilevel Feedback Queue Scheduling (다단계 피드백 큐 스케줄링)  
`다단계 큐 스케줄링`과 다르게 큐들 사이의 프로세스 이동이 허용된다.  
  
- 프로세스들을 CPU 버스트 **성격**에 따라 구분한다.
- 어떤 프로세스가 CPU 시간을 너무 **많이** 사용하면, 낮은 우선순위의 큐로 이동시킨다.
- `I/O 중심의 프로세스`와 `대화형 프로세스`들을 **높은** 우선순위의 큐에 넣는다. (이들은 통상적으로 CPU 버스트가 **짧기** 때문이다.)
- **대기시간이 길어지는** 프로세스는 높은 우선순위 큐로 이동할 수 있다. 이 방법으로 `starvation` 을 예방한다.
  
  
### Real Time 스케줄링 알고리즘  
> **참고**  
>   
> **경성 실시간 시스템:**  
>   작업이 마감시한 내에 완료되지 않으면 치명적인 결과를 초래하는 시스템, 마감 시간을 넘긴 후 완료되는 일은 아무 가치가 없음.  
>     
> **연성 실시간 시스템:**  
>   작업이 마감시한 내에 종료되지 않으면 데이터의 손실 등 피해가 발생하지만 시스템은 계속해서 운영 가능한 시스템, 마감 시간을 넘긴 후부터는 완료의 가치가 점점 떨어짐  
  
  
#### RM(Rate Monotonic) Scheduling : 정적 우선순위 스케줄링
프로세스들이 주기적으로 발생되고, `Deadline`이 주기와 같다고 가정할 때에 **주기가 짧은** 프로세스에 **높은** 우선순위를 부여한다. 
(수행시간과는 무관.)  
새로운 프로세스가 **도착**할 때에 우선순위를 판단하여 선점할 수 있는 `선점형` 스케줄링이다.  
  
> **CPU 사용률 계산**  
> : 수행시간 / 주기  
>   
> n개의 프로세스가 있을 때의 **CPU 사용률** 상한  
> ![image](https://user-images.githubusercontent.com/65759076/117816775-d7818300-b2a1-11eb-9c36-92ef772b32e4.png)   
>   
> 프로세스의 개수가 많아지면 **69.3%** 로 수렴.  
> ![image](https://user-images.githubusercontent.com/65759076/117816868-f41dbb00-b2a1-11eb-833b-f3e8e278a75b.png)  

CPU 사용량의 상한을 넘더라도 스케줄링이 가능하지만, `deadline missing`이 발생할 수도 있다.  


#### EDF(Earliest Deadline First) Scheduling : 동적 우선순위 스케줄링
프로세스의 deadline이 **가까울수록** 우선순위를 높게 부여하는 선점 방식의 스케줄링이다.  
한 프로세스의 실행이 완료될 경우에는 deadline이 가장 가까운 것을 찾아 스케줄한다.  
모든 프로세스가 주기적일 필요는 없으며 주기가 있을 경우에는 deadline을 **주기**로, 그렇지 않을 경우에는 deadline이 알려져야 한다.  
  
> **이론 상** CPU 사용률이 100%보다 작기만 하면 된다. (실제로는 `context switching`의 **비용**을 따져야.)  
>   
> 하지만 100%를 초과하게 되면 연속적으로 `deadline missing`이 일어나는 `Domino effect`가 발생할 수 있다.
> 이 경우에는 몇 개의 task를 **포기**하는 알고리즘으로 막자.  

#### RM vs. EDF  
- RM: 구현이 상대적으로 단순하고, 우선순위가 고정되기 때문에 예측성이 좋다. 하지만 CPU의 이용률이 좋지 않다는 단점이 있다.  
       따라서 태스크의 개수가 정해져 있고, 주기와 수행시간 등이 정확히 파악되어 있다면 RM을 사용하는 것이 유리할 수 있다.   
       
- EDF: 이론적으로 최적이고, CPU이용률이 거의 100%에 수렴한다. 하지만 과부하시 도미노 현상이 발생할 위험이 있다.   
  
  
### 어떤 알고리즘을 사용해야 하나? 
- **범용**  
Process의 요구되는 CPU Burst Size가 고르다면, `FCFS`방식이 유리하고,  
차이가 심하다면, `RR`방식이 유리하다. `HRRN`도 구현이 어렵진 않을 듯 하다. 더 조사해보자  
  
`다단계 피드백 큐`는 구현만 가능하다면 성능은 보장되겠지만 어려울 듯.  
이유는 여러개의 큐들의 스케줄링 알고리즘을 정해야 하며, 다른 우선순위의 큐로 프로세스를 보내는  
기준점 또한 정해야하고 고려해야 할 점이 많을 것 같다.  
  
  
- **실시간**  
EDF가 더 고성능인 것은 확실. 구현 가능성에 따라 달라질 듯.  


## 참고 자료
https://kosaf04pyh.tistory.com/191  
https://thinkpro.tistory.com/122  
  
범용 스케줄링 - https://velog.io/@mu1616/CPU-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81  
https://kim-hoya.tistory.com/11
https://sanghyunj.tistory.com/18

실시간 스케줄링 - https://inuplace.tistory.com/321
                https://manducku.tistory.com/14  
