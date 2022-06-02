<h1 align="center"> The API Documentation</h1>

### Table of Contents

- <a href="#APIs" name="id1">APIs</a>
  - <a href="#LMS" name="id1_1">LMS API</a>
    - <a href="#LMS_Login" name="id1_1_1">class biblebot.LmsAPI.Login</a>
    - <a href="#LMS_Profile" name="id1_1_2">class biblebot.LmsAPI.Profile</a>
    - <a href="#LMS_CourseList" name="id1_1_3">class biblebot.LmsAPI.CourseList</a>
    - <a href="#LMS_Attendance" name="id1_1_4">class biblebot.LmsAPI.Attendance</a>
  - <a href="#Intranet" name="id1_2">Intranet API</a>
    - <a href="#Intranet_Login" name="id1_2_1">class biblebot.IntranetAPI.Login</a>
    - <a href="#Intranet_StudentPhoto" name="id1_2_2">class biblebot.IntranetAPI.StudentPhoto</a>
    - <a href="#Intranet_Chapel" name="id1_2_3">class biblebot.IntranetAPI.Chapel</a>
    - <a href="#Intranet_Timetable" name="id1_2_4">class biblebot.IntranetAPI.Timetable</a>
    - <a href="#Intranet_Course" name="id1_2_5">class biblebot.IntranetAPI.Course</a>
    - <a href="#Intranet_GraduationExam" name="id1_2_6">class biblebot.IntranetAPI.GraduationExam</a>
    - <a href="#Intranet_TotalAcceptanceStatus" name="id1_2_7">class biblebot.IntranetAPI.TotalAcceptanceStatus</a>
    - <a href="#Intranet_Profile" name="id1_2_8">class biblebot.IntranetAPI.Profile</a>
  - <a href="#KBU" name="id1_3">KBU API</a>
    - <a href="#KBU_MainNotice" name="id1_3_1">class biblebot.KbuAPI.MainNotice</a>
    - <a href="#KBU_ScholarshipNotice" name="id1_3_2">class biblebot.KbuAPI.ScholarshipNotice</a>
    - <a href="#KBU_IllipNotice" name="id1_3_3">class biblebot.KbuAPI.IllipNotice</a>
  - <a href="#Mileage" name="id1_4">Mileage API</a>
    - <a href="#Mileage_Login" name="id1_4_1">class biblebot.MileageAPI.Login</a>
    - <a href="#Mileage_Search" name="id1_4_2">class biblebot.MileageAPI.Search</a>
    - <a href="#Mileage_Statement" name="id1_4_3">class biblebot.MileageAPI.Statement</a>
  - <a href="#Library" name="id1_5">Library API</a>
    - <a href="#Library_Login" name="id1_5_1">class biblebot.LibraryAPI.Login</a>
    - <a href="#Library_CheckoutList" name="id1_5_2">class biblebot.LibraryAPI.CheckoutList</a>
    - <a href="#Library_BookDetail" name="id1_5_3">class biblebot.LibraryAPI.BookDetail</a>
    - <a href="#Library_BookPhoto" name="id1_5_4">class biblebot.LibraryAPI.BookPhoto</a>
- <a href="#Exceptions" name="id2">Exceptions</a>




<h2 align="center"><a href="#id1" name="APIs">APIs</a></h2>

### <a href="#id1_1" name="LMS">LMS API</a>

> LMS는 한국성서대학교의 강의관리시스템입니다. LMS 정보를 가져오고 싶다면 LMS API를 이용하세요. Intranet API 와 함께 사용하면 더욱 많은 정보를 결합시킬 수 있습니다.



#### <a href="#id1_1_1" name="LMS_Login">class biblebot.LmsAPI.Login</a>

> LMS 시스템 로그인을 위한 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    user_id: str,
    user_pw: str,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
  
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description  |
| --------- | ------------ |
| user_id   | LMS 아이디   |
| user_pw   | LMS 패스워드 |



**Example:**

