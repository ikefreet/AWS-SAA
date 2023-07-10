# AWS-SAA
## IAM
**IAM : Identify and Access Management**

IAM 보안을 위하여 MFA를 이용한 설정 가능
- 하드웨어나 스마트폰, 컴퓨터 애플리케이션을 통한 2차 인증 시스템
- 타사 3rd party 하드웨어로도 가능

**AWS CLI**
- CLOUDSHELL을 통해 웹페이지에서 터미널 사용 가능
- CLOUDSHELL을 지원하는 리전이 있고 지원하지 않는 리전이 있다.

**IAM Role**
- 서비스에 역할을 부여
- EC2 서비스에 IAM Role을 부여해 AWS 다른 서비스에 접근할 수 있도록 한다.

**IAM Policy**
- Json 파일로 구성되어 있으며 정책을 생성하고 IAM 자격 증명(사용자, 사용자 그룹 또는 역할) 또는 AWS 리소스에 연결하여 AWS에서 액세스를 관리한다.

<br><br>

## EC2
**EC2 : Elastic Compute Cloud = Infrastructure as a Service**
- 부트스트래핑 : 부팅 작업을 자동화하는 것. 초기 인스턴스 시자 시 필요한 유저 데이터(관련 라이브러리, 소프트웨어 업데이트... 등), 루트 계정에서 수행된다.
- 인스턴스를 중지했다가 다시 시작하면 IPV4 Public IP는 바뀌지만 Private IP는 바뀌지 않는다.
- 인스턴스 Type
  - m5.2xlarge
  - m : 인스턴스 클래스
  - 5 : 세대 (장비 세대)
  - 2xlarge : 인스턴스 클래스의 사이즈

**보안 그룹**
-  EC2의 방화벽, VPC와 리전에 묶여있으며 상속의 개념을 갖고 있다. 여러 보안그룹을 한 개의 EC2 인스턴스에 붙일 수 있고 하나의 보안그룹을 여러 인스턴스에 붙이는 것도 가능하다.
