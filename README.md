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

**EC2 구매전략**
- 온디맨드(On-Demand) : 필요할 때 바로 이용. 하지만 비용이 비싸다. 윈도우는 1분 뒤 초단위로 청구하지만 다른 플랫폼은 1시간 단위로 청구한다. 단기적이고 중단없는 워크로드가 필요하거나 얼마나 사용할 지 알 수 없을 때 사용
- 예약형(Reserved) : 온디맨드에 비해 72% 저렴하다. 특정 인스턴스 속성을 예약한다. 1/3년단위로 예약하며 선결제나 부분결제가 가능하다.
- 절약형(Saving Plan) : 예약형처럼 장기 1/3년단위로 하며 특정 인스턴스 패밀리와 리전으로 고정된다. 시간당 비용을 확정하고 이용한다. 온디맨드에 비해 72% 저렴하다. 절약형의 한도를 다 사용하면 온디맨드 가격으로 책정한다.
- 스팟(Spot) : 지불최대 한도를 지정하고 그 금액을 초과하면 인스턴스가 종료된다. 가장 비용효율적이다. 아주 중요한 작업이나 DB작업에는 적합하지 않다.
- 전용 호스트(Dedicated Host) : 실제 물리적 서버를 수령하는 형태. 온디맨드처럼 초당 지불 혹은 1/3년단위 예약형으로도 가능하다. 라이센스 모델, 법규준수를 위해 사용되며 가장 비싼 옵션이다.
- 전용 인스턴스(Dedicated Instance) : 사용자의 전용 하드웨어에서 실행되는 인스턴스. 해당 계정의 다른 인스턴스와 함께 하드웨어를 공유할 수 있고 하드웨어에 인스턴스를 배치하는데에 대한 통제권은 없다.

**IPV4**
- Public IP
  - Public끼리 서로 통신이 가능하다.
  - 기기가 인터넷(WWW)에 식별되는 것이므로 유일해야한다.
- Private IP
  - Private IP끼리만 통신할 수 있고 외부와 통신하려면 Public IP를 가진 게이트웨이를 통해 통신해야한다.
  - IP 주소는 Private 망 내에서만 유일하면 된다.
- Elastic IP
  - EC2 인스턴스의 Public IP는 중지했다 다시 가동하면 IP 주소가 바뀐다. 이러한 것을 방지하기 위해 Elastic IP를 사용하여 Public IP를 고정한다.
  - 계정당 디폴트로 최대 5개의 Elasitc IP를 가질수 있다.
  - 구조적으로 별로 좋지 않기 때문에 잘 사용되지는 않는다.

**EC2 배치 그룹**
- EC2 인스턴스가 AWS 인프라에 위치하는 것을 제어하기 위해 사용한다.
- Cluster : 단일 AZ에 인스턴스들을 묶는 것
  - Same Rack, Same AZ로 빠르다.
  - 하드웨어에 문제가 발생하면 모든 실패가 전파된다. 하지만 빨리 수행해야 하는 빅데이터나 좋은 응답 속도로 고효율 업무를 수행할 때 사용
- Spread : 인스턴스를 여러 다른 하드웨어에 최대한 멀리 분산시키는 것. AZ마다 최대 7개의 인스턴스만 가능하다. 크리티컬한 앱일 경우 사용된다.
  - 실패 위험을 최소화하기 위하여 모든 EC2 인스턴스가 다른 하드웨어에 배치된다.
  - 7개라는 인스턴스 갯수가 제한으로 인해 그룹 규모에 제한이 있다.
  - 가용성을 극대화하고 위험성을 최소화하는 특징이 있다.
- Partition : Spread처럼 여러 파티션에 분산하지만 다른 Rack에 배치돼 AZ마다 100개 이상 배치 가능하다.
  - AZ당 여러 파티션을 둘 수 있고 각 파티션에 여러 인스턴스를 배치할 수 있다.
  - 각 파티션은 AWS 하드웨어 Rack을 의미하며 각 파티션의 위험은 독립적이다.
  - EC2가 어느 파티션에 있는지 알기 위해 메타데이터 서비스를 이용하여 접근 및 확인 가능하다.

