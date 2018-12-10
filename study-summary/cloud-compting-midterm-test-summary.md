# Index
Introduction to Cloud Computing [#](#Introduction-to-Cloud-Computing)
 - 클라우드 컴퓨팅이란?
 - 클라우드 보급 배경
 - 클라우드의 특징
 - 클라우드 서비스 모델
 - IaaS (Infrastructure as a Service)
 - Paas (Platform as a Service)
 - Saas (Software as a Service)
 - 클라우드의 장점
 - 클라우드 단점
 - 클라우드 컴퓨팅 이용모델
 - 배치 모델
 - 종류
 - deployment model
 - private cloud
 - community cloud
 - public cloud
---


# Introduction to Cloud Computing
## 클라우드 컴퓨팅이란?
> 인터넷 너머에 존재하는 클라우드 사업자의 컴퓨터에서 정보처리를 하는 서비스

특정 기술이 아닌 *사고방식* 또는 *개념*!

- 초기 투자나 장기계약 없이
- 인터넷을 통해 IT리소스와 

## 클라우드 보급 배경
- 기술적 향상
    - CPU 고속화
    - 가상화 기술 및 분산 처리 기술
- 한계
    - 거대해진 데이터 센터
- 비용적 측면
    - 빠르고 저렴한 네트워크
    - 사용자(기업): IT 투자 비용 절감 가능
    - 사업자: 지속적 매출(수요 있음)

## 클라우드의 특징

## 클라우드 서비스 모델
- IaaS (Infrastructure as a Service)
    - 데이터 센터
    - 네트워킹 방화벽/보안
    - 운영체제
- Paas (Platform as a Service)
    - 개발도구, DB관리, 비지니스 분석
- Saas (Software as a Service)
    - 호스팅된 응용프로그램/앱

### IaaS (Infrastructure as a Service)
- 사업자는 사용자에게 pay-as-you-go access 제공
- storage, networking, servers...
- https://azure.microsoft.com/ko-kr/overview/what-is-iaas/


### Paas (Platform as a Service)
- 사업자는 cloud-based environment + infrastructure 제공
- 사용자는 application만 개발
- Java, PHP, Ruby 등의 프로그래밍 언어를 지원하는 애플리케이션 실행 환경이나 데이터베이스 등이 미리 준비되어 있음
- (예)
    - 개발 및 테스트에 큰 처리 능력이 필요한 경우
    - 자사에서 운영 중인 애플리케이션의 최대 부하를 분산 처리할 때
    - IoT 데이터를 효율적으로 수집하여 처리하는 플랫폼
- https://azure.microsoft.com/ko-kr/overview/what-is-paas/


### Saas (Software as a Service)
- 업자는 사용자에게 software/application 제공
- 사용자는 subscrible를 하고 web 또는 API를 통해 access
- https://azure.microsoft.com/ko-kr/overview/what-is-saas/

> On-premise  
> - 회사 내에 자체적으로 데이터 센터를 보유
>  - 시스템 구축, 운용까지 직접 수행하는 형태

## 클라우드의 장점
- 경제성: 사용하고자 하는 기간만, 소프트웨어/데이터를 클라우드에서 통합 관리
- 유연성: 리소스를 필요할 때, 필요한 만큼 확장/축소 가능
- 가용성: 장애 발생시 계속 사용 가능
- 빠른 구축 속도
- 손쉬운 글로벌 서비스
- 강력한 보안

## 클라우드 단점
- 생각보다 비싼 비용
- 점점 커지는 클라우드 의존성
- 데이터 보관의 불안함

## 클라우드 컴퓨팅 배치 모델
### 종류
- private cloud
- community cloud
- public cloud
    - +) hybrid cloud

### private cloud
- 독점적으로 사용되는 클라우드 컴퓨팅 리소스
- 클라우드 서비스 사용자 또는 사업자의 데이터 센터에 구축한 자사 전용 환경
- 서비스와 인프라가 개인/기업네트워크에서 유지 관리 됨
- 종류
    - on-premise private cloud
        - 자사 전용 클라우드 환경 구축, 운용
        - 자체적인 보안정책 → 강력한 보안 환경
        - 부담
    - hosted private cloud
        - 클라우드 사업자가 기업 사용자별로 클라우드 환경 제공
        - 기업 전용 클라우드 환경 구축 → 비용 지불


