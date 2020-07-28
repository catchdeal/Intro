# 캐치야, 물어와! : 특가정보 모음집 '캐치딜'
<div align="center"><img src="/img/app-v4.png?raw=true" width="500px"></div>

## Related
* 앱 클라이언트 Repository : https://github.com/catchdeal/catchDeal-Client
* API 통신 / 소개 페이지 렌더링 / Database Server : https://github.com/catchdeal/CatchDeal-API
* 크롤링 (AWS Lamabda + Ruby on Jets) : https://github.com/catchdeal/CatchDeal-Lambda
* 크롤링 (라즈베리파이4B + Ruby on Rails) : https://github.com/catchdeal/CatchDeal-RaspberryPi


## Story of CatchDeal
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


##  Intro
1. 커뮤니티에는 매일 갖가지 할인행사에 대한 정보를 사람들이 올리면서 공유한다.
2. 커뮤니티 한 곳이 아닌 여러곳에 정보가 퍼져있다.
3. 똑같은 정보에 대해 A, C 커뮤니티에는 정보가 있지만, 정작 B 커뮤니티에는 없는 경우가 있다.
4. 해당 프로젝트의 역할은 각 커뮤니티에서 특가 정보를 크롤링 후, 앱(apk)과의 통신을 위해 JSON 형식으로 웹페이지에 결과물을 띄우는 것을 담당한다.
5. 크롤링에 대해선 매 시간 단위로 CronJob을 활용하여 Background Job을 통해 크롤링이 진행된다.


## CatchDeal Tech Stack
#### 1) Backend
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

<!-- #### 2) 프론트엔드
* 내용 준비중-->

## Etc
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

## Process
1. 앱 ↔ 웹 기본 통신
<img src="/img/process_connect.png" width="100%">
<br/><br/>

2. 새로운 JWT 토큰 생성
<img src="/img/process_new_token.png" width="100%">
<br/><br/>

3. JWT 토큰 검증 및 작업
<img src="/img/process_validate_jwt.png" width="100%">