```python
import asyncio

from biblebot import LmsAPI


async def main():
    response = await LmsAPI.Login.fetch("아이디", "패스워드")
    result = LmsAPI.Login.parse(response)
    print(result)

asyncio.run(main())
```

**Output:**

```python
# 정상적인 아이디/패스워드
ResourceData(data={'cookies': {'MoodleSession': 't13apafme5j2skfqr7apa9qp4c'}, 'iat': 1597653825}, link='https://lms.bible.ac.kr/login/index.php', meta={})

# 비정상적인 아이디 또는 패스워드
ErrorData(error={'title': '아이디 또는 패스워드가 잘못 입력되었습니다.', 'code': '3'}, link='https://lms.bible.ac.kr/login/index.php', meta={})
```



#### <a href="#id1_1_2" name="LMS_Profile">class biblebot.LmsAPI.Profile</a>

> LMS 에서 사용자 프로필(학번, 이름, 학과)을 가져오는 클래스

모든 프로필 정보를 가져오려면 `parse` 클래스 메서드를 사용하고, 부분적으로 필요할 경우, `parse_sid`, `parse_name`, `parse_major` 클래스 메서드 중 하나를 선택하여 사용하세요.

**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse_sid(cls, response: Response) -> APIResponseType:
    ...
    
@classmethod
def parse_name(cls, response: Response) -> APIResponseType:
    ...
    
@classmethod
def parse_major(cls, response: Response) -> APIResponseType:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description        |
| :-------- | ------------------ |
| cookies   | 로그인시 얻은 쿠키 |



#### <a href="#id1_1_3" name="LMS_CourseList">class biblebot.LmsAPI.CourseList</a>

> LMS 에서 해당 학기의 강의 목록과 강의 코드를 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    semester: Optional[str] = None,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description                                                 |
| :-------- | ----------------------------------------------------------- |
| cookies   | 로그인시 얻은 쿠키                                          |
| semester  | 학기<br/>2020학년도 1학기라면 `20201` 의 포맷으로 작성한다. |



**Example:**

```python
async def main():
    # Login
    resp = await LmsAPI.Login.fetch("아이디입력", "패스워드입력")
    result = LmsAPI.Login.parse(resp)
    cookie = result.data["cookies"]

    # Get codes of course
    resp = await LmsAPI.CourseList.fetch(cookies=cookie, semester="20201")
    result = LmsAPI.CourseList.parse(resp)
    print(result)
```

**Output:**

```text
ResourceData(
  data={
    'courses': {
      '경건훈련': '1094', 
      '전도훈련Ⅶ': '1554', 
      '엑셀스프레드시트': '1133', 
      '고급소프트웨어프로젝트': '1165', 
      '미래설계상담Ⅶ': '1178', 
      '빅데이터기술': '1183', 
      '종합설계I': '1184', 
      '창의적통합설계': '1186'
    }
  }, 
  link='https://lms.bible.ac.kr/local/ubion/user/index.php?lang=ko&year=2020&semester=10', 
  meta={
    'selected': '20201', 
    'selectable': ['20191', '20193', '20192', '20194', '20201', '20203', '20202', '20204']
  }
)
```



#### <a href="#id1_1_4" name="LMS_Attendance">class biblebot.LmsAPI.Attendance</a>

> LMS 에서 강의 출석정보를 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    course_code: str,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter   | Description                                         |
| :---------- | --------------------------------------------------- |
| cookies     | 로그인시 얻은 쿠키                                  |
| course_code | `biblebot.LmsAPI.CourseList` 를 통해 얻은 강의 코드 |



**Example:**

```python
import asyncio

from biblebot import LmsAPI


async def main():
    # Login
    resp = await LmsAPI.Login.fetch("아이디입력", "패스워드입력")
    result = LmsAPI.Login.parse(resp)
    cookie = result.data["cookies"]

    # Get Attendance
    resp = await LmsAPI.Attendance.fetch(cookies=cookie, course_code="1183")
    result = LmsAPI.Attendance.parse(resp)
    print(result)


asyncio.run(main())
```

