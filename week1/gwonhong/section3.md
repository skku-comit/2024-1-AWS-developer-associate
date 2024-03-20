# section3

## history

- 내부적으로만 쓰다가 돈이 되겠다 싶어서 SQS, S3, EC2와 같은 제품으로 출시하며 성장

## use case

- Netflix, ...
- Enterprise IT, Backup & Storage, ...
- Website, ...
- Game, ...

## https://infrastructure.aws

- aws의 물리적 서버와 연결 관게를 지도로 보여주는 사이트!

## AWS Regions

- Region: a cluster of data centers
- most AWS services are 'region-scoped'
- region 고르는 기준:
  1. 법을 따르라: 허가 없이 데이터 반출이 안되는 국가 존재
  2. 고객과 가까이: latency 감소
  3. 모든 region에 모든 서비스가 존재하지 않음!
  4. 가격: region마다 조금씩 다름

## AWS Availability Zones

- Each region has 3-6 availability zones (예를 들어 ap-southeast-2a, 2b, 2c)
- 재난으로부터 분리되어 spof를 피함
- 서로 초저지연 연결이 되어있다고 함

## AWS Points of Presence (Edge Locations)

- 나중에 자세히 다룸

## AWS Console

### Global Services

- Identity and Access Management (IAM)
- Route 53 (DNS)
- CloudFront (CDN)
- WAF (Web Application Firewall)

### 그 외 대부분의 region-scoped services

- EC2 (Infra aaS)
- Elastic Beanstack (Platform aaS)
- Lambda (Function aaS)
- Rekognition (Software aaS)
- **모두 [region table](https://aws.amazon.com/ko/about-aws/global-infrastructure/regional-product-services/?p=ngi&loc=4)에서 확인 가능**

## `New EC2 Experience`

- AWS가 대대적인 ui update를 진행 중이고 강의랑 다를 수 있으니 헷갈리면 옛날 ui로 전환해서 보세요!
