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
