## Exception 클래스 생성 규칙

1. 모든 커스텀 Exception 클래스는 다음 예시와 같이 [core 모듈](https://github.com/AikusoniTradeSystem/ats-spring-core)의 [BaseAtsException](https://github.com/AikusoniTradeSystem/ats-spring-core/blob/main/src/main/java/io/github/aikusonitradesystem/core/exception/BaseAtsException.java) 인터페이스를 구현해야 합니다.
```java
import java.nio.charset.CodingErrorAction;

@Getter // lombok 사용
public class CustomAtsException extends RuntimeException implements BaseAtsException {
    private final ErrorCode errorCode;
    private final String errorAlias;

    public AtsException(ErrorCode errorCode, String errorAlias, String message) {
        super(message);
        this.errorCode = errorCode;
        this.errorAlias = errorAlias;
    }
}
```