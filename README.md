# hello-docker

'도커, 컨테이너 빌드업!' 도서를 보고 공부한 내용을 정리한다.

<br>

## 1.1 클라우드 컴퓨팅 개요

클라우드는 인프라에 사용되는 서버, 저장소, 데이터베이스, 네트워크 소프트웨어, 데이터 분석 등을 포함해 사용자가 언제든지 인터넷과 모바일 등을 통해 IT 서비스를 제공받을 수 있도록 하는 컴퓨팅 기술이다.

여기서는 클라우드 컴퓨팅 개념에 대한 이해를 통해 도커(Docker)와 쿠버네티스(Kubernetes)의 전체적인 이해를 돕고자 한다.

<br>

### 1.1.1 클라우드 컴퓨팅이란?

가트너(미국의 정보기술 연구 및 자문회사)에서는 클라우드 컴퓨팅을 다음과 같이 정의한다.

> 인터넷 기술을 이용해서 다수의 사용자에게 하나의 서비스로서 방대한 IT 능력을 제공하는 컴퓨팅 방식

`클라우드 컴퓨팅 = 그리드 컴퓨팅 + 유틸리티 컴퓨팅` 이다.

- 그리드 컴퓨팅: 가상 네트워크를 사용하여 분산된 컴퓨팅 자원을 공유하도록 하는 기술 방식

- 유틸리티 컴퓨팅: 다양한 컴퓨팅 자원에 대한 사용량에 따라 요금을 부과하는 종량제 방식의 기술 기반으로, 필요할 때 가져다 쓴다는 온-디맨드(on-demand) 컴퓨팅 방식

- 클라우드 컴퓨팅: 기술적으로는 그리드 컴퓨팅을 따르고, 비용적으로는 유틸리티 컴퓨팅을 혼합한 포괄적인 패러다임

클라우드 컴퓨팅은 다음과 같은 특징을 갖는다.

- 주문형 셀프 서비스: 고객이 IT 서비스 제공자의 개입 없이 원하는 시점에 바로 서비스를 사용할 수 있다.

- 광대역 네트워크 접근: 각 클라우드 서비스 업체가 제공하는 광대역 네트워크를 이용하여 다양한 클라이언트 플랫폼이 빠르게 접속할 수 있다.

- 신속한 탄력성과 확장성: 자동 조정 기능을 통해 몇 분 안에 신속한 확장과 축소를 조정할 수 있다.

- 자원의 공동관리: 물리적 및 가상화된 자원을 풀(pool)로 관리하며, 탄력적으로 사용자 요구에 따라 동적으로 할당 또는 재할당된다.

- 측정 가능한 서비스: 자원 사용량이 실시간으로 수집되는 요금산정 기능을 통해 비용이 발생한다.

<br>

### 1.1.2 클라우드 컴퓨팅 구조

클라우드 컴퓨팅 구조는 최하위 계층으로 자원 활용과 관련된 물리적 시스템 계층, 가상화 계층, 프로비저닝 계층이 있고 클라우드 서비스와 관련된 클라우드 서비스 관리 계층, 클라우드 서비스 계층으로 구분한다.

그 위로는 사용자와 관련된 클라우드 접근 계층과 사용자 역할에 따른 연결성 구분을 설정할 수 있다.

**클라우드 컴퓨팅의 물리적 시스템 계층**은 여러 형태의 서버 계열을 활용하여 확장가능한 스토리지 및 네트워크 등의 물리적 요소를 의미한다.

이를 기반으로 가상화는 클라우드의 주요 이점 중 하나인 민첩성(agility)을 제공하고, 이를 통해 IT 서비스 공급자는 클라우드 서버 프로비저닝 또는 프로비저닝 해제를 신속히 수행하여 서비스 사용자의 요구를 충족하게 된다.

**클라우드 컴퓨팅 서비스 관리 계층**은 물리적 시스템 계층에서 제공되는 자원에 대한 전반적인 라이프사이클 관리와 모니터링을 지원한다.

따라서 안정적인 서비스를 위한 성능 및 고가용성, 소프트웨어 라이선스와 패치 관리, 과금 관리, 보안 관리 요소가 결합되어 있다.

이렇게 구성된 클라우드 구성 요소가 **서비스로서(as a service)** 제공되는 확장 가능한 컴퓨팅 자원을 사용한 양에 따라 비용을 지불하며, 클라우드 환경에 있는 모든 자원에 인터넷과 모바일을 통해 언제든 접근할 수 있다. 또한 서비스로서의 대상별로 유연성 있는 제어와 관리를 제공한다.

사용자는 주어진 역할(사용자, 관리자, 파트너 등)에 따라 다양한 웹 애플리케이션 프로그램 인터페이스(API)를 통해 클라우드 서비스를 호출할 수 있다.

<br>

### 1.1.3 클라우드 컴퓨팅 제공 방식과 클라우드 서비스 종류

- **클라우드 컴퓨팅 제공 방식**

  **1. 온프레미스**

  클라우드 개념이 도입되기 전, 대부분의 기업이 자사에 데이터 센서를 구축하여 IT 서비스를 수행하였고 이를 온프레미스(on-premise)라고 한다.

  이 방식은 모든 자원에 대한 초기 투자 비용과 제한된 용량으로 인해 지속적 관리 비용이 증가하는 단점이 있다. 물론 기업에 내재화된 서비스를 통해 품질 및 보안에 대한 신뢰도는 높이 평가된다.

  **2. 퍼블릭 클라우드**

  퍼블릭 클라우드(public cloud or external cloud) 방식은 인터넷을 통해 다수의 사용자에게 클라우드 자원을 클라우드 서비스 공급자(AWS, Azure 등)로부터 제공받는 방식이다.

  앞서 언급한 유틸리티 컴퓨팅 방식으로서 사용량에 따라 비용을 지불하는 요금산정 방식을 사용한다. 사용자 및 그룹 단위로 권한 관리를 통해 서비스 격리를 하기 때문에, 사용자 간의 간섭이 발생하지 않는다.

  **3. 프라이빗 클라우드**

  프라이빗 클라우드(private cloud or internal cloud) 방식은 제한된 네트워크에서 특정 사용자나 기업만을 대상으로 하는 클라우드 서비스 방식으로, 클라우드 자원과 데이터는 기업 내부에 저장되고 유지관리에 대한 책임 또한 기업이 갖는다.

  인터넷이 아닌 인트라넷 방식으로 서비스에 접근하게 되므로 보안성이 높다.

  **4. 하이브리드 클라우드**

  하이브리드 클라우드(hybrid cloud) 방식은 퍼블릭 클라우드와 프라이빗 클라우드를 네트워크를 통해 결합하여 두 서비스의 장점을 활용할 수 있도록 만든 서비스 방식이다.

  서로 다른 클라우드 간에 데이터와 애플리케이션 공유 및 이동이 유연하게 처리될 수 있고 용도에 맞는 서비스 구현에 유리하다.

  예를 들어, 민감한 데이터 처리는 프라이빗 클라우드를 이용하고 일반 업무 데이터 처리는 퍼블릭 클라우드를 사용할 수 있다.

  최근에는 단순히 가상 서버와 물리 서버의 결합으로 보기도 한다.

<br>

- **클라우드 서비스의 종류**

  **1. 서비스로서의 인프라스트럭처(IaaS)**

  인프라 하드웨어 자원을 가상화하여 사용자 요구에 따라 인프라 자원을 사용할 수 있게 제공하는 클라우드 서비스 방식이다.

  대표적으로 KT, LGU+ 등의 서비스와 AWS(아마존), GCP(구글), Azure(마이크로소프트) 등에서 IaaS 를 제공한다.

  **2. 서비스로서의 플랫폼(PaaS)**

  서비스 개발자가 애플리케이션 개발, 실행, 관리 등을 할 수 있도록 안정적인 플랫폼 또는 프레임워크를 제공하는 클라우드 서비스 방식이다.

  따라서 개발자가 서비스 개발을 위한 복잡한 설치 과정이나 환경 설정을 하지 않고 완성된 개발 소스만 제공하면 바로 서비스를 올릴 수 있는 플랫폼 서비스를 말한다.

  대표적으로 네이버 클라우드 플랫폼과 IaaS 를 제공하는 AWS, GCP, Azure 등의 대표적인 클라우드 공급자가 있다.

  **3. 서비스로서의 소프트웨어(SaaS)**

  소프트웨어 사용자가 자신의 컴퓨터에 소프트웨어를 설치하지 않고 인터넷을 통해 클라우드에 접속하여 클라우드 기반 소프트웨어의 기능을 사용할 수 있게 해주는 클라우드 서비스 방식이다.

  대표적으로 이메일, 구글 앱 서비스 등이 있다.

  <br>

