# 7장 오류 처리

## ✍️예외 처리 방식
- 오류 코드를 리턴 하지말고, 예외를 던져라
  - 오류가 발생 예상되는 부분에서 예외를 던지고 그 예외를 처리하는 Handler를 구현.
  - 오류가 발생하더라도 예외 처리를 하고 계속해서 프로그램이 실행할 수 있도록 함.
  - 자바에서는 현재 메소드내에서 에러를 처리할 수 있으면 catch해서 처리하고 처리할 수 없다면 throws 키워드를 통해 상위에서 처리 할 수 있도록 함.
        
## ✍️Exception 종류
- Checked Exception (Exception 상속)
    - 명시적인 예외처리 O
- Unchecked Exception (Runtime Exception 상속)
    - 명시적인 예외처리 X
        
## ✍️Unchecked Exception을 사용하라
- 사용자가 직접 구현하는 unchecked throwable은 모두 RuntimeException의 하위 클래스여야 한다.
- Error 클래스를 상속해서 하위 클래스를 만들지말자 → Exception으로 처리하자.
- Checked Exception이 나쁜 이유
    - 특정 메소드에서 checked exception을 throw하고 상위 메소드에서 catch하여 처리한다면 모든 중간단계 메소드들이 해당 exception을 throw해야 한다. - 무조건 예외를 처리 해야하기 때문에
    - 상위 클래스에서 하위 클래스의 디테일한 예외까지 알고 있어야 되는 것이기 때문에 OCP를 위배한다.
        
## ✍️Exception 잘 쓰기
- 예외에 메시지를 담아라
- 여러 예외들을 처리하는 경우 예외들을 감싸는 클래스를 만들어라 -exception wrapper
    
## ✍️실무 예외 처리 패턴
- getOrElse- 예외 대신 기본 값을 리턴한다.
    - null이 아닌 기본값
        - null을 반환하는 메소드를 기본값을 반환하도록 바꾸자 → null을 반환하면 계속 null 체크를 해야한다.
    - 도메인에 맞는 기본값
        - 예외처리를 데이터를 제공하는 쪽에서 처리하여 호출부를 깔끔하게 하고 null이면 default 즉 기본값을 반환하게 하자.
            
- getOrElseThrow
    - 기본값이 없다면 null 대신 차라리 예외를 던져라!!
        - null을 반환한다면?
            - null 체크지옥..
            - 가독성도 떨어진다.
        - 데이터를 제공하는 쪽에서 예외를 던져라 호출부는 깔끔하게.
- 메소드에서  파라미터 예외 처리를 통해 null을 받지 못하게 하자.
- 실무에서는 보통 자신만의 예외를 정의한다.
    - 이름만 봐도 인지할 수 있음
    - 진행 중인 프로젝트에 세부적인 에러를 정의 할 수 있음.
