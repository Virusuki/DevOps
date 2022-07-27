# Crossplane provider를 이용한 internet gateway 생성

### internet gateway 예제
- igw.yaml

```
apiVersion: ec2.aws.crossplane.io/v1beta1
kind: InternetGateway
metadata:
  name: eks-internetgateway
spec:
  forProvider:
    region: ap-northeast-2
    vpcIdRef:
      name: eks-crossplane-vpc-namuk1
  providerConfigRef:
    name: awsconfig
```


