<br>

### 트랜잭션

- 현대의 웹 보안에 있어서 매우 중요한 역할을 차지
- DB와 JAVA언어가 데이터를 주고 받는 과정에 원자성을 부여하는 수단.
- 어떤 작업  프로세스를 하나로 묶어 실행 중 하나의 작업이라도 실패하면 모두 실패처리를 해주고 전체 작업이 성공하면ㅅ 성공 처리를 해 주는 것
- ACID : DB 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 성질
  - 원자성, 일관성, 고립성, 지속성 의 성질이 있음

<br>

### 스프링 프레임워크의 트랜잭션

- JTA, JDBC, Hivernate, JPA, JDO 같은 여러가지 트랜잭션 API 간에 일관성있는 프로그래밍 모델 저공

- 선언적 트랜잭션 관리 지원

  - 단 몇줄의 코드 만으로 다이나믹 프록시와 AOP라는 기술을 통해 인터페이스, 클래스, 메서드까지 세분화하여 트랜잭션을 제어할 수 있으며 Annotation기술로 @Transactional 을 설정하는 것으로도 트랜잭션 설정이 가능하도록 해준다.

- 트랜잭션 동작 원리

  <image src="./images/howtotransactionworking.png" width="414px" height="300px"> </image>

  1. caller가 target method를 호출하면 먼저 AOP proxy가 호출됨
  2. Transaction Advisor는 새로운 트랜잭션을 생성함
  3. Custom interceptor들이 transaction advisor 전 후로 호출됨
  4. Target 비즈니스 메소드가 호출됨
  5. Transaction Advisor는 커밋 또는 롤백을 결정하고 호출자에게 넘김
  6. AOP Proxy는 결과를 받아 Caller에게 넘긴다