**Output:**

```python
ResourceData(
  data={
    'summary': {
      '강좌번호': 'IC140', 
      '분반번호': 'A', 
      '강좌명': '빅데이터기술[A]', 
      '이름': '한국인 (201504000)'
    }, 
    'head': ['출결 날짜', '시간', '출석', '결석', '지각', '기타'], 
    'body': [
      ['2020-03-09', '13:30', '○', '', '', ''], 
      ['2020-03-12', '13:30', '○', '', '', ''], 
      ['2020-03-16', '13:30', '○', '', '', ''], 
      ['2020-03-19', '13:30', '○', '', '', ''], 
      ...
      ['2020-06-18', '13:30', '○', '', '', '']
    ], 
    'foot': {'출석': '30', '결석': '0', '지각': '0', '기타': '0'}
  }, 
  link='https://lms.bible.ac.kr/local/ubattendance/my_status.php?lang=ko&id=1183', 
  meta={}
)

```


### <a href="#id1_2" name="Intranet">Intranet API</a>

> 인트라넷은 한국성서대학교 학생정보를 관리하는 시스템입니다. 인트라넷 정보를 가져오고 싶다면 Intranet API를 이용하세요.



#### <a href="#id1_2_1" name="Intranet_Login">class biblebot.IntranetAPI.Login</a>

> 인트라넷 로그인을 위한 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    user_id: str,
    user_pw: str,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
  
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description       |
| --------- | ----------------- |
| user_id   | 인트라넷 아이디   |
| user_pw   | 인트라넷 패스워드 |



**Example:**

```python
import asyncio

from biblebot import IntranetAPI


async def main():
    response = await IntranetAPI.Login.fetch("아이디", "패스워드")
    result = IntranetAPI.Login.parse(response)
    print(result)

asyncio.run(main())
```

**Output:**

```python
# 정상적인 아이디/패스워드
ResourceData(data={'cookies': {'ASP.NET_SessionId': 'g2ujwz45iyceaj45fcx33145'}, 'iat': 1597650392}, link='https://kbuis.bible.ac.kr/ble_login2.aspx', meta={})

# 비정상적인 아이디 또는 패스워드
ErrorData(error={'title': '존재하지 않는 회원ID 입니다.', 'alert_messages': ['존재하지 않는 회원ID 입니다.']}, link='https://kbuis.bible.ac.kr/ble_login2.aspx', meta={})
```



#### <a href="#id1_2_2" name="Intranet_StudentPhoto">class biblebot.IntranetAPI.StudentPhoto</a>

> 학생증 사진을 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    sid: str,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...

@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description        |
| --------- | ------------------ |
| cookies   | 로그인시 얻은 쿠키 |
| sid       | 학번               |



#### <a href="#id1_2_3" name="Intranet_Chapel">class biblebot.IntranetAPI.Chapel</a>

> 채플 정보를 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    semester: Optional[str] = None,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description                                                |
| --------- | ---------------------------------------------------------- |
| cookies   | 로그인시 얻은 쿠키                                         |
| semester  | 학기<br>2020학년도 1학기라면 `20201` 의 포맷으로 작성한다. |



**Example:**

```python
import asyncio

from biblebot import IntranetAPI


async def main():
    # Login
    resp = await IntranetAPI.Login.fetch("아이디", "패스워드")
    result = IntranetAPI.Login.parse(resp)
    cookie = result.data["cookies"]

    # Get chapel
    resp = await IntranetAPI.Chapel.fetch(cookies=cookie)
    result = IntranetAPI.Chapel.parse(resp)
    print(result)

asyncio.run(main())
```

**Output:**

