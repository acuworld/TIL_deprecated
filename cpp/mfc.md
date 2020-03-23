# MFC (Microsoft Foundation Class Library)

## 개요
- Windows API 함수가 너무 자잘하고 많아서, 유사한 기능끼리 C++ 클래스로 한 번 감싼 것.
- Application Framework Class (AFX)
  - WinAPI --> AFX --> MFC 로 발전한 계보가 있음. MFC가 AFX를 포함하고 있음.
  - CWndApp을 관리하는 역할.
- CWndApp 클래스
  - 프로그램 전체를 대표하는 역할.
  - 프로그램의 시작과 종료를 담당.
  - 프로그램 시작 시 메인 프레임 윈도우를 생성.
- GUI는 3개 클래스로 이뤄진 구조이며, 아래 3개를 CWndApp 클래스가 관리함.
  - CFrameWnd : 윈도우 프레임 담당. 윈도우 버튼(최소화, 최대화, 닫기) 및 스크롤 바 등등.
  - CView : 실제 컨텐츠 담당.
  - CDocument : 데이터 저장 및 처리 담당.
- 프로그램 실행 구조
  1. 컴파일러가 entry point를 main()이 아닌 WinMain()으로 접근하도록 컴파일.
  2. MFC 프레임워크 내부의 WinMain() 호출. (프로그램의 메인 함수. 프로그래머가 접근 불가)
  3. InitInstance() 호출. (프로그래밍 가능한 실질적인 메인 함수)
  4. Run() 호출.

## 주저리 주저리
- WinAPI를 C++ 클래스화 해서 편하게(?) 쓰도록 만든 것이기 때문에, 결국 WinAPI를 알아야 함;;
- 요즘 누가 MFC 쓰냐며 C#이나 Qt를 들이밀지만, MFC는 GUI 만을 위한 건 아니다.
  - **Console Program**을 만들 때에도 MFC를 쓸 수 있다.
  - MFC는 GUI 이외에도 자료 구조나 예외 처리 등의 유용한 클래스를 많이 포함한다.
  - 하지만 MFC를 쓰면 Windows에서만 동작함. 크로스 플랫폼 고려 시 POSIX 써야 함.

## VS 프로젝트 구조
- stdafx.h
  - 헤더들을 미리 컴파일 해 둬서 빌드를 빠르게 하는 목적.
  - 여기에 등록해 두면 Precompiled 되어 .pch 파일이 생성됨.
  - 이 기능을 사용하려면 모든 .cpp 파일들이 ```#include "stdafx.h"``` 로 시작해야 함.
- PROJECT_NAME.cpp

## 출처
- [단국대학교 수업 자료 - MFC 프로그램 구조](https://dis.dankook.ac.kr/lectures/hci07/wp-content/uploads/sites/28/1/1350897030.pdf)
- [슬라이드플레이어 - MFC Application Frameworks (AFX)](https://slidesplayer.org/slide/14019179/)
