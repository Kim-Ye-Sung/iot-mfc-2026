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


### MFC 기초 학습
#### 기초 사상
순수 Win32 컨트롤 생성 함수
```cpp
HWND wnd = CreateWindow(...);
```

MFC는 각 컨트롤을 C_ 로 만들어 놓음
```cpp

```

##### 디자인 화면
리소스 뷰 (Ctrl + Shift + E)

- 디자인 확인 가능
- Dialog Based는 리소스에서 확인 가능하지만, SDI/MDI는 전체 화면을 확인할 메뉴/디자인뷰가 없음

| 방식           | 의미           |   난이도 |
| ------------ | ------------ | ----: |
| Dialog Based | 일반 폼 형태      |     ★ |
| SDI          | 한 문서 중심 프로그램 |   ★★★ |
| MDI          | 여러 문서/창 관리   | ★★★★★ |


- 프로그램 자체
    - MFCBasic.h
    - **MFCBasic.cpp** : 프로그램 시작점
- 화면(Dialog) UI
    - **MFCBasicDlg.h** : Dialog 클래스 선언 헤더 파일
    - **MFCBasicDlg.cpp** : 화면 수정시 가장 많이 변경하는 파일
- 리소스 UI
    - **MFCBasic.rc** : 가장 중요한 리소스 파일. 다이얼로그 디자인, 메뉴, 아이콘, 툴바, 문자열 테이블, 버전, 비트맵...
    - MFCBasic.rc2 : 사용 안함, 백업과 유사
    - `Resource.h` : rc에 있는 리소스 ID를 정의
    - MFCBasic.ico : 기본 아이콘 MFC 로고
- MFC 공통설정
    - pch.h
    - pch.cpp : Precompiled Header용 cpp. 수정 안함. VS가 사용하는 파일
    - framework.h : 프로젝트 전체 사용하는 Windows 헤더 포함
    - targetver.h : 지원할 Windows 버전 지정

```plaintext
#Win32 API

WinMain() 실행
    ↓
윈도우 실행
    ↓
메시지 루프
    ↓
WndProc()
```

```plaintext
# MFC

MFC 내부 WinMain() 자동 실행
    ↓
CWinApp
    ↓
InitInstance()
    ↓
Dialog 생성
```

- MFCBasic.cpp 소스

#### CDialogEx 클래스
    - MFCBasicDlg.h 소스
```cpp

```

##### Win32와 가장 큰 차이
- Win32 API는 `HWND hwnd;`라는 핸들을 중심으로 코딩
- MFC는 `CMFCBasicDlg dlg;` C++ 객체로 코딩. 실제 MFC 내부에 HWND 로 구성되어 있고, 이걸 MFC가 핸들링
- MFC CWnd는 Win32 API의 HWND를 C++ 클래스로 감싸 놓은 것일 뿐


#### MFC로 컨트롤 구성하기



##### WM_COMMAND 가 없다
    - MFC의 Message Map에서 처리해 줌
    - MFCBasicDlg.cpp 소스
        - 버튼 추가하고 

```cpp
BEGIN_MESSAGE_MAP(CMFCBasicDlg, CDialogEx)
    ON_WM_PAINT()
    ON_WM_QUERYDRAGICON()
    ON_BN_CLICKED(IDC_BUTTON_OK, &CMFCBasicDlg::OnBnClickedButtonOk)
END_MESSAGE_MAP()
```

##### 장점

##### MFC 학습 순서
1. Dialog 