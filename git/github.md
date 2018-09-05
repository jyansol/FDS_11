# Github 특강

## commit 방법

- 스프린트 참여 - 오픈소스기여
- 책 소스 따라쓰기
- 정적블로그 운영 - 기술블로그 운영

## repo 생성
- `+` button click
- publick check : PW, 개인정보 남기기 조심!
- Initialize this -- README check!
- Add .gitignore : 내가 사용하는 언어 선택 / Add a license : MIT License (오픈소스지만, 내 소스를 가져가 사용하다가 문제발생시 책임은 없다.)
- Create repo CLICK!
- main 에서 잔디밭 우측 상단 Contribution setting 눌러서 설정 가능
- newfile > title [ git / git.md ]  : git폴더생성 / 파일생성 > markdown
- 하단 작성 > commit new file (git add . + commit + push)
- WIKI 에 정리 가능하나 markdown으로 1일1커밋 지향!

## 내 로컬과 github 연결
- profile > setting > SSH and GPG keys
- mac : terminal open! / window : git bash 설치
- Generating a new SSH key [https://help.github.com/articles/connecting-to-github-with-ssh/] 따라하기!
- rsa : 비밀번호 생성 권장 / 그냥 enter 치면 default 값
- ssh-add -K ~/.ssh/id_rsa 하면 내 컴퓨터에 rsa 등록! 재요구 안함! 
- cd ~/.ssh > .ssh파일 들어가기
- ls > 파일 목록 확인 / id_rsa.pub
- rsa.pub을 github에 등록 [https://help.github.com/articles/adding-a-new-ssh-key-to-your-github-account/]
- 위에서 나온 주소를 profile > setting > SSH and GPG keys > new SSH key > 복붙!

## repo에서 내 로컬로 가져오기 (pull)
- repo에서 clone or download CLICK > USE SSH 확인하고 URL 복사!
- 터미널실행 > 받아오고자 하는 위치 이동 > git clone "URL"
- mac : 플러그인 설치 
- git config --list : 원격저장소의 위치 확인
- git remote -v : 원격저장소의 위치 확인
- .파일명 > `.` 숨김파일이라는 의미
- ls -al 숨김파일까지 모두 보여줌
#### 원래 내 로컬에서 markdown 했는데, pull하면서 폴더가 2개가 됨. 어디서 편집?
- 파일 수정 후 터미널에서 commit 하면됨!
- git push -u origin master
- git add `.` 해도 .gitignore 파일은 업로드 안됨!

## github page에서 수정했을때
- 터미널에서 git pull하면 내 로컬에서 반영됨.
```
git pull origin master
```