# 자주 쓰는 클래스 모음

## CString
문자열 처리를 편하게 해 주는 클래스.  
원래 MFC에 포함되어 있는 녀석인데, 너무 유용하다보니 따로 헤더로 빠져나옴. (atlstr.h)  
문자 집합에 따라 CStringA와 CStringW로 내부적으로 알아서 갈린다.

### 단점
- 지역 변수로 선언해도 내부적으로 new를 하기 때문에 스택이 아닌 힙에 할당됨.

### 대표적 문법
- 콘솔 출력
  - ```printf(cstr);``` 또는 ```printf("%S", cstr); // 대문자 S```
- 포매팅
  - ```cstr.Format("my age is %d.",age);```
- 붙이기(concatenation)
  - ```cstr3 = cstr1 + "/" + cstr2;```
