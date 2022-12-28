# 🌈 Git And Markdown!! 

 ##  Markdown <br>

<span style="color:red">☁</span> 최소한의 문법으로 구성되어 있으며 순수 텍스트로 작성 가능합니다.<br><br>
<span style="color:orange">☁</span> 마크다운은 단순 텍스트 문법으로 내용을 작성하며, 다양한 환경에서 변환하여 보여집니다.<br><br>
<span style="color:yellow">☁ </span>마크다운은 오픈소스의 공식 문서를 작성하거나 개인 프로젝트의 프로젝트 소개서로 활용됩니다.<br><br><br>
## Markdown 문법 ##

### <span style="color:red">☁</span> Heading : 문서의 제목이나 소제목  <br><br>

### <span style="color:orange">☁</span> List : 목록 
* 순서가 있는 리스트 (ol) 
* 순서가 없는 리스트 (ul)
    <br><br>

### <span style="color:yellow">☁</span> Fenced Code Block
* 코드 블록은 backtick 3개를 활용해서 작성 (```) (" <- 이거 아님!) 
* 코드 블록에 특정 언어를 명시하면 Syntax Highlighting을 적용합니다.
    <br><br>

### <span style="color:palegreen">☁</span> Inline Code Block
* 코드 블록은 backtick 기호 1개를 인라인에 활용하여 작성합니다
    <br><br>
### <span style="color:cyan">☁</span> Link : 링크
* [문자열] + (URL)을 통해 링크 작성 가능
<br>
📕EX) [Kubenetis Example] + (https://junbo2.notion.site/40e85105ff6b47a5aed907f4c559af1b)<br>
📕결과)[Kubenetis Example](https://junbo2.notion.site/40e85105ff6b47a5aed907f4c559af1b)
<br><br>

### <span style="color:#800080">☁</span> Blockquotes : 인용문
<br>

### <span style="color:gold">☁</span> 그 외에도 ✔ 텍스트  강조 ✔ 수평선 ✔ 테이블 ✔등의 옵션이 있습니다.<br><br><br><br><Br>
---
 (GIT = Only_Use_Markdown)

 ##  GIT <br>
* GIT = Version Control System

* **백업 / 변경 사항 관리 / 소스 코드를 이전 상태로 되돌리기 / 협업 가능한 툴**
---
## GIT_Options
* GIT ADD → 다음 변경을 기록할 때까지 스테이징 영역에 모아놓는다. git commit를 통해 명시적으로 기록을 해야한다. 

* GIT COMMIT → 바로 로컬 저장소에 기록한다.

* GIT ADD는 GIT COMMIT를 통해 변경사항을 기록할 파일들을 모아놓는 개념이다. 그리고 GIT ADD를 하게되면 GIT ADD에 추가된 파일들만 COMMIT이 된다.
---
## git status
* **git status** - 파일의 상태를 확인
- **Untracted Files** → 트래킹 되지 않은 파일들 (add를 하지 않은 파일)
- **Changes to be committed** → 커밋될 변경사항들 → add하고 commit이 필요한 파일들

-  Tracked: 이전부터 버전으로 관리되고 있는 파일 상태

- ◾Unmodified: git status에 나타나지 않음

- ◾Modified: Changes not staged for commit  → add된 파일이 없다..?

- ◾Staged: Changes to be committed