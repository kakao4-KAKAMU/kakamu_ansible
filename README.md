# 🚀 Infrastructure Automation & K8s GitOps Bootstrap

이 저장소는 **카카오 클라우드(Kakao Cloud)** 환경에서 **Ansible**과 **Kubespray**를 사용하여 인프라 구축을 자동화하고, **ArgoCD** 기반의 GitOps 환경을 부트스트래핑하기 위한 IaC(Infrastructure as Code) 프로젝트입니다.

---

## 🏗 System Architecture

본 프로젝트는 퍼블릭 서브넷의 Bastion Host를 통해 프라이빗 서브넷의 노드들을 관리하는 보안 지향적 아키텍처를 가집니다.

*   **Public Subnet**: Bastion Host (Gateway & NAT)
*   **Private Subnet**: K8s Control Plane (1), K8s Worker Nodes (3)
*   **Automation Flow**: GitHub Actions → Bastion Host → Private K8s Nodes

---

## 🛠 Tech Stack

| Category | Technology                    |
| :--- |:------------------------------|
| **Cloud** | Kakao Cloud (VM, VPC, Subnet) |
| **Provisioning** | Ansible (v2.15+)              |
| **K8s Setup** | Kubespray                     |
| **CI/CD** | GitHub Actions                |
| **GitOps** | ArgoCD (App of Apps Pattern)  |
| **Package Mgmt** | Helm (v3.20.2)                |

---

## 📂 Repository Structure

```text
.
├── .github/workflows/
│   └── k8s-deploy.yml       # GitHub Actions 자동화 워크플로우
├── inventory/
│   └── hosts.ini            # 클러스터 구성 및 노드 IP 정보 (Bastion, Master, Worker)
├── roles/
│   ├── helm/                # Helm 바이너리 설치 및 환경 구성 역할
│   │   └── tasks/
│   │       └── main.yml
│   └── argocd/              # ArgoCD 설치 및 Root App 배포 역할 (추가 예정)
├── .gitattributes           # Git 속성 설정 파일
├── bootstrap_k8s.yml        # K8s 초기 필수 서비스(Helm, ArgoCD) 세팅 메인 플레이북
└── README.md                # 프로젝트 문서