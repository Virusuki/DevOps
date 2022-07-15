Overview
- Crossplane은 Kubernetes API를 사용하여 애플리케이션에서 필요한 인프라스트럭처를 Kubernetes에서 직접 관리할 수 있게 해주는 프로젝트이다.
- 또한, Crossplane을 K8S를 확장한 Control plane 명명하며, 클라우드에서 SaaS형태로 crossplane을 제공한다.
- upbount팀은 SaaS 형태의 Crossplane을 Hosted crossplane이라 부르며, 간략히 설명하면 upbound가 K8S cluster를 제공하고, 그 제공된 Cluster에 crossplane operator를 설치해서 제공하며, kubectl과 kubectl crossplane을 사용하는 형태이다.

