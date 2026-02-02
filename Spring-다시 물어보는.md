# 빈
```
// 1. 클래스 정의 (그냥 평범한 설계도)
public class MyService {
    public void sayHello() {
        System.out.println("안녕하세요! 직접 만든 객체입니다.");
    }
}

// 2. 클래스 사용 (Main 클래스)
public class Main {
    public static void main(String[] args) {
        // [생성] 내가 직접 'new'를 호출해서 메모리에 올림
        MyService service = new MyService(); 
        
        // [실행] 생성한 변수를 통해 메서드 호출
        service.sayHello(); 
        // 결과: "안녕하세요! 직접 만든 객체입니다."가 콘솔에 출력됨
    }
}
```

빈
@Component가 기본이고, 그 외에는 이름만 다르고 모두 @Component의 기능


```
// 1. 클래스 정의 (스프링에게 관리를 맡김)
@Component // <-- "스프링아, 이 클래스 네가 'new'해서 빈으로 가지고 있어!"
public class MyService {
    public void sayHello() {
        System.out.println("안녕하세요! 스프링이 관리하는 빈입니다.");
    }
}

// 2. 클래스 사용 (스프링 컨테이너 안에서 실행)
@Service // <-- "스프링아, 이 MyController 클래스 네가 'new'해서 빈으로 가지고 있어! 근데 이건 비즈니스 로직이야" (원랜 @Controller지만 뭐 그렇다고 해둘까?)
public class MyController {

    // [중요] 내가 직접 'new' 하지 않음! 
    @Autowired 
    private MyService service; // <-- 스프링이 보관 중인 MyService 빈을 자동으로 연결해줌

    public void runTest() {
        // [실행] 이미 스프링이 객체를 넣어줬으므로 바로 사용 가능
        service.sayHello(); 
        // 결과: "안녕하세요! 스프링이 관리하는 빈입니다."가 콘솔에 출력됨
    }
}
```

# 음

내가 4. 알아야 할 핵심 리스트 업데이트 
이제 질문자님의 **"스프링에서 꼭 알아야 할 핵심 명찰 리스트"**는 이렇게 완성됩니다. 

- 빈 등록: @Component (그 친구들 포함), @Bean 
- 빈 연결: @Autowired (부품끼리 조립) 
- 값 주입: @Value (부품에 데이터 채우기) 
- 스위치: @SpringBootApplication 

이렇게 배웠거든, 이 4분류에 포함되지 않는 니가 말한 @는 뭐가 있지?

아 👍 이거 **되게 좋은 질문**이야.
지금 네가 정리한 4분류는 사실 **“스프링의 뼈대”**거든.
그래서 내가 말한 것들 중에 **그 4칸에 안 들어가는 애들**을 딱 분리해줄게.

---

## 먼저, 네가 배운 4분류 다시 기준 잡기

1. **빈 등록**
   → “이 클래스를 스프링이 관리해라”

2. **빈 연결(DI)**
   → “이 빈이 저 빈을 쓰게 해라”

3. **값 주입**
   → “외부/설정 값을 넣어라”

4. **스위치(부트 시작)**
   → “스프링 부트 앱이다”

이 기준으로 **안 들어가는 애들만** 추려보자.

---

## ❌ 1. 웹 요청 처리용 (@MVC 계열) — **네 4분류 바깥**

| 어노테이션             | 왜 안 들어가나 |
| ----------------- | -------- |
| `@RequestMapping` |          |
| `@GetMapping`     |          |
| `@PostMapping`    |          |
| `@PutMapping`     |          |
| `@DeleteMapping`  |          |
| `@PathVariable`   |          |
| `@RequestParam`   |          |
| `@RequestBody`    |          |
| `@ResponseBody`   |          |

👉 얘네는
❌ 빈을 등록하지도
❌ 빈을 연결하지도
❌ 값을 주입하지도
❌ 앱을 켜지도 않음

👉 **“웹 요청 ↔ 메서드 연결” 전용**

---

## ❌ 2. DB / JPA 매핑용 — **스프링이 아니라 ‘ORM 세계’**

| 어노테이션             | 정체 |
| ----------------- | -- |
| `@Entity`         |    |
| `@Id`             |    |
| `@GeneratedValue` |    |
| `@Column`         |    |
| `@Table`          |    |
| `@ManyToOne`      |    |
| `@OneToMany`      |    |
| `@JoinColumn`     |    |

👉 이건 **스프링 코어 아님**
👉 “자바 객체 ↔ DB 테이블” 매핑용 명찰

---

## ❌ 3. 트랜잭션 / AOP — **행동을 바꾸는 애들**

| 어노테이션               | 뭐가 다른가                  |
| ------------------- | ----------------------- |
| `@Transactional`    | 메서드 실행 전/후에 트랜잭션을 끼워 넣음 |
| `@ExceptionHandler` | 예외 가로채기                 |
| `@ControllerAdvice` | 전역 예외 처리                |

👉 얘네는
**“이 메서드가 실행될 때 규칙을 바꿔라”** 쪽

---

## ❌ 4. 검증(Validation) — **값을 검사하는 명찰**

| 어노테이션       | 역할 |
| ----------- | -- |
| `@Valid`    |    |
| `@NotNull`  |    |
| `@NotBlank` |    |
| `@Size`     |    |

👉 “주입”이 아니라 **“검사”**

---

## ❌ 5. 편의 / 도구 (Lombok 등) — **스프링 외부**

| 어노테이션                      | 비고 |
| -------------------------- | -- |
| `@Slf4j`                   |    |
| `@Getter`                  |    |
| `@Setter`                  |    |
| `@RequiredArgsConstructor` |    |

👉 컴파일 타임 도구
👉 스프링이 직접 처리하지도 않음

---

## 🔥 핵심 정리 (이 문장만 기억해도 됨)

> 네가 배운 4분류는
> **“스프링 컨테이너를 만드는 명찰들”**이고
>
> 나머지 어노테이션들은
> 👉 **웹**, **DB**, **행위 제어**, **검증** 같은
> **‘기능 세계’의 명찰들**이다.

그래서 공부 순서도 이렇게 가는 게 맞아:

1️⃣ 지금 배운 4개 → **완벽 이해**
2️⃣ MVC (@GetMapping…)
3️⃣ JPA (@Entity…)
4️⃣ @Transactional (이건 따로 깊게)

원하면 다음 단계로
👉 **“각 어노테이션을 언제 붙이면 틀리는지”**
👉 **“이거 붙이면 왜 동작이 이상해지는지”**
같은 실전 감각 정리도 해줄게.
