# Clean Code

# 5장 형식맞추기

## 1. 포맷팅이 중요한 이유

⇒ **가독성**에 필수적이다! & 코드를 잘못 해석해 **버그를 발생할 위험을 줄인다**

---

- 형식이 맞지 않는 코드

```java
public void horriblyFormattedMethod() {
	System.out.println("First line");
			System.out.println("Second line");
		System.out.println("Third line");
	for (int i = 0; i < 3; i++)
	System.out.println("number " + i);
}
```

- 형식이 맞는 코드

```java
public void horriblyFormattedMethod() {
	System.out.println("First line");
	System.out.println("Second line");
	System.out.println("Third line");
	for (int i = 0; i < 3; i++) {
		System.out.println("number " + i);
	}
}
```

> 코드 형식은 의사소통의 일환이다.
> 

---

## 2. 클린코드 포맷팅

- **적절한 길이 유지 ⇒ 200 라인**
    - 이유
        - 작은 파일이 이해하기 쉽다
        - 200줄을 넘긴다면 클래스가 여러 일을 하고 있을 수 있다 ⇒ SRP 위배
    
- **밀접한 개념은 가까이 둔다**
  
    🕶️ **줄 바꿈** : 개념 분리
    **세로 밀집도** : 연관성 (서로 밀접한 코드 행은 세로로 가까이 둬라)
    
    예)
    
    ```java
    public class BoldWidget extends ParentWidget {
    	public static final String REGEXP = "'''.+?'''";
    	private static final Pattern pattern = Pattern.complie("'''(.+?)'''",
    		Pattern.MULTILINE + Pattern.DOTALL
    	);
    	
    	public BoldWidget(ParentWidget parent, String text) throws Exception {
    		super(parent);
    		Matcher match = pattern.matcher(text);
    		addChildWidgets(match.group(1));
    	}
    
    	public String render() throws Exception {
    		StringBuffer html = new StringBuffer("<b>")
    		html.append(childHtml()).append("</b>");
    		return html.toString();
    	}
    }
    ```
    
    - **빈 행** : 개념은 빈 행으로 구분
        - 빈 행은 새로운 개념을 시작한다는 시각적 단서
    - **변수선언** : 변수는 사용되는 위치에서 최대한 가까이 선언
    - **인스턴스 변수** : 인스턴스 변수는 클래스 제일 처음에 선언
    - **종속함수** : 한 함수가 다른 함수를 호출한다면 두 함수는 세로로 가까이 배치한다.
        - 일반적으로 함수 호출 종속성은 아래방향으로 유지
          
            ⇒ 호출되는 함수를 호출하는 함수보다 나중에 배치
            
            - 장점
                - 소스코드 모듈이 고차원에서 저차원으로 자연스럽게 내려간다.
                - 세세한 사항까지 파고들지 않아도 개념을 파악하기 쉬워진다.
                  
                    ⇒ 가장 중요한 개념들이 위쪽에 배치해있으므로 위쪽 코드만 읽어도 개념 파악을 쉽게 할 수 있다
        
    - **개념적 유사성** : 친화도가 높을 수록 코드를 가까이 배치한다
        - 예 : 종속함수, 비슷한 동작을 수행하는 함수
    
- **가로 형식 맞추기**
    - **가로 공백과 밀집도**
        - 가로로는 공백을 사용하여 밀접한 개념과 느슨한 개념을 표현
    - **들여쓰기**
        - 범위로 이루어진 계층을 표현하기 위해 들여쓴다
          
            ⇒ 들여쓰기한 파일은 구조가 한눈에 들어온다
            

---

## 3. Java Class Declarations

: 자바 클래스를 어떻게 선언해야하는지 formatting role

### Class 내부 코드 순서

1. static 변수
   
    같은 static 인 경우 : public → protected → package → private 순서
    
2. instance 변수
   
    같은 instance 변수인 경우 : public → protected → package → private
    
3. 생성자
4. 메서드
   
    같은 메서드인 경우 : public 메서드에서 호출되는 private 메서드는 그 아래에 둔다. 가독성 위주로 그룹핑 → 종속함수
    

---

## 4. Team Coding Convention

- **Coding Convention** : 코딩 스타일에 관한 약속
- **Team Coding Convention** : 팀의 코딩 스타일에 관한 약속
    - 개발 언어의 컨벤션 → 팀 컨벤션(애매한 부분 ex) 변수명))
      
        ex) MySQL Convention : 컬럼명은 snake_case로 네이밍
        
        Team Convention : enum 타입으로 사용하는 varchar 타입의 경우 컬럼명은 _type으로 끝나도록 네이밍한다.
        

🕶️ 참고할 만한 컨벤션
[Google Java Style Guide](https://google.github.io/styleguide/javaguide.html)
[Naver Hackday Java Convention](https://naver.github.io/hackday-conventions-java/) : 한글 문서, naver에서 쓰임