# Crossplane provider를 이용한 vpc 생성 및 aws 웹 콘솔 확인
### VPC 예제


```
apiVersion: ec2.aws.crossplane.io/v1beta1
kind: VPC
metadata:
  name: eks-crossplane-vpc-namuk1
spec:
  forProvider:
    region: ap-northeast-2
    cidrBlock: 10.0.0.0/16
    enableDnsSupport: true
    enableDnsHostNames: true
    instanceTenancy: default
  providerConfigRef:
    name: awsconfig
```
---
```
apiVersion: ec2.aws.crossplane.io/v1beta1
kind: VPC
metadata:
  name: eks-crossplane-vpc-namuk2
spec:
  forProvider:
    region: ap-northeast-2
    cidrBlock: 10.1.0.0/16
    enableDnsSupport: true
    enableDnsHostNames: true
    instanceTenancy: default
  providerConfigRef:
    name: awsconfig
```
