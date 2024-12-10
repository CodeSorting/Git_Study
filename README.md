# Git_Study
깃,깃헙 명령어 공부

특정 폴더로 만들거나 이미 있는 폴더로 이동 후
git init -> 초기화 및 .git 폴더 만들기

git status -> 현재 작업 디렉터리의 상태를 알려줌.
처음 만들었다면 No commits yet이 출력된다.

git add -> 스테이지에 올리기
ex) 만든 파일이름이 a.txt일 경우 git add a.txt

Changes to be committed: 가 등장하면 성공적으로 스테이지에 올라갔다는 것이다.
git add . 명령으로 현재 디렉터리의 모든 변경사항을 한번에 스테이지로 올릴 수 있다.

git commit -> 커밋하기
ex) 파일 이름이 a.txt일 경우 git commit -m "first commit"
-> -m은 message의 줄임말이고 안의 내용은 커밋 메시지(제목)이다.
git add .처럼 git commit -am "커밋 메시지" 명령으로 한 번에 사용할 수도 있다.
(단, 이 명령어는 깃이 변경 사항을 추적하는(tracked) 파일에만 사용가능하다.
즉, 한 번이라도 커밋하거나 스테이지에 이미 올라와있는 파일에만 사용할 수 있다.)

git log -> 커밋 해시,만든 사람,커밋 날짜,커밋 메시지가 출력된다.

수정된 상태면 git status가 modified: git_first.txt처럼 나타난다.

git commit에서 제목 말고도 본문 내용도 쓰고 싶을 때
git add a.txt
이 상태에서 git commit을 입력하고 a나 i를 눌러 입력 모드로 전환하면 vi 편집기로
입력이 가능하다. 끝나면 esc 후 :wq를 입력하면 write 모드 전환 후 q로 입력창을 닫는다.
ex) git commit
->i
->this is commit example

   you should write the body from third sentences
->esc 입력
->:wq
->enter

git log --oneline -> 커밋 목록을 커밋당 한 줄로 출력해주는 옵션
git log --patch 아니면 git log -p -> 해당 커밋으로 어떻게 수정됐는지 출력
git log --graph -> 소스트리 그래프처럼 표현해줌.
git log --branches -> 모든 브랜치의 커밋 목록 조회
git checkout 커밋id or git checkout 브랜치이름 -> 해당 id나 브랜치 이름로 체크아웃

git tag <태그> -> 태그 추가하기
커밋의 버전 v1.0.0을 붙일 때는 어떡할까?
git tag v1.0.0 -> 최근 커밋에 v1.0.0 태그가 붙는다.
HEAD가 가리킨 곳이 아닌 다른곳에 태그를 붙일려면 
git tag <태그> <커밋>이어야 한다.
ex) git log로 커밋 해시(bf3c800) 확인 -> git tag v0.0.1 bf3c800

git tag --list -> 태그 조회하기(git tag,git tag -l도 됨)
git tag --delete <태그> -> 태그 삭제하기
ex) git tag로 현재 태그 확인 -> git tag --delete v0.0.1 -> v0.0.1 태그 삭제

git diff -> 최근 커밋과 작업 디렉터리 비교하기
git diff --staged -> 최근 커밋과 방금 스테이지에 올라인 것 비교
git diff <이 커밋을 기준으로> <이 커밋이 달라진 점> -> 커밋끼리 비교하기

가장 최근의 커밋과 전 커밋을 비교할 때는
git diff HEAD^ HEAD or git diff HEAD~1 HEAD를 입력하면 된다.

git diff <기준이 되는 브랜치> <기준과 비교할 브랜치> -> 브랜치끼리 비교하기

git reset <되돌아갈 커밋> -> 예전 커밋으로 되돌아가기

soft reset -> 커밋만 되돌리기
git reset --soft <커밋>

mixed reset -> 스테이지까지 되돌리기
git reset <커밋>
git reset --mixed <커밋>

hard reset -> 작업 디렉터리까지 되돌리기
git reset --hard <커밋>

* 단, 일단 git log로 커밋 해시(bf3c800) 확인해서 되돌아갈 커밋에 쓰던가
HEAD~1, HEAD등을 써야한다.

git revert <취소할 커밋> -> 취소된 새로운 커밋 만들기
git log --oneline으로 커밋 해시 알기
git revert <커밋> -> 커밋을 취소한 것으로 새로운 커밋을 만든다.

git stash -> 변경 사항 임시 저장하기
ex) git stash -m "add B" -> add B라는 메시지와 함께 수정 내역을 일시적으로 저장함.