## 1.2 컨테이너 기술과 도커

<br>

### 1.2.1 가상머신과 컨테이너

클라우드 컴퓨팅에서 가상화는 하드웨어 기능을 시뮬레이션하여 애플리케이션 서버, 스토리지, 네트워크와 같은 유용한 IT 서비스를 생성하는 소프트웨어 아키텍처 기술이다. 클라우드는 기업이 추가하는 비용 효율적인 부분을 만족시킨다.

최근 사용하고 있는 가상화는 **하이퍼바이저** 를 이용한 가상머신과 **컨테이너** 를 이용한 도커 방식이다.

가상머신은 호스트 운영체제 위에 가상화 소프트웨어를 이용하여 여러 개의 게스트 OS를 구동하는 방식이다.

각각의 게스트 OS 는 호스트 운영체제로부터 독립된 자원을 할당받아 가상화된 서비스를 제공하기 때문에 수 기가바이트의 용량을 차지하는 이미지를 만들어 사용한다.

**`따라서 가상머신은 하드웨어 가상화다.`**

컨테이너를 이용한 가상화는 프로세스 격리를 통해 경량의 이미지를 실행하고 서비스할 수 있는 컨테이너(container) 기술이다.

클라우드 서비스의 컨테이너는 애플리케이션을 구동하는 환경을 격리한 공간을 의미한다.

물리적 요소에 대한 가상화인 가상머신과 다르게 **`컨테이너 가상화는 프로세스 가상화다.`**

컨테이너 기술의 장점은 다음과 같다.

- 하이퍼바이저와 게스트 OS 가 없기 때문에 가볍다. (수십 메가바이트)

- 경량이기 때문에 만들어진 이미지 복제, 이관, 배포가 쉽다.

- 게스트 OS 를 부팅하지 않기 때문에 애플리케이션 시작 시간이 빠르다.

- 가상머신보다 경량이므로 더 많은 애플리케이션을 실행할 수 있다.

<br>

### 1.2.2 도커

컨테이너는 최신기술이 아니다. 오랜 시간 동안의 변화를 통해 리눅스 컨테이너(LinuX Container, LXC) 기술로 완벽해졌고, LXC 기술을 차용한 도커를 통해 컨테이너의 생성과 배포를 위한 완벽한 가상화 솔루션, 컨테이너 표준화로 자리 잡았다.

컨테이너는 코드와 모든 종속성을 패키지화하는 표준 소프트웨어 단위로, 애플리케이션이 한 컴퓨팅 환경에서 다른 컴퓨팅 환경으로 빠르고 안정적으로 실행되도록 한다.

도커 컨테이너 이미지는 애플리케이션을 실행하는 데 필요한 모든 것을 포함하는 경량의 독립형 실행 가능 소프트웨어 패키지라고 정의할 수 있다.

도커 컨테이너 이미지는 도커 허브(docker hub)로부터 내려받거나 Dockerfile 을 통해 생성(build)하여 도커 엔진을 이용해 실행하면 컨테이너 서비스가 된다.

도커의 주요 기능은 다음과 같다.

- LXC를 이용한 컨테이너 구동: `containerd` 는 이미지 전송 및 스토리지에서 컨테이너 실행 및 감독, 네트워크 연결까지 호스트 시스템 전체 컨테이너의 라이프사이클을 관리한다.

- 통합 Buildkit: 빌드킷(buildkit)은 도커 파일의 설정 정보를 이용하여 도커 이미지를 빌드하는 오픈 소스 도구이며, 빠르고 정확하게 여러 가지 아키텍처 향상 기능을 제공한다.

- 도커 CLI 기반: 도커 명령을 수행하는 기본적인 방법은 CLI 로 제공한다.

도커를 사용하기 위해서는 두 가지 구성 요소를 다룰 수 있어야 한다.

컨테이너, 이미지를 다룰 수 있는 **`도커 엔진`** 과 이미지 업로드(push)/다운로드(pull)를 통해 컨테이너 서비스에 필요한 이미지 배포를 지원하는 **`도커 허브`** 에서 서비스를 제공받아야한다.

큰 개념의 클라우드 서비스와 연결해서 생각해 본다면, 도커 컨테이너 기술은 PaaS 서비스를 가능하게 하는 소프트웨어 개발환경을 제공하는 것이다. 다만 컨테이너 서비스에 대한 자동화된 관리, 트래픽 라우팅, 로드 밸런싱 등을 쉽게 하려면 오케스트레이션 기능이 추가로 요구된다.

도커에는 도커 엔진, 도커 허브 외에 활용도가 높은 많은 구성 요소가 있다.

- Docker Engine: 도커를 이용한 애플리케이션 실행 환경 제공을 위한 핵심 요소

- Docker Hub: 전 세계 도커 사용자들과 함께 도커 컨테이너 이미지를 공유하는 클라우드 서비스

- Docker-compose: 의존성 있는 독립된 컨테이너에 대한 구성 정보를 야믈(YAML) 코드로 작성하여 일원화된 애플리케이션 관리를 가능하게 하는 도구

- Docker Kitematic: 컨테이너를 이용한 작업을 수행할 수 있는 GUI 제공

- Docker Registry: 도커 허브 사이트를 공개된 레지스트리라고 보면됨. 사내에 도커 컨테이너 이미지를 push/pull 할 수 있는 독립된 레지스트리 구축 시 사용

- Docker Machine: 가상머신 프로그램(VMware, Virtualbox) 및 AWS EC2, MS Azure 환경에 도커 실행 환경을 생성하기 위한 도구

- Docker Swarm: 여러 도커 호스트를 클러스터로 구축하여 관리할 수 있는 도커 오케스트레이션 도구

<br>

### 1.2.3 도커 맛보기: PWD

1. https://hub.docker.com 에 접속해서 계정을 만든다.

2. 내 계정에 저장소를 만든다.

3. 도커 튜토리얼 사이트 https://www.docker.com/101-tutorial/ 에 접속한다.

4. Play with Docker 설명에 있는 1번 URL 을 클릭한다.

5. 연결 후 playground 에 `[+ADD NEW INSTANCE]` 를 이용하여 가상의 도커 터미널이 제공된다. 연습 제한 시간은 4시간임을 알 수 있다.

6. 간단히 구성된 환경을 확인해본다.

   - 가상 IP 주소와 함께 자원에 대한 리소스 현황을 볼 수 있다.

   - SSH(Secure Shell) 로 접근할 수 있는 주소를 지원한다.

   - OPEN PORT 는 도커 컨테이너를 외부로 노출 시 바인드되는 포트 번호를 보여준다.

7. 특정 테스트를 하기 위해 CentOS 7 버전이 필요한 상황을 가정한다.

   ```
   # 제공된 환경에 이미지와 컨테이너가 있는지 조회해본다. 아무것도 없을 것이다.
   $ docker image ls
   $ docker ps

   # 도커 허브 사이트로부터 CentOS 7 버전의 도커 컨테이너 이미지를 다운로드한다.
   $ docker pull centos:7

   # 다운로드한 이미지를 확인해본다.
   $ docker image ls

   # 이미지가 가지고 있는 CentOS 7 능력을 구경해보기 위해 컨테이너를 시작한다.
   $ docker run -it --name=centos7_test centos:7 /bin/bash

   # 프롬프트가 변경, CentOS 7 컨테이너 환경으로 들어온 것을 확인해 본다.
   $ cat /etc/os-release
   ```

   다운로드한 CentOS 7 이미지 용량을 살펴보자. 204MB 에 지나지 않는다. 실제 환경 또는 가상머신에서 설치했다면 아마도 3~5GB 정도의 물리적 공간을 차지했을 것이다.

8. 도커 튜토리얼 사이트에서 제공하는 2번 내용을 실행해보자.

   ```
   # 도커 허브로부터 docker 저장소에 저장된 getting-started:pwd 다운로드
   # -d(background 에서 실행), -p 80:80(호스트의 80번 포트와 컨테이너의 80번 포트 연결)
   $ docker run -d -p 80:80 docker/getting-started:pwd
   ```

   상단 `[OPEN PORT]` 옆에 포트 번호 80이 생긴 것을 확인할 수 있다.

   80 을 클릭해 보면 SSH 주소에 해당 컨테이너 내부에 저장된 웹 화면을 80번 포트로 연결해 웹 페이지에서 보여주는 것을 확인할 수 있다.

