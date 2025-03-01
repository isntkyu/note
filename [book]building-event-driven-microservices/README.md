# 이벤트 기반 마이크로서비스 구축

**툼스톤 이벤트** | 값이 없고 키만 있는 이벤트, 삭제해야 한다는 사실을 표현하는 관례로 쓰임

**컴팩션** | 최근 레코드로만 유지하고 이전 레코드 삭제

---

### 이벤트 브로커 vs 메시지 브로커

메시지 브로커는 여러 컨슈머가 메시지 사본을 받을 수 없다.  
메시지 브로커는 ACK를 받으면 이벤트를 삭제한다.

이벤트 브로커는 일반적으로 붙임 전용 불변 로그를 사용한다.

이벤트 브로커는 이벤트 스트림으로 소비될 때, 오프셋을 사용할 수 있고 컨슈머 그룹에 부하를 분산하거나 특정 컨슈머 그룹에 독점소비하도록 보장할 수 있다.  

이벤트 브로커가 큐 형태로 이벤트를 소비시킬 때는 순서가 보장되지 않고, 여러 컨슈머가 사본을 가질 수 없다.

### 대규모 머이크로서비스 관리

가상머신은 OS와 각 인스턴스를 완벽분리하므로 보안 측면에서는 컨테이너보다 우수하지만,  
비싸고 시동시간이 느리고 공간을 많이 차지한다.

---

## 통신 및 데이터 규약

이벤트의 스키마를 정의하는 방법에 대한 챕터이다.  
스키마가 역방향/정방향/단방향으로 진화할 수 있다는 것에 대한 설명과 그에 맞는 데이터유형 설정방법에 대해 말한다.  

아브로, 프로토콜 버퍼는 스키마 진화를 잘 지원하는 규약이다. json 은 진화를 지원하지 않는다.  

> 나는 Json을 사용하지만, 진화에 대해서는 전략적으로 접근하면 될 것 같고 제로페이로드 방식에서는 pk 만을 들고 있기 때문에 크리티컬하진 않아보인다.

데이터유형을 좁혀야한다.
특히. 문자열이벤트나 enum 등은 최악이라고 말한다.

그 외에 하나의 스트림은 하나의 역할을 맡아야하며, 이벤트에는 여러 인자를 추가하지 않고 결과를 담는 것이 좋다고 말한다.
