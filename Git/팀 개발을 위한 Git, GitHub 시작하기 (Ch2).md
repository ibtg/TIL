
## Ch2

- Git은 [.git] 폴더에 버전 관리한 데이터와 이를 올릴 원격 저장소 주소등 필요한 정보를 저장한다
- origin은 우리가 연결한 GitHub 원격 저장소의 닉네임이다
- 'master'는 우리가 커밋을 올리는 '줄기'의 이름
- 커밋이 줄줄이 하나의 줄기로 이어져 있는 것을 확인할 수 있다
- [master]는 내 로컬 저장소의 버전
- [origin/master]는 GitHub의 원격 저장소의 버전을 가리킨다

```
$ git remote add origin "원격 저장소 주소" # origin이라는 이름으로 원격 저장소 추가 
```

<hr>

- 하나의 버전을 만들기 위해 변경사항을 선택하는 과정이 add
- 그렇게 선택한 변경사항을 하나로 묶어 버전으로 만든 것이 commit
- Git은 커밋에 바뀐 것만 저장하는 것이 아니라 전체 코드를 저장한다
- Git으로 관리하는 파일의 4가지 상태
    1. 추적안됨(untracked) 
        - 한번도 커밋되지 않은 파일
    2. 스테이지 됨(add) 
        - add 명령어를 통해 스테이지에 파일을 올린 상태
        - 로컬저장소(.git 폴더)의 stage에 파일이 올라간다
    3. 수정없음(unmodified) 
        - commit 명령어를 통해서 버전으로 만들면 파일 상태가 '스테이지됨'에서 '수정없음(modified)'로 변경됨. push 명령어를 통해서 원격 저장소에 올린다
    4. 수정됨(modified) : 커밋된 파일을 수정한 경우 modified로 파일 상태가 변한다 
    - 파일 상태가 '수정 없음'인 파일은 변경사항이 없기 때문에 스테이지로 올릴 수 없다
    - 하지만 untracked 또는 modified 파일을 스테이지에 올리면 수정 없음 파일은 add 하지 않았지만 변경사항이 없기 때문에 같이 스테이지에 올라가게 된다
    
## Refernece
- [팀 개발을 위한 Git, GitHub 시작하기](http://www.hanbit.co.kr/store/books/look.php?p_code=B5159933380)
