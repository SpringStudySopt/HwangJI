<br>

## [트랜잭션]

- #### 현대의 웹 보안에 있어서 매우 중요한 역할을 차지

- #### DB와 JAVA언어가 데이터를 주고 받는 과정에 원자성을 부여하는 수단.

- #### <u>**어떤 작업  프로세스를 하나로 묶어 실행 중 하나의 작업이라도 실패하면 모두 실패처리를 해주고 전체 작업이 성공하면 성공 처리를 해 주는 것**</u>

- #### ACID : DB 트랜잭션이 안전하게 수행된다는 것을 보장하기 위한 성질

  - ###### 원자성, 일관성, 고립성, 지속성 의 성질이 있음

- #### Transaction의 기본 방법

  - ###### Transaction은 2개 이상의 쿼리를 하나의 커넥션으로 묶어 DB에 전송하고, 이 과정에서 에러가 발생할 경우 자동으로 모든 과정을 원래대로 되돌려 놓는다. 

  - ###### 이러한 과정을 구현하기 위해 Transaction은 하나 이상의 쿼리를 처리할 때 동일한 Connection 객체를 공유하도록 한다.

<br>

## [스프링 프레임워크의 트랜잭션]

- #### JTA, JDBC, Hivernate, JPA, JDO 같은 여러가지 트랜잭션 API 간에 일관성있는 프로그래밍 모델 제공

- #### Spring은 코드 기반의 트랜잭션(Programmatic Transaction) 처리 뿐만 아니라 선언적 트랜잭션(Declarative Transaction)을 지원 

- #### 선언적 트랜잭션 관리 지원

  - ###### 단 몇줄의 코드 만으로 다이나믹 프록시와 AOP라는 기술을 통해 인터페이스, 클래스, 메서드까지 세분화하여 트랜잭션을 제어할 수 있으며 Annotation기술로 @Transactional 을 설정하는 것으로도 트랜잭션 설정이 가능하도록 해준다.

  - ###### Spring이 제공하는 트랜잭션 템플릿 클래스를 이용하거나 설정파일, 어노테이션을 이용해서 트랜잭션의 범위 및 규칙을 정의할 수 있다. 

  - ###### Spring에서는 주로 선언적 트랜잭션을 이용하는데, <tx:advice>태그 또는 @Transactional 어노테이션을 이용하는데, 퀴리문을 처리하는 과정에서 에러가 났을 경우 자동으로 Rollback 처리를 해준다.

    - #### Rollback이란?

      - ###### 예를들어 친구에게 인터넷 뱅킹으로 10,000원을 송금할경우 나의 계좌에서 10,000원을 줄이고 친구의 계좌에 10,000원을 증가시켜야 한다. 하지만 알 수 없는 오류로 인해 나의 계좌에서는 10,000원이 줄었지만 친구 계좌에는 10,000원이 증가되지 않는다면? 나의 10,000원은 그냥 공중으로 증발해버리는 사고가 발생한다.

        ###### 이러한 경우가 생기지 않도록 중간에 오류가 발생하면 다시 처음부터 송금을 하도록 하는 것이 rollback이다.

    <br>

    <br>

- ### 트랜잭션 동작 원리

  <image src="./images/howtotransactionworking.png" width="414px" height="300px"> </image>

  1. caller가 target method를 호출하면 먼저 AOP proxy가 호출됨
  2. Transaction Advisor는 새로운 트랜잭션을 생성함
  3. Custom interceptor들이 transaction advisor 전 후로 호출됨
  4. Target 비즈니스 메소드가 호출됨
  5. Transaction Advisor는 커밋 또는 롤백을 결정하고 호출자에게 넘김
  6. AOP Proxy는 결과를 받아 Caller에게 넘김