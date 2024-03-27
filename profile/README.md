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

### 이민서

<br>
    
### 장재훈

<br>

### 장민주

<br>

### 최재훈

<br>

### 이정범
#### frontEnd GitAction 세팅
#### 쿠폰 
- 생일쿠폰, 도서쿠폰, 카테고리쿠폰, 일반쿠폰 쿠폰정책 생성
- 정책에따라 생성된 쿠폰 발급
- 쿠폰의 정책은 정책에따라 00시마다 만료.(Spring Batch)
- 쿠폰의 정책은 정책에따라 00시마다 활성.(Spring Batch)

##### 쿠폰 고려사항 : 
 1. 다음 생성되는 쿠폰의 id는 예측이 되면안된다.<br />
 -> UUID 사용
 3. UUID는 매번 insert마다 재정렬을한다. 따라서 pk로 사용할것인가?
2-1. InkBridge의 쿠폰시스템은 정책을 생성하는 것이기 때문에. 많은 Insert가없다.
 -> UUID 사용에 문제가 없다.
2-2. 이에 정책이 아닌 발급되는 쿠폰은 AutoIncrement로 생성

##### 생일쿠폰 
- 만약 이달의 정책이 생성되지 않는다면 기본 정책으로 자동생성(Spring Batch)
- 매월 1일 정책 OR 기본으로 생성된 생일 쿠폰은 자동으로 이달의 생일인 사람에게 발급한다.

##### 그 외
- 관리자는 발급중인쿠폰, 삭제된쿠폰, 만료된쿠폰, 대기중인 쿠폰의 리스트 볼 수 있다.
- 사용자는 보유중인 쿠폰리스트와, 발급가능한 쿠폰을 볼 수 있다.

#### 배송
- 요구사항에 따라 도착예정일 +3일에 배송상태를 도착으로 변경한다.

#### 포장지
- 포장지생성, 수정, 단일조회, 전체조회
<br>

### 정병훈

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
