# 📖 인터넷 서점 InkBridge

- 배포 URL : https://www.inkbridge.store
- Test ID : user@inkbridge.com
- Test PW : Test123!

<br>

## 프로젝트 소개

- 고객이 책을 검색하고 주문할 수 있는 인터넷 서점입니다.
- 판매자는 판매하고 싶은 책을 등록할 수 있습니다.
- 검색을 통해 원하시는 제목 또는 내용의 책을 구경할 수 있습니다.
- 회원 또는 비회원으로 원하시는 책을 골라 장바구니에 담고 주문할 수 있습니다.

<br>

## 팀원 구성

<div align="center">
  
| <a href="https://github.com/minseo9974"><img src="https://github.com/minseo9974.png" width="100px"><br>이민서</a> | <a href="https://github.com/nuheajiohc"><img src="https://github.com/nuheajiohc.png" width="100px"><br>최재훈</a> | <a href="https://github.com/minm063"><img src="https://github.com/minm063.png" width="100px"><br>장민주</a> |<a href="https://github.com/JBumLee"><img src="https://github.com/JBumLee.png" width="100px"><br>이정범</a> |<a href ="https://github.com/Huni0819"> <img src ="https://github.com/Huni0819.png" width ="100px"><br>장재훈</a> | <a href="https://github.com/brihgtclo"><img src="https://github.com/brihgtclo.png" width="100px"><br>정병훈</a>
|-----|-----|-----|----|-----|------|
  
</div>

<br>

## 아키텍처 구조

![alt text](profile/images/msa.png)

## CI/CD

![alt text](profile/images/cicd.png)

## ERD

![alt text](profile/images/erd.png)

## 개발 환경

