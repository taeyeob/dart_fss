## 목차
1. DART에서 재무제표 크롤링을 위한 module 다운로드하기
2. DART에서 제공하는 API 다운로드 받기
3. DART 데이터 크롤링하기

## DART에서 재무제표 크롤링을 위한 module 다운로드하기
1. 명령 프롬프트를 실행합니다.
2. 아래의 순서대로 프롬프트에 입력하여 module 설치합니다.
- **pip install dart_fss**
- **pip install dart_fss_classifier**
- **pip install htm5lib --update**
- **pip install beautifulsoup4 --update**

## DART에서 제공하는 API 다운로드 받기
1. **https://opendart.fss.or.kr/uss/umt/EgovMberInsertView.do** 사이트에 접속하여 동의 절차를 마친 후 API key를 발급받습니다.
2. 해당 API key는 아래 코드의 6번째 줄의 '' 사이에 입력합니다.
3. 해당 API key는 한번에 너무 많은 양을 hosting하면 IP가 차단될 수 있으니 다량의 데이터를 크롤링할 순 없습니다.

## DART 데이터 크롤링하기
1. 위의 폴더에 **dart.py** 라는 파일을 VSCode를 통해 생성합니다.
2. 다음 코드를 복사, 붙여넣기 한다.
```Python
import dart_fss as dart
import dart_fss_classifier

assert dart_fss_classifier.attached_plugin() == True

api_key = '' #각자 발급받은 API key 입력
dart.set_api_key(api_key=api_key)

print('기업명 입력(ex: 삼성전자)')
crp_name = input().split()

print('시작날짜 입력(ex: 20120101)')
bgndate = input().split()

corp_list = dart.get_corp_list()

for i in range(len(crp_name)):
    fsdata = corp_list.find_by_corp_name(crp_name[i])[0]
    fs = fsdata.extract_fs(bgn_de=bgndate)
    fs.save()
```


##### 해당 사용설명서대로 진행되지 않을 경우, 주저하지 마시고 연락 주시길 바랍니다.