### community cloud
- 공통의 목적을 가진 기업/조직들이 클라우드 시스템을 형성하여 데이터 센터에서 공동 운영하는 형태

### public cloud
- 클라우드 사업자가 시스템 구축
- 네트워크를 통해 기업, 개인에게 서비스 제공
- 기업/개인 방화벽 외부에 구축됨

### hybrid cloud
- public, private, community 서비스들과 on-premise 시스템을 연계시켜 활용하는 시스템

### 클라우드 서비스
## 클라우드 컴퓨팅의 용도
- 새로운 앱 및 서비스 만들기
- 데이터 저장, 백업 및 복수
- 웹 사이트 및 블로그 호스팅
- 오디오 및 비디오 스트리밍
- 주문형 소프트웨어 제공
- 데이터의 패턴을 분석하여 예측 등

## 주요 클라우드 서비스
- 가상 서버
    - 로드 밸런스, 오토 스케일링
- 스토리지 서비스
- 네트워크 서비스
    - VPN, 전용선
- 데이터베이스

### 가상 서버
#### AWS EC2(Elastic Cloud compute)
- 하나의 물리적 서버를 논리적으로 나누어 CPU나 메모리 등의 자원을 할당한 것
    - 가상화하지 않은 서버에 비해서 성능은 떨어짐
    - 고성능 요구 시 -> 실제 서버(bare-metal server)
- 이용
    - 생성, 중지, 재시작, 종료
    - 다양한 tyre: CPU, Memory
    - Root disk: 시동 디스크
    - OS: CentOS, Ubuntu, MS Window Server...
- 추가 기능
    - 로드 밸런서: 하나의 리전 내의 복수 개의 존에 서버를 설치하여 부하를 분산시킴
    - 오토 스케일링: 가상 서버의 갯수를 자동으로 증감시킴
    - 스냅샷: 서버 디스크 백업
### 스토리지 서비스
데이터 보관, 백업, 파일 서버, 재해 복구 등의 용도로 이용됩
#### S3(Simple Storage Service)
- 여러 개의 데이터 센터에 데이터를 분산 저장
#### EBS(Elastic Block Store)
- 엄격한 응당 시간이 요구되는 데이터베이스 용도
- 블록 단위 액세스
#### EFS(Elastic File System)
- 기업의 파일 서버, 파일 단위 액세스

### 네트워크 서비스
#### Amazon VPC (Virtual Private Cloud)
- AWS위에 가상네트워크를 만들어, 개인 클라오드 처럼 사용할 수 있는 서비스
#### 보안 기능
- 필터링을 통해 불필요한 통신 차단
- 보안 그룹: 송수신 정책 설정 -> 가상 서버에 대한 접속 제어

#### Amazon Route 53
- DNS 서비스

### 데이버테이스 서비스
#### RDBMS
- Amazon RDS : MySQL, PsotgreSQL, Oracle Database...
- Amazon RDS for Aurora
#### 데이터웨어하우스
- Amazon Redshift: 페타바이트급 데이터 처리
#### NoSQL
- Amazon DynamoDB
 
