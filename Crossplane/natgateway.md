
# Crossplane provider를 이용한 natgateway 생성 및 aws 웹 콘솔 확인
### natgateway 예제


```
apiVersion: ec2.aws.crossplane.io/v1beta1
kind: NATGateway
metadata:
  name: sample-natgateway
spec:
  forProvider:
    region: ap-northeast-2
    allocationIdRef:
      name: sample-eip
    subnetIdRef:
      name: eks-score-namuk1
    tags:
      - key: Name
        value: eks-natgateway
  providerConfigRef:
    name: awsconfig
```
