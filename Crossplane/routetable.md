# Crossplane provider를 이용한 routetable 생성

### RouteTable 예제
- routetable.yaml

```
apiVersion: ec2.aws.crossplane.io/v1beta1
kind: RouteTable
metadata:
  name: eks-routetable-namuk
spec:
  forProvider:
    region: ap-northeast-2
    routes:
      - destinationCidrBlock: 0.0.0.0/16
        gatewayIdRef:
          name: eks-internetgateway
    associations:
      - subnetIdRef:
          name: eks-score-namuk1
      - subnetIdRef:
          name: eks-score-namuk2
    vpcIdRef:
      name: eks-crossplane-vpc-namuk1
  providerConfigRef:
    name: awsconfig
```
