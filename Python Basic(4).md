# Python Basic(4)

23.04.27

---

### 문제풀이 정리
- 리스트에 저장된 데이터를 아래와 같이 출력하기
    
    ```
    **apart = [ [101, 102], [201, 202], [301, 302] ]**
    301호
    302호
    201호
    202호
    101호 
    102호 
    ```
    ```python
    apart = [ [101, 102], [201, 202], [301, 302] ]
    
    for i in range(3,0,-1):
      for j in range(2,0,-1):
        print(apart[i-1][j-2],"호")
    ```
    
    **i,j**가 역순으로 인덱스에 접근하면서 **for문**을 수행하는 것 까지는 쉽게 생각해냈다.
    
    다만 인덱스에 접근할 때 처리를 어떻게 해줘야하는 지 살짝 고민했다.
    
    (층은 내림차순으로 접근하면서 호수는 오름차순으로 출력해줘야 하는 부분이 
    
    바로 생각되지 않았다.)
    
    
    **i**는 역순으로, **j**는 오름차순으로 접근하면 쉽게 풀 수 있는 문제였다.
    
    ```python
    apart = [ [101, 102], [201, 202], [301, 302] ]
    
    for i in range(3,0,-1):
      for j in range(2):
        print(apart[i-1][j],"호")
    ```
    

- 문제의 결과값을 result라는 이름의 리스트에 2차원 배열로 저장하기
    
    C++의 경우 2차원 배열을 생성할때 단순하게 **arr[i][j]**로 작성하면 되는데,
    
    파이썬은 그렇지 못해서 구글링을 했다.
    
    결과는 리스트 하나를 만들어서 또다른 리스트 안에 넣는 것이었다.
    
    조금 더 쉬운 방법이 있을거라 생각했는데 아니었다.
    
    ```
    data에는 매수한 종목들의 OHLC (open/high/low/close) 가격 정보가 바인딩 되어있다.
    
    data = 
    [ [ 2000, 3050, 2050, 1980], [ 7500, 2050, 2050, 1980], [15450, 15050, 15550, 14900] ]
    
    수수료를 0.014 %로 가정할 때, 각 가격에 수수료를 포함한 가격을 
    result라는 이름의 리스트에 2차원 배열로 저장하라.
    ```
    
    ```python
    data = 
    	[[2000,3050,2050,1980], [7500,2050,2050,1980], [15450,15050,15550,14900]]
    result = []
    
    for i in range(len(data)):
      comp = []
      for j in range(len(data[0])):
        comp.append(data[i][j]*1.00014)
      result.append(comp)
    
    result
    ```
    
    **comp**라는 리스트에 수수료를 포함한 가격을 계산하여 넣고, 
    
    최종적으로 **result** 리스트에 넣었다.
    

### 클래스

클래스는 기본적으로 객체를 생성하기 위한 일종의 ‘틀’에 비유하곤 한다.

클래스를 통해 객체의 속성과 동작을 정의할 수 있다.

클래스의 대표적인 특징은 다음과 같다.

1. 캡슐화(Encapsulation)
    
    클래스는 객체를 생성하기 위한 속성과 메서드를 캡슐화하여 외부에서 직접 접근할 수 없게 한다. 이를 통해 객체의 내부 구조를 숨길 수 있으며, 객체의 외부 인터페이스만을 노출시켜 객체의 안정성을 높일 수 있다.
    
2. 상속성(Inheritance)
    
    클래스는 상속을 통해 다른 클래스에서 정의된 속성과 메서드를 물려받을 수 있다. 이를 통해 코드의 재사용성을 높일 수 있으며, 상속 관계를 통해 클래스 간의 계층 구조를 만들어 효과적으로 코드를 구성할 수 있다.
    
3. 다형성(Polymorphism)
    
    다형성은 같은 이름의 메서드가 다른 객체에서 서로 다른 구현을 갖는 것을 의미한다. 이를 통해 객체의 타입에 따라 다른 메서드를 호출할 수 있으며, 코드의 유연성을 높일 수 있다.
    
4. 재정의(Override)
    
    부모 클래스에 이미 구현된 메서드를 자식 클래스에서 새로운 구현으로 덮어쓰는 것.
    자식 클래스에서 오버라이드한 메서드는, 부모 클래스에서 정의된 메서드와 같은 이름과 인자를 가지고 있지만, 자식 클래스에서 정의된 새로운 동작을 수행한다. 이를 통해 자식 클래스는 부모 클래스의 동작을 수정하거나 보완할 수 있다.
    오버라이드는 객체 지향 프로그래밍의 상속 개념과 밀접하게 관련되어 있다. 자식 클래스에서 부모 클래스의 메서드를 오버라이드하여 자식 클래스에서 새로운 동작을 구현하면, 부모 클래스와 자식 클래스 간의 계층 구조가 유지되면서 코드의 재사용성과 유지보수성이 향상된다.
    

