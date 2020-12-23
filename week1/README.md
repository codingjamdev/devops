## week1

__개발 빌드 환경 구성 및 Docker 빌드 자동화__

CI 도구를 통해 소스 관리 하고 master에 merge가 되면 어플리케이션을 도커로 빌드 자동화, 레지스트리에 등록

__Before you start make sure you have permission and account:__
* Create your private registery:  https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html 

### Setup the codebuild
* Go to: https://ap-northeast-2.console.aws.amazon.com/codesuite/codebuild/projects?region=ap-northeast-2&projects-meta=eyJmIjp7InRleHQiOiIiLCJzaGFyZWQiOmZhbHNlfSwicyI6eyJwcm9wZXJ0eSI6IkxBU1RfTU9ESUZJRURfVElNRSIsImRpcmVjdGlvbiI6LTF9LCJuIjoyMCwiaSI6MH0