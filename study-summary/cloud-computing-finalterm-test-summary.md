# 중요 목록
1. 가상화 [#](#1-가상화)
2. 클라우드 컴퓨팅을 위한 기술들 [#](#2-클라우드-컴퓨팅을-위한-기술들)
3. 클라우드 업체가 제공하는 대표적 서비스들 [#](#3-클라우드-업체가-제공하는-대표적-서비스들)
4. Azure에서 Applcation을 Hosting 하는 방식들 [#](#4-azure에서-application을-hosting-하는-방식들)
5. AWS의 AS와 ELB에 대하여 [#](#5-AWS의-AS와-ELB에-대하여)
6. 기타 Cloud computing에 대한 일반적 내용 [#](#6-기타-Cloud-computing에-대한-일반적-내용)
---
# 1. 가상화
- 물리적 자원의 추상화라는 의미로, 하나의 물리적 자원을 논리적으로 분할하여 사용하고나 물리적으로 분리된 여러 자원을 논리적으로 통합하는 기술을 말한다.
- 클라우드 컴퓨팅의 핵심 기술이며, 서버 가상화, 네트워크 가상화, 스토리지 가상화 등을 통하여 사용자들에게 여러 자원을 제공한다.


# 2. 클라우드 컴퓨팅을 위한 기술들
## 기반 기술 [#](http://gotocloud.co.kr/?p=615) 
- 서버 가상화
  - 서버 가상화는 독립적인 CPU, 메모리, 네트워크 및 운영 체제를 갖는 여러 대의 가상 머신(Virtual Machine)들이 물리적인 서버의 자원을 분할해서 사용하는 기술을 의미한다. 물리적 하드웨어 상에서 가상 머신에 대한 운영을 담당하는 플랫폼을 하이퍼바이저(Hypervisor)라고 통칭한다.
- 네트워크 가상화
  - 클라우드 환경에서는 다양한 사용자가 원하는 때에 원하는 IT 자원을 제공받게 되는데, 이 때 각 사용자 별로 네트워크를 격리하고 격리된 네트워크가 인터넷과 통신을 하도록 하는 가상 라우터가 가장 중요한 역할을 하게 된다.
  - 가상으로 격리된 네트워크와 서브넷을 제공한다.
    - 관련 리소스의 그룹화 및 격리가 가능하다. 여기에는 자체 전용 IP 주소 공간 할당, 서브넷 생성, 라우팅 테이블 생성, 상태 유지 방화벽 구성이 포함되며, 
- 분산 스토리지 및 파일 동기화(스토리지 가상황)

## 요소 기술 [#](https://docs.google.com/presentation/d/1DAgEePJdq_QlaPoSd3fkUBFo7-Oekwyv0V6I9WfbBdw/edit#slide=id.g27c33833d3_0_0)
- 가상화 기술
- 클러스터 관리
- 분산 시스템
- 서비스 지향 구조
  - 클라우드 컴퓨팅은 서비스지향 아키텍처를 따르며, 사용자에게 서비스 단위로 표준화된 자원 이용 방법을 제공한다.
- Saas 플랫폼
- 보안

## 단어
- 프로비저닝
  - 프로비저닝(provisioning)은 사용자의 요구에 맞게 시스템 자원을 할당, 배치, 배포해 두었다가 필요 시 시스템을 즉시 사용할 수 있는 상태로 미리 준비해 두는 것을 말한다.


# 3. 클라우드 업체가 제공하는 대표적 서비스들
## 클라우드가 제공하는 다양한 서비스 [#](https://docs.google.com/presentation/d/1XGiCDbj4pwtAkkSKcif9ywNArbNHwnRPKxhR6Mu4hG4/edit#slide=id.g4164461e5c_0_83)
  - 가상 서버 (virtual server)
    - 로드 밸런스 (load balance) - 이중화, 부하 분산
    - 오토 스케일링 (auto scaling)
  - 스토리지 서비스 (storage)
    - 데이터 보관, 백업, 복구기능 제공
  - 네트워크 서비스
    - VPN, 전용선, 보안, DNS 기능 제공
  - 데이터베이스
    - RDBMS, NoSQL, 데이터 웨어하우스
## 클라우드 서비스 모델
![](./image/service-model.png)

# 4. Azure에서 application을 hosting 하는 방식들 [#](https://docs.microsoft.com/ko-kr/azure/guides/developer/azure-developer-guide)
- 전체 인프라를 VM으로 관리
- Azure에서 제공하는 플랫폼 관리 기능 사용
- 코드 실행만 호스트하는 Serverless 프레임워크
### Azure Virtual Machines
- 응용 프로그램 인프라를 완전히 제어하거나 온-프레미스 응용 프로그램 워크로드를 변경할 필요 없이 Azure에 마이그레이션하려는 경우 Virtual Machines를 사용한다.
- IaaS와 PaaS를 제공한다.
### Azure App service
- 웹 응용 프로그램, REST API 및 모바일 백 엔드를 호스팅 하는 서비스
- 웹 기반 프로젝트를 가장 빠른 경로로 게시할 때 이용하며, 인프라를 관리할 필요 없이 선택한 프로그래밍 언어로 웹 응용 프로그램을 빌드하고 호스팅 할 수 있다.
- App Service를 사용하면 웹앱을 쉽게 확장하여 모바일 클라이언트를 지원하고 사용된 REST API를 쉽게 게시할 수 있으며 소셜 공급자, 트래픽 기반 자동 크기 조정, 프로덕션 환경에서 테스트, 연속 배포 및 컨테이너 기반 배포를 사용하여 인증을 제공한다.
- 다양한 DevOps 도구를 지원한다.
### Azure Service Fabric
- 손쉽게 빌드, 패키지, 배포 및 확장 가능하고 안정성이 뛰어난 마이크로 서비스를 관리하는 분산된 시스템 플랫폼
- 배포된 응용 프로그램의 프로비전, 배포, 모니터링, 업그레이드/패치 및 삭제를 위한 포괄적인 응용 프로그램 관리 기능을 제공한다.
### Azure Functions
- HTTP 요청, Webhook, 클라우드 서비스 이벤트 또는 일정에 따라 작성한 코드(Function)만 실행되는 Serverless 플랫폼
- 코드를 실행하기 위해 전체 프로그램 또는 인프라를 빌드, 관리하지 않아도 되며, 오직 비지니스 로직만 구현된 코드만 작성하면 된다.


# 5. AWS의 AS와 ELB에 대하여
### ELB 기능 및 특징
- 트래픽 분산
- 사용자 세션을 특정 인스턴스에 고정
- **Auto Scaling**
- 인스턴스의 상태를 자동으로 감지해서 오류가 있는 시스템은 배제
- SSL 암호화 지원
- IPv4, IPv6 지원
- 모니터링 기능
### Auto Scaling
- 트래픽량에 따라 EC2의 인스턴스 규모를 자동으로 확대(scale out)/축소(scale in)하는 기능
- 미리 만들어진 이미지(AMI)를 이용해서 자동으로 인스턴스 생성한다.
- 처리량에 빠르게 대응 가능하며 확대/축소에 대한 다양한 조건 설정 가능하다

# 6. 기타 cloud computing에 대한 일반적 내용
- 클라우드 컴퓨팅의 용도
  - 새로운 앱 및 서비스 만들기
  - 데이터 저장, 백업 및 복구
  - 웹 사이트 및 블로그 호스팅
  - 오디오 및 비디오 스트리밍
  - 주문형 소프트웨어 제공
  - 데이터의 패턴을 분석하여 예측

# 강의 자료
#### 1주차
- [강의 개요](https://drive.google.com/open?id=1zbrCzcLV8x88qysaWdH4ebbCIgtDf6ePnPB3krdtkM8)

#### 2주차
1. [클라우드 컴퓨팅 소개](https://docs.google.com/presentation/d/1DssmdpDCAlVKvQ9mPn6oU-nBeI4A6BLMZE1J2WZ8yds/edit?usp=sharing)
2. [클라우드 컴퓨팅 서비스](https://docs.google.com/presentation/d/1XGiCDbj4pwtAkkSKcif9ywNArbNHwnRPKxhR6Mu4hG4/edit?usp=sharing)

#### 3주차
- [AWS-Introduction](https://docs.google.com/presentation/d/1dyjXfrV6JngfhvhR1TAjZ0c6I_u_S0fxou72sLW2F-8/edit#slide=id.p)
- [AWS, AWS Educate 계정 가입](https://drive.google.com/file/d/0B0rw9HlzTK7qQ1NRV3cxQlczQy1GaDU4eWZqZ1VYUno4Skxz/view)
- [AWS Educate 설명](https://docs.google.com/presentation/d/1OVzDTBh53JfVI78bZSxtrM4woYgUhPIzSWoPWXJjy3w/edit#slide=id.p)

#### 4주차 
AWS 실습 1
1. [AWS 실습 1-1 - Free-tier 및 계정보안](https://drive.google.com/open?id=1QqFjKwDqW-SrY54v-0lMignTaIVqSr4GXYqAr9ygMeA)
   1. [IAM user 및 MFA 인증](https://cms.hansung.ac.kr/em/5bac62e36619c)
   2. [Free-tier 및 결제 알람 설정](https://cms.hansung.ac.kr/em/5bac77bf912f5)
2. [AWS 실습 1-2 - EC2 service](https://drive.google.com/open?id=1OxM85IEsh1WgMGY1qWKEKbto599LgYXnfT08d1kBIAU)
   1. [EC2 시작 - 키페어 생성, VPC, 보안그룹](https://cms.hansung.ac.kr/em/5bac81d1f8d0b)
   2. [Linux EC2 생성 및 연결](https://cms.hansung.ac.kr/em/5bac9566d0bf1)
   3. [Windows EC2 생성 및 연결](https://cms.hansung.ac.kr/em/5baca274b0d0)


#### 5주차
AWS 실습 2
1. [AWS SDK & CLI](https://drive.google.com/open?id=1m1Job6Sljgrnu3Ug-CrVeuEIQFkVEY6kk-2XqvP7WcQ)
2. [AWS 이론 1 - EC2 Service](https://drive.google.com/open?id=10ZPxGJfgzwNfpYyVO_33Wc_nUzi08w2XFCo80WpDnKY)
3. AWS 실습 1 (계속) - EC2 Service

#### 6주차
AWS 실습 2
1. AWS 실습 2-1 - LAMP 웹서버 설치
   - [자료](https://drive.google.com/open?id=1Kio5IvUUcU-9h_yMRFugaES7v8BI7l8dyg5DR25IBEg)
   - [동영상1](https://cms.hansung.ac.kr/em/5bb6f50ef8eb2)
   - [동영상2](https://cms.hansung.ac.kr/em/5bb6f4ab0f1e0)
2. AWS 실습 202 - WordPress 블로그 호스팅
   - [자료](https://drive.google.com/open?id=1YRqtwCKFfBAExnKBHCiVXv6008kf0AhDjNdIzkBwcpU)
   - [동영상](https://cms.hansung.ac.kr/em/5bb6f26cbb788)

#### 7주차
AWS 실습 3
1. [AWS 실습 3-1 - WordPress Website](https://drive.google.com/open?id=1Hdbm2h_Uixo9nB-m78O4Xb7VNWyEezseR23IZ6TOErw)
2. [AWS 실습 3-2 - 정적 웹 사이트 호스팅](https://docs.google.com/presentation/d/13zaEjroXrv2zG0xY7Q39RjcBhD388HG-1RM_y1fiVHw/edit?usp=sharing)

#### 8주차

[AWS 실습 4: Elastic Load Balancer -  AWS 실습 4-1-ELB](https://docs.google.com/presentation/d/10peH8tJBk9teTWxsbvP2BNM5AuGPRDnsgOz5RM5pIgU/edit#slide=id.p)

#### 10주차

1. [AWS Q&A](https://drive.google.com/open?id=1_7kXrcMm9BByYPi6Eh75R4vs8Ywv3IEVM0p3q8HTYOs)
2. [Cloud Architecture](https://drive.google.com/open?id=1iIH7vEjLubIFgcOutkuZJQKPORhpcSnY15iHUz5DwwI)
3. [Cloud System 요소기술](https://drive.google.com/open?id=1DAgEePJdq_QlaPoSd3fkUBFo7-Oekwyv0V6I9WfbBdw)
4. [Cloud를 실현하는 기술](https://drive.google.com/open?id=1x93GVLFWGl9jFUqAc7FFapZ8-jMTUpuOH7mcVjBZb0o)
5. [AutoScaling 실습 1](https://drive.google.com/open?id=1_PEnwC_3Dq5k3lyyMx_PYaJP_6xlSohS7C9pjOuoNaw)

#### 11주차

AWS 이론
- [Auto Scaling - AWS 이론 2 - AutoScaling](https://docs.google.com/presentation/d/1-06xEGxuPBNESkDFBmrUFWh4n9W9fzJhz8THaCxFii8/edit)
- [Elastic Load Balancing - AWS 이론 3 - ElasticLoadBalancing](https://docs.google.com/presentation/d/1KHn83oEOsuv7AUHGQxOisYIO1HgfT6ip5SRBKOzRmUM/edit#slide=id.p)
- [CloudWatch - AWS 이론 4 - CloudWatch](https://docs.google.com/presentation/d/16uFPuV9MGQhy1iEKAGP0vvb1ZkbvnTtdwT5QrAywA5E/edit#slide=id.p)
- [RDS - AWS 이론 5 - RDS](https://docs.google.com/presentation/d/1l8oLe5xvDwaOjXvUPLOp9K4sSNKtnDCigfilRpujQbE/edit#slide=id.p)

AWS 실습

- [Auto Scaling 1 - AWS 실습 6 - AutoScaling2](https://docs.google.com/presentation/d/1_PEnwC_3Dq5k3lyyMx_PYaJP_6xlSohS7C9pjOuoNaw/edit#slide=id.p)
- [Auto Scaling 2 -AWS 실습 7 - AutoScaling3](https://docs.google.com/presentation/d/1qFwdR0H-JkT3Y3TY5l37V8ppZSIDvtG5BUiD4WhRzpk/edit#slide=id.p)
- [RDS 1 - AWS 실습 7 - RDS1](https://docs.google.com/presentation/d/1QtkOvAe3m3vMpi2LgVtTxQa78JBkIE6GUj8ysi7ZQ5w/edit#slide=id.p)
- [RDS 2 - AWS 실습 7 - RDS2](https://docs.google.com/presentation/d/1MwToqsGOc6TTERsbWopog0wvp_3PQGs-3EZKr3zndKY/edit#slide=id.p)


#### 12주차

- [Azure 이론 1 - Introduction - Azure 이론 1 - Introduction](https://docs.google.com/presentation/d/1tgG_I7Up3cWJEQO1-1BsjQb9cNsyePBCQ1vEoTB6sgg/edit)
- [Azure 이론 2 - Functions - Azure 이론 2 - Functions](https://docs.google.com/presentation/d/1k9ez6dip8t0s7DYLWTA9KYmnIIPX14VeT_xcHRvk5lk/edit#slide=id.p)
- [Azure 실습 1 - VM - Azure 실습 1 - VM](https://docs.google.com/presentation/d/13PlE05l3DBz394F1gNUHx2u26NLSUJwblx6noBcePRA/edit#slide=id.p)
- [Azure 실습 2 - App Service - Azure 실습 2 - AppService](https://docs.google.com/presentation/d/14QObc9MZqhmgi7uJYUgt0tCuxCG-n2VjFrAVA26jXfI/edit#slide=id.p)
- [Azure 실습 3 - Functions - Azure 실습 3 - Function](https://docs.google.com/presentation/d/19uGh_y-UrPwLoAV_pfRhJGKiCsKaJS2Ef4UBX6XdPiY/edit#slide=id.p)