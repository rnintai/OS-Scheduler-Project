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
  
> **상대적으로 Burst Time이 긴 프로세스는 무한히 뒤로 밀려 서비스를 받지 못하는 `기아 현상`이 일어날 수 있다.**  
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
  
  
  
  
  
#### Multilevel Queue Scheduling(다단계 큐 스케줄링)
  
  
  
  
#### Multilevel Feedback Queue Scheduling (다단계 피드백 큐 스케줄링)  
  
  
  
  
### Real Time 스케줄링 알고리즘

#### RM(Rate Monotonic) Scheduling : 정적 우선순위 스케줄링


#### EDF(Earliest Deadline First) Scheduling : 동적 우선순위 스케줄링


### 어떤 알고리즘을 사용해야 하나? 
Process의 요구되는 CPU Burst Size가 고르다면, FCFS방식이 좋고,  
차이가 심하다면, RR방식이 좋다.

## 참고 자료
https://kosaf04pyh.tistory.com/191  
https://thinkpro.tistory.com/122  
https://manducku.tistory.com/14  
범용 스케줄링 - https://velog.io/@mu1616/CPU-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81  
https://kim-hoya.tistory.com/11
https://sanghyunj.tistory.com/18

실시간 스케줄링 - https://inuplace.tistory.com/321