<br>

## 1.3 쿠버네티스

도커가 기존 컨테이너 생태계에 큰 변화를 가져온 것은 사실이나, 지속적으로 수요가 급증하는 컨테이너에 대한 관리, 애플리케이션 컨테이너 간의 네트워킹, 컨테이너 인스턴스의 확장에 대한 문제 해결을 위해서는 컨테이너 오케스트레이션 도구가 필요하다.

그 중 하나가 쿠버네티스다.

도커를 이용한 컨테이너 기술이 증가하면서 컨테이너 관리를 위한 도구가 발표되기 시작했다.

도커스웜, 아파치 메소스, AWS 의 ECS(Elastic Container Service) 등 많은 오케스트레이션 도구가 나왔고, 그 중 하나가 2014년 구글이 자사 서비스 개발을 위한 보그(Borg) 프로젝트를 통해 얻은 경험을 토대로 만든 쿠버네티스다.

2015년 정식 1.0 버전이 출시되었고, 현재 클라우드 시장은 쿠버네티스 중심으로 진행중이며 마이크로서비스 아키텍처의 기준도 쿠버네티스 사용 여부에 초점을 맞추고 있다.

사실상 컨테이너화된 애플리케이션에 대한 대규모 배포 작업에 가장 적합한 오케스트레이션 도구의 표준이라 할 수 있다.

쿠버네티스가 유용한 이유는 다음과 같다.

1. 온프레미스 환경에서 수행하는 서버 업그레이드, 패치, 백업등의 작업을 자동화(오토 스케일링, 서비스 디스커버리, 로드 밸런싱 등)하여 인프라 관리보다는 서비스 관리에 집중할 수 있다.

2. 컨테이너에 장애 발생 시 자가 회복 기능을 통해 곧바로 복제 컨테이너를 생성하기 때문에 서비스를 지속할 수 있다.

3. 컨테이너화를 통해 소프트웨어를 패키지화하면 점진적 업데이트를 통해 다운타임없이 쉽고 빠르게 릴리스 및 업데이트할 수 있다.

<br>

## 1.4 데브옵스

데브옵스(DevOps)는 개발(Development)과 운영(Operations)의 합성어다.

이 두 업무의 각 목표와 이해 방향이 다르기 때문에 부딪히는 경우가 많았다.

클라우드 환경에서는 이 두 업무 영역을 제한하지 않고 협업과 이해 공유, 책임 공유를 통해 전체 개발 및 인프라의 라이프사이클 혁신에 기여할 수 있다.

데브옵스는 단순히 업무, 부서, 방법론, 기술 형태로 제한하지 않는다. 업무적으로 상충관계에 있는 모든 형태에 적용할 수 있다.

결국 조직 내의 모든 업무자 간의 소통과 협력은 효율성을 높이고 서비스 품질 향상을 통한 기업의 성장을 가져올 수 있다는 것이 데브옵스의 기본 철학이자 하나의 문화다.

<br>

## 2.1 도커 엔진

가상화 기술로 전 세계적으로 개인과 기업 모두에게 인기 있는 도커(Docker)는 2013년 3월에 닷클라우드(dotCloud, Inc.)의 엔지니어였던 솔로몬 하익스가 오픈소스로 공개 발표했다.

도커는 기존의 리눅스 컨테이너(LXC) 기술을 이용하여 애플리케이션을 컨테이너로서 사용할 수 있게 만들었고, 버전 정보를 확인해 보면 Go 언어로 구성된 것을 확인할 수 있다.
출시 이후 꾸준한 기술 개발을 통해 사실상 컨테이너 가상화를 이용한 차세대 클라우드 인프라 솔루션의 표준이 되었다.

도커 컨테이너 기술은 가상화된 공간을 만들기 위해 리눅스 커널에서 컨테이너를 제어하는 chroot, cgroup, namespace API 를 런타임으로 사용함으로써 프로세스 단위의 격리 환경을 만들 수 있다.

컨테이너는 호스트 운영체제의 커널을 공유하여 사용하고, 애플리케이션 컨테이너 자체에는 필요한 실행 파일과 라이브러리만 존재한다. 그래서 만들어진 컨테이너 이미지의 용량이 가상머신의 수 기가바이트에 비해, 수 메가바이트로 작고 배포 시간도 빠르다.

<br>

## 2.2 Linux용 도커 엔진 설치

권장했던 CentOS 7, Ubuntu 배포판을 기반으로 도커 엔진을 설치해본다. CentOS 는 yum 을, Ubuntu 는 apt 라는 도구를 사용해 설치한다.

자세한 설치 방법은 생략한다.

<br>

## 2.3 windows/macOS용 도커 엔진 설치

도커는 리눅스 기반의 프로그램이기 때문에 리눅스 환경에서 테스트 및 개발 용도로 만들어 사용하는 것을 권장한다. 하지만, 초보자이거나 리눅스 환경에 익숙하지 않은 사용자를 위해 윈도우나 macOS 에서 설치하여 사용하는 것도 가능하다.

Docker Desktop 을 이용한다.

자세한 설치 방법은 생략한다.

<br>

## 2.4 도커 확인

<br>

### 2.4.1 도커 컨테이너 서비스

어떤 OS 에 도커 엔진을 설치했든 상관없이 도커의 기본 명령줄 사용은 동일하므로 계속 진행한다. 여기서는 Ubuntu 18.04, Docker 20.10.10 버전으로 진행된다.

리눅스 컨테이너의 미래(The Future of Linux Container)라는 제목으로 도커 엔진을 처음 발표한 솔로몬 하익스는 docker라는 새로운 명령으로 'Hello, World' 문자열을 출력하는 데모를 시연했다.

```
# 도커 허브 레지스트리에서 제공하는 busybox 이미지를 다운로드 후 이미지 조회.
$ docker pull busybox
$ docker images

# 다운로드한 이미지를 실행하면 컨테이너가 됨. 이미지 뒤에 태그가 latest이면 생략가능.
$ docker run busybox
$ docker ps -a
# docker ps -a 명령은 실행된 모든 컨테이너의 정보를 제공한다. 리눅스 명령인 ps(process status)와 같은 맥락으로 사용된다. 결국, 도커 컨테이너는 '프로세스 가상화' 라는 의미를 되새긴다.
# busybox 를 실행하면 기본적으로 sh(셸)을 이용하여 지정한 명령을 실행하는데, 처음 실행한 명령에서는 busybox 뒤에 명령을 기재하지 않았기 때문에 실행되자마자 곧바로 종료된 것이다.

# 컨테이너에도 운영체제가 있는 걸까? 명령 sh(셸)을 이용하여 컨테이너 내부에 접속해 보면 Ubuntu 리눅스인 것을 알 수 있다. 도커 가상화는 호스트의 커널을 공유해서 사용한다. Ubuntu 리눅스가 설치된 busybox 의 이미지 용량을 보면 1.22MB 이다. 이렇게 작은 용량으로 운영체제가 가동될 수 있을까라는 의문이 들 수도 있다. 의미를 되새겨보면, 도커 컨테이너는 호스트의 커널을 공유해서 사용하고 가동에 필요한 도구만 일부 탑재한 '격리된 경량의 리눅스 프로세스' 다.

$ docker run -it busybox sh

# 셸에 echo 명령을 이용해 'Hello World' 를 출력해 본다.
$ docker run busybox echo 'Hello World'

# 출력된 'Hello World' 는 어디서 출력되었을까? 정답은 컨테이너다. 단순히 리눅스 운영체제에서 출력할 수 있는 에코 명령이지만, 호스트가 아닌 컨테이너라는 서비스를 통해 명령을 수행할 수 있다는 것이다.
예를 들어, Nginx 웹 애플리케이션 서버라고 생각해 보자. 우리는 Nginx 를 위한 환경 구성, 설치, 서비스 시작 그 어떤 것도 하지 않고 도커를 이용해 컨테이너 Nginx 서비스를 배포할 수 있다. 이것이 도커가 가지고 있는 민첩한 애플리케이션 배포 기능이다.
```

<br>

### 2.4.2 도커 정보 확인

도커 설치 이후 가장 먼저 확인했던 명령어 **`docker version`** 이다.

```
# docker 버전 정보만 확인
$ docker -v

# 설치된 도커 엔진의 세부 정보 확인
$ docker version
```

