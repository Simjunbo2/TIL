## Git 내용 정리 2022 - 12 - 28
---
### 🍯오늘은 local의 Git버전관리 Directory를 GIthub Repository와 연동하여 로컬 디렉터리 안의 파일을 Push하는 방법에 대해 배웠습니다

---
## 🌈Command
* **로컬 저장소를 Git 버전관리 저장소로 만들기**
    * directory 내에서 git init<br><br>
* **수정된 파일을 스테이징 영역에 추가하기 ⚡commit으로 변경할 파일들을 스테이징 영역에 모아놓는다.**
    * git add <파일명><br><br>
* **스테이징 영역에 추가된 파일을 commit**
    * 스테이징 영역에 존재하는 파일들을 변경하고 기록을 남긴다.<br><br>
* **Github 원격 저장소 추가하기**
    * git remote add origin <저장소 경로.git><br><br>
* **GITHUB원격저장소에 Commit된 파일들 Push하기**
    * git push origin master(branch name)<br><br>
*  **Github 원격 파일 삭제하기**
    * 원격 저장소만 삭제 : git rm --cached <file_name> 
    * 원격 저장소와 로컬 저장소에 있는 파일을 삭제 : git rm [File Name]
---
## 🌞GIt 디렉터리 이름을 변경해도 괜찮을까❓
* 답은 O 
* 디렉터리 내의 .git이 버전관리를 위한 파일이기 때문에  디렉터리 이름을 바꾸어도 .git으로 버전관리가 된다.
---
## 🌞.Git 디렉터리를 지워도 될까❓
* 답은 X
* 버전관리 했던 내역이 모두 지워진다.
---
## 🌞목표라는 디렉터리를 다른 곳으로 이동 가능할까❓
* 답은 반반
* 가능하지만 다른 GIT저장소 디렉터리의 하위 디렉터리로 들어오게 되면 X
---
<br><br>
## 중앙 집중식 버전관리란 ❓
* 로컬에서 파일을 편집하고 서버에 반영
* 중앙 서버에서 파일에 대한 버전관리 실행

<br><br>
## 분산 버전 관리 시스템 ❓
* Git이 대표적!
* 서버가 아닌 **로컬에서도 버전을 기록하고 관리**가 가능!
* Github 클라우드를 활용하여 협업이 가능!<br><br>

---
## .gitignore❗
- 버전관리를 하지 않을 파일을 지정한다.
- commit전에 미리 gitignore에 파일명을 지정한다.
- docker의 .dockerignore와 동일한 개념이다.<br><br><br><br>
    * 작성방법
```

```
---

## Git push 실패 ❓

![실패시 나오는 문구](./jenkins%26K8S%20%EC%9D%B4%EB%AF%B8%EC%A7%80/PushError.png)
* **원인** = 로컬과 원격 저장소의 커밋 이력이 다르기 때문에
* **해결방법(순서대로)** 
    * 원격저장소의 커밋을 로컬로 pull
    * 로컬에서 두 커밋을 병합
    * 다시 git push