```text
ResourceData(
  data={
    'summary': {
        '주중수업일수': '4', 
        '규정일수': '51',
        '출석': '55', 
        '지각': '1', 
        '확정': '56'
    }, 
    'head': ['연도', '월', '일', '시분초', '요일', '주야참석', '출석여부', '교목실인정', '비고사유'], 
    'body': [
      ['2020', '06', '08', '11:59:00', '월', '주', '출석', '출석', '(2020-06-10)'], 
      ['2020', '06', '04', '11:59:00', '목', '주', '출석', '출석', '(2020-06-08)'], 
      ...
    ]
  }, 
  link='https://kbuis.bible.ac.kr/StudentMng/SM050.aspx', 
  meta={
      'selected': '20201', 
      'selectable': ['20201', '20192', '20191', '20182', '20181', '20162', '20152', '20151']
  }
)
```



#### <a href="#id1_2_4" name="Intranet_Timetable">class biblebot.IntranetAPI.Timetable</a>

> 수강신청한 내역을 바탕으로 시간표를 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    semester: Optional[str] = None,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description                                                |
| --------- | ---------------------------------------------------------- |
| cookies   | 로그인시 얻은 쿠키                                         |
| semester  | 학기<br>2020학년도 1학기라면 `20201` 의 포맷으로 작성한다. |



#### <a href="#id1_2_5" name="Intranet_Course">class biblebot.IntranetAPI.Course</a>

> 수강신청한 강의들의 상세정보를 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    semester: Optional[str] = None,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description                                                |
| --------- | ---------------------------------------------------------- |
| cookies   | 로그인시 얻은 쿠키                                         |
| semester  | 학기<br>2020학년도 1학기라면 `20201` 의 포맷으로 작성한다. |



#### <a href="#id1_2_6" name="Intranet_GraduationExam">class biblebot.IntranetAPI.GraduationExam</a>

> 졸업시험 합격 여부 정보를 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description                                                |
| --------- | ---------------------------------------------------------- |
| cookies   | 로그인시 얻은 쿠키                                         |


**Example:**

```python
import asyncio

from biblebot.api import IntranetAPI


async def main():
    # Login
    response = await IntranetAPI.Login.fetch("아이디", "패스워드")
    result = IntranetAPI.Login.parse(response)
    cookie = result.data["cookies"]

    # Get TotalAcceptanceStatus
    resp = await IntranetAPI.GraduationExam.fetch(cookies=cookie)
    result = IntranetAPI.GraduationExam.parse(resp)
    print(result)
asyncio.run(main())
```

**Output:**

```text

ResourceData(
    data={
       "head":[
          "번호",
          "학년도 학기",
          "시헙종목",
          "신청기간",
          "신청"
       ],
       "body":[
          [
             "1",
             "2022 - 1",
             "영어",
             "2022-03-28 ~ 2022-04-07",
             "합격자 신청 불가"
          ],
          [
             "2",
             "2022 - 1",
             "성경",
             "2022-05-02 ~ 2022-05-10",
             ""
          ],
          [
             "3",
             "2022 - 1",
             "컴퓨터",
             "홈페이지 공지사항 참고",
             "합격자 신청 불가"
          ],
          [
             "4",
             "2022 - 1",
             "컴퓨터2",
             "홈페이지 공지사항 참고",
             ""
          ]
       ]
    },
    "link=""https://kbuis.bible.ac.kr/SchoolRegMng/SR050.aspx",
    "meta="{}
)
```


#### <a href="#id1_2_7" name="Intranet_TotalAcceptanceStatus">class biblebot.IntranetAPI.TotalAcceptanceStatus</a>

> 전체 이수현황 정보를 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description                                                |
| --------- | ---------------------------------------------------------- |
| cookies   | 로그인시 얻은 쿠키                                         |


**Example:**

```python
import asyncio

from biblebot.api import IntranetAPI


async def main():
    # Login
    response = await IntranetAPI.Login.fetch("아이디", "패스워드")
    result = IntranetAPI.Login.parse(response)
    cookie = result.data["cookies"]

    # Get TotalAcceptanceStatus
    resp = await IntranetAPI.TotalAcceptanceStatus.fetch(cookies=cookie)
    result = IntranetAPI.TotalAcceptanceStatus.parse(resp)
    print(result)
asyncio.run(main())
```

