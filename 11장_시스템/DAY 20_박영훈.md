# 11장 시스템

# 🗒️ 관심사 분리

**생성**과 **사용**은 아주다르다!

- 시작에 대한 관심사 분리
    - 객체의 생성은 시작 단계에서!
        - 비즈니스 로직은 객체를 편하게 사용하고 로직에 집중!
- 요청에 대한 관심사 분리
    - Spring에서는 요청이 들어올때 계층 별로 나뉘어져서 필요한 역할들을 수행한다.
        - Filter : 서블릿 필터는 요청 내용을 변경하거나 요청을 처리하기 전에 작업을 수행.
        - Interceptor : 여러 인터셉터를 활용하여 로그인 처리, 권한체크, 프로그램 실행시간 계산작업, 로그 확인 수행
            - AOP : 필터와 인터셉터는 Servlet 단위에서 실행되는 반면 AOP는 메소드 앞에서 Proxy 패턴으로 실행된다. 
            주로 로깅, 트랜잭션, 에러처리 등 비즈니스 관점에서 더 세밀하게 조정하고 싶을 때 사용.
- Dependency Injection (의존성 주입)
    - 객체 의존성을 DI 컨테이너에 맡긴다.
        - 필요한 객체의 인스턴스를 생성하고 의존성 주입을 통해 객체들간의 의존성을 연결 시켜준다.
    - Spring IoC Container
        - 컴포넌트 스캔 or Configuration 으로 빈을 spring container에 등록하고 
        여러 빈들의 의존성 관계를 @Autowired를 통해 연결해준다.
- Cross Cutting Concerns 분리 (횡단 관심 분리)
    - Presentation Layer, Business Layer, Data Access Layer 가 공통적으로 갖는 관심사가 있다.
    - Logging, Transaction, Security 등 이것들을 분리시키자!
    
    ```java
    public Response executeBusinessLogic(Request request) {
    	// 공통 기능
    	checkAuth(request)
    
    	// 비즈니스 로직
    	Response response = businessLogic(userName, message)
    
    	// 공통 기능
    	logging(response)
    }
    ```
    
    ```java
    public Response executeBusinessLogic(Request request) {
    	// 비즈니스 로직
    	Response response = businessLogic(userName, message)
    }
    // 공통 기능은 별도의 코드로 분리.
    ```
    
    - 예시
        - Java Proxy API
        - 순수 Java AOP Framework
        - EJB3 - JPA 같은 객체 영속성 관리 표준 API
