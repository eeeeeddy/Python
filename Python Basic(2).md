# Python Basic(2)

23.04.25

---

### String(문자열)

1. url에 저장된 웹 페이지 주소에서 도메인만 걸러내는 문제 <br>
나는 슬라이싱을 이용해 단순하게 걸러냈지만 또 다른 방법으로는 **split()** 을 사용하는 방법도 있다.
활용도를 생각하면 **split()** 이 좀 더 범용적으로 사용될 수 있어보였다.
    
    ```python
    url = "http://sharebook.kr"
    url_split = url.split(".")
    print(url_split)
    print(url_split[1])
    ```
    
1. 문자열 formatting
    
    ```python
    name = "김민수"
    age = "10"
    
    #1
    print("이름: %s"%name, "나이: %d"%age)
    #1-1 (튜플로 format)
    print("이름: %s 나이: %d" %(name, age))
    #2
    print("이름: {}".format(name), "나이: {}".format(age))
    #2-1
    print("이름: {} 나이: {}".format(name, age))
    #3 f-string 이용
    print(f"이름: {name}", f"나이: {age}")
    ```
    

### List

1. 리스트에는 평균을 계산하는 내장함수가 없다. <br>
기본적으로 #1과 같이 계산할 수 있지만, 패키지를 이용하여(#2, #3) 계산할 수 있다.
    
    ```python
    #1
    nums = [1, 2, 3, 4, 5]
    print(sum(nums)/len(nums))
    ```
    
    ```python
    #2
    import numpy
    
    nums = [1, 2, 3, 4, 5]
    numpy.mean(nums)
    ```
    
    ```python
    #3
    import statistics
    
    nums = [1, 2, 3, 4, 5]
    statistics.mean(nums)
    ```
    

### Tuple

1. 기본적으로 요소 여러개를 괄호 사용없이 나열하여 변수로 지정하면 자료형은 튜플이다.
    
    ```python
    t = 1, 2, 3, 4
    type(t)
    
    >>
    tuple
    ```
    
2. 튜플은 값을 수정하려면 리스트로 변경하였다가 다시 튜플로 변경해야한다.
    
    ```python
    t = ('a', 'b', 'c')
    
    t = list(t)
    t[0] = t[0].upper()
    t = tuple(t)
    
    print(t)
    
    >>
    ('A', 'b', 'c')
    ```
    
3. 튜플 언팩킹
하나의 튜플에 담겨있는 여러 개의 값을 각각의 변수에 할당하는 것
    
    ```python
    temp = ('apple', 'banana', 'cake')
    a, b, c = temp
    print(a, b, c)
    
    >>
    apple banana cake
    ```
    

### Dictionary

1. **star expression** <br>
기본적으로 언팩킹은 좌변의 변수와 우변의 데이터 갯수가 같아야한다. <br>
하지만 **star expression**을 이용하면 변수의 갯수가 달라도 데이터 언팩킹을 할 수 있다.
    
    ```python
    a, b, *c = (0, 1, 2, 3, 4, 5)
    print(a)
    print(b)
    print(c)
    
    >>
    0
    1
    [2, 3, 4, 5]
    ```
    
2. **update method** <br>
A 딕셔너리 뒤에 B 딕셔너리를 추가하는 메서드이다. <br>
처음에 **append()**, **insert()** 로 시도했다가 안되서 구글링했더니, 
딕셔너리는 해당 메서드를 통해 추가가 가능함을 알았다.
    
    ```python
    icecream = {'탱크보이': 1200, '폴라포': 1200, '빵빠레': 1800, '월드콘': 1500}
    new_product = {'팥빙수':2700, '아맛나':1000}
    
    icecream.update(new_product)
    print(icecream)
    
    >>
    {'탱크보이': 1200, '폴라포': 1200, '빵빠레': 1800, '월드콘': 1500, '팥빙수': 2700, '아맛나': 1000}
    ```
    
3. **zip method** <br>
**zip()** 은 두 개의 튜플을 하나의 딕셔너리로 (key : value로) 변환하는 메서드이다.
    
    ```python
    keys = ("apple", "pear", "peach")
    vals = (300, 250, 400)
    
    result = dict(zip(keys, vals))
    dict(result)
    
    >>
    {'apple': 300, 'pear': 250, 'peach': 400}
    ```