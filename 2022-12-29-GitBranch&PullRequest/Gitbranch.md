 # Branch❔
---
## 📌Branch Command
*  **git branch (branch_name)** -> 생성
*  **git checkout (branch_name)** -> branch 이동 
    * **<span style="color:cyan">git checkout -b (branch_name)** -> branch이동 + 생성</span>

* **git branch** -> branch 목록
* **git branch -d (branch_name)** -> branch 삭제 
--- 
<br><br><br> 
 
 
>  # Github flow❔
 ## Github Pull Request(PR)을 통한 프로젝트 관리법 입니다.
---
* Local에서 개발자들이 Github Repository의 내용을 로컬에 clone.
* 이후 개발자들은 Branch라는 자신만의 작업 프로세스를 생성. 
* 독립된 작업 공간에서 소스 코드를 수정하고 commit.
* 해당 branch의 commit된 내용을 github으로 push.
* github에서 해당 branch의 Pull Request(PR)이벤트가 발생하고 해당 PR요청을 수락하여 master branch와 병합.
* merge이후에 최신화된 소스 코드를 다른 개발자가 pull로 받아오고 해당 개발자의 개별 branch에서 작업을 진행.
---
<br><br>
> # 개발 프로세스 실제 예
---
* **조장** : Github Repository 생성 후 소스코드 commit &Collaborator등록.<br>
<span style="color:cyan">(보통 오픈 소스의 경우에는 fork이후에 PullRequest를 날리고 PR요청을 받은 호스트가 허용을 하면 수정된 내용이 Update된다.)</span><br><br>
* 1️⃣**조원** : Local 환경에 Clone.
* 2️⃣**조원** : Local 환경에 branch 생성.
* 3️⃣**조원** : branch에서 수정된 파일을 commit 
* 4️⃣**조원** : git push origin (branchName)
* 5️⃣**조원** : Github -> Pull Request -> 승인을 받은 Host가 Merge진행
* 이후 Merge된 Master를 로컬에 pull해서 새로운 작업 진행


---
<br><br>