git stash list -> 임시 저장된 작업 내역 조회하기
stash@{0},stash@{1}처럼 리스트가 나옴.

git stash apply <스태시> -> 임시 저장된 작업 적용하기
ex) git stash apply stash@{0}

git stash drop <스태시> -> 임시 저장된 작업 삭제하기
git stash clear -> 임시 저장된 작업을 전부 삭제
ex) git stash drop stash@{0}

git branch -> 현재 브래치의 목록과 함께 현재 작업중인 브랜치가 *로 표시됨.
git branch <브랜치> -> 브랜치 나누기
ex) git branch foo -> foo 브랜치로 나눠짐
git checkout <브랜치> -> 체크아웃하기
ex) git checkout foo -> foo 브랜치로 체크아웃됨

다른 브랜치로 체크아웃을 바꾸면 서로 브랜치가 다른 개수의 파일을 가지고 있을 때 파일 개수가 폴더에서 바뀜.

git branch --delete <브랜치> -> 브랜치 삭제하기
ex) git branch --delete foo -> foo 브랜치 삭제하기

git merge <브랜치> -> 브랜치 병합하기
git rebase <브랜치> -> 브랜치 재배치하기
ex) git rebase master -> 마스터 쪽으로 재배치하기

깃헙(원격 저장소)와 상호 작용하기
상호작용 종류
1. clone : 원격 저장소를 복제하기
2. remote : 원격 저장소를 추가하고, 조회하고, 삭제하기
3. push : 원격 저장소에 밀어넣기
4. fetch : 원격 저장소를 일단 가져만 오기
5. pull : 원격 저장소를 가져와 합치기

1. clone
깃헙에서 특정 리포지토리에 들어가 SSH에 있는 링크를 복사한다.
그리고 복사할 내 디렉터리로 cd해서 
git clone <원격 저장소>를 입력하면 된다.
(이때 이 명령어는 암묵적으로 현재 경로에 원격 저장소를 클론한다.
아닐 경우에는 git clone <원격 저장소> <클론받을 경로> 형식으로 입력해야한다.

2. remote
예를 들어 원격 저장소 A와 로컬 저장소 B가 있다면 로컬 저장소 B에서 작업하고
A와 상호작용 하기 위해서는 원격 저장소 A를 로컬 저장소 B에 추가해야한다.

로컬 저장소에 원격 저장소를 추가하는 명령은 git remote add <원격 저장소 이름> <원격 저장소 경로>이다.
ex) 경로 중 하나인 git@github.com:gittest/test-repo.git(홈페이지에서 복사 가능)

이 원격 저장소를 origin이라는 이름으로 로컬 저장소에 추가하기
git remote add origin git@github.com:gittest/test-repo.git

git remote -> 추가했던 원격 저장소를 알 수 있고
git remote -v or git remote --verbose -> 원격 저장소의 이름과 경로를 알 수 있다.
git remote rename <기존 원격 저장소 이름> <바꿀 원격 저장소 이름>
-> 원격 저장소의 이름을 바꾸는 명령
git remote remove <원격 저장소 이름> -> 원격 저장소 삭제하기

3. push
파일 만들기 -> git add,commit -> git remote add origin git@github.com.... 
-> git branch -M main -> git push -u origin main
순서대로 보면 로컬 저장소에 파일 만들고 커밋하기 -> 원격 저장소와 연결하기
-> 원격 저장소에 로컬 저장소에 저장한 파일 밀어넣기이다.
파일 형식은 git push <원격 저장소 이름> <브랜치> 이다.
위의 예시에서는 원격 저장소 origin으로 로컬 저장소 main 브랜치의 변경사항을 푸시하는 거임.
-u 옵션은 처음 푸시할 때 한 번만 사용하면 추후 간단히 git push 명령만으로 origin의 main 브랜치로 푸시할 수 있다.

4. fetch
github에 새로운 추가사항이 갱신되었을 때 로컬 저장소에 일단 가져오기만 할 수가 있다. (업데이트X,비교용)
git fetch <원격 저장소 이름> -> 변경 사항을 가져온다.
remote로 원격 저장소 이름을 알고 가져오면 된다.

5. pull
풀 리퀘스트를 보내는 과정
1. 기여하려는 저장소를 본인 계정으로 포크하기
2. 포크한 저장소를 클론하기
3. 브랜치 생성 후 생성한 브랜치에서 작업하기
4. 작업한 브랜치 푸시하기
5. 풀 리퀘스트 보내기
git pull <원격 저장소 이름> -> 원격 저장소를 가져와서 합치기

git <명령> --help -> 메뉴얼 페이지 보기
git-scm.com = 공식 사이트