**ECS Volume**
- Elastic Block Store의 약자로 인스턴스 실행 중 연결 가능한 네트워크 드라이브로 인스턴스가 종료되어도 이전 EBS Volume을 마운트하면 데이터를 다시 받을 수 있다.
- 물리 드라이브가 아닌 네트워크 드라이브
- EC2 인스턴스 생성 시 Delete on terminate 옵션이 존재하며 이를 통해 인스턴스가 종료시 EBS Volume 역시 디폴트로 삭제된다. 삭제되지 않고 유지하기를 원하는 경우 이 옵션을 해제한다.
- Type
  - gp2/gp3 (SSD) : 다양한 워크로드에 대해 가격과 성능의 절충안.
      - gp2 : 최대 3000IOPS
      - gp3 : 기본 성능 3000IOPS, 초당 125 MiB/s throughput
  - io1/io2 (SSD) : 고성능의 SSD이고 mission-critical하고 저지연으로 좋은 성능을 내는 워크로드에 적합
  - st1(HDD) : 저비용의 HDD 볼륨으로 잦은 접근과 처리량이 많은 워크로드에 적합. Max Throughput : 500 MiB/s
  - sc 1(HDD) : 가장 싼 HDD 볼륨으로 접근 빈도가 낮은 워크로드를 위한 설계. Max Throughput : 250 MiB/s
    
- SSD
  - EC2 인스턴스의 Booting Volume으로 사용할 수 있다.
- HDD
  - EC2 인스턴스의 Booting Volume으로 사용할 수 없다.
  - 125Mib to 16TiB


- EBS Snapshot
- EBS Volume을 특정 시점에 대해 백업하는 기능
- 다른 AZ 혹은 다른 리전으로 백업 가능
- 기능
  - EBS snapshot Archive : 스냅샷을 archive tier로 옮겨 75% 싸게할 수 있고 아카이브된 스토리지를 복원하는데 24~72시간 소요된다.
  - Recycle Bin for EBS snapshots : EBS 스냅샷을 삭제하는 경우 영구 삭제 대신 휴지통에 일정기간 보관하는 것. 보관되므로 실수로 삭제해도 복원이 가능하다.
  - Fast Snapshot Restore(FSR) : 스냅샷을 전체 초기화해 첫 사용에서의 지연시간이 없게한다. 스냅샷이 아주 크고 EBS Volume 혹은 EC2 인스턴스를 빠르게 초기화할 때 유용하지만 비용이 비싸다.
- EBS Encryption
  - EBS Volume을 암호화하는 것
    - 저장 데이터가 Volume 내부에 암호화된다.
    - 인스턴스와 Volume 간의 데이터 전송도 암호회된다.
    - Snapshot도 암호회되며 Snapshot으로 생성한 볼륨도 암호화된다.
  - 암호화 되지 않은 EBS Volume 암호화 과정
    1. Volume의 EBS Snapshot 생성
    2. EBS Snapshot을 복사하며 암호화
    3. Snapshot으로 새 EBS Volume 생성
    4. 암호화된 Volume을 인스턴스에 연결

**AMI**
- Amazon Machine Image로 EC2 인스턴스를 통해 만든 이미지를 말한다.
- EC2에 설정하고자 하는 소프트웨어나 설정을 pre-package하기 때문에 빠른다.
- 리전 사이 복제가 가능

**Amazon EFS**
- Elastic File System
  - 여러 EC2에 마운트되는 NFS(Network File System)을 관리
  - EFS는 Multi-AZ에서 EC2 인스턴스들에 작용된다.
  - 가용성과 확장성이 뛰어나지만 gp2 EBS Volume에 비해 3배 정도 비싸다. 사용량만큼 지불하므로 미리 용량 프로비저닝할 필요가 없다.
  - Linux 기반 AMI에서만 사용가능

**EBS VS EFS**
- EBS
  - 한 개의 인스턴스에만 연결되고 하나의 AZ에 종속된다.
  - EBS Volume을 다른 AZ로 이주시키고자 할 때
    - Snapshot 생성 -> EBS Snapshot을 다른 AZ에 저장
    - EBS 백업은 IO를 사용하므로 앱이 큰 트래픽을 사용할 시 적합하지 않다.
- EFS
  - 수 백개의 인스턴스들을 여러 AZ에 생성하고 연결할 수 있다.
  - 파일을 공유하는 방식
  - Linux 인스턴스에서만 가능
  - EBS에 비해 비용이 비싸다.