설치된 도커 엔진은 클라이언트와 서버로 구분된다.

클라이언트는 도커 명령을 받고 결과를 출력하는 역할을 한다.

서버는 도커 엔진, 즉 도커 데몬을 이용해 컨테이너 시작, 운영, 정지 등을 담당한다.

시스템에 설치된 도커 구성 정보는 **`docker info`** 를 통해 확인한다. 다음과 같은 정보를 출력하여 보여준다.

- 커널 정보, 현재 컨테이너 수 및 이미지 수 출력

- 사용 중인 스토리지 드라이버에 따른 풀 이름

- 데이터 파일, 메타 데이터 파일, 사용된 데이터 공간, 총 데이터 공간, 사용된 메타 데이터 공간, 총 메타 데이터 공간 정보 표시

**`docker [system] info`** 를 실행해서 출력 정보를 하나씩 살펴본다. system 은 생략할 수 있다.

```
$ docker [system] info
...
# JSON 파일 형식으로 출력
$ docker info --format '{{json .}}'
```

**`docker system df`** 를 실행해서 도커 시스템이 사용하는 디스크 사용량에 대한 현재 상태를 조회할 수 있다.

```
$ docker system df

# 세부 정보 확인
$ docker system df -v
```

회수 가능한 공간 확보는 **`docker system prune`** 명령을 이용하여 제거할 수 있다.

```
$ docker system prune
```

**`docker system events`** 를 실행해서 도커 서버에서 발생하는 도커 관련 이벤트 정보를 표시하는 명령이다. 해당 명령어는 도커 관련 명령이 실행되지 않는 동안에는 아무것도 출력이 되지 않는다. 터미널을 두개 띄워놓고 한쪽에는 Nginx 웹 애플리케이션을 조작하고, 다른 한쪽에는 도커 명령이 실행될 때마다 내부적으로 발생하는 이벤트 기록이 나타남을 확인 할 수 있다.

```
# 터미널 1
$ docker system events
```

```
# 터미널 2, 도커를 이용해 Nginx 조작. 이때 터미널 1에는 도커 명령이 실행될 때마다 이벤트 기록이 나타남.
$ docker run -itd -p 80:80 --name=webapp nginx
```

많은 정보가 기록되기에 식별하기가 쉽지 않다. 이벤트 옵션 필터(--filter)를 통해 원하는 정보만 추출해서 볼 수 있다. docker events 는 롤링 로그이며, 최대 1000개의 이벤트를 보유한다.

```
# --filter 옵션을 이용하여 식별
$ docker system events --filter 'type=image'
$ docker system events --filter 'event=stop'
$ docker system events --filter 'container=webapp'
$ docker system events --filter 'container=webapp' --filter 'event=stop'

# 지난 24시간 동안의 로그를 출력
$ docker system events --since 24h

# JSON 형식으로 로그 출력
$ docker system events --format '{{json .}}'
```

도커 엔진이 안정적으로 설치되면 기본적으로 구성되는 요소는 도커 데몬이다.

도커 데몬에 문제가 발생하면 컨테이너 서비스에 큰 영향을 주기에, 문제 해결 시 도커 데몬 로그를 통해 원인 파악에 도움을 얻을 수 있다.

이것을 도커 데몬 디버깅이라고 한다.

디버깅 로그를 출력해보자. journalctl 은 systemd 영역의 명령어다.

```
# 로그 내용 중 msg 키워드 정보가 상세 로그 내용.
# 이 방법은 systemctl 또는 service 명령을 통해 도커 서비스가 시작된 경우 디버깅하는 방법을 보여줌.
$ sudo journalctl -u docker
```

위와 유사한 도커 데몬 디버그 방법이 dockerd 명령이다.

```
# 터미널 1
# 'dockerd' 명령도 도커 데몬을 시작할 수 있고, 다른 작업 창에서 수행되는 모든 도커 명령에 대한 정보를 디버깅하여 화면에 출력한다.
$ sudo dockerd -D

# 터미널 2
$ docker ps -a

# 정지되어 있는 컨테이너 시작
$ docker start webapp
```

도커 데몬 로그를 도커 자체적으로 로깅, 디버깅하는 방법을 살펴봤다.

리눅스 시스템에도 syslogd, rsyslogd 처럼 기본적인 로그 수집 데몬이 있다. 이를 이용해 도커 로그를 호스트 운영체제의 로그 수집 데몬에 연결해서 로그를 기록하는 방법도 사용할 수 있다. 도커 문서에서 확인 할 수 있다.

<br>

## 3.1 컨테이너 서비스

<br>

### 3.1.1 컨테이너 서비스란?

컨테이너를 사전적으로 해석해보면 **어떤 사물을 격리할 수 있는 공간** 을 뜻한다.

IT 에서 컨테이너라는 용어를 사용하는 것은 컨테이너에 우리가 서비스하고자 하는 애플리케이션 코드와 프로세스를 격리한다는 의미로 해석할 수 있다.

최근 클라우드 기반의 컨테이너 서비스, 데브옵스, 마이크로서비스 아키텍처라는 단어는 데이터 기반의 애플리케이션 프로젝트에서 빠지지 않는다. 애플리케이션 개발환경이 도커 기반의 컨테이너 서비스 환경으로 전환된 이유는 무엇일까.

대부분의 개발자가 개발, 테스트, 배포, 운영의 컴퓨팅 환경(스토리지, 네트워크, 보안, 패치 등) 차이로 인한 시행착오 및 다양한 오류 해결에 너무 많은 시간을 쏟는 문제를 겪고 있다. 바로 가변적 인프라 환경으로 인한 일관성 없는 환경 제공 때문이다.

컨테이너 서비스는 기존 환경과 다르게 애플리케이션 실행에 필요한 바이너리, 라이브러리 및 구성 파일 등을 패키지로 묶어 배포하는 방식으로 논리적 패키징 메커니즘을 제공한다. 애플리케이션이 가지고 있는 의존성 문제를 해결한 것이다. 따라서 어떤 환경에서든 컨테이너 기반의 애플리케이션을 개발하고 배포할 수 있다.

이렇게 호스트 운영체제를 공유하고 애플리케이션에 필요한 환경을 패키징하는 것을 **운영체제 레벨 가상화** 라고 부른다. 일반적으로 가상화 방식을 크게 두 가지로 구분한다.

- 하드웨어 레벨 가상화: 하이퍼바이저 등을 이용한 가상머신 방식

- 운영체제 레벨 가상화: 컨테이너 기반의 애플리케이션 서비스 방식

컨테이너화를 통해 개발자는 애플리케이션 개발에 집중하고, IT 부서는 애플리케이션 운영에 필요한 세부적인 것을 관리하여 낭비되는 시간을 없애고 각자의 업무에 집중할 수 있다.

<br>

### 3.1.2 왜 도커 컨테이너 서비스일까?

도커를 도입하려고 할 때 분명 번거로움을 느끼거나 굳이 왜라는 의문을 갖는 사람이 있을 것이다.

도커 도입이 갖는 의미를 알기 위해서는 도커를 이용한 컨테이너 애플리케이션 서비스 개발이 이루어지는 일반적인 과정을 이해할 필요가 있다.

1. 애플리케이션 코드 개발: 특정 서비스 구동을 위한 애플리케이션 코드 및 웹 화면 구성 등을 개발한다.

2. 베이스 이미지를 이용한 Dockerfile 작성: 개발에 필요한 인프라 구성 요소를 DOckerfile 에 작성한다. 즉, 도커 허브를 통해 베이스 이미지(base image)를 다운로드하고 다양한 구동 명령어(FROM, RUN, CMD, ENDPOINT, ENV, ADD 등)와 `1` 에서 작성한 애플리케이션 코드, 라이브러리, 여러도구를 Dockerfile 에 포함시킨다.

3. Dockerfile build 를 통한 새로운 이미지 생성: docker build 명령을 통해 작성한 Dockerfile 을 실행한다. 각 단계별로 실행되는 로그를 화면에서 확인하며 이때 오류 발생 내용도 확인할 수 있다.

4. 컨테이너 실행

   4-1. 생성된 이미지를 이용한 컨테이너 실행: 도커 명령어 docker images 를 통해 생성된 이미지를 확인하고 이미지를 통한 컨테이너를 구동(docker run)한다.

   4-2. 도커 컴포즈를 이용한 다중 컨테이너 실행: 도커 실행 옵션을 미리 작성한 ㅇocker-compose.yml 을 통해 다중 컨테이너 간 실행 순서, 네트워크, 의존성 등을 통합 관리할 수 있고 마이크로서비스(MSA) 개발에 활용한다.

