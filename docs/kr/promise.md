# Promise

이 페이지는 Promise 모듈의 공개 API 표면을 요약합니다.

## 생성자

- `Promise.new(executor)`
- `Promise.defer(executor)`
- `Promise.resolve(value)`
- `Promise.reject(reason)`
- `Promise.try(fn, ...)`

비동기 실행자, 즉시 값 또는 예외(Throw)가 발생할 수 있는 코드로부터 Promise 값을 생성할 때 사용합니다.

## 어댑터 (Adapters)

- `Promise.promisify(callback)`
- `Promise.fromEvent(event, predicate?)`
- `Promise.delay(seconds)`

이 헬퍼들은 콜백 스타일이나 이벤트 스타일의 워크플로우를 Promise 기반 워크플로우로 변환합니다.

## 조합기 (Combinators)

- `Promise.all(promises)`
- `Promise.some(promises, count)`
- `Promise.race(promises)`
- `Promise.any(promises)`
- `Promise.allSettled(promises)`
- `Promise.each(list, predicate)`
- `Promise.fold(list, reducer, initialValue)`

이 함수들은 여러 비동기 작업을 조율하는 데 도움을 줍니다.

## 재시도 헬퍼 (Retry Helpers)

- `Promise.retry(callback, times, ...)`
- `Promise.retryWithDelay(callback, times, seconds, ...)`

오류가 일시적일 수 있는 경우에 유용합니다.

## 인스턴스 메서드

- `andThen(onFulfilled?, onRejected?)`
- `catch(onRejected)`
- `finally(onFinally)`
- `tap(onTap)`
- `andThenCall(callback, ...)`
- `andThenReturn(...)`
- `finallyCall(callback, ...)`
- `andThenReturn(...)`
- `finallyReturn(...)`
- `now(rejectionValue?)`
- `timeout(seconds, rejectionValue?)`
- `cancel()`
- `getStatus()`
- `awaitStatus()`
- `expect()`
- `await()`

## 상태 상수

- `Promise.Status.Pending`
- `Promise.Status.Fulfilled`
- `Promise.Status.Rejected`
- `Promise.Status.Cancelled`

## 에러 API

- `Promise.Error.new(options?)`
- `Promise.Error.is(value)`
- `Promise.Error.Kind.ExecutionError`
- `Promise.Error.Kind.AlreadyCancelled`
- `Promise.Error.Kind.NotResolvedInTime`
- `Promise.Error.Kind.TimedOut`

## 훅 (Hooks)

- `Promise.onUnhandledRejection(callback) -> disconnectFn`

처리되지 않은(Rejected) Promise에 대한 중앙 보고가 필요할 때 사용합니다.

## 관련 문서

- [설치 방법 (Installation)](./installation.md)
- [사용 패턴 (Usage Patterns)](./usage-patterns.md)

## 라이선스

MIT. `LICENSE` 파일을 참조하세요.
