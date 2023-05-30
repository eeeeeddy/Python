# Seaborn

23.05.17

```python
import seaborn as sns
```

### 막대 그래프

x축 데이터로 grouping한 y축 데이터의 평균값을 계산하여 그래프를 그린다.
신뢰구간(CI:Confidence Interval)을 함께 표시한다.

```python
sns.barplot(data=DataFrame, x=x_col, y=y_col, ci=None)
```

```python
# estimator : 통계함수
sns.barplot(data=df, x=x_col, y=y_col, ci=None, estimater=sum)

# hue : y를 grouping할 column
# hue 색상 변경 : palette = {구분 : 색상 딕셔너리}
sns.barplot(data=df, x=x_col, y=y_col, ci=None, estimater=sum, heu=col1
						, palette = {'Yes' : 'gray', 'No' : 'red'})
```

### Scatter plot

```python
sns.scatterplot(data=DataFrame, x=x_col, y=y_col)
```

### Line plot

```python
sns.lineplot(data=DataFrame, x=x_col, y=y_col, estimator=통계함수)
```

### 기타 그래프

1. **Counterplot**
    
    ```python
    sns.countplot(data=DataFrame, x=x_col)
    ```
    
2. **Rugplot**
    
    ```python
    sns.rugplot(data=DataFrame, x=x_col)
    ```
    
3. **Histogram**
    
    kde : 커널 밀도 함수 표시 (True/False)
    
    ```python
    sns.displot(data=DataFrame, x=x_col)
    ```
    
4. **Boxplot**
    
    ```python
    sns.boxplot(data=DataFrame)
    ```
    
5. **Violinplot**
    
    ```python
    sns.violinplot(data=DataFrame)
    ```
    
6. **Stripplot**
    
    ```python
    sns.stripplot(data=DataFrame)
    ```
    
7. **Swarmplot**
    
    ```python
    sns.swarmplot(data=DataFrame)
    ```