5. 서비스 테스트

   5-1. 컨테이너 애플리케이션 서비스 테스트: `4-1` 에서 예를 들면 Nginx 를 이용한 서비스였다면 연결하는 IP 와 포트 번호를 이용하여 웹 브라우저를 이용한 페이지 연결을 확인할 수 있다.

   5-2. 마이크로서비스 테스트: `5-1` 과 마찬가지로 해당 서비스에 대한 테스트를 진행한다.

6. 로컬 및 원격저장소에 이미지 저장: 로컬(도커 서버 또는 프라이빗 레지스트리) 및 원격(Docker hub)에 있는 이미지 저장소(repository)에 생성한 이미지를 저장(push)하여 다른 팀 간의 공유 및 지속적인 이미지 관리를 수행한다.

7. 깃허브 등을 활용한 Dockerfile 관리: Dockerfile 코드를 깃허브 사이트에 저장 및 관리할 수 있고, 도커 허브 사이트와 연동하게 되면 자동화된 빌드(automated build)기능을 이용한 이미지 생성도 가능하다.

8. 동일 환경에서의 지속적 애플리케이션 개발 수행: `1~7` 과정을 통해 업무용 애플리케이션 이미지를 지속적으로 개발, 운영 및 관리할 수 있다.

도커 작동 과정에서 눈여겨볼 것은 컨테이너 동작에 필요한 모든 내용을 사전에 코드로 작성하여 인프라 프로비저닝(provisioning) 도구로 자동화하게 되면 기업이 필요할 때마다 애플리케이션 및 서버 환경을 적은 비용으로 빠르게 개발, 배포, 확장할 수 있다는 것이다. 이러한 개념은 `IaC(Infrastructure as Code) - 코드로서의 인프라스트럭처` 라고 한다.

이 기능을 통해 개발자는 애플리케이션 개발, 테스트, 배포 시마다 모든 인프라 구성 요소를 하나하나 수동적으로 체크하거나 맞출 필요가 없고, **`변경 불가능한 인프라(Immutable infrastructure)`** 환경에서 언제든 동일한 상태에서의 개발이 가능해진다.

물론 버전 업이나 패치 등의 작업이 필요하면 기존 이미지를 변경하지 않고 해당 작업을 수행한 새로운 이미지를 생성하여 신규 인프라 서버로 사용 가능하다.

이처럼 수많은 소프트웨어, 애플리케이션을 민첩하고 탄력적으로 제공하려는 기업이라면 필수적으로 구성해야 하는 것이 바로 컨테이너 서비스 환경이다.

<br>

## 3.2 도커 명령어 활용

