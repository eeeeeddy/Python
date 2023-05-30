# Python Basic(5)

23.04.28

---

1. 텍스트 파일의 데이터를 읽고 문자열 처리하기
2. 모듈 생성 및 호출
3. 파이썬 내장 모듈 호출
4. 정규표현식 및 문자열 검사

1~3은 크게 어려움이 없는 부분이라 따로 정리하지 않고, 4에 대해서만 정리하고자 한다.

### 정규표현식 및 문자열 검사

- **정규 표현식**
    
    ```python
    - 메타문자 : 정규표현식에서 일정한 의미를 가지고 있는 특수 문자
    .x 또는 x. : 임의의 한 문자가 x앞이나 뒤에 오는 패턴 지정
    ^x : x로 시작하는 문자열
    x$ : x로 끝나는 문자열  
    x* : x가 0번이상 반복
    x+ : x가 1번이상 반복
    x? : x가 0개 또는 1개 존재
    abc|ABC : abc 또는 ABC 두개중 하나 선택
    [x] : x문자 한개 일치
    [^x] : x문자 제외
    x{n} : x문자 n개 연속
    x{n,} : x문자 n개 이상 연속
    x{m,n} : x문자 ㅡ~n개 사이 연속
    ```
    
    ```python
    - 이스케이프 문자 : \(역슬래시)로 시작해서 의미를 갖는 문자
    \s : 공백문자
    \b : 문자와 공백사이
    \d : 숫자 [0-9]와 같다
    \w : 단어[0-9a-zA-Z_]와 같다.영문자+숫자+_
    \n : 줄바꿈 문자
    \t : 탭 문자
    이스케이프 문자로 해석하지 않게 하는 방법 : \(역슬래시)를 하나 더 붙이거나 문자 앞부분에 'r' 문자를 붙인다.
    ```
    
    ```python
    # 방법1 : 정규표현식 모듈
    import re
    
    # 방법2
    from re import findall, match, sub 
    ```
    

- **문자열 찾기**
    
    ```python
    findall('pattern', string) >> 리스트 반환
    ```
    
    1. 숫자 찾기
        
        ```python
        #1
        findall('1234', st1, flags=0)
        >> ['1234']
        
        print(findall('[0-9]', st1)
        >> ['1', '2', '3', '4', '5', '5', '5', '6']
        
        print(findall('[0-9]{3}', st1) # {3}:숫자가 3개 연속된 패턴
        >> ['123', '555']
        
        print(findall('[0-9]{3,}', st1) # {3,}:숫자가 3개 이상 연속된 패턴 
        >> ['1234', '555']
        
        print(findall('\\d{3,}', st1)
        >> ['1234', '555']
        ```
        
    2. 문자열 찾기
        
        ```python
        st1 = '1234 abc홍길동 ABC_555_6 이사도시'
        
        findall('[가-힣]{3,}', st1) # 이름 찾기
        >> ['홍길동', '이사도시']
        
        findall('[a-z]{3}', st1)
        >> ['abc']
        
        findall('[a-z|A-Z]{3}', st1)
        >> ['abc', 'ABC']
        ```
        
        ```python
        st2 = 'test1abcABC 123mbc 45test'
        
        findall('^test', st2) # ^:접두어 - ['test']
        
        findall('st$', st2) # $:접미어 - ['st']
        
        findall('.bc', st2) # '.bc':bc로 끝나는 3자리 문자 
        >> ['abc', 'mbc']
        
        findall('t.', st2) # 't.': t로 시작되는 2자리 문자 
        >> ['te', 't1', 'te']
        ```
        
    3. 단어 찾기
        
        ```python
        st3 = 'test^홍길동 abc 대한*민국 123$tbc'
        
        # '\\w{3,}:한글,영문,숫자가 3자리 이상인 문자열
        words = findall('\\w{3,}', st3) 
        >> ['test', '홍길동', 'abc', '123', 'tbc']
        ```
        
    4. 문자열 제외
        
        ```python
        st3 = 'test^홍길동 abc 대한*민국 123$tbc'
        
        # [^t]:t 문자 제거 '[^t]+':t 반복 문자 제거 
        findall('[^t]+', st3) 
        >> ['es', '^홍길동 abc 대한*민국 123$', 'bc']
        
        # 특수문자 제외
        findall('[^^*$]+', st3)
        >> ['test', '홍길동 abc 대한', '민국 123', 'tbc']
        ```
        

- **문자열 검사**
    
    ```python
    from re import match
    
    # 패턴 일치 여부 반환
    match(pattern, string, flags)
    >> 일치 : object 반환
    >> 불일치 : NULL
    ```
    

- **문자열 치환**
    
    ```python
    from re import sub
    
    # 텍스트 전처리 용도
    # pattern을 repl로 치환
    sub(pattern, repl, string)
    ```
    

- **문자열 전처리 (한글)**
    
    ```python
    # 1. 대/소문자 변경
    string.upper()
    string.lower()
    
    # 2. 숫자 제거
    sub("[0-9]", '', text)
    
    # 3. 문장부호 제거
    sub("[,.?!:;]", '', text)
    
    # 4. 특수문자 제거
    sub("[@#$%^&*()]", '', text)
    
    # 5. 영문 제거
    [''.join(findall("[^a-z]", text)) for text in texts_re4] 
    # findall("[^a-z]", text) : 영문자 제거
    # join() : 문자들을 결합
    
    # 6. 공백 제거
    [' '.join(text.split()) for text in texts_re5]
    # 공백기준 split -> join
    ```
    

- **for 문 if 문 한 줄 코딩 작성하기**
    
    1. for 문
        
        ```python
        sample = [1,2,3]
        
        # 원래 코드
        for i in sample:
            print(i)
        
        # 한줄 코드
        [i for i in sample]
        ```
        
    2. if 문
        
        ```python
        sample = 3
        
        if sample > 2: print(True)
        ```
        
    3. if else 문
        
        if 앞에 참일 경우에 실행할 코드를 적는다.
        
        ```python
        sample = 3
        
        True if sample > 2 else False
        ```
        
    4. for문 + if문
        
        for문 뒤에 조건을 적는다.
        
        ```python
        sample = [1,2,3]
        
        [i for i in sample if i > 2]
        ```
        
    5. for문 + if else 문
        
        for문 앞에 조건을 적는다.
        
        ```python
        sample = [1,2,3]
        
        [True if i > 2 else False for i in sample ]
        ```
        
    6. lambda 함수
        
        lambda 함수는 익명함수로 이름이 없는 함수를 만들 수 있다.
        
        장점은 코드의 간결함과 메모리의 절약이다.
        
        (**def** 키워드를 통해 함수를 생성하는 방법은 리터럴 표기법에 따른 함수 생성 방법이다.)
        
        lambda 함수는 **return**이 없어도 자동으로 **return** 해준다.
        
        ```python
        lambda 매개변수 : 표현식(결과)
        
        def 함수이름(매개변수):
        	return 결과
        ```
        
        ```python
        def hap(x, y):
        	return x + y
        
        >> hap(10, 20)
        30
        
        (lambda x,y: x + y)(10, 20)
        >>
        30
        ```
        
        ```python
        map(함수, 리스트)
        
        list(map(lambda x: x ** 2, range(5)))
        >>
        [0, 1, 4, 9, 16]
        ```
        