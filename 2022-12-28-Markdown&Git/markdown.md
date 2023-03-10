## ๐์ค๋ ํด์ผํ  ์ผ ##
---
* ๐๋งํฌ ๋ค์ด ์์ฑ ๋ณต์ต   
      **๐[Markdown_Practice_Link](https://jbt.github.io/markdown-editor/)**
* ๐k8s + jenkins ์ฐ๋ํ๊ธฐ
---
## ๐ํด์ผ ํ  ์ผ์ Python print๋ก ์์ฑํด๋ณด์ ##

```python
print("k8s + jenkins")
print("๊น๋ํ ํ์ด์ฌ ๋จ๋จํ ๋ฐฑ์๋ 5๋จ์ ๊น์ง ์ฝ๊ธฐ")
```
---
## ๐k8s + jenkins Logo ##
![์๋ฌด์ด๋ฆ](./jenkins%26K8S%20%EC%9D%B4%EB%AF%B8%EC%A7%80/jenkins.gif)
![์๋ฌด๊ฑฐ๋2](./jenkins%26K8S%20%EC%9D%B4%EB%AF%B8%EC%A7%80/k8s.gif)
## ๐์ฒ๋ฆฌ ๋ก์ง ##
* cluster ํ๊ฒฝ์์ jenkins์คํ
* ๋์ปค sock๊ณต์ ํ์ฌ dockerํ๊ฒฝ์ ๊ณต์ ํ๋ dood๋ฐฉ์ ์ค์ 
* jenkins github pushํธ๋ฆฌ๊ฑฐ๋ฅผ ์ด์ฉํ๋ webhook ์ค์ 
* pipeline ์ค์  ->gitํ๋ก์ ํธ rootํด๋์ jenkinsfile์ ์ฝ๊ฒ ์ค์ ํ๋ค. ์ด๋ Definition์ ํ์ฐฝ์์ Pipeline script from SCM์ ์ ํ
* kubeconfig์ ์ ๊ทผํ๊ธฐ ์ํ k8s config credential์ค์ 
* From a file on the Jenkins master -> ๋ง์คํฐ ๋ธ๋์ kube-config.yaml ํ์ผ์ jenkins ์๋ฒ ํน์  ์์น์ ์์น์ํค๊ณ  ๊ฒฝ๋ก๋ฅผ ๊ธฐ์ํจ์ผ๋ก์จ ์ฝ๋ ๋ฐฉ๋ฒ
* ์ฟ ๋ฒ๋คํฐ์ค ์ฐ๋ ํ์ธ

## โจpipe line ex ##
```yaml
\/* pipeline ๋ณ์ ์ค์  */
def app

node {
    // gitlab์ผ๋ก๋ถํฐ ์์ค ๋ค์ดํ๋ stage
    stage('Checkout') {
            checkout scm   
    }
 
    // mvn ํด ์ ์ธํ๋ stage, ํ์์ ๊ฒฝ์ฐ maven 3.6.0์ ์ฌ์ฉ์ค
    stage('Ready'){  
        sh "echo 'Ready to build'"
        mvnHome = tool 'Maven 3.6.0'
    }

    // mvn ๋น๋๋ก jarํ์ผ์ ์์ฑํ๋ stage
    stage('Build'){  
        sh "echo 'Build Spring Boot Jar'"
        sh "'${mvnHome}/bin/mvn' clean package"
    }

    //sonarqube ์ ์ ๋ถ์ ์คํํ๋ stage, jenkins์ sonarqube์ฐ๋์ ํ์ง ์์๋ค๋ฉด ์ด๋ถ๋ถ์ ์ฃผ์์ฒ๋ฆฌ
    stage('Static Code Analysis') {  
        sh "'${mvnHome}/bin/mvn' clean verify sonar:sonar -Dsonar.projectName=pipeline_test -Dsonar.projectKey=pipeline_test -Dsonar.projectVersion=$BUILD_NUMBER"
    }

    //dockerfile๊ธฐ๋ฐ ๋น๋ํ๋ stage ,git์์ค root์ dockerfile์ด ์์ด์ผํ๋ค
    stage('Build image'){   
        app = docker.build("cross9308/dockertest")
    }


    //docker image๋ฅผ pushํ๋ stage, ํ์๋ dockerhub์ ์ด๋ฏธ์ง๋ฅผ ์ฌ๋ ธ์ผ๋ ๋ณดํต private image repo๋ฅผ ๋ณ๋ ๊ตฌ์ถํด์ ์ฌ์ฉํ๋๊ฒ์ด ์ข์
    //docker.withRegistry์ dockerhub๋ ์์ ์ค์ ํ dockerhub credentials์ ID์ด๋ค.
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
    
    // kubernetes์ ๋ฐฐํฌํ๋ stage, ๋ฐฐํฌํ  yamlํ์ผ(ํ์์ ๊ฒฝ์ฐ test.yaml)์ jenkinsfile๊ณผ ๋ง์ฐฌ๊ฐ์ง๋ก git์์ค root์ ์์น์ํจ๋ค.
    // kubeconfigID์๋ ์์ ์ค์ ํ Kubernetes Credentials๋ฅผ ์๋ ฅํ๊ณ  'sh'๋ ์ฟ ๋ฒ๋คํฐ์ค ํด๋ฌ์คํฐ์ ์๊ฒฉ์ผ๋ก ์คํ์ํฌ ๋ช๋ น์ด๋ฅผ ๊ธฐ์ ํ๋ค.
    stage('Kubernetes deploy') {
        kubernetesDeploy configs: "test.yaml", kubeconfigId: 'Kuberconfig'
        sh "/usr/local/bin/kubectl --kubeconfig=/u01/kube-config.yaml rollout restart deployment/test-deployment -n zuno"
    }

    stage('Complete') {
        sh "echo 'The end'"
    }
}
```
## Fin๐ ##
---