모든 도커 명령은 상위 키워드로 `docker` 를 앞에 사용하고, 기본적인 명령어 사용법은 헬프(docker COMMAND -help) 명령을 통해 확인하거나 도커에서 제공하는 문서(https://docs.docker.com/engine/reference/builder)를 참고한다.

<br>

### 3.2.1 도커 이미지 명령어

도커 컨테이너는 일반적으로 도커 허브(hub.docker.com)에서 제공(공개 저장소)하는 이미지(image)를 기반으로 실행된다.

도커 이미지는 도커의 핵심 기술이며 코드로 개발된 컨테이너 내부 환경 정보(바이너리, 라이브러리, 각종 도구 등)를 고스란히 복제하여 사용할 수 있다.

도커 컨테이너로 사용할 도커 이미지는 docker search 를 통해 조회하면 도커 허브 및 개인 사용자들이 공개한 관련 이미지를 살펴볼 수 있다. 로컬 서버 및 데스크탑에 도커 이미지를 저장하기 위해서는 Dockerfile 을 통해 새로운 이미지를 생성(docker build)하거나 도커 허브로부터 이미지를 내려받는(docker pull) 방법이 있다.

Dockerfile 로 생성된 이미지는 도커 허브에 로그인을 통한 자격 증명 후 업로드(docker push)하고 공개 및 비공개로 설정할 수 있다. 또는 깃허브를 통해 Dockerfile 코드를 공유하여 관리하는 방법도 있다. 이렇게 만들어진 이미지를 실행(docker run)하면 우리가 서비스하려고 하는 애플리케이션 컨테이너가 된다.

<br>

도커 이미지를 내려받거나 레지스트리에 업로드하는 과정을 수행하기 위해 다음 명령을 사용한다.

- docker pull: 도커 허브 레지스트리에서 로컬로 도커 이미지 내려받기

- docker push: 로컬에 있는 도커 이미지를 도커 허브 레지스트리에 업로드하기

- docker login: 업로드를 하기 전 도커 허브 계정으로 로그인 수행하기

- docker logout: 도커 허브에서 로그아웃하기

도커 이미지 다운로드는 기본적으로 도커 허브 레지스트리로 자동 지정되고 특정 레지스트리를 수동으로 지정해서 받는 방법도 있다. 다음 구분을 보면 이미지 다운로드를 위해 docker pull 명령을 이용하고 옵션 및 태그 등을 지정하여 세부 사항을 지정할 수 있다.

```
docker [image] pull [OPTIONS] name[:TAG | @IMAGE_DIGEST]
```

배포판 리눅스 이미지인 debian 다운로드를 통해 자세히 알아본다.

```
$ docker pull debian
1. Using default tag: latest
2. latest: Pulling from library/debian
3. 90fe46dd8199: Pull complete
4. Digest: sha256: 2857...
5. Status: Downloaded newer image for debian:latest
6. docker.io/library/debian:latest

# 다운로드한 이미지 정보 조회
$ docker image ls
```

1. 이미지 명 뒤에 `:태그` 를 포함하지 않으면 자동으로 최신버전으로 지정되므로 기본 태그값이 latest 라고 출력된다. 만약 특정 버전을 지정하게 되면 지정한 버전명이 포함된다.

2. 라이브러리(library)는 도커 허브가 이미지를 저장하고 있는 네임스페이스로 제공된다. 도커 이미지명의 기본 형식은 `<네임스페이스>/<이미지명>:<태그>` 이고, 별도로 특정 레지스트리를 지정하지 않으면 자동으로 도커 허브의 라이브러리가 네임스페이스로 지정된다.

3. 도커 허브에서 제공된 이미지의 분산 해시 값 표시. 다운로드한 이미지는 여러 계층(layer) 로 만들어지는데 그중 이미지의 핵심 정보를 바이너리 형태의 정보로 제공하는 것이다.

4. 다이제스트값은 원격 도커 레지스트리(도커 허브)에서 관리하는 이미지의 고유 식별값을 뜻하고 이 값을 포함한 조회는 `docker images --digests` 옵션을 사용한다.

5. 다운로드한 이미지 정보가 로컬에 저장되었음을 나타내는 상태 표시.

6. `debian:latest` 와 동일한 값으로 `docker.io` 는 도커 허브의 이미지 저장소 주소를 나타낸다. `docker info` 명령의 출력 정보 중 `Registry: https://index.docker.io/v1/` 와 동일하다.

다운로드한 이미지 정보는 `docker image ls` 또는 `docker images` 를 통해 조회된다. `docker pull` 명령의 옵션은 다음과 같다.

- --all-tags, -a: 저장소에 태그로 지정된 여러 이미지를 모두 다운로드함

- --disable-content-trust: 이미지 검증 작업 건너뛰기(기본값 true)

- --platform: 플랫폼 지정, 윈도우 도커에서 리눅스 이미지를 받아야 하는 경우 사용(ex. --platform=linux)

- --quiet, -q: 이미지 다운로드 과정에서 화면에 나타나는상세 출력 숨김

아래 내용은 이미지를 다운로드하는 여러 가지 방법이다.

```
# 명시적으로 최신 버전 지정
$ docker pull debian:latest

# 이미지 식별 정보인 다이제스트 지정
$ docker pull debian:sha256:2857...

# 도커 허브 레지스트리 명시적 지정
$ docker pull library/debian:latest
$ docker pull docker.io/library/debian:latest
$ docker pull index.docker.io/library/debian:latest

# 외부 레지스트리 주소를 이용하는 방법. 주의할 것은 웹 주소 URL 에서 도메인 주소의 시작인 http:// 를 붙이지 않고 이미지 주소를 써야 한다는 점이다.
$ docker pull gcr.io/google-samples/hello-app:1.0
```

<br>

도커 오브젝트(이미지, 컨테이너 등)에 대한 세부 정보 조회를 위해 docker image inspect, docker image history, 물리적으로 호스트 운영체제에 저장된 영역을 이용한다.

**docker inspect** 에 대해 알아본다.

```
docker image inspect [OPTIONS] IMAGE [IMAGE...]
```

이 명령의 출력 결과는 JSON 언어 형태로 출력되는 정보가 많기 때문에 포맷 옵션을 이용하여 원하는 정보만 출력할 수 있다.

docker image inspect 명령 옵션은 아래와 같다.

- --format, -f: JSON 형식의 정보 중 지정한 형식의 정보만 출력할 수 있고, {} 중괄호 형식과 대소문자에 유의해야한다.

출력되는 세부 내용 중 몇가지 주요 정보는 다음과 같다.

- image ID: 'Id'

- 생성일: 'Created'

- Docker 버전: 'DockerVersion'

- CPU 아키텍처: 'Architecture'

- 이미지 다이제스트 정보: 'RootFS'

- 이미지 레이어 저장 정보: 'GraphDriver'

테스트하기 위해 아파치 웹 서비스를 할 수 있는 httpd 도커 이미지를 다운로드해 본다.

```
# docker search 수행전 hub.docker.com 에 가입한 본인 계정으로 docker login 을 먼저 수행하고 조회
$ docker search httpd
...

# httpd 최신 버전으로 다운로드
$ docker pull httpd:latest
...

# 다운로드한 이미지 조회
$ docker images
...

# 다운로드한 이미지 세부 정보 조회
$ docker image inspect httpd
...

# 계층 형식으로 되어 있어 하위 정보 조회 시 .상위[.하위] 방식으로 조회
$ docker image inspect --format="{{ .RepoTags}}" httpd

$ docker image inspect --format="{{ .Os}}" httpd

$ docker image inspect --format="{{ .ContainerConfig.Env}}" httpd

$ docker image inspect --format="{{ .RootFS.Layers}}" httpd

```

다음은 **docker image history** 를 이용해 조회해 본다.

```
docker image history [OPTIONS] IMAGE
```

이 명령을 통해 현재 이미지 구성을 위해 사용된 레이블 정보와 각 레이어의 수행 명령, 크기 등을 조회할 수 있다. 아래는 이미지를 구성하고 있는 레이어와 실행 정보에 관련된 내용이다.

```
$ docker image history httpd
...
```

출력 결과중 CREATED BY 열을 보면 특정 이미지를 구성하기 위해 사용된 명령과 환경 설정 정보 등을 볼 수 있다. 정보 중 용량을 가지고 있는 라인이 레이어다. CMD, EXPOSE, ENV, WORKDIR 등의 명령을 통해 베이스 이미지에 필요한 설정 정보를 결합하여 새로운 이미지를 만들게 된다. 이러한 메타 데이터 관련 명령은 Dockerfile 을 통해 배우게 된다.

이미지가 다운로드되는 과정을 보면, 처음 다운로드한 데비안 리눅스와 달리 아파치 웹 서버 이미지인 httpd 는 다운로드한 레이어 수가 더 많은 것을 볼 수 있다.

참고로, 출력된 다이제스트 값은 도커 허브에서 관리하는 다이제스트 값이 아닌 로컬에 다운로드될 때 생기는 레이어들의 디스트리뷰션 아이디다.

간단히 표현하면 `도커 유니언 파일 시스템`은 다음과 같은 구조다.

1. 도커 이미지 구조의 기본 운영체제 레이어들을 쌓는다.

2. 운영체제 베이스 이미지 위에 아파치 웹 서버를 설치한 레이어를 올린다.

3. 아파치 웹 서비스에 필요한 리소스 정보 및 환경 정보가 포함된 레이어를 올린다. 이렇게 구성된 이미지는 불변의 읽기 전용 레이어들의 집합 구조인 유니언 파일 시스템이다. (이미지 레이어는 불변이지만, 관리자 권한으로 호스트 운영체제에서 각 레이어에 접근하게 되면 파일 생성 및 변경이 가능)

4. 도커 이미지를 실행하면 여러 개의 컨테이너를 구동할 수 있다. 각각의 컨테이너에서 발생한 모든 변경 정보를 저장하기 위해 읽고-쓰기 레이어를 두고 저장하게 된다.

`이러한 구조를 사용하는 이유는,` 이미지를 실행하여 여러 개의 컨테이너를 구동했을 때 처음 내려받은 이미지는 수백 메가의 용량을 가지고 있지만 컨테이너를 구동할 때마다 이미지를 내려받지 않고 로컬에 저장된 이미지를 계속 사용한다. 또한 이미지 레이어의 상단에 있는 웹 애플리케이션 소스 레이어의 환경 설정 및 리소스 설정이 변경되어 이미지로 `변경되더라도 기존 레이어를 제외한 변경된 웹 소스 레이어만 내려받아 사용하기 때문에 효율적이다.`

<br>

호스트 운영체제에서는 어떻게 저장되는지 살펴본다.

```
# 도커 저장소에 사용되는 스토리지 드라이버를 조회한다. Overlay2 를 사용하고 있다.
$ docker info | grep storage

# 도커의 모든 데이터 및 로그 정보는 다음 경로에 저장된다(관리자 권한으로 변경).
$ sudo su -
$ cd /var/lib/docker
$ ls
...

# 이미지 레이어 데이터는 다음 경로에 저장된다.
$ cd image/overlay2/layerdb/sha256
$ ls
...

```

출력된 디렉터리 이름은 다이제스트 값이다.

내려받은 httpd 의 저장된 레이어를 조회하고 첫 번째 주소와 비교해 보면 일치하는 디렉터리가 있다.

```
# 도커 조회 명령으로 렝리어 정보를 필터링한다.
$ docker image inspect --format="{{ .RootFS.Layers}}" httpd
[sha256: a...
 sha256: b...
 sha256: c...]

# 일치하는 디렉터리의 diff 로 이동하고, cached-id 파일 정보를 통해 실제 데이터가 저장된 디렉터리의 다이제스트값을 확인한다.
$ cd a...
$ ls
...
$ cat cache-id
d...

# 이 값과 일치하는 영역을 다음 경로에서 확인한다. 이 영역이 이미지 실행을 통해 만들어지는 컨테이너의 최상위 경로/영역이 된다.
$ cd
$ cd /var/lib/docker/overlay2/
$ ls
...
d...
...
$ cd d.../diff/
$ ls

# 다른 터미널을 이용하여 컨테이너를 실행해본다. 다음 명령은 httpd 이미지로부터 webserver 라는 이름의 컨테이너를 80번 포트 번호로 연결하여 실행하고, bash 명령으로 컨테이너 내부 셸로 접속한다.
$ docker run -it -p 80:80 --name=webserver httpd:latest /bin/bash
$ cd /
$ ls

# 확인을 위해 관리자 권한이 있는 터미널에서 임시 파일을 생성한다.
$ touch Hello-docker
$ ls

# 컨테이너로 접속한 터미널에서 위에서 생성한 임시 파일을 바로 확인할 수 있다.
$ ls

# 로컬에서 httpd 레이어를 추적해서 그 위치를 파악하고 컨테이너가 그 레이어에서 수행되는 것을 확인할 수 있다.
```

내려받은 이미지에 대한 레이어 구조에 대해 알아봤다. 여러 레이어로 구성된 이미지는 몇 개의 컨테이너를 실행해도 별도의 읽고 쓰기가 가능한 컨테이너 레이어가 상위에 추가되므로 하위 이미지 레벨의 레이어에는 영향을 주지 않으면서 동작하는 것이 컨테이너 가상화의 특징 중 하나다.

<br>

도커 태그(tag)는 원본 이미지에 참조 이미지 이름을 붙이는 명령이다. 사용법은 다음과 같다.

> docker tag 원본 이미지[:태그] 참조 이미지[:태그]

태그 설정은 단순히 새로운 참조명을 붙이는 작업이므로 이미지 ID 는 변경되지 않는다. 어떤 경우에 태그 설정을 하는지 알아본다.

```
# 이미지 ID에 세부 정보(OS, 버전 등)를 붙여 태그 지정.
$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
httpd        latest    c18831e834fc   5 weeks ago    195MB
nginx        latest    12ef77b9fab6   6 weeks ago    192MB
debian       latest    48f404e78da4   6 weeks ago    139MB
busybox      latest    fc9db2894f4e   4 months ago   4.04MB

$ docker image tag c18831e834fc debian-httpd:1.0
$ docker images
REPOSITORY     TAG       IMAGE ID       CREATED        SIZE
debian-httpd   1.0       c18831e834fc   5 weeks ago    195MB
httpd          latest    c18831e834fc   5 weeks ago    195MB
nginx          latest    12ef77b9fab6   6 weeks ago    192MB
debian         latest    48f404e78da4   6 weeks ago    139MB
busybox        latest    fc9db2894f4e   4 months ago   4.04MB


# 이미지 이름[:태그]에 세부 정보(OS, 버전 등)를 붙여 태그 지정.
$ docker image tag httpd:latest debian-httpd:2.0
$ docker images
REPOSITORY     TAG       IMAGE ID       CREATED        SIZE
debian-httpd   1.0       c18831e834fc   5 weeks ago    195MB
debian-httpd   2.0       c18831e834fc   5 weeks ago    195MB
httpd          latest    c18831e834fc   5 weeks ago    195MB
nginx          latest    12ef77b9fab6   6 weeks ago    192MB
debian         latest    48f404e78da4   6 weeks ago    139MB
busybox        latest    fc9db2894f4e   4 months ago   4.04MB

# 도커 허브와 같은 레지스트리에 업로드하는 경우 저장소명과 함꼐 태그 지정.
$ docker image tag httpd:latest [본인 아이디]/httpd:3.0
$ docker images
REPOSITORY     TAG       IMAGE ID       CREATED        SIZE
httpd          latest    c18831e834fc   5 weeks ago    195MB
hws522/httpd   3.0       c18831e834fc   5 weeks ago    195MB
debian-httpd   1.0       c18831e834fc   5 weeks ago    195MB
debian-httpd   2.0       c18831e834fc   5 weeks ago    195MB
nginx          latest    12ef77b9fab6   6 weeks ago    192MB
debian         latest    48f404e78da4   6 weeks ago    139MB
busybox        latest    fc9db2894f4e   4 months ago   4.04MB

# 알기 쉬운 이름으로 설정하고자 하는 경우 태그 지정.
$ docker image tag httpd webserver:4.0
$ docker images
REPOSITORY     TAG       IMAGE ID       CREATED        SIZE
debian-httpd   1.0       c18831e834fc   5 weeks ago    195MB
debian-httpd   2.0       c18831e834fc   5 weeks ago    195MB
httpd          latest    c18831e834fc   5 weeks ago    195MB
webserver      4.0       c18831e834fc   5 weeks ago    195MB
hws522/httpd   3.0       c18831e834fc   5 weeks ago    195MB
nginx          latest    12ef77b9fab6   6 weeks ago    192MB
debian         latest    48f404e78da4   6 weeks ago    139MB
busybox        latest    fc9db2894f4e   4 months ago   4.04MB

# 도커 허브에 가입 후 생성한 본인 아이디(hws522) 에 http 라는 저장소와 3.0 태그가 지정되어 업로드 됨.

# 터미널에서 docker login 을 통해 도커 허브에 원격 접속(접속 해제는 docker logout)
$ docker login
Username: 본인 아이디 입력
Password: 본인 암호 입력
...
Login Succeeded

$ docker push [본인아이디]/httpd:3.0
The push refers to repository [docker.io/hws522/httpd]
99bf1d462439: Mounted from library/httpd
d904146ab7a0: Mounted from library/httpd
838b5c76c02b: Mounted from library/httpd
e245681d1f55: Mounted from library/httpd
32f2ee38f285: Mounted from library/httpd
3.0: digest: sha256:a8db96a1de15bc0a63b9c591dfecadf2d55ed3aebe8de9410f2159ed6bb6cb2b size: 1366

# 본인의 도커 허브 저장소에 업로드된 이미지를 내려받을 수 있다.
$ docker pull hws522/httpd:3.0
3.0: Pulling from hws522/httpd
Digest: sha256:a8db96a1de15bc0a63b9c591dfecadf2d55ed3aebe8de9410f2159ed6bb6cb2b
Status: Image is up to date for hws522/httpd:3.0
docker.io/hws522/httpd:3.0
```

도커 허브에서 본인이 업로드한 이미지를 확인해 본다.

일반적으로 본인이 베이스 이미지에 특정 애플리케이션을 서비스와 코드 등을 포함해 컨테이너로 실행한 경우, `docker commit` 명령을 통해 컨테이너를 이미지로 저장할 수 있다.

이렇게 저장된 이미지를 본인의 도커 허브 저장소에 업로드하고 지속적으로 활용할 수도 있고, 팀 간 이미지 공유도 할 수 있다.

도커 허브 사이트에서 제공하는 저장소에 호스트에서 생성한 이미지 및 보유하고자 하는 이미지를 업로드하려면 `docker login` 명령을 통해 호스트에서의 접속이 이루어져야 한다. 도커 허브 사이트 접속은 기본적으로 두 가지 방법을 사용할 수 있다.

1. ### docker login

   ```
   $ docker login
   Log in with your Docker ID or email address to push and pull images from Docker Hub. If you don't have a Docker ID, head over to https://hub.docker.com/ to create one.
   You can log in with your password or a Personal Access Token (PAT). Using a limited-scope PAT grants better security and is required for organizations using SSO. Learn more at https://docs.docker.com/go/access-tokens/

   Username:
   Password:
   Login Succeeded
   ```

2. ### hub.docker.com / access token

   1. hub.docker.com 에 로그인한다.

   2. 본인 계정을 클릭하면 [Account settings] 가 나온다.

   3. 좌측 메뉴 중 [Security] 를 선택한다.

   4. [Access Tokens] 의 [New Access Token] 을 선택한다.

   5. 임의의 값을 입력하면 사용방법이 제공된다.

   6. 복사된 액세트 토큰을 사용해본다.

      ```
      $ vi .access_token
      만들어놓은 토큰

      # 별도의 암호 입력 없이 액세스 토큰을 이용해 로그인된다.
      $ cat .access_token | docker login --username 본인ID --password-stdin
      ...

      # 경고 메세지에 제시된 파일을 열어 확인해본다.
      $ cat /.../.docker/config.json
      ...
      ```

   7. 생성된 액세스 토큰의 [Edit] 를 선택해 보면 마지막 사용 메뉴가 [Active] 로 되어 있다.

   8. 이 값을 [Inactive] 로 변경 후 재접속 해보면 접속 거부됨을 확인할 수 있다.

<br>

`docker image save` 명령은 도커 원본 이미지의 레이어 구조까지 포함한 복제를 수행하여 확장자 `tar(Tape Archiver)` 파일로 이미지를 저장한다.

- 도커 허브로부터 이미지를 내려받아 내부망으로 이전하는 경우

- 신규 애플리케이션 서비스를 위해 `Dockerfile` 로 새롭게 생성한 이미지를 저장 및 배포해야 하는 경우

- 컨테이너를 완료(commit)하여 생성한 이미지를 저장 및 배포해야 하는 경우

- 개발 및 수정한 이미지 등

네트워크 제한 등으로 도커 허브를 이용하지 못하는 경우 이미지 이전과 배포를 위해 로컬에 저장된 이미지를 파일로 저장하거나 불러올 수 있다.

```
# 도커 이미지를 tar 파일로 저장.
$ docker image save [옵션] <파일명> [image명]

# docker save 로 저장한 tar 파이을 이미지로 불러옴.
$ docker image load [옵션]
```

아래는 이미지를 다운로드해서 파일로 저장하고 불러오는 과정이다.

```
# mysql:latest 이미지를 다운로드 하고 확인한다
$ docker pull mysql:latest
$ docker images
REPOSITORY     TAG       IMAGE ID       CREATED        SIZE
mysql          latest    5d2fb452c483   4 weeks ago    622MB
hws522/httpd   3.0       c18831e834fc   5 weeks ago    195MB
debian-httpd   1.0       c18831e834fc   5 weeks ago    195MB
debian-httpd   2.0       c18831e834fc   5 weeks ago    195MB
httpd          latest    c18831e834fc   5 weeks ago    195MB
webserver      4.0       c18831e834fc   5 weeks ago    195MB
nginx          latest    12ef77b9fab6   6 weeks ago    192MB
debian         latest    48f404e78da4   6 weeks ago    139MB
busybox        latest    fc9db2894f4e   4 months ago   4.04MB

# docker image save 명령을 이용해 이미지를 tar 파일로 저장한다
$ docker image save mysql:latest > test-mysql.tar
$ ls -lh test-mysql.tar
-rw-r--r--  1 user  user   608M 11 26 17:29 test-mysql.tar

# tar 명령의 옵션 중 tvf(t(list), v(verbose), f(file))를 이용해 묶인 파일 내용을 확인할 수 있다. 이미지 레이어들의 다이제스트값으로 만들어진 디렉터리 파일이다.
$ tar tvf test-mysql.tar
drwxr-xr-x  0 0      0           0 10 25 01:24 006018549fe46f72d6f5c313afeac1557962aa5a2ea78a84c3ea9f10db14ff71/
-rw-r--r--  0 0      0           3 10 25 01:24 006018549fe46f72d6f5c313afeac1557962aa5a2ea78a84c3ea9f10db14ff71/VERSION
-rw-r--r--  0 0      0         477 10 25 01:24 006018549fe46f72d6f5c313afeac1557962aa5a2ea78a84c3ea9f10db14ff71/json
-rw-r--r--  0 0      0        6656 10 25 01:24 006018549fe46f72d6f5c313afeac1557962aa5a2ea78a84c3ea9f10db14ff71/layer.tar
drwxr-xr-x  0 0      0           0 10 25 01:24 240ad7f04d4be32670bfd2f8d30e6ae1edee95a3eaebc2652cb0f4d66376220d/
-rw-r--r--  0 0      0           3 10 25 01:24 240ad7f04d4be32670bfd2f8d30e6ae1edee95a3eaebc2652cb0f4d66376220d/
...

# 다시 불러오는 실습을 위해 이미지 삭제 후 조회
$ docker image rm mysql:latest
$ docker images

# docker image load 명령을 이용해 파일로 만들어진 이미지 tar 파일 내용을 불러온다
$ docker image load < test-mysql.tar
03486b619b8a: Loading layer [==================================================>]  121.1MB/121.1MB
3dd67e0995d4: Loading layer [==================================================>]  11.26kB/11.26kB
ab43e2b85120: Loading layer [==================================================>]  2.406MB/2.406MB
57131b673ab1: Loading layer [==================================================>]   14.3MB/14.3MB
b8eecd8e6843: Loading layer [==================================================>]  6.656kB/6.656kB
dd5e71bdf24c: Loading layer [==================================================>]  3.072kB/3.072kB
5b5efa882b3f: Loading layer [==================================================>]  196.9MB/196.9MB
855ace31b698: Loading layer [==================================================>]  3.072kB/3.072kB
60881a8cc619: Loading layer [==================================================>]  302.6MB/302.6MB
484a9239a160: Loading layer [==================================================>]  17.41kB/17.41kB
Loaded image: mysql:latest

# 도커 허브로부터 내려받은 이미지처럼 조회가 가능하다
$ docker images
```

tar 파일로 가져온 이미지를 불러오는 다른 방법으로 `docker import` 를 이용할 수 있다. 로컬에 저장된 tar 파일을 기반으로 새롭게 지정한 이미지명과 태그로 이미지 등록이 가능하다.

```
$ cat test-mysql.tar | docker import - mysql:1.0
sha256:8de74d9b3a4c8de77eb16f1b3d64502f5eee3a6742228ef4367af1c0ff0f8295

$ docker images
```

만약 tar 파일의 용량을 줄이고 싶다면 docker image save 에 gzip 옵션을 추가할 수 있다.

```
$ docker image save mysql:latest | gzip > test-mysqlzip.tar.gz
$ ls -lh test-mysqlzip.tar.gz
-rw-r--r--  1 user  user   162M 11 26 17:40 test-mysqlzip.tar.gz

# 약 500MB 정도 용량이 감소된 것을 확인할 수 있다. 불러오는 방법은 동일하다.
```

셸 스크립트 변수 방식을 이용하여 모든 이미지를 하나의 파일로 저장할 수 있다.

```
$ docker image save -o all_image.tar $(docker image ls -q)
$ ls -lh all_image.tar
-rw-------  1 user  user   1.6G 11 26 17:43 all_image.tar
```

도커는 `docker image save` 와 같이 이미지를 파일로 관리하는 몇 가지 다른 방식이 있다.

컨테이너를 파일로 관리하는 `docker export/import` 와 컨테이너를 이미지로 생성하는 `docker commit` 도 제공한다.

<br>

**도커 이미지 삭제**

도커 허브를 통해 다운로드한 이미지는 종류에 따라 용량이 다르다. 이미지를 계속 다운로드하게 되면 로컬 서버의 저장 용량을 많이 차지하여 공간문제를 야기하기도 한다. 이런 문제를 해결하기 위해 `docker image save` 를 통해 이미지를 백업하거나 주기적으로 불필요한 이미지는 삭제하는 것이 좋다.

하나 이상의 도커 이미지를 삭제하는 방법은 다음과 같다. 정식 명령은 `docker image rm` 이고, 단축 명령으로 `docker rmi` 를 제공한다.

```
$ docker image rm [옵션] {이미지 이름[:태그] | 이미지 ID}

$ docker rmi [옵션] {이미지 이름[:태그] | 이미지 ID}
```

도커 이미지는 현재 사용 중인 컨테이너가 없으면 바로 삭제된다.

태그가 있는 이미지 원본은 태그된 이미지와 상관없이 삭제할 수 있다.

```
# 이미지 삭제 시 latest 버전을 제외한 나머지는 반드시 태그명을 명시해야 한다.
$ docker image rm ubuntu
Error: No such image: ubuntu

$ docker image rm ubuntu:14.04
Untagged: ubuntu:14.04

# 이미지 ID를 이용한 이미지 삭제, 현재 다른 태그 참조로 인한 오류 발생.
$ docker image rm c18831e834fc
Error response from daemon: conflict: unable to delete c18831e834fc (must be forced) - image is referenced in multiple repositories

# 태그가 지정된 모든 httpd 관련 이미지 모두 삭제 (-f 옵션 이용)
$ docker image rm -f c18831e834fc (이미지ID 앞 글자 몇 자만 써도 삭제 가능)

# 리눅스 셸 스크립트의 변수 활용 방식을 활용할 수 있다.
# 이미지 전체 삭제
$ docker rmi $(docker images -q)

# 특정 이미지 이름이 포함된 것만 삭제
$ docker rmi $(docker images | grep debian)

# 반대로 특정 이미지 이름이 포함된 것만 제외하고 모두 삭제
$ docker rmi $(docker images | grep -v centos)

# 자주 사용하는 명령을 alias 로 적용하여 활용하면 편리하다
$ vi .bashrc
...

# 상태가 exited 인 container 를 찾아서 모두 삭제
alias cexrm='docker rm $(docker ps --filter 'status=exited' -a -q)'

# 설정한 alias 를 적용하고 확인
$ source .bashrc
$ alias
...
```

컨테이너가 실행 중인 이미지를 삭제한다면 다음과 같은 에러가 발생한다. 현재 참조중인 컨테이너가 있기 때문에 삭제되지 않는다는 메세지다.

```
$ docker rmi nginx
Error response from daemon: conflict: unable to remove repository reference "nginx" (must force) - container d29fb919526d is using its referenced image 12ef77b9fab6
```

먼저 구동 중인 컨테이너를 stop 한 뒤 rm 을 통해 제거한 후 이미지 삭제가 가능하다.

이미지는 컨테이너 구동을 위해 존재한다. 로컬에 다운로드한 이미지 중 하나 이상의 컨테이너가 연결 되지 않은 모든 이미지 제거를 위해 `docker image prune` 명령을 사용한다.

`--filter` 옵션을 이용하면 특정 기간이나 이미지 라벨을 지정하여 제거 대상 이미지를 선별할 수 있다.

```
# -a 옵션을 이용하면 사용 중이 아닌 모든 이미지가 제거
$ docker image prune -a
WARNING! This will remove all images without at least one container associated to them.
Are you sure you want to continue? [y/N] y
Deleted Images:
...

# 사용 중이 아닌 48시간 이전(--filter)의 모든 이미지(-a)를 별도 확인 없이(-f) 제거
$ docker image prune -a -f --filter 'until=48h'
```

여기까지 도커 이미지와 관련된 명령에 대해 알아봤다.

이제 이미지를 참조해서 애플리케이션 서비스로 동작시킬 수 있는 컨테이너에 대해 알아본다.

<br>
