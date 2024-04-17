---
layout: post
title: 완벽한 IT 인프라 구축을 위한 Kubernetes - 용어정리
subtitle: Kubernetes
date: 2023-11-22
author: Warner
header-img: img/bg/post-bg-kubernetes.png
catalog: true
tags:
  - Kubernetes
---

## Kubernetes의 개요

### Kubernetes란?

Kubernetes는 여러 개의 호스트를 하나로 묶어 Docker를 이용하기 위한 오케스트레이션 툴로,

분산 환경에서 ‘마치 한 대의 컴퓨터’처럼 투과적으로 컨테이너에 액세스할 수 있습니다.

주요기능

- 여러 서버들에서의 컨테이너 관리
- 컨테이너 간 네트워크 관리
- 컨테이너의 부하분산
- 컨테이너의 감시
- 무정지로 업데이트

### Kubernetes의 서버구성

**마스터서버(Kubernetes Master)**

- Kubernetes 클러스터 안의 컨테이너를 조작하기 위한 서버
- kubectl 커맨드 수행
- 리소스 사용상황 확인, 컨테이너를 시작할 노드를 자동으로 선택

**백엔드 데이터베이스(etcd)**

- etcd라 부르는 분산 키 밸류 스토어(KVS)를 사용하여 클러스터의 구성 정보를 관리
- 데이터베이스를 마스터 서버 상에 구축하는 경우도 있음
- 다중화를 검토할 필요가 있음

**노드(Node)**

- 실제로 Docker 컨테이너를 잘동시키는 서버
- 노드를 여러개 마련하여 클러스터를 구성
- 노드의 관리는 마스터 서버가 진행
- 클라우드에서는 가상 머신의 인스턴스가 노드가 된다.

### 애플리케이션 구성 관리

**Pod(포드)**

- Kubernetes에서는 여러 개의 컨테이너를 모아서 ‘Pod’로 관리
- Pod는 반드시 동일한 노드 상에 동시에 전개되는 특징이 있음
- Pod안의 여러 컨테이너가 가상NIC를 공유하는 구성, 컨테이너끼리 localhost경유로 통신 가능
- 공유 디렉토리를 통하여 로그 정보를 주고받을 수 있음
- 노드안에는 여러 개의 Pod가 배치

![pod.png](/img/post/2023/2023-11-22/pod.png)
**ReplicaSet(리플리카 셋)**

- Kubernetes 클러스터 상에서 미리 지정된 Pod를 작성하여 실행시켜 두는 장치이다.
- 클러스터 상에 정해진 수의 Pod를 반드시 실행시켜 둔다
- 실행중인 Pod를 감시, 장애와 같은 이유로 정지된 경우 해당Pod를 삭제하고, 새로운 Pod를 실행
- 클라우드 안에 Pod를 얼마나 실행시켜 둘지를 ‘리플리카 수’ 라고 한다.
- ReplicaSet을 사용하면 애플리케이션 개발자는 전개한 Pod가 어떤 상태인지를 신경 쓸 필요 없이 항상 지정한 개수만큼 Pod가 실행된 상태를 Kubernetes가 유지해 준다.

**Deployment(디플로이먼트, 전개)**

- Pod와 ReplicaSet을 모은것으로, ReplicaSet의 이력을 관리하는 것 이다.
- 정의된 리플리카의 수를 유지하는 역할은 ReplicaSet이고, ReplicaSet의 작성이나 갱신을 정의하는 것이 Deployment이다.

### 네트워크 관리(Service)

- Kubernetes클러스터 안에서 실행되는 Pod에 대해 외부로부터 엑세스할 때는 서비를 정의한다.
- Load Balancer
    - Service에 대응하는 IP주소 + 포트 번호에 엑세스하면 여러Pod에 대한 레이어 4 레벨의 부하분산이 일어난다.
- IP주소
    - Cluster IP주소
        - 클러스터 안의 Pod끼리 통신을 하기 위한 프라이빗 IP주소
        - 클러스터 안의 Pod에서 Cluster IP로 보내는 패킷은 Proxy 데몬이 받아 수신 Pod로 전송한다.
    - External IP주소
        - 외부 클라이언트가 연결하기 위한 퍼블릭IP 주소이다.
        - Pod를 새로 실행하면 기존 서비스의 IP주소와 포트번호는 환경변수로 참조할 수 있다.
- Ingress
    - Pod 에 대한 통신을 제어하는 기능
    - 서비스와 연결된 통신 내용을 프록시한다.