**Output:**

```text
ResourceData(
   data={       
       "summary":{
          "신청학점":"115",
          "이수학점":"115",
          "평점평균":"3.29",
          "백분율":"87.76"
       },
       "head":[
          "이수과목",
          "학점",
          "등급",
          "학년도학기"
       ],
       "body":{
          "교양선택":[
             [
                "디지털사회의소통(GE669-A)",
                "3",
                "B+",
                "20172"
             ],
             ...
          ],
          "교양필수":[
             [
                "경건훈련(GE264-A)",
                "0",
                "F ",
                "20221"
             ],
             ...
          ],
          ...
       }
    },
    "link=""https://kbuis.bible.ac.kr/GradeMng/GD010.aspx?viewRef=0",
    "meta="{}
)
```        


#### <a href="#id1_2_8" name="Intranet_Profile">class biblebot.Intranet.Profile</a>

> Intranet 에서 사용자 프로필(학번, 이름, 학과)을 가져오는 클래스

모든 프로필 정보를 가져오려면 `parse` 클래스 메서드를 사용하고, 부분적으로 필요할 경우, `parse_sid`, `parse_name`, `parse_major` 클래스 메서드 중 하나를 선택하여 사용하세요.

**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse_sid(cls, response: Response) -> APIResponseType:
    ...
    
@classmethod
def parse_name(cls, response: Response) -> APIResponseType:
    ...
    
@classmethod
def parse_major(cls, response: Response) -> APIResponseType:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description        |
| :-------- | ------------------ |
| cookies   | 로그인시 얻은 쿠키 |


**Example:**

```python
import asyncio

from biblebot.api import IntranetAPI


async def main():
    # Login
    response = await IntranetAPI.Login.fetch("아이디", "비밀번호")
    result = IntranetAPI.Login.parse(response)
    cookie = result.data["cookies"]

    # Get Profile
    resp = await IntranetAPI.Profile.fetch(cookies=cookie)
    result = IntranetAPI.Profile.parse(resp)
    print(result)
    
asyncio.run(main())
```

**Output:**

```text
ResourceData(data={'sid': '201704036', 'name': '신범철', 'major': '컴퓨터소프트웨어학과'}, link='https://kbuis.bible.ac.kr/SchoolRegMng/SR030.aspx', meta={})
```



### <a href="#id1_3" name="KBU">KBU API</a>

> 한국성서대학교의 공식사이트 정보를 가져오는 API입니다. 현재는 공지사항 API만 제공하고 있습니다. 모든 공지사항 API는 `NoticeList` 의 서브클래스이고, 노출된 메서드 signature가 동일합니다.



#### <a href="#id1_3_1" name="KBU_MainNotice">class biblebot.KbuAPI.MainNotice</a>

> 학사/취창업 공지사항을 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    page: Union[int, str] = 1,
    search_keyword: Optional[str] = None,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter      | Description            |
| :------------- | ---------------------- |
| page           | 페이지 번호            |
| search_keyword | 검색어 (없다면 `None`) |



#### <a href="#id1_3_2" name="KBU_ScholarshipNotice">class biblebot.KbuAPI.ScholarshipNotice</a>

> 장학/등록금 공지사항을 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    page: Union[int, str] = 1,
    search_keyword: Optional[str] = None,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter      | Description            |
| :------------- | ---------------------- |
| page           | 페이지 번호            |
| search_keyword | 검색어 (없다면 `None`) |



#### <a href="#id1_3_3" name="KBU_IllipNotice">class biblebot.KbuAPI.IllipNotice</a>

> 신앙/채플/봉사 공지사항을 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    page: Union[int, str] = 1,
    search_keyword: Optional[str] = None,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter      | Description            |
| :------------- | ---------------------- |
| page           | 페이지 번호            |
| search_keyword | 검색어 (없다면 `None`) |



