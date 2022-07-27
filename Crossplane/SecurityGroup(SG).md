```
apiVersion: ec2.aws.crossplane.io/v1beta1
kind: SecurityGroup
metadata:
  name: ingress-lb-namuktest2
spec:
  deletionPolicy: Delete
  forProvider:
    region: ap-northeast-2
    vpcId: vpc-091267f3adf55ac33
    groupName: ingress-lb-namuk
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
