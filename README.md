# AikusoniTradeSystem 문서

:construction:아직 작업 중인 프로젝트입니다.:construction:

## 목차

- [소개](#소개)
- [프로젝트 개요](#프로젝트-개요)
- [주요 예상 시나리오](#주요-예상-시나리오)
- [시스템 아키텍처](#시스템-아키텍처)
    - [프론트엔드](#프론트엔드)
    - [백엔드](#백엔드)
    - [데이터베이스](#데이터베이스)
    - [라이브러리](#라이브러리)
    - [기타](#기타)
    - [웹 서버 및 리버스 프록시](#웹-서버-및-리버스-프록시)
- [기술 스택](#기술-스택)
- [추가로 개발하고 싶은 부분](#추가로-개발하고-싶은-부분)
- [브랜치 관리 전략](#브랜치-관리-전략)
- [컨벤션](./convention/convention.md)

## 소개
AikusoniTradeSystem 프로젝트는 여러 웹 개발 기술을 연습하고 학습하기 위한 개인 프로젝트입니다. \
실사용 목적이 아니며 개인적인 학습과 실험을 위한 프로젝트입니다. \
이 문서에서는 프로젝트의 개요와 각 구성 요소에 대해 설명합니다.

## 프로젝트 개요
AikusoniTradeSystem은 게임내 아이템 경매장을 구현하기 위한 플랫폼입니다. \
이 시스템은 여러 개의 작은 서비스로 구성되어 있으며, 각각의 서비스는 플랫폼의 특정 부분을 처리합니다. \
관리를 용이하게 하기 위해 이런 구조를 선택했습니다. 

## 기능 개요
각 기능에 대한 상세 시나리오는 [상세 시나리오](./details/scenario.md)문서에 작성되어 있습니다.
- 회원 가입 및 로그인
- 관리자의 아이템 정보 관리
- 인벤토리를 가진 게임 캐릭터 생성 / 삭제
- 캐릭터의 아이템 루팅 처리
- 계정 창고 및 캐릭터 인벤토리 기능
- 경매장을 통한 아이템 거래
- 아이템 거래 통계

## 시스템 아키텍처 (초안)
![system-architecture-draft](./imgs/system-architecture-draft.svg)

### 프론트엔드
#### 포탈 페이지 및 회원가입 / 로그인UI
- 레포 : [portal-web-ui](https://github.com/AikusoniTradeSystem/portal-web-ui)
- 프레임워크 : Angular 또는 React
- 설명 : 포탈 사이트입니다. 로그인 및 회원가입 기능을 제공합니다.

#### 아이템 등록 관리용 관리자 UI (작업전)
- 레포: [item-registration-web-ui](https://github.com/AikusoniTradeSystem/item-registration-web-ui)
- 프레임워크: Angular 또는 React
- 설명: 관리자가 아이템 정보를 등록/관리 할 때 사용하는 화면입니다.

#### 경매장 UI (작업전)
- 레포 : [auction-web-ui](https://github.com/AikusoniTradeSystem/auction-web-ui)
- 프레임워크: Angular 또는 React
- 설명 : 일반 유저가 사용하는 인벤토리 및 아이템 경매장 화면입니다.

### 백엔드
#### 거래 API 서버 (작업전)
- 레포: [trade-api](https://github.com/AikusoniTradeSystem/trade-api)
- 기술: Spring Boot (Spring MVC)
- 설명: 거래 요청을 수신하고, 메시지 큐에 거래 요청 메시지를 등록합니다.

#### 거래 처리 데몬 (작업전)
- 레포: [trade-processor](https://github.com/AikusoniTradeSystem/trade-processor)
- 기술: Spring Boot
- 설명: 메시지 큐에서 거래 요청 메시지를 받아 거래를 처리합니다.

#### 푸시 알림 서버 (작업전)
- 레포: [push-notification-server](https://github.com/AikusoniTradeSystem/push-notification-server)
- 기술: Spring Boot (Firebase Cloud Messaging 혹은 WebSocket 혹은 SSE)
- 설명: 거래 처리 완료 메시지를 받으면 프론트엔드에 푸시 알림을 보냅니다.

#### 아이템 등록 API 서버 (작업전)
- 레포: [item-registration-api](https://github.com/AikusoniTradeSystem/item-registration-api)
- 기술: Node.js + express
- 설명: 아이템 정보 등록/관리 API가 있는 서버입니다.

#### 인벤토리 API 서버 (작업전)
- 레포: [inventory-api](https://github.com/AikusoniTradeSystem/inventory-api)
- 기술: Spring Boot (Spring MVC)
- 설명: 인벤토리 정보와 소유권 정보를 관리합니다.

#### 아이템 거래 통계 API 서버 (작업전)
- 레포: [item-trade-statistics-api](https://github.com/AikusoniTradeSystem/item-trade-statistics-api)
- 기술: Spring Boot (Spring MVC)
- 설명: 아이템 거래 내역을 사용해 통계 정보를 반환하는 API 서버입니다. 빠른 응답을 위해 캐시를 사용합니다.

#### 인증 서버 (작업중)
- 레포: [session-auth-server](https://github.com/AikusoniTradeSystem/session-auth-server)
- 서버: Spring Boot (Spring MVC)
- 설명: 사용자 인증 처리 및 세션 정보를 관리합니다. HTTP 헤더에 사용자 세부 정보를 추가하여 다른 API 서비스에서 사용할 수 있도록 합니다. Redis를 세션 클러스터링에 사용할 예정입니다.

#### 테스트 서버 1
- 레포: [test-server-spring](https://github.com/AikusoniTradeSystem/test-server-spring)
- 서버: Spring Boot (Spring MVC)
- 설명: 인증 처리 완료된 API 호출에 인가 기능 테스트를 진행하기 위한 Spring Boot 서버입니다.

#### 테스트 서버 2
- 레포: [test-server-node](https://github.com/AikusoniTradeSystem/test-server-node)
- 서버: Node.js + express
- 설명: 인증 처리 완료된 API 호출에 인가 기능 테스트를 진행하기 위한 node.js 서버입니다.

### 라이브러리
```
공통적으로 사용되는 모듈의 경우 GitHub Package Repository를 통해 배포해서 사용합니다.
```
#### AikusoniTradeSystem 스프링부트 앱용 Core 모듈 (작업중)
- 레포: [ats-spring-core](https://github.com/AikusoniTradeSystem/ats-spring-core)
- 설명: 스프링 부트 애플리케이션에서 공통으로 사용될 Core 모듈 

#### AikusoniTradeSystem 스프링부트 앱용 Web MVC 모듈 (작업중)
- 레포: [ats-spring-mvc-standard](https://github.com/AikusoniTradeSystem/ats-spring-mvc-standard)
- 설명: 스프링 부트 애플리케이션 중 WEB-MVC를 사용하는 서버 애플리케이션에서 사용될 WEB-MVC 표준 모듈

### 기타
#### packages
- 레포: [packages](https://github.com/AikusoniTradeSystem/packages)
- 설명: GitHub Package Repository를 통해 배포되는 패키지를 등록하기 위한 레포지토리

### 데이터베이스
- DB: DB 정보는 각 도메인에 해당되는 프로젝트에서 관리
- 기술: MySQL (핵심 데이터용), Redis(세션클러스터링), 또, 게임 아이템 세부 정보 관리를 위해 NoSQL (예: MongoDB)을 고려 중입니다.

### 웹 서버 및 리버스 프록시
- 레포: [nginx-config](https://github.com/AikusoniTradeSystem/nginx-config)
- 기술: nginx
- 설명: 웹팩(혹은 vite)으로 번들링된 프론트엔드 페이지를 서비스하는 웹 서버 역할을 하고, API 요청을 라우팅하는 리버스 프록시 역할을 합니다. 요청을 전달하기 전에 auth_request를 사용해 인증 체크를 진행하여, 비즈니스 로직이 있는 서비스와 인증 서비스를 분리합니다. 추후 토큰 방식등으로 인증 시스템 전환을 용이하게 하기 위해 이렇게 구성했습니다.

## 기술 스택
- 프론트엔드: Angular 또는 React
- 백엔드: Spring Boot, Node.js
- 데이터베이스: MySQL, Redis, (MongoDB도 고려 중)
- 인증: Spring Boot와 Redis를 사용한 세션 클러스터링
- 메시지 큐 : RabbitMQ
- 웹 서버 및 리버스 프록시: nginx
- 라이브러리 패키지 배포 방식: GitHub Package Repository 사용

## 추가로 개발하고 싶은 부분
- Docker Compose를 사용해 한번에 배포해보기
- 인증 서버 전환 해보기
- 거래 기록 관리를 위한 ELK 적용
- Spring Webflux 사용해보기

## 브랜치 관리 전략
- 기본적인 기능 개발이 완료되어 최초 배포버전이 만들어지면 [git flow](https://techblog.woowahan.com/2553/) 또는 [github flow](https://docs.github.com/ko/get-started/using-github/github-flow)와 유사한 형태로 진행합니다.
