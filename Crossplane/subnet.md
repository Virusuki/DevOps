apiVersion: ec2.aws.crossplane.io/v1beta1
kind: Subnet
metadata:
  name: eks-score-namuk1
spec:
  forProvider:
    region: ap-northeast-2
    availabilityZone: ap-northeast-2a
    cidrBlock: 10.0.1.0/24
    vpcIdRef:
      name: eks-crossplane-vpc-namuk1
    mapPublicIPOnLaunch: true
  providerConfigRef:
    name: awsconfig

---

apiVersion: ec2.aws.crossplane.io/v1beta1
kind: Subnet
metadata:
  name: eks-score-namuk2
spec:
  forProvider:
    region: ap-northeast-2
    availabilityZone: ap-northeast-2b
    cidrBlock: 10.0.2.0/24
    vpcIdRef:
      name: eks-crossplane-vpc-namuk1
    mapPublicIPOnLaunch: true
  providerConfigRef:
    name: awsconfig
    
