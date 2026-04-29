# 사용 패턴 (Usage Patterns)

이 페이지는 개별 함수보다는 Promise가 실제 Roblox 코드에 어떻게 적용되는지에 중점을 둡니다.

## 비동기 작업 래핑 (Wrapping)

기본 작업이 비동기적이고 결과를 명시적이고 조합 가능하게 만들고 싶을 때 `Promise.new`를 사용합니다.

```luau
local function loadPlayerData(userId)
	return Promise.new(function(resolve, reject)
		task.delay(1, function()
			if userId <= 0 then
				reject("유효하지 않은 사용자 ID")
				return
			end

			resolve({
				UserId = userId,
				Coins = 100,
			})
		end)
	end)
end
```

## 결과 변환

하나의 비동기 결과가 다음 단계로 이어져야 할 때 `andThen`을 사용합니다.

```luau
loadPlayerData(42)
	:andThen(function(profile)
		return profile.Coins
	end)
	:andThen(function(coins)
		print("보유 코인:", coins)
	end)
```

## 실패 처리

현재 경계(Boundary)에서 오류(Rejection)를 처리할 책임이 있을 때 `catch`를 사용합니다.

```luau
loadPlayerData(0)
	:catch(function(err)
		warn("플레이어 데이터를 로드할 수 없습니다:", err)
	end)
```

## 여러 작업 대기

여러 비동기 작업이 하나의 논리적 흐름에 속할 때 조합기(Combinators)를 사용합니다.

```luau
Promise.all({
	loadInventory(),
	loadStats(),
	loadSettings(),
})
```

일반적인 규칙:
- `all`: "모두 성공해야 함"
- `race`: "가장 빠른 결과가 승리"
- `any`: "가장 빠른 성공이 승리"
- `allSettled`: "모든 결과를 확인"

## 취소 (Cancellation)

작업이 완료되기 전에 호출자가 사라질 수 있는 경우 취소가 가장 중요합니다:
- UI 화면이 닫힐 때
- 플레이어가 게임을 떠날 때
- 객체가 파괴될 때
- 요청이 최신 요청으로 대체될 때

```luau
local p = loadPlayerData(42):timeout(5)
p:cancel()
```

실행자(Executor)가 백그라운드 작업을 시작하는 경우, `onCancel`을 사용하여 정리를 등록하세요.

## 코루틴 기반 코드에서의 대기

이미 코루틴 내부에 있는 경우 `await`가 가장 깔끔한 가교 역할을 하는 경우가 많습니다.

```luau
local ok, result = loadPlayerData(42):await()
if ok then
	print(result.Coins)
end
```

동기식 스타일이 더 읽기 쉬운 경계에서만 제한적으로 사용하세요. 재사용 가능한 라이브러리 코드 내부에서는 Promise를 반환하는 것이 일반적으로 더 좋습니다.

## 실용적인 조언

- 예기치 않게 Yield를 발생시키는 대신 비동기 API에서 Promise를 반환하세요.
- 깊게 중첩된 콜백보다는 작은 체인을 선호하세요.
- 외부 또는 플레이어 주도 작업에는 타임아웃을 추가하세요.
- 모든 곳이 아닌 소유권 경계에서 오류를 포착(Catch)하세요.

## 다음 단계

- [설치 방법 (Installation)](./installation.md)
- [Promise API](./promise.md)

## 라이선스

MIT. `LICENSE` 파일을 참조하세요.
