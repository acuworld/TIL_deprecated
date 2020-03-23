# 문자열(String)
C++ 코드 보다보면 뭔 괴상한 문자열 자료형들이 많이 나온다. (내가 아는 건 std::string과 char name[10] 뿐인데??)

LPSTR, LPCSTR, LPTSTR, LPCTSTR , LPWSTR, LPCWSTR <--- 머냐 이게??

- **STR**: String
- **LP**: Long Pointer (거의 필수)
- **C**: Constant
- **W**: Wide (unicode를 의미)
- **T**: 문자 집합에 따라 알아서 동작하는 것. (W 대신 사용하는 거)

## 자료형의 의미
- ```LPSTR``` = Long Pointer STR = ```char*```
- ```LPWSTR``` = LP Wide STR = ```wchar_t*``` **(비추. T 사용 권장)**
- ```LPCSTR``` = LP Const STR = ```const char*```
- ```LPCWSTR``` = LP Const Wide STR = ```const wchar_t*``` **(비추. T 사용 권장)**
- ```LPTSTR``` = LP t_char STR = ```char*``` 또는 ```wchar_t*```
- ```LPCTSTR``` = LPC t_char STR = ```const char*``` 또는 ```const wchar_t*```

## 자주 쓰는 형변환
- CString --> char*
  - ```str = (LPSTR)(LPCTSTR)cstr;```
  - CString을 const char* 로 먼저 변환 후, char* 로 변환하는 단계를 거친다. 대체 왜?
  - 정확히는, CString이 맨앞 16 byte를 자료형 표현에 사용하므로 이를 잘라내고 읽어야 함.
  - LPCTSTR이 이 16 byte를 잘라내고 읽어오는 역할을 해 준다. (!!)(단순 형변환이 아니었다..)
