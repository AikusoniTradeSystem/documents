# 구현 고려 요소들

이 문서는 미래에 구현해서 넣을까 고민 중엔 요소들을 작성해 넣은 문서입니다.

### 회로차단기 (Circuit Breaker)
- 서비스 장애시, 서비스의 장애를 최소화하기 위해 회로차단기를 구현
- 사용자 단에서 API 호출시, 서비스가 장애일 경우, 회로차단기가 서비스 호출을 차단하고, 대체 데이터를 제공
- 사용자 단에서 화면 표시시, 서비스가 장애일 경우, 회로차단기가 대체 데이터를 제공

### 격벽 (Bulkhead)
- 서비스 장애시, 서비스의 장애를 최소화하기 위해 격벽을 구현
- 각 서비스마다 다른 큐나 스레드 풀을 사용해 격벽을 구현
- 격벽을 통해 서비스의 장애가 전체 서비스에 영향을 미치지 않도록 함

### 커넥션풀 (Connection Pool)
- 서비스 장애시, 서비스의 장애를 최소화하기 위해 커넥션풀을 구현
- 커넥션풀을 사용해 특정 서비스의 지연시간이 길어지더라도, 다른 서비스에 영향을 미치지 않도록 함