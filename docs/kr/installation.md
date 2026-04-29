# 설치 방법

이 페이지에서는 Roblox 프로젝트에 Promise를 추가하는 실용적인 방법을 설명합니다.

## 방법 1: Wally

이미 Wally를 사용하고 있는 프로젝트의 경우 가장 깔끔한 설정입니다.

```toml
[dependencies]
Promise = "cometahn142/promise@^0.1"
```

이후 일반적인 Wally 워크플로우를 통해 종속성을 설치하고, 다른 공유 모듈과 마찬가지로 Rojo 프로젝트를 통해 패키지를 노출합니다.

## 방법 2: 수동 설치

아직 패키지 관리자를 사용하지 않는 경우 라이브러리를 직접 사용할 수도 있습니다.

1. `Promise`라는 이름의 `ModuleScript`를 생성합니다.
2. `src/init.luau`의 내용을 해당 스크립트에 복사합니다.
3. 코드에서 일관되게 불러올 수 있는 위치에 배치합니다.

이 방법은 소규모 프로젝트, 프로토타입 또는 로컬 실험에 적합합니다.

## 방법 3: 소스 제어 서브모듈 또는 벤더(Vendor) 폴더

라이브러리를 소스 제어에 직접 포함하는 경우, Promise를 타사 모듈 폴더에 배치하고 Rojo를 통해 동기화합니다. 이 방식은 버전 변경을 완전히 제어하고 변경 사항을 검토하고자 할 때 유용합니다.

## 설치 확인

설치가 완료되면 다음 코드가 작동해야 합니다.

```luau
local Promise = require(Packages.Promise)

Promise.resolve("ok"):andThen(function(value)
	print(value)
end)
```

출력 결과에 `"ok"`가 표시되면 패키지가 올바르게 연결된 것입니다.

## 다음 단계

- [사용 패턴 (Usage Patterns)](./usage-patterns.md)
- [Promise API](./promise.md)

## 라이선스

MIT. `LICENSE` 파일을 참조하세요.