### <a href="#id1_4" name="Mileage">MileageAPI</a>

> 한국성서대학교의 마일리지를 위탁 관리하는 OKPOS 의 정보를 가져오는 API 입니다. 다른 API는 한국성서대학교 학생 누구나 사용할 수 있지만, 마일리지 API는 학교에서 부여받은 관리자 계정이 있어야만 이용할 수 있습니다.



#### <a href="#id1_4_1" name="Mileage_Login">class biblebot.MileageAPI.Login</a>

> Mileage 시스템(OKPOS) 로그인을 위한 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    user_id: str,
    user_pw: str,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
  
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description    |
| --------- | -------------- |
| user_id   | OKPOS 아이디   |
| user_pw   | OKPOS 패스워드 |



#### <a href="#id1_4_2" name="Mileage_Search">class biblebot.MileageAPI.Search</a>

> OKPOS 에서 사용자 검색을 위한 클래스



**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    search_param: Optional[SearchParamData] = None,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter    | Description                                                  |
| :----------- | ------------------------------------------------------------ |
| cookies      | 로그인시 얻은 쿠키                                           |
| search_param | 검색 파라미터 (`biblebot.MileageParam.SearchParamData` 이용) |



#### <a href="#id1_4_3" name="Mileage_Statement">class biblebot.MileageAPI.Statement</a>

> 사용자의 마일리지 변동 내역 또는 상품 구매 내역을 가져오는 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    search_param: Optional[StatementParamData] = None,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter    | Description                                                  |
| :----------- | ------------------------------------------------------------ |
| cookies      | 로그인시 얻은 쿠키                                           |
| search_param | 검색 파라미터 (`biblebot.MileageParam.StatementParamData` 이용) |



### <a href="#id1_5" name="Library">LibraryAPI</a>

> 한국성서대학교 도서관의 대출 목록을 가져오는 API입니다. 



#### <a href="#id1_5_1" name="Library_Login">class biblebot.LibraryAPI.Login</a>

> 도서관홈페이지 로그인을 위한 클래스

**Method:**

```python
@classmethod
async def fetch(
    cls,
    user_id: str,
    user_pw: str,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
  
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter | Description    |
| --------- | -------------- |
| user_id   | 도서관홈페이지 아이디   |
| user_pw   | 도서관홈페이지 패스워드 |



**Example:**

```python
import asyncio

from biblebot import LibraryAPI


async def main():
    response = await LibraryAPI.Login.fetch("아이디", "비밀번호")
    result = LibraryAPI.Login.parse(response)
    print(result)

asyncio.run(main())
```

**Output:**

```text
# 정상적인 아이디/패스워드
ResourceData(data={'cookies': {'ASP.NET_SessionId': 'w2ijlsks20scje20tnkbkcev'}, 'iat': 1610438537}, link='https://lib.bible.ac.kr/Account/LogOn', meta={})

