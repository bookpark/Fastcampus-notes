# Git 정리

[Git 복습하기]('https://git-scm.com/book/ko/v2/Git%EC%9D%98-%EA%B8%B0%EC%B4%88-%EC%88%98%EC%A0%95%ED%95%98%EA%B3%A0-%EC%A0%80%EC%9E%A5%EC%86%8C%EC%97%90-%EC%A0%80%EC%9E%A5%ED%95%98%EA%B8%B0')

## 버전 관리 역사
* 로컬 버전 관리

* 중앙 버전 관리

* 분산 버전 관리


## Git 차이점
* 파일의 변화를 저장하는 것보다 시간순으로 프로젝트 스냅샷 저장


## Git 무결성
* 중복 되지 않는 SHA-1 해시를 사용하여 체크섬을 만든다

## 파일의 세 가지 상태
* Working Directory 
	* 프로젝트 당 한개의 폴더
* Staging Area
	* 저장소에 저장하기 전의 단계 (commit)
* .git directory
	* Git 디렉토리에 영구적인 스냅샷으로 저장

## 사용 방법
* CLI
* GUI

## Git 설치

### macOS

```shell
brew install git
brew link --force git
```

## Git 파일 관리

* Tracked (committed)
* Untracked (uncommitted or unstaged)
	* Unmodified (once added or staged)
	* Modified

## Git 명령어

```git
vi .gitignore (*.DS_Store)
git add .gitignore
git commit -m 'Add gitignore'

echo 'First git project' > README.md
git add README.md
git commit -m 'Add README.md'

echo 'Contributing' > CONTRIBUTING.md
echo 'Add line' > CONTRIBUTING.md
git rm --cached ' '(add 한게 취소됨, git에서만 없어지고 로컬에선 unstaged 상태로 변경)
git commit -m '  ' (commit을 하면서 commit에 대한 제목 또는 메시지를 입력)
git log -p -2 최근 두개의 결과만 보여주기
git log --stat 통계 정보
git log --pretty=format 포맷정리
git commit -amend 되돌리기 & 다시 수정하기
git reset (Unstage로 변경)
git checkout -- 파일명 (Modified 파일 되돌리기 / 위험: 수정한 내용 전부 사라짐)
```
## Git 리모트 저장소

* Github
* Github Education
* BitBucket

### 리모트 저장소 데이터 가져오기
* Pull
```git
$ git fetch [remote-name]
```

* Push
```git
$ git push origin master
```

### 태그
* 태그는 수동으로 올려주어야함
```git
git push origin v1.5
```

## Git 브랜치

* 합치는 행위
* commit -> tree -> 파일 갯수만큼 객체가 생김
* Initial commit은 Parent가 없고 다음 commit은 그 전 단계를 Parent로 설정
* "master" 브랜치는 기본적으로 생성됨

```git
git branch testing (브랜치 추가, 한 커밋을 동시에 가리킴) * Head 제외
git checkout branch-name (브랜치 이동)

git checkout -b asdf 
= git branch asdf & git checkout asdf

git branch --merged (merge한 브랜치 )
git branch --no-merged (merge되지 않은 브랜치)

git branch -d (브랜치 지우기)

```

## Git Merge

> 복습 필요 [Merge]('https://git-scm.com/book/ko/v2/Git-%EB%B8%8C%EB%9E%9C%EC%B9%98-%EB%B8%8C%EB%9E%9C%EC%B9%98%EC%99%80-Merge-%EC%9D%98-%EA%B8%B0%EC%B4%88')

* 새로운 브랜치
* 핫픽스 
* 3 way merge

```
pull은 자동 merge
fetch는 수동으로 merge해야함
```

### 고급 Merge
[공부하기]('https://git-scm.com/book/ko/v2/Git-%EB%8F%84%EA%B5%AC-%EA%B3%A0%EA%B8%89-Merge')

### Rebase

* Rebase는 브랜치의 변경사항을 순서대로 다른 브랜치에 적용하며 합침
* Merge는 두 브랜치의 최종결과만 가지고 합침
* 리모트 등 어딘가에 Push로 내보낸 커밋에 대해서는 절대 Rebase 하지 말아야 함
* git pull 명령을 실행할 때 기본적으로 --rebase 옵션이 적용되도록 pull.rebase 설정을 추가할 수 있다. git config --global pull.rebase true 명령으로 추가

```
git checkout experiment
git rebase master

git checkout master
git merge experiment
```	

