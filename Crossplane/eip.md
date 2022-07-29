# Crossplane provider를 이용한 eip 생성

### eip 예제
- eip.yaml

```
apiVersion: ec2.aws.crossplane.io/v1beta1
kind: Address
metadata:
  name: sample-eip
spec:
  forProvider:
    region: ap-northeast-2
    domain: vpc
  providerConfigRef:
    name: awsconfig
```
