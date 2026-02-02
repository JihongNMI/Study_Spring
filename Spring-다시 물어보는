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
```
// 1. 클래스 정의 (스프링에게 관리를 맡김)
@Component // <-- "스프링아, 이 클래스 네가 'new'해서 빈으로 가지고 있어!"
public class MyService {
    public void sayHello() {
        System.out.println("안녕하세요! 스프링이 관리하는 빈입니다.");
    }
}

// 2. 클래스 사용 (스프링 컨테이너 안에서 실행)
@Service // 설명을 돕기 위한 예시 클래스
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
