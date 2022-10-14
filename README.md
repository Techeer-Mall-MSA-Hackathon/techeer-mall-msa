### 진행 동기

MSA와 EDA에 대해 좀 더 깊게 알고 그동안 머리 속에만 가지고 있던 개념들을 적용해 보면서 정리하기 위함이다. 또한 그 동안 공부한 Kubernetes와 CQRS, Event Sourcing를 적용해 보면서 보다 명확하게 내 지식으로 만들기 위해 진행한다.

아래 영상에 나오는 이벤트 스토밍을 활용하여 시스템을 설계 한다.

[https://www.youtube.com/watch?v=hUcpv5fdCIk](https://www.youtube.com/watch?v=hUcpv5fdCIk)
![image](https://user-images.githubusercontent.com/58874807/195865949-424e1d1f-b77d-4ff0-a278-f3003f066521.png)
### 진행 기간

1주일 동안 끝낼 수 있는 규모로 제작한다.

### 적용 기술

Terraform, Ansible을 통한 aws 관리

- 적용 이유
    - 학생이기 때문에 gcp를 계속 켜 놓는 것은 비용적으로 부담이 된다.
    - 따라서 프로젝트를 수행하는 시간 이외에는 서비스를 꺼놓고 싶은데
    - 매번 프로젝트를 실행할 때마다 인프라 세팅을 하는 것은 시간적으로도 낭비가 있고
    - 다른 환경에서 작업할 수 있는 확률도 존재하므로 프로젝트 환경을 통일하고 시간을 절약하기 위해 사용하기로 결정

gcp Pub/Sub

- 적용 이유
    - Apache Kafka를 직접 사용할 수도 있지만 환경을 세팅하는 것이 까다롭고 availabilty나 확장성 부분에서 gcp Pub/Sub가 더 유용하다고 판단이 되어 선택하게 되었다.

Spring Boot - java

- 적용 이유
    - 프로젝트

kubernetes

- 적용 이유
    - 도커 보다 확장에 용이 하며 kubernetes 생태계가 지원하는 다양한 플랫폼을 사용할 수 있다. 또한 kubernetes를 사용하면 기존 spring cloud를 활용하여 msa를 구성했을 때보다 인증 서버나 spring eruka server를 별도로 관리할 필요가 없다. 따라서 더욱 안정성 있는 서비스를 할 수 있기 때문에 사용하도록 했다. 여담으로 실리콘밸리 개발자의 조언을 들었는데 spring cloud를 이용한 MSA는 8~9년 전에 사용한 legacy로 현재는 잘 쓰지 않은 방식이라고 들었다. 따라서 k8s를 활용한 서비스를 구성하고자 한다.

모니터링 - prometheus + grafana

- 우선은 기본적인 모니터링 툴로 가장 대표적인 prometheus + grafana를 통해 모니터링 하기로 했으며 eks와 kenesis를 쓰는 만큼 google monitoring tool를 사용하기로 변경될 수도 있다. 모니터링 할 주요 포인트는 cpu memory 사용률, memory swap 여부 등을 모니터링 할 계획이다. memory swap 여부를 모니터링 하는 이유는 실제 서비스에서 memory swap이 일어날 경우 성능 상의 문제를 일으킬 수 있기 때문이다.

GCP GKE 기반으로 제작

- 자체 Kubernetes 제어 영역이나 작업자 노드를 설치 및 운영할 필요 없이 GCP에서 Kubernetes를 손쉽게 실행할 수 있다. 또한 확장성, 비정상 노드 탐지 및 보안에 유리하며 모니터링 측면에서도 이점이 있어 사용하게 되었다. 또한 AWS 보다 크레딧을 많이 제공하기 때문에 GCP를 사용하기로 했다.
