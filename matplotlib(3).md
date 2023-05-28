# matplotlib(3)

23.05.17

### 그래프에 설명적기

- **텍스트 추가하기**
    
    ```python
    plt.text(x좌표, y좌료, text)
    ratation : 회전각도
    ha : horizontal alignment
    va : vertical alignment
    bbox : {'boxstyle':상자스타일(round/square), 'fc':facecolor, 'ec':edgecolor, ...}
    ```
    
    ```python
    plt.text(2.1, 3, '(x:2, y:3)', ha='left', va='bottom', fontsize=12, rotation=45
            , bbox={'boxstyle':'round', 'fc':'skyblue', 'ec':'b', 'alpha':0.3})
    ```
    
    ![Untitled](matplotlib(3)%2071e67a429c6944e78ed71d88626e2abb/Untitled.png)
    

- **화살표와 텍스트 추가하기**
    
    ```python
    plt.annotate(
    	'text', xy=(화살표x, 화살표y), xytext(텍스트x, 텍스트y)
    	, arrowprops=화살표속성(딕셔너리)
    )
    
    * 화살표 속성
    - width : The width of the arrow in points
    - headwidth : The width of the base of the arrow head in points
    - headlength : The length of the arrow head in points
    - shrink : Fraction of total length to shrink from both ends
    ```
    
    ```python
    plt.annotate(
    	'(x:1,y:2)', xy=(1,2), xytext=(1.5,2.5), arrowprops={'width':1, 
    	'headwidth':10, 'headlength':10, 'shrink':0.1, 'fc':'r'}, fontsize=12, 
    	color='r'
    )
    ```
    
    ![Untitled](matplotlib(3)%2071e67a429c6944e78ed71d88626e2abb/Untitled%201.png)
    

### 이중 y축 사용하기

- **2가지 정보를 하나의 그래프에 그리기**
    
    ```python
    # 축을 분리하기 위해 객체 2개를 만든다.
    fig, ax = plt.subplots()
    ax.bar(age, height, color='skyblue', width=0.5, ec='lightgray', label='height')
    ax.plot(age, weight, color='darkred', marker='o', ls='-.', label='weight')
    plt.legend()
    plt.show()
    ```
    
    ![Untitled](matplotlib(3)%2071e67a429c6944e78ed71d88626e2abb/Untitled%202.png)
    

- **이중 y축 만들기**
    
    ```python
    # x축을 공유하는 새로운 객체(axes)를 생성한다. 
    # axes객체.twinx()
    
    fig, ax1 = plt.subplots()
    ax1.bar(age, height, color='skyblue', width=0.5, ec='lightgray', label='height')
    
    ax2 = ax1.twinx()
    ax2.plot(age, weight, color='darkred', marker='o', ls='-.', label='weight')
    plt.show()
    ```
    
    ![Untitled](matplotlib(3)%2071e67a429c6944e78ed71d88626e2abb/Untitled%203.png)
    

- **축 레이블 표시하기**
    
    ```python
    axes객체.set_xlabel(x레이블)
    axes객체.set_ylabel(y레이블)
    ```
    
- **y축 범위 지정**
    
    ```python
    axes객체.set_ylim(y축 눈금 시작숫자, y축 눈금 종료숫자)
    ```
    

- **데이터 y축 눈금 표시**
    
    ```python
    axes.객체.set_yticks(y축 눈금)
    axes.객체.tick_params(...)
    ```
    
    ```python
    ax1.set_yticks(height)
    ax2.set_yticks(weight)
    
    ax1.tick_params(axis='y', colors='skyblue')
    ax2.tick_params(axis='y', colors='darkred')
    ```
    
    ![Untitled](matplotlib(3)%2071e67a429c6944e78ed71d88626e2abb/Untitled%204.png)
    

- **범례 표시**
    
    axes 객체별로 legend 메서드 호출
    
    ```python
    ax1.legend()
    ax2.legend()
    ```
    

- **그리드 표시**
    
    ```python
    axes객체.grid()
    ```
    
    ```python
    ax1.grid(axis='y', ls='--', color='skyblue')
    ax2.grid(axis='y', ls='--', color='pink')
    ```
    
    ![Untitled](matplotlib(3)%2071e67a429c6944e78ed71d88626e2abb/Untitled%205.png)