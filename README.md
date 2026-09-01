# iot-mfc-2026
IoT반 MS MFC 학습 리포지토리

## MFC?
Microsoft Foundation Class 의 약자. C++ 기반의 윈도우 프로그래밍 라이브러리 중 하나.

GUI를 디자인, 실행하는 앱을 만들기 위해서 MS에서 만든 기술

- Linux : Qt, GTK, wxWidget ....
- Windows : Qt, Win32API, ...

리눅스와 윈도우가 OS 기반이 다르기때문에 초기에 표준화를 못함. Win32API 기반으로 GUI를 라이브러리화 -> MFC

윈도우에서만 동작하는 GUI 라이브러리 프레임워크임

현재는 리눅스에서 Wine 에뮬레이터로 Windows 기반 GUI도 실행 가능(PC카톡 윈도우 버전)

### MFC 단점 및 장점
#### 단점
- 너무 어렵다. 최소 6개월은 공부를 해야하는 문제
- 오래된 기술로 생각보다 최신 튜토리얼이 별로 없음.
- 기업이 예전부터 사용하던 솔루션 기반이 변경하기 힘들어서 계속 사용

#### 장점
- C++ 자체가 어려운데 MFC를 사용하면 복잡한 Win32 API를 직접 다루지 않아도 구현이 가능
- 생산성 향상 : 기존 C/C++ 대비하여 생산성 높다는 의미. C#, Java등 OOP와는 비교하면 안됨
- C++ 실력이 많이 좋아짐

### MFC 학습 링크
- [Microsoft Learn]() 


## MFC 튜토리얼
### 순수 Win32 API로 윈도우 만들기
- 중요! Windows 32 bit에서 C++에 있는 여러 기능을 손쉽게 쓰도록 만들어놓은 API(Application Programming Interface)
- 최초에는 이를 통해서 윈도우를 직접 개발

- 애플리케이션 종류
    - 콘솔 : 터미널에서 실행하는 CLI 앱
    - 데스크톱 : GUI로 실행하는 앱
    - 동적 연결 라이브러리(dll) : 다른 앱과 연결되는 라이브러리 또는 함수만 가지고 있는 패키지. 실행 후에 필요할 때 호출
    - 정적 라이브러리(lib) : dll과 거의 유사. 컴파일시에 포함되는 라이브러리

#### 기본 Win32 코드 작성
- `#include <Windows.h>` 작성 후 저장하면 위 외부 종속성 헤더파일들 추가됨. windows와 관련된 함수들을 마음대로 쓸 수 있다라는 의미
```cpp
// 윈도우 메시지를 처리하는 함수!!!!
LRESULT CALLBACK WndProc(		// LRESULT int64 타입의 포인터로 리턴
	HWND hwnd,
	UINT message,
	WPARAM wParam,
	LPARAM lParam
);

// 개념적
WndProc(
    현재창의 HWND,
    WM_DESTROY, // 윈도우창을 닫으라는 메시지
    추가정보,
    다른 추가정보
);
```
- LRESULT : int64 타입 LONG_PTR 포인터 크기를 의미. 32비트 OS든 64비트 OS든 기존 소스 그대로 사용하고자 만든 타입
    - Windows 메시지를 처리한 다음 Windows에게 돌려주는 값
- CALLBACK : 타입이 아니고 함수를 어떤 방식으로 호출할지 지정하는 매크로
- HWND : 윈도우 핸들. 식별번호와 참조값. 윈도우 내부 객체(포인터)를 직접 접근하면 위험함. 그래서 조금만 잘못하면 프로그램이 깨질 수 있기 때문에 핸들값으로 전달
- UINT : UnSigned Integer
- WPARAM : Word Parameter(윈도우 크기만큼의 Unsigned Integer), 메시지에 첫번째 추가 메시지 데이터.
    - 마우스 클릭시 위치값(x, y 좌표 등)
- LPARAM : Long Parameter(uint), 두번째 추가 메시지 데이터

### MFC 프로젝트 생성
