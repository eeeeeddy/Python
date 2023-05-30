# Python Basic(3)

23.04.26

---

### Function

1. **Parameter(매개변수) & Argument(전달인자)**
둘은 함수내에서 비슷한 위치에 작성된다.
    
    ```python
    # Parameter
    # 다음 함수 func에서 param1과 param2는 매개변수이다.
    def func(param1, param2):
    	return param1, param2
    ```
    
    ```python
    # Argument
    # func 함수를 호출할 때, 입력값 "Parameter"와 "Argument"는 전달인자이다.
    func("Parameter", "Argument")
    ```
    
1. **Lambda 함수**
    
    ```python
    def func(x):
    	y = x + 2
    	return y
    func(2)
    
    # 위 코드를 Lambda 함수로 작성
    (lambda x : x+2)(2)
    ```
    

### OS Package

OS 패키지는 운영체제와의 상호작용을 하기위해 제공하는 패키지이다. <br>
이를 통해서 파일/디렉토리 조작, 환경 변수 설정, 프로세스 생성 등을 할 수 있다. <br>
주요 모듈과 함수는 다음과 같다.

- **`os.name`**: 현재 운영체제의 이름을 반환
- **`os.getcwd()`**: 현재 작업 디렉토리의 경로를 반환
- **`os.chdir(path)`**: 작업 디렉토리를 지정된 경로로 변경
- **`os.listdir(path='.')`**: 지정된 디렉토리 내의 파일과 디렉토리 목록을 반환
- **`os.mkdir(path, mode=0o777)`**: 지정된 디렉토리를 생성
- **`os.makedirs(name, mode=0o777, exist_ok=False)`**: 지정된 디렉토리와 중간 경로의 디렉토리를 모두 생성
- **`os.remove(path)`**: 지정된 파일을 삭제
- **`os.rmdir(path)`**: 지정된 디렉토리를 삭제
- **`os.path.join(path, *paths)`**: 지정된 경로를 포함한 새 경로를 생성
- **`os.path.abspath(path)`**: 지정된 경로의 절대 경로를 반환
- **`os.path.exists(path)`**: 지정된 경로의 존재 여부를 반환
- **`os.path.isdir(path)`**: 지정된 경로가 디렉토리인지 여부를 반환
- **`os.path.isfile(path)`**: 지정된 경로가 파일인지 여부를 반환
- **`!pwd`**: 현재 작업 중인 파일이 위치한 디렉토리의 경로 반환 (셸에서 사용되는 명령어)

### File I/O

파일을 통한 입출력이 가능하게하는 코드

1. **open**
**myFile.txt**라는 파일을 쓰기모드로 생성하는 코드이다.
파일을 open한 후에는 꼭 **f.close()**를 통해 파일 객체를 닫아주어야 한다.
    
    ```python
    f = open("myFile.txt", mode="w")
    f.close()
    ```
    
2. **read**
다음과 같이 변수를 설정하여 파일 안의 내용을 불러올 수 있다. 
(데이터 타입은 문자열이다.)
    
    ```python
    f = open("myFile.txt", mode="w")
    file_text = f.read()
    f.close()
    ```
    
    다음과 같이 작성한 파일 안의 내용을 라인별로 읽어 변수에 저장할 수 있다.
    **readline()**을 사용하면 라인 한 줄을 저장하고,
    **readlines()**를 사용하면 여러 라인을 한 리스트에 저장한다.
    
    ```python
    f = open('two_times_table.txt', mode='w')
    
    for num in range(1,6):
      format_string = "2 x {0} = {1}\n".format(num, 2*num)
      f.write(format_string)
    
    f.close()
    
    >>
    2 x 1 = 2
    2 x 2 = 4
    2 x 3 = 6
    2 x 4 = 8
    2 x 5 = 10
    ```
    
    ```python
    f = open('two_times_table.txt')
    line1 = f.readline()
    line2 = f.readline()
    f.close()
    print(line1, end="")
    print(line2, end="")
    
    >>
    2 x 1 = 2
    2 x 2 = 4
    # **readline()**을 사용할 때마다 한 줄 씩 읽어오는 것을 알 수 있다.
    ```
    
    ```python
    f = open("two_times_table.txt")
    lines = f.readlines()
    f.close()
    
    print(lines)
    
    >>
    ['2 x 1 = 2\n', '2 x 2 = 4\n', '2 x 3 = 6\n', '2 x 4 = 8\n', '2 x 5 = 10\n']
    # 개행문자까지 포함되어 리스트에 저장됨을 알 수 있다.
    ```
    
    ```python
    f = open("two_times_table.txt")
    lines = f.read()
    f.close()
    
    print(lines)
    
    >>
    2 x 1 = 2
    2 x 2 = 4
    2 x 3 = 6
    2 x 4 = 8
    2 x 5 = 10
    #개행까지 적용하여 파일의 내용을 불러온 것을 알 수 있다.
    ```
    
3. **write**
    
    ```python
    f = open("myFile.txt", mode="w")
    f.write("Hello")
    f.close()
    ```
    
4. **append**
    
    ??
    

### 예외처리

```python
try:
	실행문
except:
	예외처리 실행문1
except Exception as e:
	예외처리 실행문2
else:
	오류가 발생하지 않았을 경우에만 실행되는 실행문
finally:
	예외 발생에 관계없이 항상 실행할 실행문
```

예외가 발생하면 **변수 e**에 오류 메세지가 저장된다.
보통 **변수 e**를 출력하여 어떤 오류가 있는지 파악한다.

### star expression 2

**Double Asterisk** : 딕셔너리에서 키-값 쌍을 키워드 인수로 전달하거나, 합치기 위해서 사용된다.

```python
def kwpacking(s, *n, **kwargs):
  print("s",s)
  print("n",n)
  print(type(n))
  print(kwargs)
  print(type(kwargs))

kwpacking("string", 1, "a", a=1, b=2, c=3)

>> 
s string
n (1, 'a')
<class 'tuple'>
{'a': 1, 'b': 2, 'c': 3}
<class 'dict'>
```

![Untitled](img/Python Basic(3)/Untitled.png)

![Untitled](img/Python Basic(3)/Untitled%201.png)
