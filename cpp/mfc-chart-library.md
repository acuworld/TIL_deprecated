# MFC 차트 라이브러리

MFC를 지원하는 차트 라이브러리가 극소수이다. 아무리 찾아 봤자 아래 두 개 정도 나온다.
- ChartFX
  - 유료. 근데 기능이 엄청 좋다.
- ChartDirector
  - 오픈 소스. 대신 차트 아래에 저작권 문구가 뜬다. 결제하면 사라짐.

## ChartDirector
### 개요
- 사전 컴파일 된 dll 형태로 제공됨. (implicit linking 방식으로 호출)
- 차트를 컨트롤 할 수 있는 CChartViewer 클래스를 제공함.
- 내부적으로 이미지 형태로 차트를 그려낸다.
  - MFC의 Chart Control 에 그려내는 형태
  - Dynamic Resize가 불가능하며, 크기 변화를 원하면 Redraw를 해야 함.

### 설치
- dll 파일을 exe 파일과 동일한 위치에 둔다.
- 나머지 lib 파일, 클래스 파일, 인클루드 파일을 프로젝트 폴더에 때려박기.
- DLL implicit linking
  - 적절한 파일에 ```#pragma comment(lib,"chartdir60.lib")``` 추가.
- Dialog에 Chart Control 추가
  - ID는 임의로 **IDC_CHART** 같은거로 설정
  - Type : Bitmap
- 차트 컨트롤을 위해 클래스 변수 추가
  - (Chart Control 우클릭 해서 Add Variable 로 해도 되고, 메뉴얼로 해도 됨)
  - ```CChartViewer m_ChartViewer;```
- DDX Control 연결
  - DoDataExchange 콜백 함수에 아래 내용 추가해서 **클래스 변수**와 **컨트롤**을 연결.
  - ```DDX_Control(pDX, IDC_CHART, m_ChartViewer);```

### 자세한 사용법
- 파일로 제공되는 도움말이 상당히 괜찮다. 보고 따라하면 됨. (doc/cppchartdir.chm)
