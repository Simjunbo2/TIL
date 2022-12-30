## 📕오늘 해야할 일 ##
---
* 🎈마크 다운 작성 복습   
      **📂[Markdown_Practice_Link](https://jbt.github.io/markdown-editor/)**
* 🎈k8s + jenkins 연동하기
---
## 📕해야 할 일을 Python print로 작성해보자 ##

```python
print("k8s + jenkins")
print("깔끔한 파이썬 단단한 백엔드 5단원 까지 읽기")
```
---
## 📕k8s + jenkins Logo ##
![아무이름](./jenkins%26K8S%20%EC%9D%B4%EB%AF%B8%EC%A7%80/jenkins.gif)
![아무거나2](./jenkins%26K8S%20%EC%9D%B4%EB%AF%B8%EC%A7%80/k8s.gif)
## 📕처리 로직 ##
* cluster 환경에서 jenkins실행
* 도커 sock공유하여 docker환경을 공유하는 dood방식 설정
* jenkins github push트리거를 이용하는 webhook 설정
* pipeline 설정 ->git프로젝트 root폴더에 jenkinsfile을 읽게 설정한다. 이는 Definition선택창에서 Pipeline script from SCM을 선택
* kubeconfig에 접근하기 위한 k8s config credential설정
* From a file on the Jenkins master -> 마스터 노드의 kube-config.yaml 파일을 jenkins 서버 특정 위치에 위치시키고 경로를 기입함으로써 읽는 방법
* 쿠버네티스 연동 확인

## ✨pipe line ex ##
```yaml
\/* pipeline 변수 설정 */
def app

node {
    // gitlab으로부터 소스 다운하는 stage
    stage('Checkout') {
            checkout scm   
    }
 
    // mvn 툴 선언하는 stage, 필자의 경우 maven 3.6.0을 사용중
    stage('Ready'){  
        sh "echo 'Ready to build'"
        mvnHome = tool 'Maven 3.6.0'
    }

    // mvn 빌드로 jar파일을 생성하는 stage
    stage('Build'){  
        sh "echo 'Build Spring Boot Jar'"
        sh "'${mvnHome}/bin/mvn' clean package"
    }

    //sonarqube 정적분석 실행하는 stage, jenkins와 sonarqube연동을 하지 않았다면 이부분은 주석처리
    stage('Static Code Analysis') {  
        sh "'${mvnHome}/bin/mvn' clean verify sonar:sonar -Dsonar.projectName=pipeline_test -Dsonar.projectKey=pipeline_test -Dsonar.projectVersion=$BUILD_NUMBER"
    }

    //dockerfile기반 빌드하는 stage ,git소스 root에 dockerfile이 있어야한다
    stage('Build image'){   
        app = docker.build("cross9308/dockertest")
    }


    //docker image를 push하는 stage, 필자는 dockerhub에 이미지를 올렸으나 보통 private image repo를 별도 구축해서 사용하는것이 좋음
    //docker.withRegistry에 dockerhub는 앞서 설정한 dockerhub credentials의 ID이다.
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
    
    // kubernetes에 배포하는 stage, 배포할 yaml파일(필자의 경우 test.yaml)은 jenkinsfile과 마찬가지로 git소스 root에 위치시킨다.
    // kubeconfigID에는 앞서 설정한 Kubernetes Credentials를 입력하고 'sh'는 쿠버네티스 클러스터에 원격으로 실행시킬 명령어를 기술한다.
    stage('Kubernetes deploy') {
        kubernetesDeploy configs: "test.yaml", kubeconfigId: 'Kuberconfig'
        sh "/usr/local/bin/kubectl --kubeconfig=/u01/kube-config.yaml rollout restart deployment/test-deployment -n zuno"
    }

    stage('Complete') {
        sh "echo 'The end'"
    }
}
```
## Fin🎉 ##
---