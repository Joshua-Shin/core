## Spring을 활용한 웹 백엔드 개발 프로젝트
- 본 프로젝트는 <스프링 핵심 원리 :기본편 - 김영한> 강의를 수강하며 진행한 실습 프로젝트 입니다.
- 사용 스킬 : Java(JDK 1.8), Spring Boot(2.7.6), JUnit5, IntelliJ(2022.2.3)
-------
### 강의 내용 자유회상
- 스프링은 좋은 객체 지향 프로그래밍을 위한 것.
- 객체 지향의 꽃은 '다형성' + SOLID
- IoC = Inversion of Control 제어의 역전. 실행 영역과 구성 영역을 구분해서 객체를 생성하고 의존관계를 주입하는걸 외부에서 해주는거.
- DI = 의존관계 주입. 생성자 주입으로. 
- AppConfig 클래스를 통해 구성 역할을 분리하지 않았다면, 클래스내에서 참조하고자 하는 객체를 생성하고 주입했음. 이는 추상화도 구체화도 둘다 의존하게 되며 결과적으로 SRP, DIP, OCP를 어기게됨
- 프레임워크 : 내가 작성한 코드를 제어하고 대신 실행해줌. Spring, JUnit..
- DI 컨테이너 : AppConfig 클래스 처럼 객체를 생성하고 의존관계를 주입해주는거.
- 정적인 클래스 다이어그램 : 실행되기 전에 코드상으로 봐도 의존관계를 분석할 수 있는..
- 동적인 클래스 다이어그램 : 실행됐을때, 실제 어떤 클래스가 어떤 객체를 의존하고 있는가 보여주는거.
- 싱글톤. 유일한 객체임을 보장.
- 컴포넌트 스캔과 의존관계 자동 주입. @Configuration, @ComponentScan, @Component, @Autowired
- 스프링 부트에는 이미 @ComponetScan이 들어있음.
- 생성자 주입, 필드 주입, 수성자(setter) 주입,,, 주로 생성자 주입 사용
- 생성자가 하나 있을때는 의존관계를 위해 @autowired 안써도 됨
- 롬복. @Setter, @Getter, @RequiredArgsConstructor 활용
- 빈 생명주기 콜백을 위해 @PostConstruct, @PreDestroy
- 스코프에는 싱글톤, 프로토타입, 웹 관련 스코프 등이 있음. 웹 관련 스코프 에는 requeust, session 등이 있음.
- request 스코프 선언을 한 빈을 ObjectProvider로 감싼 이유
  - request 스코프 빈은 http 요청이 있어야만 생성 가능함.
  - 애플리케이션을 실행하면, 스프링 컨테이너는 component 등록된 빈들을 찾아 생성하려함.
  - 아직 http 요청이 없는 상태임.
  - 스프링 컨테이너는 request 스코프 빈을 생성하는데 실패함.
  - 따라서 빈 생성을 http 요청 이후 시점으로 지연시켜야함.
  - 그 방법이 DL 방법을 사용한 ObjectProvider임. 물론 javax의 Provider도 가능.
  - ObjectProvider<T>의 구현체가 .getObject()를 할때! 그때 스프링 컨테이너가 타입 인자로 들어간 빈을 생성, 의존관계주입, 초기화 해줌.
  - 또한, 매번 http 요청이 있을때마다, .getObject()를 호출하기에, 매번 새로운 빈을 생성해줄것이고, 때문에 요청마다 구분이 가능해짐.



