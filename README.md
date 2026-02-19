# 🏥 Medicine WMS (Warehouse Management System)

> 신세계 아이앤씨 자바 백엔드 개발자 트랙 4차수 1차 프로젝트

의약품 창고 관리를 위한 종합 물류 시스템입니다. 입고, 출고, 재고, 재무 관리 등 창고 운영에 필요한 모든 기능을 제공합니다.

## 📋 목차
- [프로젝트 소개](#-프로젝트-소개)
- [주요 기능](#-주요-기능)
- [기술 스택](#-기술-스택)
- [프로젝트 구조](#-프로젝트-구조)
- [설치 및 실행](#-설치-및-실행)
- [사용 방법](#-사용-방법)
- [데이터베이스 구조](#-데이터베이스-구조)

## 🎯 프로젝트 소개

Medicine WMS는 의약품 창고의 효율적인 운영을 위해 개발된 CLI 기반 창고 관리 시스템입니다.

### 개발 정보
- **교육 과정**: 신세계 아이앤씨 자바 백엔드 개발자 트랙
- **차수**: 4차수
- **프로젝트**: 1차 프로젝트
- **개발 기간**: 2024년 8월

## ✨ 주요 기능

### 👥 회원 관리
- 회원가입 및 로그인
- 아이디/비밀번호 찾기
- 회원 유형별 권한 관리 (일반회원, 배송기사, 관리자)
- 승인 대기 회원 관리

### 📦 입고 관리
- 입고 요청 등록
- 입고 승인 처리
- 입고 내역 조회

### 🚚 출고 관리
- 출고 요청 생성
- 출고 검수
- 배차 및 운송장 관리
- 출고 예정 현황 조회

### 📊 재고 관리
- 실시간 재고 조회
- 재고 실사
- 로트번호별 재고 관리
- 창고/섹션별 재고 현황

### 🏢 창고 관리
- 창고 등록 및 관리
- 섹션 관리
- 창고별 재고 현황

### 💰 재무 관리
- 수익 관리
- 비용 관리
- 재무 현황 조회

## 🛠 기술 스택

### Backend
- **Language**: Java
- **Database**: MySQL 8.0
- **JDBC**: MySQL Connector/J

### Libraries
- **Lombok**: 코드 간소화

### Architecture
- **Design Pattern**: MVC (Model-View-Controller)
- **Database Connection**: Singleton Pattern (ConnectionFactory)

## 📁 프로젝트 구조

```
medicine-wms/
│
├── src/
│   ├── Main.java                    # 애플리케이션 진입점
│   │
│   ├── config/                      # 설정 파일
│   │   ├── ConnectionFactory.java   # DB 연결 관리 (Singleton)
│   │   ├── ObjectDBIO2.java         # DB I/O 추상 클래스
│   │   ├── LOGO.java                # 로고 출력
│   │   ├── SystemIn.java            # 입력 처리 유틸
│   │   └── UtilMethod.java          # 공통 유틸 메서드
│   │
│   ├── controller/                  # 컨트롤러 레이어
│   │   └── CLIController.java       # CLI 메뉴 컨트롤러
│   │
│   ├── dao/                         # Data Access Object
│   │   ├── AdminFunctions.java      # 관리자 기능
│   │   └── memberServices.java      # 회원 서비스 DAO
│   │
│   ├── interfaces/                  # 서비스 인터페이스
│   │   ├── ExpenditureService.java
│   │   ├── RevenueService.java
│   │   ├── StockPrintService.java
│   │   ├── StockTakingService.java
│   │   ├── InboundApprovalService.java
│   │   ├── warehouse/
│   │   │   └── WarehouseService.java
│   │   └── release/
│   │       ├── ReleaseRequestService.java
│   │       └── ReleaseService.java
│   │
│   ├── services/                    # 서비스 구현체
│   │   ├── FinanceServiceImpl.java
│   │   ├── StockPrintServiceImpl.java
│   │   ├── StockTakingServiceImpl.java
│   │   ├── warehouse/
│   │   │   └── WarehouseServiceImpl.java
│   │   └── release/
│   │       ├── ReleaseMainMenu.java
│   │       ├── ReleaseRequestServiceImpl.java
│   │       └── ReleaseServiceImpl.java
│   │
│   ├── vo/                          # Value Object (DTO)
│   │   ├── Stock.java               # 재고 VO
│   │   ├── StockTaking.java         # 재고 실사 VO
│   │   ├── Expenditure.java         # 비용 VO
│   │   └── InboundApproval.java     # 입고 승인 VO
│   │
│   └── enums/                       # Enum 클래스
│       ├── Messeges.java            # 시스템 메시지
│       └── UserMessege.java         # 사용자 메시지
│
└── .gitignore
```

### 아키텍처 설명

#### MVC 패턴
- **Model**: `vo/` (데이터 객체), `dao/` (데이터 접근)
- **View**: CLI 기반 콘솔 출력
- **Controller**: `controller/` (사용자 입력 처리 및 흐름 제어)

#### 계층 구조
1. **Controller Layer**: 사용자 입력 처리 및 메뉴 관리
2. **Service Layer**: 비즈니스 로직 구현
3. **DAO Layer**: 데이터베이스 CRUD 작업
4. **VO Layer**: 데이터 전송 객체

## 🚀 설치 및 실행

### 사전 요구사항
- JDK 8 이상
- MySQL 8.0 이상
- Lombok 라이브러리

### 데이터베이스 설정

1. MySQL 데이터베이스 생성
```sql
CREATE DATABASE wms;
```

2. `src/config/ObjectDBIO2.java` 파일에서 데이터베이스 연결 정보 수정
```java
private String db_url = "jdbc:mysql://localhost:3306/wms";
private String db_id = "root";
private String db_pwd = "mysql1234";  // 본인의 MySQL 비밀번호로 변경
```

### 실행 방법

```bash
# 컴파일
javac -cp .:lib/* src/Main.java

# 실행
java -cp .:lib/* Main
```

## 📖 사용 방법

### 시작 화면
```
  #####   ##     ##    ######     ######   #######  #########
##    ##  ###   ###   ##    ##   ##    ##  ##           ##   
##        #### ####  ##      ## ##      ## ##           ##   
##        ## ### ##  ##      ## ##      ## #######      ##   
 ######   ##  #  ##  ##      ## ##      ## ##           ##   
     ##   ##     ##  ##      ## ##      ## ##           ##   
##   ##   ##     ##   ##    ##   ##    ##  ##           ##   
 #####    ##     ##    ######     ######   ##       #########

SMOOFI에 오신 것을 환영합니다

메인 메뉴 : 1.로그인 | 2.회원가입 | 3.아이디 찾기 | 4.비밀번호 찾기
```

### 회원 유형별 메뉴

#### 일반 회원
- 입고 관리
- 출고 요청
- 재고 조회
- 재무 현황

#### 배송 기사
- 배송 할당 확인
- 배송 상태 업데이트
- 운송장 관리

#### 관리자
- 전체 회원 관리
- 입고/출고 승인
- 창고/섹션 관리
- 재고 실사
- 재무 관리

## 💾 데이터베이스 구조

### 주요 테이블

#### member (회원)
- member_id: 회원 ID (PK)
- member_name: 이름
- member_password: 비밀번호
- member_phoneNumber: 전화번호
- member_email: 이메일
- member_type: 회원 유형
- approval: 승인 여부
- member_status: 회원 상태

#### Stock (재고)
- productLotNo: 제품 로트 번호
- productName: 제품명
- total: 재고 수량
- productId: 제품 ID
- sectionId: 섹션 ID
- warehouseName: 창고명

## 👥 팀원 및 역할

- **프로젝트 참여자**: firstsm41
- **원본 프로젝트**: [Smoofi0729/medicine-wms](https://github.com/Smoofi0729/medicine-wms)

## 📝 참고사항

- 본 프로젝트는 교육 목적으로 개발되었습니다.
- MySQL 데이터베이스 연결 정보는 반드시 본인의 환경에 맞게 수정해야 합니다.
- Lombok을 사용하므로 IDE에 Lombok 플러그인 설치가 필요합니다.

## 📄 라이선스

이 프로젝트는 교육용으로 제작되었습니다.

---

**신세계 아이앤씨 자바 백앤드개발자트랙 4차수 1차 프로젝트**
