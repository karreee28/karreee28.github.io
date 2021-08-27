---
layout: post
title:  "git 관련"
date:   2021-07-13 00:00:00 +0900
categories: data
tags: [git]
---
Git 관련

`git 초기 설치`
{% highlight ruby %}
1. nodejs 설치 (기본경로 권장)
https://nodejs.org/ko/
10.16.3 LTS 다운
2. C:\Users\사용자 경로에 .ssh 넣기 //인증 키
3. git bash 없으면 설치 후 git bash 실행
https://git-scm.com/downloads
4. 설치를 원하는 위치에 순차적으로 입력
$ git clone 'github주소'
$ cd 'clone한 git 디렉토리'
$ npm install
$ npm run dev
{% endhighlight %}

`Github 설정`
{% highlight ruby %}
1. github 로그인 후 repository 생성
2. git bash에서
  $ cd 'Github에 올릴 디렉토리' (오른 쪽 클릭 후 git Bash Here 가능)
3. $ git init (로컬 저장소 설정)
4. $ git status 로 디렉토리 리스트 확인 (git add .을 하면 녹색으로 변함)
5. $ git add .
6. $ git commit -m "커밋할 내용"
7. $ git remote add origin [repository 주소(주소 뒤에 .git이 붙음)]
8. $ git remote -v (repository 연결 확인)
9. $ git push origin master

//github 정책으로 인해 master브랜치 이름이 main으로 바뀌어서 이 후에 master브랜치를 main으로 바꾸는 작업 필요
//main에 master를 머지 한 후, git repository와 로컬에서 master 브랜치 삭제
{% endhighlight %}

`Git Push`
{% highlight ruby %}
1. $ npm run fix (에러 무시npm)
2. $ git add . (작업 내용 올리기 전 단계) //git add src/components/WalletManage 처럼 경로 지정 가능
3. $ git commit -m "커밋할 내용" //" " 안에 어떤 작업을 했나 로그 작성 - 로그작성 규칙 있음
4. $ git push (에러 없으면 성공)
4-1. 에러 시 $ git pull로 받아서 merge 후 (고쳐야 할 부분 파일 표시됨)
다시 단계 2. 부터 시작
{% endhighlight %}

`Git Pull`
{% highlight ruby %}
1. $ cd '로컬 디렉토리'
2. $ git pull
3. 에러 시 $ git stash 후 $ git pull //내가 수정한 부분을 다른 곳에 임시 저장
4. $ npm install
5. $ npm run dev
6. 127.0.0.1:8080 로 확인
//$ git stash pop - 내가 수정한 부분 되돌리기 (git stash 한 부분)
{% endhighlight %}
