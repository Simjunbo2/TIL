 # Branchโ
---
## ๐Branch Command
*  **git branch (branch_name)** -> ์์ฑ
*  **git checkout (branch_name)** -> branch ์ด๋ 
    * **<span style="color:cyan">git checkout -b (branch_name)** -> branch์ด๋ + ์์ฑ</span>

* **git branch** -> branch ๋ชฉ๋ก
* **git branch -d (branch_name)** -> branch ์ญ์  
--- 
<br><br><br> 
 
 
>  # Github flowโ
 ## Github Pull Request(PR)์ ํตํ ํ๋ก์ ํธ ๊ด๋ฆฌ๋ฒ ์๋๋ค.
---
* Local์์ ๊ฐ๋ฐ์๋ค์ด Github Repository์ ๋ด์ฉ์ ๋ก์ปฌ์ clone.
* ์ดํ ๊ฐ๋ฐ์๋ค์ Branch๋ผ๋ ์์ ๋ง์ ์์ ํ๋ก์ธ์ค๋ฅผ ์์ฑ. 
* ๋๋ฆฝ๋ ์์ ๊ณต๊ฐ์์ ์์ค ์ฝ๋๋ฅผ ์์ ํ๊ณ  commit.
* ํด๋น branch์ commit๋ ๋ด์ฉ์ github์ผ๋ก push.
* github์์ ํด๋น branch์ Pull Request(PR)์ด๋ฒคํธ๊ฐ ๋ฐ์ํ๊ณ  ํด๋น PR์์ฒญ์ ์๋ฝํ์ฌ master branch์ ๋ณํฉ.
* merge์ดํ์ ์ต์ ํ๋ ์์ค ์ฝ๋๋ฅผ ๋ค๋ฅธ ๊ฐ๋ฐ์๊ฐ pull๋ก ๋ฐ์์ค๊ณ  ํด๋น ๊ฐ๋ฐ์์ ๊ฐ๋ณ branch์์ ์์์ ์งํ.
---
<br><br>
> # ๊ฐ๋ฐ ํ๋ก์ธ์ค ์ค์  ์
---
* **์กฐ์ฅ** : Github Repository ์์ฑ ํ ์์ค์ฝ๋ commit &Collaborator๋ฑ๋ก.<br>
<span style="color:cyan">(๋ณดํต ์คํ ์์ค์ ๊ฒฝ์ฐ์๋ fork์ดํ์ PullRequest๋ฅผ ๋ ๋ฆฌ๊ณ  PR์์ฒญ์ ๋ฐ์ ํธ์คํธ๊ฐ ํ์ฉ์ ํ๋ฉด ์์ ๋ ๋ด์ฉ์ด Update๋๋ค.)</span><br><br>
* 1๏ธโฃ**์กฐ์** : Local ํ๊ฒฝ์ Clone.
* 2๏ธโฃ**์กฐ์** : Local ํ๊ฒฝ์ branch ์์ฑ.
* 3๏ธโฃ**์กฐ์** : branch์์ ์์ ๋ ํ์ผ์ commit 
* 4๏ธโฃ**์กฐ์** : git push origin (branchName)
* 5๏ธโฃ**์กฐ์** : Github -> Pull Request -> ์น์ธ์ ๋ฐ์ Host๊ฐ Merge์งํ
* ์ดํ Merge๋ Master๋ฅผ ๋ก์ปฌ์ pullํด์ ์๋ก์ด ์์ ์งํ


---
<br><br>