## 주요 클라우드 서비스 업체
[#](https://docs.google.com/presentation/d/1XGiCDbj4pwtAkkSKcif9ywNArbNHwnRPKxhR6Mu4hG4/edit#slide=id.g4164461e5c_0_137)
- Amazon Web Services (AWS)
- Microsoft Azure
- IBM SoftLayer
- IBM Bluemix
- Google Cloud Platform
  
# AWS 실습
## IAM (Identity and Access Management) [#](https://docs.google.com/presentation/d/1QqFjKwDqW-SrY54v-0lMignTaIVqSr4GXYqAr9ygMeA/edit#slide=id.g4121047eff_0_10)
## MFA (Multi-Factor Authentication [#](https://docs.google.com/presentation/d/1QqFjKwDqW-SrY54v-0lMignTaIVqSr4GXYqAr9ygMeA/edit#slide=id.g4121047eff_0_43)
## VPC(Virtual Private Cloud) [#]()
## 보안 그룹

## AWS SDK [#](https://docs.google.com/presentation/d/1m1Job6Sljgrnu3Ug-CrVeuEIQFkVEY6kk-2XqvP7WcQ/edit#slide=id.g36182664e1_0_0)
- 재사용 가능 코드를 활용해 AWS 자원을 관리하는 가장 좋은 방법
- 매우 간단한 명령을 사용해 인프라 자동화 및 에러 처리 가능

## CLI [#](https://docs.google.com/presentation/d/1m1Job6Sljgrnu3Ug-CrVeuEIQFkVEY6kk-2XqvP7WcQ/edit#slide=id.g42f7820107_0_5)
- Command Line Interface
- AWS 서비스와 상호작용하는 명령을 제공하는 AWS SDK for Pyton(Boto)을 기반으로 구축된 Open source tool
- Terminal 프로그램에서 AWS management console이 제공하는 모든 기능 사용 가능

# AWS 이론
> Amazon Elastic Compute Cloud
## Amazon EC2 [#](https://docs.google.com/presentation/d/10ZPxGJfgzwNfpYyVO_33Wc_nUzi08w2XFCo80WpDnKY/edit#slide=id.g4121859ba7_0_7)
참고: https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/concepts.html
## 키워드

- 리전 & 가용영역
- 탄력적 IP 주소 (Elastic IP Address) [#](https://docs.google.com/presentation/d/10ZPxGJfgzwNfpYyVO_33Wc_nUzi08w2XFCo80WpDnKY/edit#slide=id.g41338284bd_1_41)
- Amazon EBS
- 루트 디바이스 볼륨 (Root devide volume) [#](https://docs.google.com/presentation/d/10ZPxGJfgzwNfpYyVO_33Wc_nUzi08w2XFCo80WpDnKY/edit#slide=id.g412c12e449_0_18)
- EBS(Elastic Block Storage) [#](https://docs.google.com/presentation/d/10ZPxGJfgzwNfpYyVO_33Wc_nUzi08w2XFCo80WpDnKY/edit#slide=id.g41338284bd_1_162)
- 인스턴스 스토어 (Instance store) [#](https://docs.google.com/presentation/d/10ZPxGJfgzwNfpYyVO_33Wc_nUzi08w2XFCo80WpDnKY/edit#slide=id.g41338284bd_1_71)
- AMI (Amazon Machine Image) [#](https://docs.google.com/presentation/d/10ZPxGJfgzwNfpYyVO_33Wc_nUzi08w2XFCo80WpDnKY/edit#slide=id.g412c12e449_0_6)

# LAMP 실습 [#](https://docs.google.com/presentation/d/1Kio5IvUUcU-9h_yMRFugaES7v8BI7l8dyg5DR25IBEg/edit#slide=id.p)
참고: https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/ec2-lamp-amazon-linux-2.html
## 키워드
- LAMP(Linux Apache MySQL PHP)
- 과정
    1. LAMP 서버 준비
    2. LAMP 서버 테스트
    3. 데이트베이스 서버 보안 설정
    4. phpMyAdmin 설치

# WordPress 블로그 호스팅 [#](https://docs.google.com/presentation/d/1YRqtwCKFfBAExnKBHCiVXv6008kf0AhDjNdIzkBwcpU/edit#slide=id.p)
참고: https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/hosting-wordpress.html
## 키워드
- 과정
    1. WordPress 설치
    2. 데이터베이스 사용자 및 데이터베이스 생성
    3. wp-config.php 파일 생성 및 편집
    4. Wordpress 파일을 Apache 문서 루트 아래 설치
    5. Wordpress에서 permalinks를 사용
    6. Apache 웹 서버에 대한 파일 권한 수정
    7. WordPress 설치 스크립트 실행
  
# Host Static Website on S3 [#](https://docs.google.com/presentation/d/13zaEjroXrv2zG0xY7Q39RjcBhD388HG-1RM_y1fiVHw/edit#slide=id.p)
참고: https://aws.amazon.com/ko/getting-started/projects/host-static-website/
## 키워드
- S3
- Amazon CloudFront 
- CND (Contents Delivery Network)
- 리전 & 가용영역([AWS 문서](https://docs.aws.amazon.com/ko_kr/AWSEC2/latest/UserGuide/using-regions-availability-zones.html#concepts-regions-availability-zones))

# Elastic Load Balancer [#](https://docs.google.com/presentation/d/10peH8tJBk9teTWxsbvP2BNM5AuGPRDnsgOz5RM5pIgU/edit#slide=id.g448ff704fa_0_0)
## 키워드
- VPC (Virtual Personal Cloud)
- CIDR (Class Inter-Domain Routing)
    - 10.0.0.0/16
    - 10.0.0.1/24, - 10.0.0.2/24, ...
- 
---

# 강의안
#### 1주차
- [강의 개요](https://drive.google.com/open?id=1zbrCzcLV8x88qysaWdH4ebbCIgtDf6ePnPB3krdtkM8)

#### 2주차
1. [클라우드 컴퓨팅 소개](https://docs.google.com/presentation/d/1DssmdpDCAlVKvQ9mPn6oU-nBeI4A6BLMZE1J2WZ8yds/edit?usp=sharing)
2. [클라우드 컴퓨팅 서비스](https://docs.google.com/presentation/d/1XGiCDbj4pwtAkkSKcif9ywNArbNHwnRPKxhR6Mu4hG4/edit?usp=sharing)

#### 3주차
1. [PPT] [AWS 실습 1-1 - Free-tier 및 계정보안](https://drive.google.com/open?id=1QqFjKwDqW-SrY54v-0lMignTaIVqSr4GXYqAr9ygMeA)
    1. [동영상] [IAM user 및 MFA 인증](https://cms.hansung.ac.kr/em/5bac62e36619c)
    2. [동영상] [Free-tier 및 결제 알람 설정](https://cms.hansung.ac.kr/em/5bac77bf912f5)
2. [PPT] [AWS 실습 1-2 - EC2 service](https://drive.google.com/open?id=1OxM85IEsh1WgMGY1qWKEKbto599LgYXnfT08d1kBIAU)
    1. [동영상] [EC2 시작 - 키페어 생성, VPC, 보안그룹](https://cms.hansung.ac.kr/em/5bac81d1f8d0b)
    2. [동영상] [Linux EC2 생성 및 연결](https://cms.hansung.ac.kr/em/5bac9566d0bf1)
    3. [동영상] [Windows EC2 생성 및 연결](https://cms.hansung.ac.kr/em/5baca274b0d0)

#### 5주차
1. [AWS SDK & CLI](https://drive.google.com/open?id=1m1Job6Sljgrnu3Ug-CrVeuEIQFkVEY6kk-2XqvP7WcQ)
2. [AWS 이론 1 - EC2 Service](https://drive.google.com/open?id=10ZPxGJfgzwNfpYyVO_33Wc_nUzi08w2XFCo80WpDnKY) 
3. AWS 실습 1 (계속) - EC2 Service

#### 6주차
1. AWS 실습 2-1 - LAMP 웹서버 설치
- [자료](https://drive.google.com/open?id=1Kio5IvUUcU-9h_yMRFugaES7v8BI7l8dyg5DR25IBEg)
- [동영상1](https://cms.hansung.ac.kr/em/5bb6f50ef8eb2)
- [동영상2](https://cms.hansung.ac.kr/em/5bb6f4ab0f1e0)
2. AWS 실습 202 - WordPress 블로그 호스팅
- [자료](https://drive.google.com/open?id=1YRqtwCKFfBAExnKBHCiVXv6008kf0AhDjNdIzkBwcpU)
- [동영상](https://cms.hansung.ac.kr/em/5bb6f26cbb788)

#### 7주차
1. [AWS 실습 3-1 - WordPress Website](https://drive.google.com/open?id=1Hdbm2h_Uixo9nB-m78O4Xb7VNWyEezseR23IZ6TOErw)
2. [AWS 실습 3-2 - 정적 웹 사이트 호스팅](https://docs.google.com/presentation/d/13zaEjroXrv2zG0xY7Q39RjcBhD388HG-1RM_y1fiVHw/edit?usp=sharing)

#### 8주차
[AWS 실습 4: Elastic Load Balancer -  AWS 실습 4-1-ELB](https://docs.google.com/presentation/d/10peH8tJBk9teTWxsbvP2BNM5AuGPRDnsgOz5RM5pIgU/edit)