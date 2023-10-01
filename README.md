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
