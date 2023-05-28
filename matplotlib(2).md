# matplotlib(2)

23.05.16

### 막대 그래프 그리기

```python
# 세로 막대 그래프
plt.bar(x축 데이터, y축 데이터)

# 세로 막대 그래프 폭 지정 (0 < width < 1)
plt.bar(df1['요일'], df1['매출액'], width=0.4)

# 가로 막대 그래프
plt.barh(x축 데이터, y축 데이터)

# 가로 막대 그래프 폭 지정 (0 < height < 1)
plt.barh(df1['요일'], df1['매출액'], height=0.4)

# 막대 색상 지정
plt.bar(df1['요일'], df1['매출액'], width=0.4, color='r')

# 막대마다 다른 색 지정
plt.bar(df1['요일'], df1['매출액'], width=0.4, color=['r','orange','y','g','b','navy','violet'])

# 막대 테두리 설정 (edgecolor : 테두리 색상, linewidth : 테두리 두께)
plt.bar(df1['요일'], df1['매출액'], width=0.4, edgecolor='gray',linewidth=2)

# 막대에 패턴 지정 
# (hatch 파라미터에 기호 전달 : '/', '\', '|', '-', '+', 'x', 'o', 'O', '.', '*')
plt.bar(df1['요일'], df1['매출액'], width=0.4, hatch='x')

# 막대 패턴의 밀도 지정 (패턴 기호의 갯수로 밀도를 조정)
plt.bar(df1['요일'], df1['매출액'], width=0.4, hatch='xx')

# 막대마다 다른 패턴 지정
bars = plt.bar(df1['요일'],df1['매출액'], width=0.4)

bars[0].set_hatch('.')
bars[1].set_hatch('/')
bars[2].set_hatch('+')
bars[3].set_hatch('-')
bars[4].set_hatch('*')
bars[5].set_hatch('|')
bars[6].set_hatch('o')

# 막대 위치 지정 (default : center)
# edge로 지정하면 막대의 왼쪽 끝과 틱을 맞춘다.
# 막대의 오른쪽 끝과 틱을 맞추려면 width를 음수로 지정한다.
plt.bar(df1['요일'],df1['매출액'], width=0.4, align='edge')
plt.bar(df1['요일'],df1['매출액'], width=-0.4, align='edge')
```

### 산점도 그리기 (버블 차트)

점의 크기, 색깔로 정보를 표현 ( 크기는 s, 색상은 c로 지정)

- 기본 작성

```python
x = [1,5,6,9,10]
y = [1,5,3,9,7]

plt.scatter(x, y)

# plot을 이용하여 같은 표현 가능
plt.plot(x, y, 'o')
```

- 점의 크기
    
    s = 크기 공통 지정
    
    s = 크기 목록 (점마다 다른 크기로 지정)
    
    ```python
    plt.scatter(x, y, s=[100,200,50,80,30])
    ```
    

- 점의 색상
    
    c = 색상 공통 지정
    
    c = 색상 목록 (점마다 다른 색상으로 지정)
    
    ```python
    # 단일 색 지정
    plt.scatter(x, y, c='r')
    
    # 값에 따른 색상 지정 (색상 목록)
    plt.scatter(x, y, c=['r', 'b', 'g', 'k', 'y'])
    
    # 컬러맵으로 색상 지정
    plt.scatter(x, y, c=y, cmap='cool')
    plt.colorbar()
    
    # 컬러맵 종류
    plt.colormaps()
    
    # 색상 투명도 지정 (alpha) : 0(투명), 1(완전 불투명)
    plt.scatter(x, y, c='r', alpha=0.5)
    ```
    

### 히트맵

- matplotlib

```python
# 2차원 데이터
plt.pcolor(df, cmap='Blues')
plt.colorbar()
```

- seaborn
    
    heatmap(data) (data는 2차원 데이터)
    
    cmap = 컬러맵 (컬러맵 지정)
    
    annot = True (수치 표시)
    
    fmt = ‘d’ (정수로 표시)
    

```python
sns.heatmap(df, cmap='Blues', annot=True, fmt='d')
```

### 히스토그램

자료의 도수분포를 나타내는 그래프

수치를 나타내는 자료를 일정 구간(계급)으로 나누어 각 구간별 값의 개수(도수)를 나타낸다.

x축은 계급(값의 구간), y축은 도수(구간별 값의 개수)를 나타냄

```python
plt.hist(data)

# 구간의 개수 변경
plt.hist(data, bins=20)

# 누적 히스토그램
plt.hist(data, bins=20, cumulative=True)

# 범위 지정
plt.hist(data, bins=8, range=(min, max))

# 밀도 표시
plt.hist(data, density=Ture)

# 가로 히스토그램
plt.hist(data, orientation='horizontal')

# 막대 스타일 - 선만 표시
plt.hist(data, histtype='step')

# 막대 스타일
rwidth : 막대 폭 (0~1)
color : 막대 색
alpha : 투명도
edgecolor(ed) : 선 색상
linewidth(lw) : 선 두께
linestyle(ls) : 선 스타일
hatch : 패턴
```