<br><br>
## 고가용성(High Availability) & 스케일링(Scalability)
- Scalability & High Availability
  - Vertical Scalability(수직적 스케일링)
    - 인스턴스 자체의 크기(사이즈 혹은 사양)를 늘리는 것
    - 분산되지 않은 데이터베이스 같은 시스템에서 적합하다. (RDS, ElasticCache)
  - Horizontal Scalability (수평적 스케일링)
    - 인스턴스 혹은 시스템의 개수를 늘리는 것
    - 일을 분산 처리하는 시스템

- High Availability
  - 데이터 센터에서의 손실에서 살아남는 것이 목표. 하나가 중지되어도 나머지가 가동하여 정상적으로 운용되는 것
  - Auto Scaling Group multi AZ 혹은 Load Balancer multi AZ를 이용하면 고가용성

- Load Balancing
  - Load Balancing이란 서버 혹은 서버 집합으로 트래픽을 백이나 다운스트림 EC2로 전달하는 역할을 한다.
  - 목적
    -  트래픽 분산
    -  앱에 단일 접근 포인트 DNS를 통해 노출할 수 있다.
    -  정기적인 Health Check를 통해 하위 인스턴스들의 failure에 대처할 수 있다.
    -  웹 사이트에 SSL termination(HTTPS)를 제공한다.
    -  가용영역 내 고가용성을 가질 수 있다.
    -  클라우드 내에서 Private Traffic과 Public Traffic을 분리할 수 있다.
  - ELB(Elastic Load Balancer)를 사용하는 이유
    - 관리형 로드 밸러서로 AWS가 관리하며 어떤 경우에도 작동할 것을 보장함.
    - 고가용성, 업그레이드 유지 및 관리를 전부 AWS가 한다.
    - 연결할 수 있는 AWS 서비스가 많다.
    - 종류
      - ALB(Application Load Balancer)
        - 7계층의 HTTP 전용 앱단 Load Balancer
        - 다수의 HTTP 앱들이 장비간 라우팅에 사용됨
        - 다수의 앱이 구동되는 동일 장비의 로드 밸런싱 지원
        - Redirect 지원 (HTTP -> HTTPS)
        - 다른 타켓 그룹에 대한 라우팅 테이블
          - URL 내 경로에 따른 라우팅
          - URL 내 호스트 이름으로 라우팅
          - 쿼리스트링 & 헤더에 따른 라우팅
        - 마이크로 서비스 혹은 컨테이너 기반 애플리케이션에서도 사용하기 적합하다.
  
      - NLB(Network Load Balancer)
        - 4계층(L4) Load Balancer로 TCP와 UDP를 다룬다. HTTP를 다루는 L7보다 하위 계층
        - 성능이 매우 좋음. 초당 수백만건 요청 처리 가능. ALB에 비해 지연시간이 짧음
          - ALB = 400ms, NLB = ~100ms
          - AZ마다 1개의 static IP를 갖고 Elastic IP 할당을 지원
        - 백엔드(HTTP) <-> 프론트(TCP) 혹은 백엔드(TCP) <-> 프론트(TCP) 일 때 사용
        - 대상 그룹
          - EC2 인스턴스
          - NLB가 TCP 또는 UDP 트래픽을 EC2 인스턴스로 리다이렉트하는 것도 가능
          - IP Address
      - GWLB(Gateway Load Balancer)
        - 배포 및 확장과 AWS의 타사 네트워크 가상 어플라이언스를 위해 사용됨.
        - 모든 트래픽이 방화벽을 통과하게 하거나 침입 탐지 및 방지 시스템에 사용된다.
        - - 대상 그룹
          - EC2 인스턴스
          - IP Address
  - Sticky Sessions (Session Affinity in ELB)
    - LB에 2가지 요청을 수행하는 클라이언트가 요청에 응답하기 위해 백엔드에 동일한 인스턴스를 갖는 것
      - 유저1이 ALB를 거칠 때 몇번이고 같은 인스턴스로 통신하게 되는 것
      - 이는 CLB와 ALB에서도 사용 가능
      - 쿠키를 통해서 이러한 Stickyness(고정성)이 가능하고 있고 만료 기간이 있다.
      - 유저가 세션 데이터를 잃으면 안될 때 사용가능하다
      - 하지만 Stickiness를 활성화하면 백엔드 EC2인스턴스에서 트래픽 불균형을 가질 수도 있다.

    - Cookie
      - Application-based Cookies
      - Duration-based Cookies
  - 
