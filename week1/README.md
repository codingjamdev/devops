## week1

__개발 빌드 환경 구성 및 Docker 빌드 자동화__

CI 도구를 통해 소스 관리 하고 master에 merge가 되면 어플리케이션을 도커로 빌드 자동화, 레지스트리에 등록

### Create your private registery 

https://docs.aws.amazon.com/AmazonECR/latest/userguide/repository-create.html 


### Upload source code to github repo

```bash
├── Dockerfile
├── app.py
├── buildspec.yml
└── requirements.txt
```

### Setup the codebuild

https://ap-northeast-2.console.aws.amazon.com/codesuite/codebuild/projects

1. 소스: Github, 내 GitHub 계정의 리포지토리
2. Webhook: 코드 변경이 이 리포지토리에 푸시될 때마다 다시 빌드 선택
3. 이벤트 유형: PULL_REQUEST_*
4. 환경: 관리형 이미지, Ubuntu, Standard, aws/codebuild/standard:4.0, 권한 승격 활성화
5. 서비스 역할: 새 서비스 역할 (프로젝트 생성 후 IAM에서 추후 업데이트)
6. 환경 변수:
   ```
   AWS_DEFAULT_REGION: ap-northeast-2
   AWS_ACCOUNT_ID: <Account-ID>
   IMAGE_TAG: latest
   IMAGE_REPO_NAME: <ECR-Repo-name>
   ```


### Add permission in IAM role

CodeBuild가 도커 이미지를 Amazon ECR 리포지토리에 업로드 가능 하도록 역할 __codebuild-devops-service-role__ 에 정책 추가

```
{
    "Action": [
        "ecr:BatchCheckLayerAvailability",
        "ecr:CompleteLayerUpload",
        "ecr:GetAuthorizationToken",
        "ecr:InitiateLayerUpload",
        "ecr:PutImage",
        "ecr:UploadLayerPart"
    ],
    "Resource": "*",
    "Effect": "Allow"
}
```

### Verify Codebuild Job manually

수동으로 수행 및 콘솔에서 확인

### ECR image 

이미지가 정상적으로 업로드 되었는지 확인 