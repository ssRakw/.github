# ✅ C++ 코드 컨벤션 (언리얼 엔진용)

---

## 📌 1. 네이밍 규칙

| 항목           | 규칙                                   | 예시                                 |
| :------------- | :------------------------------------- | :-------------------------------------- |
| **지역 변수** | **카멜 케이스 (CamelCase)** (접두사 `_` 사용 안 함) | `playerName`, `totalScore`              |
| **상수** | `const` 또는 `constexpr` **파스칼 케이스 (PascalCase)** | `const int MaxBufferSize`               |
| **함수명** | **파스칼 케이스 (PascalCase)** | `CalculateTotal()`                      |
| **클래스/구조체** | **파스칼 케이스 (PascalCase)** | `APlayerInfo`, `UGameManager`           |
| **멤버 변수** | `_` + **카멜 케이스 (CamelCase)** (UObject 멤버는 public/protected인 경우 `_` 생략 가능) | `_health`, `_maxSpeed` (UObject가 아닌 경우), `Health`, `MaxSpeed` (UObject 프로퍼티의 경우) |
| **메서드** | **카멜 케이스 (CamelCase)** | `GetName()`, `SetScore()`               |
| **열거형** | `enum class` 또는 `UENUM()`와 함께 타입은 **파스칼 케이스 (PascalCase)**, 열거자(enumerator)는 **파스칼 케이스 (PascalCase)** | `enum class EPlayerState { Idle };` 또는 `UENUM() enum class EPlayerState : uint8 { Idle, Walking };` |
| **타입 정의 (typedef/using)** | `_` 접두사 + **파스칼 케이스 (PascalCase)** (`T`는 템플릿, `F`는 구조체, `U`는 클래스, `A`는 액터, `I`는 인터페이스) | `typedef class UMyClass FMyClassDefinition;`, `using FMyCustomStruct = MyStruct;` |

---

## 📌 2. 들여쓰기 & 포맷팅

-   `if`, `while`, `for` 등의 제어문 뒤의 여는 중괄호(`{`)는 해당 문장의 **다음 줄**에 위치합니다:

    ```cpp
    if (Condition)
    {
        // ...
    }
    ```

    ```cpp
    void PrintScore(); // 선언

    void PrintScore()
    { // 정의
        // ...
    }
    ```

-   **한 줄에 한 명령어**:

    ```cpp
    int A = 5;
    A += 1;
    ```

-   **한 줄에 하나의 변수만 선언**:

    ```cpp
    int X;
    int Y;
    ```

-   함수 내부에 선언할 수 있는 변수의 개수에 대한 **엄격한 제한은 없습니다**. 가독성에 중점을 둡니다.
-   함수 매개변수의 개수에 대한 **엄격한 제한은 없습니다**. 너무 많다면 구조체를 전달하는 것을 고려합니다.
-   `void` 함수는 조기 종료하는 경우가 아니라면 일반적으로 **명시적으로 `return;`를 작성하지 않습니다**.
-   **함수는 간결하게 유지**해야 하지만, 40줄과 같은 엄격한 제한은 없습니다. 복잡한 함수는 분리합니다.

---

## 📌 3. 파일 구조 및 헤더 처리

-   **헤더 가드는 반드시 작성**해야 합니다. **`#pragma once`를 강력히 권장**합니다.

    ```cpp
    #pragma once

    // 선언
    ```

-   모든 `#include` 지시문은 **파일 시작 부분에 위치**합니다.
-   **사용하지 않는 헤더는 포함하지 않습니다**.
-   **변수는 블록 시작 시 한꺼번에 선언할 필요 없이**, 처음 사용하기 직전에 선언할 수 있습니다 (C++ 모범 사례를 따름).

---

## 📌 4. 함수 주석 규칙

언리얼 엔진은 문서 생성을 위해 Doxygen 스타일 주석을 선호합니다. 헤더 파일의 **함수 선언부 위에 주석을 작성**합니다.

```cpp
/**
 * @brief 표준 출력으로 메시지를 출력합니다.
 * @param Message 출력할 문자열입니다.
 */
void PrintMessage(const FString& Message); // 언리얼 타입에는 FString 사용에 유의