### 박스플롯

데이터로부터 얻어진 다섯 가지 요약 수치를 사용해서 그려진다. (최소값, Q1, Q2, Q3, 최대값)

다른 값들과 동떨어진 값을 이상치(outlier)로 표현한다. (최소값보다 작거나, 최대값보다 큰 경우)

IQR = Q3 - Q1 / Max = Q3 + 1.5*IQR / Min = Q1 - 1.5*IQR

- Outlier 구하기
    
    ```python
    Q1 = Series.quantile(.25)
    Q3 = Series.quantile(.75)
    
    # outlier의 범위
    outlier < Q1 - 1.5*(Q3-Q1)
    Q3 + 1.5*(Q3-Q1) < outlier
    ```
    

- 박스플롯 그리기
    
    ```python
    plt.boxplot(data)
    
    # 평균 표시하기
    plt.boxplot(data, showmeans=True, meanline=True)
    
    # 수평 박스플롯
    plt.boxplot(data, showmeans=True, meanline=True, vert=False)
    
    # 여러 개의 데이터 비교하기
    plt.boxplot([data[label1], data[label2], data[label3]]
    						 , labels=['label1', 'label2', 'label3'])
    ```
    

### 바이올린플롯

```python
plt.violinplot(data)

# 최대값/최소값 표시
# 최대값/최소값에 직선 표시 (default:True)
plt.violinplot(data, showextrema=True/False)

# 평균값 표시 (default:False)
plt.violinplot(data, showmeans=True/False)

# 중간값 표시 (default:False)
plt.violinplot(data, showmedians=True/False)

# 분위수 지정하기 (quantiles: 0~1 사이의 실수 리스트)
plt.violinplot(data, quantiles=[0.25, 0.75])

# 스타일 지정하기 (객체를 받아서 스타일을 지정한다.)
v1 = plt.violinplot(data)
v1['bodies'][0].set_facecolor('r')
v1['cmins'].set_edgecolor('g')
v1['cmaxes'].set_edgecolor('g')
v1['cbars'].set_edgecolor('k')
v1['cmedians'].set_edgecolor('r')
v1['cquantiles'].set_edgecolor('w')
v1['cmeans'].set_edgecolor('y')

# 여러 개의 데이터 비교하기
plt.violinplot([df1[col1], df1[col2], df1[col3], df1[col4]])
```

### 파이차트

전체에 대한 각 부분의 비율을 부채꼴 모양으로 나타낸 그래프

각 부채꼴의 중심각이 전체에서 해당 데이터가 차지하는 비율을 나타낸다.

1차원 리스트, 배열, 시리즈를 이용하여 그린다.

```python
plt.pie(date)
```

- 레이블 달기
    
    labels : label 목록
    
    labeldistance : 그래프로부터 레이블을 떨어뜨릴 정도 (default : 1.1)
    
    ```python
    plt.pie(data, labels=label목록, labeldistance=1.2)
    ```
    
- 비율 표시하기
    
    autopct : ‘%소수점 자리수%%’
    
    pctdistance : 중심에서의 거리
    
                    (반지름을 1이라고 했을 때 반지름으로부터 떨어뜨릴 정도, default : 0.6)
    
    ```python
    plt.pie(data, autopct='%.1f%%', pctdistance=0.8)
    ```
    
- 돌출효과
    
    explode : 돌출 정도 리스트 (반지름의 길이를 1이라고 했을 때를 기준으로 돌출 정도 지정)
    
    ```python
    plt.pie(data, explode=[0,1,0,0,0])
    ```
    
- 색상 바꾸기
    
    color : 색상 리스트
    
    ```python
    plt.pie(data, colors=['lightcoral', 'gold', 'greenyellow', 'skyblue'])
    ```
    
- 시작각도
    
    startangle : 시작 각도 (default : 3시 방향)
    
    시작 각도를 지정하면 3시 방향으로부터 반시계 방향으로 각도만큼 이동
    
    ```python
    plt.pie(Personnel, startangle=90)
    ```
    
- 회전방향
    
    counterclock : True/False (반시계/시계)
    
    ```python
    plt.pie(Personnel, counterclock=False)
    ```
    
- 범례
    
    legend(레이블 리스트)
    
    ```python
    plt.pie(Personnel)
    plt.legend(loc=(1,0.5))
    ```
    
- 반지름
    
    radius : 반지름 (default : 1)
    
    ```python
    plt.pie(Personnel, radius=1)
    ```
    
