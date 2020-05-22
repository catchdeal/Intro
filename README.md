# 캐치야, 물어와! : 특가정보 모음집 '캐치딜'
<div align="center"><img src="/img/app-v4.png?raw=true" width="500px"></div>

## 팀원
#### 서현석, 김철민, 이인하

## 1. 프론트엔트/백엔드 언어 정보
#### 1) 프론트엔드
* react : 16.9.0
* react-native : 0.61.5

#### 2) 백엔드
* Ruby : 2.6.3
* Rails : 5.2.3
 

## 2. 해당 Repository와의 연결고리
* 앱 클라이언트 Repository : https://github.com/catchdeal/catchDeal-Client
* API 통신 / 소개 페이지 렌더링 / Database Server : https://github.com/catchdeal/CatchDeal-API
* 크롤링 (AWS Lamabda + Ruby on Jets) : https://github.com/catchdeal/CatchDeal-Lambda
* 크롤링 (라즈베리파이4B + Ruby on Rails) : https://github.com/catchdeal/CatchDeal-RaspberryPi


## 3. 캐치딜 개발 이야기
1. [(Intro) 싼 것만 물어드려요 : 캐치딜 서비스!]
2. [캐치딜 백엔드 개발이야기 : 좌충우돌 서버운영 이야기]
3. [캐치딜 백엔드 개발이야기 : 문서화]
4. [캐치딜 백엔드 개발이야기 : 디자이너와의 협업]
5. [캐치딜 백엔드 개발이야기 : 크롤링]
6. [캐치딜 백엔드 개발이야기 : Restful API 설계의 다양한 고민]
7. [캐치딜 백엔드 개발이야기 : 나에게 맞는 합리적인 서버 비용을 찾아서..]

[(Intro) 싼 것만 물어드려요 : 캐치딜 서비스!]: https://kbs4674.tistory.com/113
[캐치딜 백엔드 개발이야기 : 좌충우돌 서버운영 이야기]: https://kbs4674.tistory.com/114
[캐치딜 백엔드 개발이야기 : 문서화]: https://kbs4674.tistory.com/115
[캐치딜 백엔드 개발이야기 : 디자이너와의 협업]: https://kbs4674.tistory.com/116
[캐치딜 백엔드 개발이야기 : 크롤링]: https://kbs4674.tistory.com/117
[캐치딜 백엔드 개발이야기 : Restful API 설계의 다양한 고민]: https://kbs4674.tistory.com/118
[캐치딜 백엔드 개발이야기 : 나에게 맞는 합리적인 서버 비용을 찾아서..]: https://kbs4674.tistory.com/125


## 4. 캐치딜 : 전체적인 프로젝트 개요
1. 커뮤니티에는 매일 갖가지 할인행사에 대한 정보를 사람들이 올리면서 공유한다.
2. 그런데 커뮤니티 한 곳이 아닌 여러곳에 정보가 퍼져있다.
3. 그렇다보니 똑같은 정보에 대해 A, C 커뮤니티에는 정보가 있지만, 정작 B 커뮤니티에는 없는 경우가 있다.
4. 해당 프로젝트의 역할은 각 커뮤니티에서 특가 정보를 크롤링 후, 앱(apk)과의 통신을 위해 JSON 형식으로 웹페이지에 결과물을 띄우는 것을 담당한다.
5. 크롤링에 대해선 매 시간 단위로 CronJob을 활용하여 Background Job을 통해 크롤링이 진행된다.


## 5. 해당 Repository 내 Rails 프로젝트의 역할
1. 해당 프로젝트의 웹사이트 상에는 모든 데이터 결과를 json으로 처리한다.
2. 앱과의 통신 때 있어 json 방식으로 데이터 통신이 이루어지게 한다.
    * 결국 모든 데이터 자료는 앱이 아닌 해당 프로젝트로 구축된 사이트가 관리하게 된다.
3. 대용량 트래픽을 대비, 새로운 기능 추가를 염두하며 효율적인 API 설계를 한다.


## 6. 해당 프로젝트의 고민
#### 1) 백엔드
1. 대용량 트래픽을 고려하여 서버가 구축/설계가 되어야한다.
    * Redis-server
    * Nginx
    * Table Join, View, Index, ...
2. 외부의 보안 취약점을 찾아내려는 시도로 부터 대응책을 갖춰야 한다.
    * SQL Injection
    * URL 입력을 통한 특정 페이지(어드민페이지 등) 접근 시도
    * [Solution] Nginx, https, ... ?
3. 편리한 배포(CD)
    * Capistrano
    * Docker (Further more... K8S)

#### 2) 프론트엔드
* 내용 준비중

#### 3) 공통
1. 협업 문서화
    * 백엔드↔프론트에 있어 개발 요구사항/버그를 발견 시, 개발하면서 유의사항이 있을 시 서로에게 알려줘야 할 필요가 있다.
        * 카카오톡 : 즉각적으로 이슈를 남길 순 있으나, 다른 메세지에 묻힐 수 있다는 단점이 존재
        * 노션 : 주로 백엔드 개발 시 Crontab(백업 주기Time, 크롤링 주기 등) 등을 Notion에 기록.
        * Github 이슈 : 개발 요구사항/버그를 발견 시 즉각 남겨가며 최대한 까먹지 않도록 후에 To do List로서의 역할을 한다.
        * POSTMAN : Restful API 명세서로서 활용한다.
            * 프론트엔드 개발자는 백엔드의 설계에 맞추어 Restful API 규칙에 맞게 개발을 진행해야 한다.
                * Method
                * json 양식
                * Params
            * POSTMAN 대신 Swagger로 대체 가능
        * 제플린
            * 버전업 전 프로토타입 시안, 원본 이미지 저장

## 7. 프로젝트 작동 Process
1. 앱 ↔ 웹 기본 통신
<img src="/img/process_connect.png" width="100%">
<br/><br/>

2. 새로운 JWT 토큰 생성
<img src="/img/process_new_token.png" width="100%">
<br/><br/>

3. JWT 토큰 검증 및 작업
<img src="/img/process_validate_jwt.png" width="100%">


## 8. 테이블 설명
* hit_products: 특가 정보에 대한 데이터를 담아놓는다.
* notices: 공지사항에 대한 데이터를 담아놓는다.
* book_marks: 유저가 핫딜 데이터에 대해 북마크 표시를 해둔다.
* keyword_alarms: 유저가 등록한 키워드 데이터
* keyword_pushalarm_lists: 유저에게 발송된 푸쉬알람 기록
* manner_modes: 유저가 설정한 매너모드 (시작시간, 종료시간)
* product_categories: 핫딜 데이터가 속해있는 카테고리
* app_users: 유저에 대한 기록이 담겨져 있다.
* search_word_collections: 유저가 검색한 기록


## 9. Contact
shsdf302@gmail.com