## Overview
- Crossplane은 Kubernetes API를 사용하여 애플리케이션에서 필요한 인프라스트럭처를 Kubernetes에서 직접 관리할 수 있게 해주는 프로젝트이다.
- 또한, Crossplane을 K8S를 확장한 Control plane 명명하며, 클라우드에서 SaaS형태로 crossplane을 제공한다.
- upbount팀은 SaaS 형태의 Crossplane을 Hosted crossplane이라 부르며, 간략히 설명하면 upbound가 K8S cluster를 제공한다.
- 그 제공된 Cluster에 crossplane operator를 설치해서 제공하며, kubectl과 kubectl crossplane을 사용하는 형태이다.
- AWS 클라우드 예) AWS 사용자는 aws provider package를 Crossplane이 설치된 K8S 클러스터에 설치 후, AWS Access Credential 정보를 갖는 config를 생성 후, 해당 config를 가지고 CR로 AWS resource를 생성/관리하게 된다.

### Crossplane Operator 설치
```
kubectl create namespace crossplane-system
helm repo add crossplane-stable https://charts.crossplane.io/stable
helm repo update 
helm install crossplane --namespace crossplane-system crossplane-stable/crossplane --version 1.3.0
```

### Crossplane CLI 설치
[방법1]
```
curl -sL https://raw.githubusercontent.com/crossplane/crossplane/master/install.sh | sh
sudo mv kubectl-crossplane /usr/bin
kubectl crossplane --help
```

[방법2]
아래는 AWS Provider CR 예로 실제로 동작하는 yaml 이다.
- AWS-Provider.yaml
```
apiVersion: pkg.crossplane.io/v1
kind: Provider
metadata:
  name: aws-provider
spec:
  package: crossplane/provider-aws:alpha
```

- 아래의 명령어는 설치된 패키지 확인 (aws provider 패키지)
```
kubectl get provider.pkg
```

### Provider Config 설정
- Secret 생성: AWS Access ID/Key pair를 저장하는 Secret 생성 : AWS 웹 콘솔에서 보안자격증명에서 확인 가능
```
echo "aws_access_key_id = 당신의아이디\naws_secret_access_key = 당신의키" > creds.conf
kubectl create secret generic aws-secret-creds -n crossplane-system --from-file=creds=./creds.conf
```

### Provider Config 생성
- provider-config.yaml
```
apiVersion: aws.crossplane.io/v1beta1
kind: ProviderConfig
metadata:
  name: awsconfig
spec:
  credentials:
    source: Secret
    secretRef:
      namespace: crossplane-system
      name: aws-secret-creds
      key: creds
```
- kubectl 파일 적용
```
kubectl -n crossplane-system apply -f provider-config.yaml
```

- 프로바이더 설정 확인
```
kubectl -n crossplane-system get provider
```

### AWS Security Group 생성
- securitygroup.yaml
```
apiVersion: ec2.aws.crossplane.io/v1beta1
kind: SecurityGroup
metadata:
  name: ingress-lb
spec:
  deletionPolicy: Delete
  forProvider:
    region: ap-northeast-2
    vpcId: vpc-0590570e043xxxxxx
    groupName: ingress-lb
    description: Security group for LB of Ingress Controller
    egress:
    - ipProtocol: "-1"  #all protocol
      ipRanges:
      - cidrIp: 0.0.0.0/0 #any
    ingress:
    - fromPort: 80
      toPort: 80
      ipProtocol: tcp
      ipRanges:
      - cidrIp: 0.0.0.0/0
    - fromPort: 443
      toPort: 443
      ipProtocol: tcp
      ipRanges:
      - cidrIp: 0.0.0.0/0
    tags:
    - key: creator
      value: crossplane-test
  providerConfigRef:
    name: awsconfig  ## 사용할 provider config
```




