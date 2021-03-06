
## 표기 방법이 일정하지 않은 문구를 한번에 치환하기 

- 정규표현식을 일괄 치환에서도 사용할 수 있다



```
grep -E "(야메노|Yameno|yameno) *(타로|Taro|taro)

```

- -E : 인수로 지정한 패턴을 확장 정규식 표현식으로 해석하라는 지정 방법


- 정규 표현식 규칙에는 여러가지 종류가 있다
    - 기본 정규 표현식
    - 확장 정규 표현식
    - Perl 호환 정규 표현식 등
    

- vim에서 검색이나 치환할 때 \v를 쓰면 확장 정규 표현식을 사용할 수 있다 

```
#vim

:%s/\v검색할 패턴/치환 후 문자열/



:%s/\v(반환중|회수중|반송)/회수완료/

#반환중, 회수중, 반송 3종류 회수완료로 치환된다 
```

```

#vim

%s;path *= *"/shared/;path = "/var/shared/;

#(스페이스)*: 스페이스가 0회 이상 반복됨

#아래와 같은 것들 모두 포함된다 

path="/shared/publicity
path= " /shared/default
path= "/shared/usr

#다음과 같이 변환
path = "/var/shared/publicity;
path = "/var/shared/default;
path = "/var/shared/usr;



```

- sed도 옵션을 지정하면 확장 정규 표현식을 사용할 수 있지만 옵션명이 환경에 따라서 조금씩 다르다
- 예를 들어 리눅스용 GNU는 sed -r 옵션으로 확장 정규 표현식이 사용가능 하지만
- OS X나 BSD의 BSD sed는 -E 옵션을 사용한다 
- 따라서 변수나 함수로 환경에 따른 옵션을 지정한 상태의 sed를 정의해 둔다 

```
case "(uname)" in # 실행 환경 정보를 사용해서 처리를 분기 
    Darwin|*BSD) sed = "sed -E" ;;
    *) sed = "sed -r";;
esac

```

- OS열이 windows XP이고 status가 사용중인 줄을 status 열을 회수 완료로 치환
- 단, windows XP이외의 줄은 변경하지 않음

- 역참조 방법을 사용한다 
- 역참조를 사용하려면 우선 치환 전후에 변하지 않을 부분을 포함해서 치환 대상이 될 문자열 전체를 나타내는 정규표현식을 만들어야 한다 

```
# vim
:%s/\v(windows XP.+)사용중/\1회수완료/

# sed

$sed -r -e "s/(window XP.+)사용중/\1회수완료/

# .: 임의의 1글자를 의미
# +: 직전 문자가 1회 이상 반복됨을 의미 
# ( ) : 치환 후 문자열에 인용하고 싶은 부분을 괄호로 둘러싸 준다 

# 치환 대상 정규 표현식을 인용해서 괄호로 감싼 부분을 "\번호"로 바꾸어 쓴다 
# 번호가 2개 이상이면 \1 \2라고 쓴다 

```

```
$sed -r -e "s/(windows XP.+)사용중 (.+)/\1회수완료\2파기예정/"

# 결과

windows px, 2013-12-10,회수완료,user,파기예정
# 치환한 내용이 그대로 인용된 부분          치환 결과 새로운 열이 추가 된다 
# (.+)부분을 \2가 참조한다 
```

- vim 검색이나 치환에는 확장 정규 표현식을 사용할 때 \v 뒤에 정규 표현식을 작성한다 


- sed로 치환할 때 확장 정규 표현식을 사용하려면 OS마다 다르게 옵션을 지정한다 



- 정규 표현식은 치환후 지정에 \번호를 써서 괄호()로 감싼 치환전 내용을 치환후 내용에 인용가능하다 (역참조)



## Reference
- [만화로 배우는 리눅스 시스템 관리](http://www.yes24.com/Product/Goods/32402055?Acode=101)