# 비정상적인 아이디 또는 패스워드
ErrorData(error={'title': '제공한 사용자 이름 또는 암호가 잘못되었습니다.'}, link='https://lib.bible.ac.kr/Account/LogOn', meta={})
```



#### <a href="#id1_5_2" name="Library_CheckoutList">class biblebot.LibraryAPI.CheckoutList</a>

> 대출 목록을 가져오는 클래스



**Method:**

```python
@classmethod
async def fetch(
    cls,
    cookies: Dict[str, str],
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter    | Description                                                  |
| :----------- | ------------------------------------------------------------ |
| cookies      | 로그인시 얻은 쿠키                                           |



**Example:**

```python
import asyncio

from biblebot import LibraryAPI


async def main():
    # Login
    response = await LibraryAPI.Login.fetch("아이디", "비밀번호")
    result = LibraryAPI.Login.parse(response)
    cookie = result.data["cookies"]

    # Get CheckoutList
    response = await LibraryAPI.CheckoutList.fetch(cookies=cookie)
    result = LibraryAPI.CheckoutList.parse(response)
    print(result)

asyncio.run(main())
```

**Output:**

```text
# 대출 내역이 있는 경우
ResourceData(
   data={
       "head":[
          "No",
          "서지정보",
          "대출일자",
          "반납예정일",
          "대출상태",
          "연기신청",
          "상세페이지 URL"
       ],
       "body":[
          [
             "1",
             "여자 20대, 10년 후 명함을 준비하라",
             "2021-01-11",
             "2021-01-20",
             "대출중",
             "연장",
             "/Search/Detail/83029"
          ],
          [
             "2",
             "계속 모드 : 목표달성이 쉬워지는 계속하는 기술",
             "2021-01-11",
             "2021-01-20",
             "대출중",
             "연장",
             "/Search/Detail/83826"
          ]
       ]
    },
   link="https://lib.bible.ac.kr/MyLibrary",
   meta={}
)

# 대출 내역이 없는 경우
ErrorData(error={'title': '대출한 내역이 없습니다.'}, link='https://lib.bible.ac.kr/MyLibrary', meta={})
```



#### <a href="#id1_5_3" name="Library_BookDetail">class biblebot.LibraryAPI.BookDetail</a>

> 대출된 도서의 상세 정보를 가져오는 클래스



**Method:**

```python
@classmethod
async def fetch(
    cls,
    path: str,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> List[str]:
    ...
```

| Parameter    | Description                                                  |
| :----------- | ------------------------------------------------------------ |
| path      | 대출된 도서의 상세페이지로 가는 경로                                           |



**Example:**

```python
import asyncio

from biblebot import LibraryAPI


async def main():
    # Login
    response = await LibraryAPI.Login.fetch("아이디", "비밀번호")
    result = LibraryAPI.Login.parse(response)
    cookie = result.data["cookies"]

    # Get CheckoutList
    response = await LibraryAPI.CheckoutList.fetch(cookies=cookie)
    result = LibraryAPI.CheckoutList.parse(response)

    # Get BookDetail
    for book in result.data["body"]:
        response = await LibraryAPI.BookDetail.fetch(path=book[-1])
        print(LibraryAPI.BookDetail.parse(response))

asyncio.run(main())
```

**Output:**

```text
# 도서 상세 정보(ISBN넘버, 이미지 URL) 결과
['9788990987418', None]

# 이미지가 없는 경우
['9788992555814', 'https://bookthumb-phinf.pstatic.net/cover/045/792/04579220.jpg?type=m1&udate=20130713']
```



#### <a href="#id1_5_4" name="Library_BookPhoto">class biblebot.LibraryAPI.BookPhoto</a>

> 대출된 도서의 이미지를 가져오는 클래스



**Method:**

```python
@classmethod
async def fetch(
    cls,
    photo_url: str,
    *,
    headers: Optional[Dict[str, str]] = None,
    timeout: Optional[float] = None,
    **kwargs,
) -> Response:
    ...
    
@classmethod
def parse(cls, response: Response) -> APIResponseType:
    ...
```

| Parameter    | Description                                                  |
| :----------- | ------------------------------------------------------------ |
| photo_url      | 대출된 도서의 이미지를 가져오는 URL                                           |



**Example:**

```python
from typing import Dict, Union
from base64 import b64encode
from io import BytesIO
import asyncio

from PIL import Image

import biblebot
from biblebot import LibraryAPI


def get_image_info(raw_img: bytes) -> Dict[str, Union[int, str]]:
    img = Image.open(BytesIO(raw_img))
    width, height = img.size
    fmt = img.format
    return {
        "width": width,
        "height": height,
        "format": fmt,
        "img": b64encode(raw_img).decode(),
    }


async def main():
    """
    CheckoutList를 통해
    ['No', '서지정보', '대출일자', '반납예정일', '대출상태', '연기신청', '상세페이지 URL']의 데이터를 갖는다.

    상세 정보가 필요하면
    CheckoutList → BookDetail → BookPhoto를 거쳐야하는데,
    CheckoutList 결과 데이터에 변화가 이루어진다.

    최종적으로
    ['ISBN', '서지정보', '대출일자', '반납예정일', '대출상태', '연기신청', '도서이미지']의 데이터가 완성된다.
    """
    # Login
    response = await LibraryAPI.Login.fetch("아이디", "비밀번호")
    result = LibraryAPI.Login.parse(response)
    cookie = result.data["cookies"]

    # Get CheckoutList
    response = await LibraryAPI.CheckoutList.fetch(cookies=cookie)
    result = LibraryAPI.CheckoutList.parse(response)

    # Get BookDetail
    result.data["head"][0] = "ISBN"
    result.data["head"][-1] = "도서이미지"
    for book in result.data["body"]:
        response = await LibraryAPI.BookDetail.fetch(path=book[-1])
        isbn, photo_url = LibraryAPI.BookDetail.parse(response)
        # Put ISBN at book[0]
        book[0] = isbn
        # Get BookPhoto at book[-1]
        if photo_url:
            response = await LibraryAPI.BookPhoto.fetch(photo_url=photo_url)
            photo_result = LibraryAPI.BookPhoto.parse(response)
            book[-1] = (
                get_image_info(photo_result.data["raw_image"])
                if isinstance(photo_result, biblebot.ResourceData)
                else None
            )
        else:
            book[-1] = None
    print(result)

asyncio.run(main())
```

**Output:**

```text
ResourceData(
    data={
       "head":[
          "ISBN",
          "서지정보",
          "대출일자",
          "반납예정일",
          "대출상태",
          "연기신청",
          "도서이미지"
       ],
       "body":[
          [
             "9788990987418",
             "여자 20대, 10년 후 명함을 준비하라",
             "2021-01-11",
             "2021-01-20",
             "대출중",
             "연장",
             "None"
          ],
          [
             "9788992555814",
             "계속 모드 : 목표달성이 쉬워지는 계속하는 기술",
             "2021-01-11",
             "2021-01-20",
             "대출중",
             "연장",
             {
                "width":82,
                "height":117,
                "format":"JPEG",
                "img":"/9j/4AAQSkZJRgABAQAAAQABAAD/..."
             }
          ]
       ]
    },
    link="https://lib.bible.ac.kr/MyLibrary",
    meta={}
)
```



<h2 align="center"><a href="#id2" name="Exceptions">Exceptions</a></h2>

biblebot은 exception을 계층적으로 관리하고 있습니다. 모든 예외는 `RootError`의 서브 클래스로 관리됩니다.

**Exception hierarchy chart:**

```python
Exception
   RootError
      RequestError
         RequestTimeoutError
         StatusError
            ClientError
               * 4xx - HTTPError
            ServerError
               * 5xx - HTTPError
      ResponseError
         ParsingError
```

| Exceptions                                | Description                                                  |
| ----------------------------------------- | ------------------------------------------------------------ |
| biblebot.RootError(message)               | biblebot 예외들의 베이스 클래스                              |
| biblebot.RequestError(message)            | 스크래이핑을 위해 HTTP 요청을 보낼 때 발생하는 에러들의 최상위 예외 |
| biblebot.RequestTimeoutError(message)     | HTTP 요청시 타임아웃 발생                                    |
| biblebot.StatusError(message)             | HTTP 요청에 대한 응답이 성공적이지 못할 때 발생하는 에러들의 최상위 예외 |
| biblebot.ClientError(message)             | HTTP 요청에 대한 응답이 4xx 일 때 발생                       |
| biblebot.ServerError(message)             | HTTP 요청에 대한 응답이 5xx 일 때 발생                       |
| biblebot.ResponseError(message, response) | HTTP 요청을 성공했으나, 정상적으로 구문 분석을 할 수 없을 때 발생하는 에러들의 최상위 예외 |
| biblebot.ParsingError(message, response)  | 응답 본문을 정상적으로 파싱할 수 없을 때 발생                |