클래스 문제풀이

```
🔍 ***용어 정리**
- 메서드 : 클래스 내에서 정의된 함수
- 인스턴스 : 클래스를 기반으로 생성된 객체
```

```python
import random

# Account 클래스 생성
class Account:
	
	# 멤버 변수 초기화
  account_count = 0
  deposit_count = 0
  dh = [] # deposit history
  wh = [] # withdraw history
	
	# 생성자
  def __init__(self, name, balance):
    Account.account_count += 1 # 은행 계좌의 수로 생성자가 호출될 때 마다 1씩 증가
    self.bankName = 'SC은행'
    self.name = name
    accNum1 = str('%03d'%(random.randint(0,999)))
    accNum2 = str('%02d'%(random.randint(0,99)))
    accNum3 = str('%06d'%(random.randint(0,999999)))
    self.accNum = accNum1 + '-' + accNum2 + '-' + accNum3
    self.balance = balance
	
	# 고객 이름과 잔액을 입력받아 객체를 생성한 후 
	# 은행이름과 부여된 계좌번호를 출력해주는 메서드
  def display(self):
    print("은행이름: ", self.bankName)
    print("계좌번호: ", self.accNum)
    print("-----------------------")
	
	# 객체를 여러번 생성하면 생성한 횟수에 따라 생성된 계좌의 수 출력
  def get_account_num(self):
    print("생성된 계좌의 갯수:", Account.account_count)
    print("-----------------------")

	# 입금을 위한 메서드
	# 입금은 최소 1원부터 가능하며, 입금횟수가 5회가 될 때마다 1%의 이자 지급
	# deposit_count를 통해 입금횟수를 계산하고, 
	# 5가 될 때마다 이자 지급 및 deposit_count를 0으로 바꿔주었다.
	# 입금이 발생할 때 마다 deposit_history 메서드 실행
  def deposit(self, money):
    if money >= 1:
      Account.deposit_count += 1
      if Account.deposit_count == 5:
        self.balance *= 1.01
        Account.deposit_count = 0
      self.balance += money
    print("입금 금액: {0:,} 원".format(money))
    print("현재 잔액: {0:,} 원".format(self.balance))
    print("-----------------------")
    Account.deposit_history(self, money)

	# 출금을 위한 메서드
	# 출금이 발생할 때 마다 withdraw_history 메서드 실행
  def withdraw(self, money):
    if money <= self.balance:
      self.balance -= money
    print("출금 금액: {0:,} 원".format(money))
    print("현재 잔액: {0:,} 원".format(self.balance))
    print("-----------------------")
    Account.withdraw_history(self, money)

	# Account 인스턴스에 저장된 정보를 출력하는 메서드
	# 잔고는 3자리마다 쉼표를 출력
  def display_info(self):
    print("은행이름: ", self.bankName)
    print("예금주: ", self.name)
    print("계좌번호: ", self.accNum)
    print("잔고: ", format(self.balance, ','),"원")
    print("-----------------------")
	
	# 입금 내역을 저장하기 위한 메서드
  def deposit_history(self, money):
    Account.dh.append(money)

	# 출금 내역을 저장하기 위한 메서드    
  def withdraw_history(self, money):
    Account.wh.append(money)
```

```python
# 여러개의 계좌가 정상적으로 생성되고, 생성된 계좌의 수 확인

new_acc1 = Account("홍길동", "1,000,000원")
new_acc1.display()
new_acc1.get_account_num()
new_acc2 = Account("김철수", "2,000,000원")
new_acc2.display()
new_acc2.get_account_num()

>>
은행이름:  SC은행
계좌번호:  234-24-993262
생성된 계좌의 갯수: 1
은행이름:  SC은행
계좌번호:  647-25-868943
생성된 계좌의 갯수: 2
```

```python
# 입/출금이 제대로 실행하는지 확인

new_acc1 = Account("홍길동", 1000000)
new_acc1.display()
new_acc1.get_account_num()
new_acc1.deposit(200000)
new_acc1.withdraw(500000)
new_acc1.display_info()

>>
은행이름:  SC은행
계좌번호:  35-94-64368
-----------------------
생성된 계좌의 갯수: 1
-----------------------
입금 금액:  200000
현재 잔액:  1200000
-----------------------
출금 금액:  500000
현재 잔액:  700000
-----------------------
은행이름:  SC은행
예금주:  홍길동
계좌번호:  35-94-64368
잔고:  700,000 원
-----------------------
```

