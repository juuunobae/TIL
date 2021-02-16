## git init
#### git 초기화. git으로 버전관리를 할 경로에서 사용한다. .git폴더가 생성되며 구조는 아래와 같다.
```
  HEAD
  config
  description
  /branches
  /hooks
  /objects
  /refs
```

## git status
#### 현재 git 프로젝트에서 파일들의 상태를 보여준다.  

## git add
#### 파일의 변경 내용을 스테이징 영역에 추가하기 위해 사용하는 명령어이다. 스테이징 영역으로 추가 변경 이력만 commit 할 수 있다.

## git rm
#### 파일을 지우거나 스테이지에서 해제할 때 사용한다.

## git restore
#### 워킹 트리의 변경된 파일을 복원해 주는 역할을 한다.

## git clean
#### 투적되지 않은 상태의 파일을 삭제한다. 삭제가 되면 복구할 수 없으니 stash를 고려해보는 것도 좋다.

## git commit
#### 변경된 내용을 저장한다.

## git log
#### commit 목록을 볼 수 있다. 굉장히 많은 옵션이 있으니 git log --help 명령어로 옵션을 찾을 수 있다.

## git show
#### commit의 상세정보를 확인한다.

## git reset HEAD [file]
#### commit을 취소할 수 있다.
```
  # commit을 취소하고 해당 파일들은 스테이징 영역에 보존
  git reset --soft HEAD^
  
  # commit을 취소하고 해당 파일들은 Unstaging
  git reset --mixed HEAD^
  git reset HEAD^
  
  # commit을 취소하고 해당 파일들의 변경점 삭제
  git reset --hard HEAD^
```
#### push를 취소할 수 있다.
```
  git reset HEAD^
  git push - forigin 브랜치명
  git pull
```

## git remote
#### 원격저장소를 관리하는 명령어이다.

## git push
#### 원격저장소에 변경된 코드를 업로드한다.

## git branch
#### branch에 관련한 명령어이다.

## git switch
#### branch를 변경하는 명령어 이다. checkout에서 복원하는 기능을 제거했다.

## git checkout
#### branch를 변경하고 워킹트리에서 변경점을 복원하는 명령어이다. switch나 restore 명령어를 사용하는 것을 추천한다.

## git fetch
#### 원격저장소의 데이터를 가져온다. pull로 병합하기 전에 어떤 변경점이 있나 살펴볼 때 사용하기 좋다.

## git pull
#### 원격저장소의 데이터를 가져온 후 로컬 branch에 병합한다.

## git stash
#### 현재 작업중인 변경점을 임시 저장하거나 볼러올 수 있다. 현재와 다른 branch로 가서 작업을 하기전에 사용하면 유용하다.

## git blame
#### 특정 파일의 수정 이력을 확인할 수 있다. 각 라인별로 누가, 언제 마지막으로 수정 했는지 알 수 있다.

## git diff
#### 소스를 비교하여 볼 수 있다.

## git revert
#### 지정한 커밋으로 되돌려 커밋한다. 되돌린 이력이 남기 때문에 충돌이 발생할 위험이 적으며 협업 상황에서 사용하는 것을 추천한다.

## git tag
#### 특정 커밋에 표기하는 기능이다. 주로 릴리즈 시 이요한다. 두 가지 종류가 있는데 Lightweight 태그와 Annotated태그이다. Lightweigh 태그는 단순히 버전등의 이름을 남길 때 사용한다. Annotated태그는 만든 사람의 이름, 이메일, 날짜, 메시지까지 저장하며 gps로 서명까지 가능하다.

## git merge
#### 현재 브랜치를 특정 브랜치의 소스와 병합한다. merge 하기 전엔 워킹 디렉토리를 stash 등으로 깔끔하게 정리하고 진행하는 것을 추천한다.

## git rebase
#### merge처럼 브랜치를 함치는 기능을 하는데, 작동방식이 merge와 다르다. 
#### 사용하면 좋을 경우
- master 브랜치에서 feature 브랜치로 분기하여 커밋 후, master 브랜치의 새로운 커밋이 있을 때 feature 브랜치가 master 브랜치의 새로운 커밋을 병합해야 할 때, merge 커밋을 남기기 싫을 경우.
- 쉽게 말해서, 작업하는 브랜치를 병합할 브랜치에 병합 이력없이 변경 커밋만 남기고 싶을 때 사용하면 좋다.

> 중요한 점은 원격 저장소에 올라가 사용중인 커밋을 rebase 하는 것은 최대한 지양해야 한다는 것이다.