- 버전 및 이슈관리 : Github, Github Issues, Github Project
- 협업 툴 : Dooray, Notion, Github Wiki
- 서비스 배포 환경 : Nhn Cloud
- 디자인 : [Figma](https://www.figma.com/file/AH7UFpxhWSk7jSt0a0JONY/Ink-Bridge?type=design&node-id=0-1&mode=design&t=McQHargAgtQk4Vgo-0)
- [컨벤션](https://devminseo.notion.site/InkBridge-b521a2123e024836a7c2f0caddd02ee2?pvs=4)
  <br>

## 브랜치 전략

### 브랜치 전략

- Git-flow 전략을 기반으로 main, develop 브랜치와 feature 보조 브랜치를 운용했습니다.
- main, develop, Feat 브랜치로 나누어 개발을 하였습니다.
  - **main** 브랜치는 배포 단계에서만 사용하는 브랜치입니다.
  - **develop** 브랜치는 개발 단계에서 git-flow의 master 역할을 하는 브랜치입니다.
  - **Feature** 브랜치는 기능 단위로 독립적인 개발 환경을 위하여 사용하고 네이밍은 각 이슈번호를 사용했습니다.

<br>

## 역할 분담
----

## 이민서

### Nginx
 - https 설정, L4 로드밸런싱
### 인증/인가
 - JWT 발급
   - Access,Refresh 토큰 두 개로 발급.
 - JWT 재발급
   - Refresh 토큰 유효성 검사 후 Access 토큰 재발급.
 - Gateway Jwt 인가
   - access 토큰 유효성 검사 후 헤더에 MemberId 추가.
 - Redis
   - Refresh 토큰, MemberId를 UUID를 키값으로 저장.
### Security
 - Auth Server
   - 로그인 성공
     - Front에서 받아온 회원정보와 API에서 가져온 DB정보를 매치시켜 인증후 토큰 발급.
   - 로그인 실패
     - 매치 실패시 발생한 예외를 UnSuccess에서 Front로 보냄.
 - Front Server
   - 로그인 성공
     - Auth Server 인증 성공시 받아온 토큰을 쿠키에 넣어주고 로그인 처리.
   - 로그인 실패
     - Auth Server 인증 실패시 다시 홈으로 Redirect.
### 회원
  - 회원가입
    - 이메일 중복확인과 Dooray HookSender 인증후 회원가입 합니다.
  - 로그인
    - Security login filter로 보내줍니다.
  - 회원 정보 수정
    - 회원 정보를 새로 수정합니다.
  - 탈퇴
    - 상태를 CLOSE로 바꾸고 로그인을 하지못하게 처리합니다.
<br>
    
## 장재훈
#### 주문

- 도서 상세 페이지, 장바구니에서 주문
- 회원/비회원 주문 처리
    - 보유한 쿠폰, 포인트를 사용해 구매 가격 할인
- 관리자가 주문 관리를 통해 주문 승인
    - 주문 승인 후 적절한 포인트 적립
        - 등급별 포인트
        - 도서별 포인트
- Daum 주소 API 사용해 배송지 입력
- 포장할 도서 선택 가능
- 주문 조회
    - 회원
        - 마이 페이지에서 조회 가능
    - 비회원
        - 주문시 발급된 주문 코드로 조회 가능

#### 결제

- Toss Payment API를 사용해 결제 구현
- 대기 상태의 주문에 대해서만 결제 취소 가능
    - 회원의 경우 사용 포인트 적립
- 결제 저장이 외부에 영향을 받지 않도록 트랜잭션 전파 속성을 설정

#### 기타

- 포인트, 배송비 정책 관리
- API Gateway, Netflix Eureka 설정
    - Backend API 서버 무중단 배포 설정

<br>

## 장민주

- gateway Github Action 설정
### 도서
- 도서 조회, 등록, 수정, 메인 페이지 도서 캐싱
- Redis Cache를 사용
  - 빈번한 조회가 이루어지는 메인 페이지에 캐싱을 적용하여 페이지 로딩 시간 단축
- tui-editor 설정
  - 오픈 소스인 toast ui editor를 사용하여 도서 등록 시 설명 기입 관리
  - markdown으로 저장한 설명을 markdown-it을 사용하여 html로 변환하여 표시

### 장바구니
- 장바구니 조회, 등록, 수정, 삭제가 가능하도록 구현
- redis를 사용하여 비회원과 회원의 장바구니 관리
  - 비회원은 만료 기간을 설정하여 기간이 지나면 장바구니가 삭제되도록 구현
  - 회원은 로그인 - 로그아웃을 할 때마다 DB에서 조회하고 장바구니를 저장하는 방식을 사용
- 조회가 잦은 장바구니를 위해 장바구니용 도서 정보를 캐싱하여 레디스에 저장

### 작가
- 작가 조회, 등록, 수정 구현

### 리뷰
- 리뷰 조회, 등록, 수정 구현
- 리뷰 등록 시 포인트 누적, 포인트 내역 추가
- 도서 상세 화면에서 평균 평점을 조회할 수 있도록 설정
<br>

## 최재훈

### 출판사
- 출판사 등록, 수정, 조회 기능 구현
- 출판사 관리자 뷰

### 카테고리
- 카테고리 등록, 수정, 조회 기능 구현
- 카테고리 관리자 뷰
- 재귀적인 계층구조로 카테고리 구성

### 검색
- 검색 설정 및 로직
  - Elasticsearch를 활용한 검색 기능 구현
  - 로그 스태시를 활용하여 데이터베이스 테이블의 칼럼들을 필요에 맞게 가공
  - 키비나의 데이터 시각화를 통해 개발 생산성 증대
  - 노드 3개를 하나의 클러스터로 만들어서 데이터 안전성 확보
  - 검색 가중치 설정을 통해 검색 최적화
- 검색 편의성
  - 인기순, 신상품순, 가격순, 평점순, 리뷰순으로 정렬가능
  - 동의어 처리 (ex. 자바 = java)
  - 10, 20, 50개의 도서로 페이징 처리
  - 도서에 해당하는 작가, 출판사, 태그 등 클릭으로 검색가능
  - 도서 수량 설정과 함께 도서 장바구니로 이동과 바로구매 가능
  
### 메인뷰
- 메인에서 신상도서, 인기도서, 할인 도서, 평점이 높은 도서 8개를 볼 수 있도록 설계
- 국내도서, 국외도서 
<br>

## 이정범
### frontEnd GitAction 세팅
### 쿠폰 
- 생일쿠폰, 도서쿠폰, 카테고리쿠폰, 일반쿠폰 쿠폰정책 생성
- 정책에따라 생성된 쿠폰 발급
- 쿠폰의 정책은 정책에따라 00시마다 만료.(Spring Batch)
- 쿠폰의 정책은 정책에따라 00시마다 활성.(Spring Batch)

#### 쿠폰 고려사항 : 
 1. 다음 생성되는 쿠폰의 id는 예측이 되면안된다.<br />
 -> UUID 사용
 2. UUID는 매번 insert마다 재정렬을한다. 따라서 pk로 사용할것인가?<br />
2-1. InkBridge의 쿠폰시스템은 정책을 생성하는 것이기 때문에. 많은 Insert가없다.<br />
   -> UUID 사용에 문제가 없다.<br />
2-2. 이에 정책이 아닌 발급되는 쿠폰은 AutoIncrement로 생성

#### 생일쿠폰 
- 만약 이달의 정책이 생성되지 않는다면 기본 정책으로 자동생성(Spring Batch)
- 매월 1일 정책 OR 기본으로 생성된 생일 쿠폰은 자동으로 이달의 생일인 사람에게 발급한다.

#### 그 외
- 관리자는 발급중인쿠폰, 삭제된쿠폰, 만료된쿠폰, 대기중인 쿠폰의 리스트 볼 수 있다.
- 사용자는 보유중인 쿠폰리스트와, 발급가능한 쿠폰을 볼 수 있다.

### 배송
- 요구사항에 따라 도착예정일 +3일에 배송상태를 도착으로 변경한다.

### 포장지
- 포장지생성, 수정, 단일조회, 전체조회
<br>

## 정병훈
### 포인트 내역
- 회원 조소 등록, 수정, 삭제, 조회 기능 구현
- 회원 포인트 내역 조회 기능 구현
- 포인트 수정 및 포인트 내역 등록 기능 구현
- 회원 등급 수정, 조회 기능 구현
- 관리자 회원 등급 뷰
- 회원 포인트 내역, 배송지 뷰

### 파일
- 파일 등록, 조회

### 파일 저장 및 관리 최적화
- 로컬 파일 저장 및 불러오기 기능을 통해 기본적인 파일 관리 시스템을 구축
    -  문제점 로컬 스토리지의 사용은 배포 환경에서 재배포 시 데이터 유실과 로드 밸런싱 환경에서의 불균형한 파일 저장 문제를 발생
    -  해결첵 ObjectStorage를 도입하여 공유 스토리지 환경을 구축
-  ObjectStorage의 활용
    -   여러 서버를 사용하는 환경에서도 파일 데이터의 일관성과 접근성을 보장
    -  서비스의 안정성과 확장성을 향상

### 태그
- 테그 등록, 수정, 조회, 삭제 기능 구현
- 관리자 테그 뷰
  

<br>

## 개발 기간 및 작업 관리

### 개발 기간

- 전체 개발 기간 : 2024-02-05 ~ 2024-03-29

<br>

### 작업 관리

- GitHub Projects와 Issues를 사용하여 진행 상황을 공유했습니다.
- 매일 스크럼 회의를 진행하며 작업 순서와 방향성에 대한 고민을 나누고 GitHub project에 회의 내용을 기록했습니다.
  ![alt text](profile/images/image-1.png)

<br>

<details>
<summary>WBS</summary>
    <img width="100%" src="profile/images/image-2.png"/>
    <img width="100%" src="profile/images/image-3.png"/>
    <img width="100%" src="profile/images/image-4.png"/>
    <img width="100%" src="profile/images/image-5.png"/>
    <img width="100%" src="profile/images/image-6.png"/>
</details>

<br>

### 테스트 커버리지

<br>

## 기술 스택

**Language**

<div>
  <img src="https://img.shields.io/badge/java-007396?style=for-the-badge&logo=java&logoColor=white"> 
</div>

<br>

**Framework**
<div>
  <img src="https://img.shields.io/badge/spring boot-6DB33F?style=for-the-badge&logo=springboot&logoColor=white">
<img src="https://img.shields.io/badge/spring security-6DB33F?style=for-the-badge&logo=springsecurity&logoColor=white">
  <img src="https://img.shields.io/badge/spring batch-6DB33F?style=for-the-badge&logo=spring&logoColor=white">
  <img src="https://img.shields.io/badge/spring cloud-6DB33F?style=for-the-badge&logo=spring&logoColor=white">
  <img src="https://img.shields.io/badge/spring gateway-6DB33F?style=for-the-badge&logo=spring&logoColor=white">
  <img src="https://img.shields.io/badge/spring eureka-6DB33F?style=for-the-badge&logo=spring&logoColor=white">
  <img src="https://img.shields.io/badge/spring Data JPA-6DB33F?style=for-the-badge&logo=spring&logoColor=white">
  <img src="https://img.shields.io/badge/spring Data Redis-6DB33F?style=for-the-badge&logo=spring&logoColor=white">
  <img src="https://img.shields.io/badge/spring RESTdocs-6DB33F?style=for-the-badge&logo=spring&logoColor=white">
</div>

<br>

**Database**

<div>
  <img src="https://img.shields.io/badge/MySQL-4479A1?style=for-the-badge&logo=MySQL&logoColor=white"/>
<img src="https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=Redis&logoColor=white"/>
</div>

<br>

**Build**

<div>
  <img src="https://img.shields.io/badge/Maven-C71A36?style=for-the-badge&logo=ApacheMaven&logoColor=white"/>
</div>

<br>

**CI/CD**

<div>
  <img src="https://img.shields.io/badge/Jenkins-D24939?style=for-the-badge&logo=Jenkins&logoColor=white"/>
  <img src="https://img.shields.io/badge/Github Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white"/>
</div>

<br>

**DevOps**

<div>
  <img src="https://img.shields.io/badge/DOCKER-2496ED?style=for-the-badge&logo=docker&logoColor=white"/>
  <img src="https://img.shields.io/badge/sonarqube-4E9BCD?style=for-the-badge&logo=SonarQube&logoColor=white"/>
</div>

<br>

**ETC**

<div>
  <img src="https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white"/>
  <img src="https://img.shields.io/badge/sonarqube-4E9BCD?style=for-the-badge&logo=SonarQube&logoColor=white"/>
  <img src="https://img.shields.io/badge/JUnit5-25A162?style=for-the-badge&logo=junit5&logoColor=white"/>
  <img src="https://img.shields.io/badge/Git-F05032?style=for-the-badge&logo=git&logoColor=white"/>
  <img src="https://img.shields.io/badge/Github-181717?style=for-the-badge&logo=github&logoColor=white"/>
  <img src="https://img.shields.io/badge/elasticsearch-005571?style=for-the-badge&logo=elasticsearch&logoColor=white"/>
  <img src="https://img.shields.io/badge/Logstash-005571?style=for-the-badge&logo=Logstash&logoColor=white">
  <img src="https://img.shields.io/badge/kibana-005571?style=for-the-badge&logo=kibana&logoColor=white">
</div>

<br>

**View**

<div>
  <img src="https://img.shields.io/badge/thymeleaf-005F0F?style=for-the-badge&logo=thymeleaf&logoColor=white"/>
  <img src="https://img.shields.io/badge/html5-E34F26?style=for-the-badge&logo=html5&logoColor=white"/>
  <img src="https://img.shields.io/badge/css3-1572B6?style=for-the-badge&logo=css3&logoColor=white"/>
  <img src="https://img.shields.io/badge/javascript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=white"/>
</div>

<br>

**Document**

<div>
  <img src="https://img.shields.io/badge/asciidoctor-E40046?style=for-the-badge&logo=asciidoctor&logoColor=white"/>
</div>