```python
# 입금 5회마다 이자가 정상적으로 추가되는지 확인

new_acc1 = Account("홍길동", 1000000)
new_acc1.display()
new_acc1.get_account_num()
new_acc1.deposit(100000)
new_acc1.deposit(200000)
new_acc1.deposit(300000)
new_acc1.deposit(400000)
new_acc1.deposit(500000)
new_acc1.deposit(600000)
new_acc1.display_info()

>>
은행이름:  SC은행
계좌번호:  878-14-705043
-----------------------
생성된 계좌의 갯수: 1
-----------------------
입금 금액:  100000
현재 잔액:  1100000
-----------------------
입금 금액:  200000
현재 잔액:  1300000
-----------------------
입금 금액:  300000
현재 잔액:  1600000
-----------------------
입금 금액:  400000
현재 잔액:  2000000
-----------------------
입금 금액:  500000
현재 잔액:  2520000.0
-----------------------
입금 금액:  600000
현재 잔액:  3120000.0
-----------------------
은행이름:  SC은행
예금주:  홍길동
계좌번호:  878-14-705043
잔고:  3,120,000.0 원
-----------------------
```

```python
# 반복문을 통해 리스트에 있는 객체를 순회하면서 잔고가 100만원 이상인 고객의 정보 출력

acc_list = []

acc1 = Account("A", 100000)
acc2 = Account("B", 300000)
acc3 = Account("C", 1000001)

acc_list.append(acc1)
acc_list.append(acc2)
acc_list.append(acc3)

for i in range(len(acc_list)):
  if acc_list[i].balance > 1000000:
    print(acc_list[i].display_info())

>>
은행이름:  SC은행
예금주:  C
계좌번호:  268-08-977902
잔고:  1,000,001 원
-----------------------
```

```python
# 입/출금 내역을 기록하고, 출력되는지 확인

new_acc1 = Account("홍길동", 1000000)
new_acc1.display()
new_acc1.get_account_num()
new_acc1.deposit(100000)
new_acc1.deposit(200000)
new_acc1.withdraw(300000)
new_acc1.deposit(400000)
new_acc1.deposit(500000)
new_acc1.withdraw(600000)
new_acc1.display_info()
print("입금내역 : ", Account.dh)
print("출금내역 : ", Account.wh)

>>
은행이름:  SC은행
계좌번호:  924-69-895915
-----------------------
생성된 계좌의 갯수: 1
-----------------------
입금 금액: 100,000 원
현재 잔액: 1,100,000 원
-----------------------
입금 금액: 200,000 원
현재 잔액: 1,300,000 원
-----------------------
출금 금액: 300,000 원
현재 잔액: 1,000,000 원
-----------------------
입금 금액: 400,000 원
현재 잔액: 1,400,000 원
-----------------------
입금 금액: 500,000 원
현재 잔액: 1,900,000 원
-----------------------
출금 금액: 600,000 원
현재 잔액: 1,300,000 원
-----------------------
은행이름:  SC은행
예금주:  홍길동
계좌번호:  924-69-895915
잔고:  1,300,000 원
-----------------------
입금내역 :  [100000, 200000, 400000, 500000]
출금내역 :  [300000, 600000]
```

문제를 풀면서 구글링했던 포인트가 2가지

1. 랜덤으로 계좌번호 생성 (3자리-2자리-6자리)
    
    계좌번호 생성은 처음에 (3자리일 경우) **random.randint(100,999)**로 작성하였다.
    풀고보니 앞자리가 1로 고정되어 “001”, “083” 이런 숫자들은 생성이 안되는 것이었다.
    **'%03d'%(random.randint(0,999))**
    이런 식으로 작성하면 3자리수 고정으로 숫자를 생성하고, 빈자리에 0을 채워준다고 한다.
    
2. 숫자에 천단위마다 (,) 붙이기
    
    여러가지 방법이 있었지만 내가 처음에 사용했던 방법과 좀 더 효율적이라고 생각된
    방법, 총 2가지를 정리하고자 한다.
    
    1) **print("잔고: ", format(self.balance, ','),"원")**
    
    2) **print("입금 금액: {0:,} 원".format(money))**
    

상속

```python
class 차:
  def __init__(self, wheel, price):
    self.wheel = wheel
    self.price = price

**# 부모 클래스를 상속받을 때, 부모 클래스의 생성자의 변수를 생략하면 안된다.**
class 자전차(차):
  def __init__(self, wheel, price, 구동계):
    self.구동계 = 구동계

bicycle = 자전차(2, 100, "시마노")

print(bicycle.구동계)
```