- 부채꼴 스타일
    
    wedgeprops = {’ec’ : 테두리 색상, ‘lw’ : 선 두께, ‘ls’ : 선 스타일, ‘width’ : 반지름에 대한 비율}
    
    ```python
    plt.pie(Personnel, wedgeprops = {'ec':'k', 'lw':1, 'ls':':', 'width':0.7})
    ```
    
- 폰트
    
    textprops = {’fontsize’ : 폰트 사이즈, ‘color’ : 폰트 색상, ‘rotation; : 폰트 회전 각도}
    
    ```python
    plt.pie(Personnel, textprops = {'fontsize':12, 'color':'b', 'rotation':0})
    ```
    

### 공통 스타일 지정하기

rcParams(Runtime Configuration Parameters)을 통해 그래프를 구성하는 공통 속성을 설정함

```python
# rcParams의 종류 확인 코드
plt.rcParams
```

- figure
    
    ```python
    # figure 크기
    plt.rcParams['figure.figsize']=(9,4)
    ```
    
- axes
    
    ```python
    # 그래프 테두리 두께
    plt.rcParams['axes.linewidth'] = 2
    
    # 그래프 테두리 색
    plt.rcParams['axes.edgecolor'] = 'navy'
    
    # 그래프 바탕 색
    plt.rcParams['axes.facecolor'] = 'ghostwhite'
    
    # 그리드 표시
    plt.rcParams['axes.grid'] = True
    
    # 그래프 제목
    plt.rcParams['axes.titlecolor'] = 'navy'
    plt.rcParams['axes.titlesize'] = 15
    plt.rcParams['axes.titleweight']='bold'
    
    # 레이블
    plt.rcParams['axes.labelcolor'] = 'gray'
    plt.rcParams['axes.labelsize'] = 12
    ```
    
- 그리드
    
    ```python
    plt.rcParams['grid.alpha'] = 0.3
    plt.rcParams['grid.color'] = 'skyblue'
    plt.rcParams['grid.linestyle'] ='--'
    ```
    
- 폰트
    
    ```python
    plt.rcParams['font.size']=12
    ```
    
- 눈금
    
    ```python
    plt.rcParams['xtick.top'] = True
    plt.rcParams['ytick.right'] = True
    plt.rcParams['xtick.direction'] = 'in'
    plt.rcParams['ytick.direction'] = 'in'
    plt.rcParams['xtick.major.size'] = 10
    plt.rcParams['ytick.major.size'] = 10
    ```
    
- 선
    
    ```python
    plt.rcParams['lines.linewidth']=3
    plt.rcParams['lines.linestyle']='--'
    plt.rcParams['lines.marker'] ='o'
    ```
    
- 패턴
    
    ```python
    plt.rcParams['hatch.linewidth']=3
    plt.rcParams['hatch.color'] = 'w'
    ```
    
- 박스
    
    ```python
    # 박스
    plt.rcParams['boxplot.boxprops.color'] = 'b'
    plt.rcParams['boxplot.boxprops.linewidth'] = 2
    
    # 최대값, 최소값
    plt.rcParams['boxplot.capprops.color'] = 'r'
    plt.rcParams['boxplot.capprops.linewidth'] = 2
    
    # 평균
    plt.rcParams['boxplot.showmeans'] = True
    ```
    

### 그래프 강조하기 - 영역 채우기

- 가로 방향으로 채우기
    
    ```python
    # 슬라이싱 범위가 같아야 한다.
    plt.fill_between(x슬라이싱, y슬라이싱)
    ```
    
- 세로 방향으로 채우기
    
    ```python
    # 슬라이싱 범위가 같아야 한다.
    plt.fill_betweenx(y슬라이싱, x슬라이싱)
    ```
    
- 두 그래프 사이의 영역 채우기
    
    ```python
    plt.fill_between(x슬라이싱, y1슬라이싱, y2슬라이싱)
    ```
    
- 다각형 채우기
    
    ```python
    plt.fill([x축의 좌표들], [y축의 좌표들])
    ```
    

### 그래프 강조하기 - 수직선과 수평선

- 수평선 그리기
    
    수평선의 길이가 1이라고 했을 때, x축 시작 위치, x축 끝 위치를 지정한다.
    따로 지정하지 않으면 x축 전 범위에 걸쳐 그려진다.
    
    ```python
    plt.axhline(y좌표, x축 시작 위치, x축 끝 위치)
    plt.hlines(y, x축 시작 좌표, x축 끝 좌표)
    ```
    
- 수직선 그리기
    
    수직선의 길이가 1이라고 했을 때, y축 시작 위치, y축 끝 위치를 지정한다.
    따로 지정하지 않으면 y축 전 범위에 걸쳐 그려진다.
    
    ```python
    plt.axvline(x좌표, y축 시작 위치, y축 끝 위치)
    plt.vlines(x, y축 시작 좌표, y축 끝 좌표)
    ```