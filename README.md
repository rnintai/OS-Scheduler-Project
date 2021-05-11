# OS-Scheduler-Project

## 스케줄러  
### Short Term Scheduler  
> **어떤 프로세스에 CPU를 할당해 줄 것인가?**
  
ready state의 프로세스 중에서 어떤 프로세스를 running state로 만들 것인지 결정한다.  
실행 속도가 ms단위 이하로 빈번하게 호출되기 때문에 알고리즘의 수행 속도가 빨라야한다.  
  
> Long Term Scheduler : 어떤 프로세스를 ready queue에 넣어줄 것인지 결정한다.  
> Mid Term Scheduler : 메모리에 적재된 프로세스의 개수를 관리한다.  
  
  
  
### 스케줄링의 목표
- CPU Utilization: 전체 시스템 시간 중 CPU가 작업을 처리하는 시간의 비율.  
- Throughput: 단위시간 당 완료된 프로세스의 개수.  
- turnaround time: 프로세스가 시작해서 끝날 때 까지 걸리는 시간이다. 준비큐에서 대기한 시간, CPU에서 실행하는 시간, I/O 시간을 합한 시간이다.  
- waiting time: 프로세스가 ready queue에서 대기하며 보낸 시간의 합.  
- response time: request를 제출한 후 첫 번째 응답이 나올 때 까지 걸린 시간. (출력하는데 걸리는 시간은 비포함)  
  
> ![image](https://user-images.githubusercontent.com/65759076/117789012-e0af2780-b282-11eb-817d-ac923735f034.png)  

## 스케줄링 알고리즘

### 범용 스케줄링 알고리즘

####
####

### Real Time 스케줄링 알고리즘

####
####


## 참고 자료
https://kosaf04pyh.tistory.com/191  
https://thinkpro.tistory.com/122  
https://manducku.tistory.com/14  
https://velog.io/@mu1616/CPU-%EC%8A%A4%EC%BC%80%EC%A4%84%EB%A7%81  
