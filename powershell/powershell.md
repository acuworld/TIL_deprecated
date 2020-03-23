# PowerShell

## 파워쉘이란?
- 리눅스에 bash, csh, ksh 등등 다양한 쉘 존재하듯, 윈도우에도 PowerShell이 있음.
- 명령어 체계가 bash나 명령 프롬프트랑 많이 다르므로 새로 공부해야 함.
- 다른 쉘 대비 장점:
  - COM, WMI에 완전한 액세스 가능하므로, 장치 관리나 원격 관리 등 거의 모든 작업 가능.
    - 환경 변수, 레지스트리, 서비스 제어, 프로세스 제어 등의 업무 자동화 가능.
  - 파이프라인 전달 시 단순 텍스트가 아니라 오브젝트를 전달하므로 데이터 가공 유연함.
  - C# 및 .NET 기반이며, Linux나 Mac OS에서도 동작 가능.
    - 닷넷 스크립팅도 가능.
  - 기존 cmd.exe 명령어 전부 지원하며, bash 명령어도 별명(alias)으로 유사하게 지원.
  - 자체 help가 상세하고 편리하게 되어 있음.
- 다른 쉘과 차이점:
  - 독자적인 명령 체계(cmdlet)가 있어, 명령어 이름이 기본적으로 완전 다르다.

---

## 명령어 체계
- **Cmdlet** 이라는 체계를 사용.
- 명령어가 **'동사-명사'** 형태.
  - ```Get-Process```
  - ```Get-Service```
  - ```Clear-Item```
- 명령어에 별명(alias) 기능 지원
  - ```alias``` 명령으로 모든 별명 목록 출력.
  - ```cd``` -> ```Set-Location```
  - ```cp``` -> ```Copy-Item```

---

## 스크립트 문법
### 변수
- ```$a = 1234``` : 변수 선언 및 초기화. 자료형이 없음.
- ```[int]$b = 9225``` : 변수가 int형만 담을 수 있음 (```$b = 12.34``` 시 ```12``` 저장됨)
- ```$c = "this is string"```

### 연산자
- 비교 연산자: ```-eq``` ```-ne``` ```-gt``` ```-match``` ```-like``` ```-contains``` 등등
- 논리 연산자: ```-and``` ```-or``` ```-xor``` ```!```

### 조건문
- ```if(조건) { } elseif(조건) { } else { }```
- Switch (아래 기본형 말고도 정규표현식, 와일드카드, 조건문, 배열 문법도 존재)
```powershell
switch(변수) {
    1 { }
    2 { }
    'first' { }
    'second' { }
    default { }
}
```

### 반복문
- ```while(조건) { }```
- ```for($i=0; $i -lt 10; $i++) { }```
- ```foreach($one in $many) { $one }```

---

## 파이프라인 문법
### 대표적 명령어 및 예제
- **ForEach-Object** : 여러 개체에 대해 작업 반복.
  - ```$_``` : 단일 개체 접근.
  - ```$_.속성``` : 개체 속성 접근.
  - ```ForEach-Object {  }``` : 기본형 문법.
  - ```ForEach-Object -Begin { } -Process { } -End { }``` : 3부분으로 스크립트 분할 가능.
  - ```%``` : alias.
  - 예제:
    - ```Get-Process | ForEach-Object { $_.ProcessName }```
    - ```Get-CimInstance -Class Win32_LogicalDisk | ForEach-Object { $_.FreeSpace/1GB }```
    - ```Get-Process | % { $_.ProcessName }```

- **Sort-Object** : 결과 정렬.
  - ```-Property [속성1], [속성2], ...``` : 정렬 기준 설정.
  - ```-Descending``` : 내림차순 정렬. (기본: 오름차순)
  - 예제:
    - ```Get-Process | Sort-Object -Property CPU -Descending```
    - ```Get-Service | Sort-Object -Property status,name```

- **Where-Object** : 원하는 결과만 얻을 수 있는 필터.
  - ```Where-Object { 조건 }```
  - ```?``` : alias.
  - 예제:
    - ```Get-Process | Where-Object { $_.Name -eq "svchost" }```
    - ```Get-Process | Where-Object { $_.Handles -gt 1000 }```
    - ```Get-Service | Where-Object { $_.Status -eq "Running" }```
    - ```Get-Service | ? { $_.Status -eq "Running" }```

- **Format-List**, **Format-Table**, **Format-Wide** : 출력 보기 변경.
  - ```Format-List [속성1], [속성2], ...``` : 여러 속성을 리스트 형태로 표현.
    - 예제: ```Get-Service | Format-List Name,DisplayName,CanStop```
  - ```Format-Table [속성1], [속성2], ...``` : 여러 속성을 테이플 형태로 표현.
    - 예제: ```Get-Service | Format-Table Name,DisplayName,CanStop```
  - ```Format-Wide [속성] -Column 3``` : 하나의 속성을 여러 컬럼 표 형태로 표현.
    - 예제: ```Get-Service | Format-Wide DisplayName -Column 5```

- **Get-Member**
- **Select-Object**
- **Out-File**
- **ConvertTo-html**

---

## 간단 명령어
- **Start-Sleep** [초]
  - ```-Milliseconds```
- **Write-Host** [메시지]

---

## 고급 명령어
### Add-Type
- Microsoft .NET Core 클래스를 파워쉘 세션에 추가.
- 예제:
  - ```Add-Type -AssemblyName Microsoft.VisualBasic```
  - ```Add-Type -AssemblyName System.Windows.Forms```
- 클래스 추가 후 사용법
  - ```[클래스명]::함수명(인자)```
  - 예제:
    - ```[Microsoft.VisualBasic.Interaction]::AppActivate("Windows Security")```
    - ```[System.Windows.Forms.SendKeys]::SendWait("{ENTER}")```

### Get-WmiObject
- WMI(Windows Management Instrumentation)
- WMI 객체 목록 출력 : ```Get-WmiObject -List```
- 주요 객체
  - **Win32_PNPEntity** : Plug & Play 디바이스 목록.
