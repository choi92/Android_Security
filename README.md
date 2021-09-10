# 안드로이드 보안 개선 프로그램
이 프로젝트는 2020 서운고 보안탐구부의 활동 중 안드로이드의 보안을 개선하는 프로그램 제작 프로젝트입니다.

## 개요
안드로이드의 build.prop 중 ro.modversion 주석 처리하면 커스텀롬이 감지되지 않은 보안 상의 취약점을 개선하여 커스텀롬을 감지하는 프로그램입니다.

## 소스 코드
https://github.com/choi92/Android_Security/blob/master/ro.modversion%20detect.java

## 구동 모습
![image](https://user-images.githubusercontent.com/65582244/132807566-ca3e26e6-f33b-4985-a428-f5678816720c.png) <br>
![image](https://user-images.githubusercontent.com/65582244/132807577-7e2dcb7c-2841-42d7-b4b4-e81c1fbbe9f0.png) <br>
![image](https://user-images.githubusercontent.com/65582244/132807583-eec86cfc-b865-46e6-9d79-7a9fbdbee3fd.png)

## 안드로이드에 적용
https://github.com/choi92/Android_Security/blob/master/ReadModVersion.jar <br>
unity를 이용

___

## 기본 용어 이해 및 법적 근거 탐색
### 기본 용어
루팅 : 루트 권한이 원래 허가되지 않은 기기나 OS에서 루트 권한을 취득하는 것 <br>
커스텀롬 : 전자기기에 사용되는 펌웨어(통칭 순정)를 대체하는, 자작 혹은 편집된 펌웨어 <br>
해킹 : 타인의 컴퓨터 시스템에 무단 침입해 데이터에 접속할 수 있는 권한을 얻는 것이다. <br>

### 법적 근거
안드로이드 OS 및 기반이 되는 리눅스는 대표적인 오픈소스 OS 이며, 제조사별로 커널 및 부트로더 등 중요 영역에 대한 소스를 공개하고 있는 상태입니다. 루팅 및 커스텀 펌웨어는 공개되어있는 오픈소스에 대해서 변형을 진행하는 것이기 때문에 저작권법 의 기술적 보호조치 대상에 포함되지 않습니다. <br>
한국 내에서는 법적 판례가 없지만, 2010년 루팅과 탈옥 자체에 대해서 미국 내 저작권법을 관장하는 북미 저작권청에서는 합법으로 인정한 바 있습니다. <br>

### 인강 수강 어플리케이션 이용약관 (이투스 이용약관 중)
제 18조 불법사용 규제 관련 <br>
1. (1) 회사는 다음 각 호에 해당하는 경우 회원에게 경고 등 주의 조치를 취할 수 있으며, 필요한 경우 이용계약을 해지하거나 서비스 이용을 중지시키는 등 서비스 이용에 제한을 가할 수 있습니다.1. 동일한 ID로 2대 이상의 PC에서 동시접속이 발생하는 경우2. 동일한 ID로 다수의 PC 또는 IP에서 서비스를 이용하는 경우3. 자신의 ID 및 강좌 등의 서비스를 타인이 이용하도록 하는 경우4. 자신의 ID 및 강좌 등의 서비스를 타인에게 판매, 대여, 양도하는 행위 및 이를 광고 하는 행위5. 서비스 이용 중, 복제프로그램을 실행하는 경우 또는 녹화를 하거나 시도하는 경우 <br>
5. (5) 부정이용 식별방법 및 차단1. 회사는 회원의 서비스 이용중에 수집ㆍ확인된 맥어드레스, 디바이스 정보 및 IP정보 등의 자료를 토대로, 서버를 통하여 부정이용 여부를 분류ㆍ확인합니다.2. 회사는 이용자가 서비스 이용중에 복제프로그램을 실행시키거나 동일한 ID로 동시 접속을 하는 경우, 서비스 이용 접속을 강제로 종료 시킵니다. <br>

이용약관 어디에도 루팅과 커스텀 펌웨어 관련 내용은 있지 않다. <br>
또한 고객센터 문의 결과 이투스 수강앱은 구글사의 권장 API를 토대로 제작되는 부분으로 커스텀롬, 해외향 저사양 기기에서의 안정적인 이용을 권장해드리기 어려운 부분이므로 이용 시 많은 문제를 수반할 수 있는 부분이 있어 가급적 이용을 지양할 것을 당부 할 뿐 이용에는 문제가 없다고 하였다. <br>

**따라서 우리의 활동은 법적으로 아무런 문제가 있지 않음을 알 수 있다.** 

## 안드로이드 앱의 보안 알고리즘 종류의 이론적 탐구
안드로이드 앱은 사용자가 루트 권한을 획득하여 불법행위를 저지르지 않도록 기기의 루팅 여부를 확인하는 알고리즘을 가지고 있다.

### Su 바이너리 탐지
리눅스에서 root 권한으로 권한을 상승하는 경우 su 명령어를 사용하게 되는데, 보통 루팅을 하고나면 추후에 다시 루트 권한을 이용하기 위해 su 명령어(바이너리 파일)을 만들어 놓게 된다. 그래서 앱은 su라는 이름을 갖는 바이너리 파일을 검색한다.

### 프로세스 리스트 탐지
프로세스 리스트 탐지는 루팅과 관련된 알려진 프로세스가 현재 실행되고 있는지를 탐지하는 방법으로, 경우에 따라서는 루팅 탐지를 우회하기 위해 su 명령을 일부러 숨기거나 하는 프로세스가 동작할 수 있어 이러한 루팅 또는 루팅 탐지를 방해하는 프로세스가 존재하는지 검사하여 루팅 여부를 판단하는 방법이다. 

### build.prop을 통한 루팅과 커스텀 펌웨어 탐지
![image](https://user-images.githubusercontent.com/65582244/132808132-4b55d65d-4a18-4218-9d91-af827485b983.png) <br>
커스텀 펌웨어의 대다수는 루팅이 기본적으로 되어 있어 앱은 커스텀펌웨어 여부를 확인하기도 한다. 
기본적으로 안드로이드에서 /system/build.prop 파일의 ro.build.tag 옵션을 비롯한 몇몇 옵션들은 release-keys로 설정되어 있다. 루팅이 되는 경우 이 값이 test-keys로 되어 있으므로 이를 체크하는 방법이다. 이외에도 루팅의 경우 내부에 있는 옵션들이 기본값과는 다르게 되어 있는 경우가 있으므로 이 정보들을 수집하여 각 항목이 변경되는지 확인하는 방법을 통해 루팅탐지를 수행할 수 있다. 그러나 루팅 탐지를 우회하기 위해 해당 값들을 다시 release-keys로 수정될 수 있는 가능성도 존재한다.
또한 리니지OS나 CyanogenMod등의 커스텀 펌웨어는 build.prop에 ro.modversion이라는 코드를 가지고 있으므로 이 코드를 통해 커스텀 펌웨어 여부를 확인할 수 있다.

### 폴더 권한 확인
루팅 후에는 편의를 위해 쓰기 권한을 추가해서 remount 하고 write 권한을 주는 경우가 있다. 
/ <br>
/data <br>
/system <br>
/vendor/bin <br>
/sys <br>
/sbin <br>
/etc <br>
  ... <br>
이러한 디렉토리들의 쓰기 권한 검증을 수행할 수 있다.

## 안드로이드 태블릿 Nook HD+을 이용한 실제 보안 알고리즘 탐구
\* Nook HD+란? <br>
Barnes&Noble社가 2012년 11월 8일 미국에서 발매한 태블릿 컴퓨터 <br>
안드로이드 4.0.3 (Icecream Sandwich) 기반의 Barnes&Noble社의 커스텀 OS가 탑재됨 <br>
Barnes&Noble社가 2013년 6월 25일 공식발표를 통해 Nook 태블릿의 실패를 인정하고, 7월, 초기 발매가격인 $269/$299에서 $149/$179로 가격을 대폭 하락시켰다. 이로 인해 XDA등의 해외 포럼에서 주목하여 CyanogenMod 10.1, 10.2, 11 공식 지원제품이 되었다. <br>

### 실험 과정
1. OS업그레이드
안드로이드 4.0.3 (Icecream Sandwich)는 수 세대 전의 OS이지만 이투스 수강앱등 대부분의 안드로이드 앱은 현재 안정적인 이용을 위해 안드로이드 버전은 6.0 이상을 권장하고 있다. 따라서 
안드로이드 7.0 (Nougat) 기반의 커스텀 OS인 Lineage 14.0.0로 업그레이드를 시킨다.
- SDFormatter로 sd카드 포맷
- win32diskimager로 sd 카드에 부팅용 이미지(CWM 리커버리)인 emmc-cwm-early3.1.img를 write 하기
- 그 후 twrp, 롬파일, 구글 앱스를 sd카드에 복사
- sd카드를 nook에 넣고 리커버리 모드로 진입
- 포맷, 캐시 삭제 후 twrp, 롬파일, 구글앱스 순으로 설치
- 캐시 삭제후 sd카드 제거 후 재부팅

2. 루팅
다른 루팅 프레임워크와 다르게 system 파티션을 건드드리 지 않는 시스템 리스 방식의 모듈을 사용하여 루트 권한을 관리하는 루팅 프레임워크인 Magisk를 이용하여 루팅을 한다.

3. 보안 알고리즘 탐구
커스텀 펌웨어에서 루팅을 한 기기로 여러 앱을 실행시켜서 앱이 Su 바이너리 탐지와 커스텀 펌웨어 탐지를 통해 보안 알고리즘을 수행하는지 확인한다.

### 실험 결과
인강 수강 어플리케이션 | 메가스터디 | 이투스 | 대성마이맥 | 스카이에듀 | EBS 
---|:---:|:---:|:---:|---|---
Su 바이너리 탐지 | O | | O | | |
커스텀 펌웨어 탐지 | | O | | | |

게임 어플리케이션 | 카카오(쿠키런) | 포켓몬고 | 슈퍼셀(클래시로얄) | 넥슨(넥슨 플래이, 피온4) | 넷마블( 모두의 마블) | Su 바이너리 탐지
---|:---:|:---:|:---:|---|---
커스텀 펌웨어 탐지 | | | | | 

금융/공공 어플리케이션 | 카카오뱅크 | 국세청 홈텍스 | 토스 | 신한 쏠 뱅크 | KB스타뱅크
---|:---:|:---:|:---:|:---:|:---:
Su 바이너리 탐지 | O | O | O | O | O
커스텀 펌웨어 탐지 | | | | |






