## 대출금 연체 고객에 대한 인사이트 분석 
- 고객 특성을 반영한 리스크 관리방안 수립으로 수익성 향상


## 데이터 확인
df1= pd.read_csv('bank.csv')
  <table>
        <thead>
            <tr>
                <th>BAD</th>
                <th>LOAN</th>
                <th>MORTDUE</th>
                <th>VALUE</th>
                <th>REASON</th>
                <th>JOB</th>
                <th>YOJ</th>
                <th>DEROG</th>
                <th>DELINQ</th>
                <th>CLAGE</th>
                <th>NINQ</th>
                <th>CLNO</th>
                <th>DEBTINC</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>1700</td>
                <td>30548</td>
                <td>40320.0</td>
                <td>HomeImp</td>
                <td>Other</td>
                <td>9.0</td>
                <td>0</td>
                <td>0</td>
                <td>101.466002</td>
                <td>1.0</td>
                <td>8</td>
                <td>37.113614</td>
            </tr>
            <tr>
                <td>1</td>
                <td>1800</td>
                <td>28502</td>
                <td>43034.0</td>
                <td>HomeImp</td>
                <td>Other</td>
                <td>11.0</td>
                <td>0</td>
                <td>0</td>
                <td>88.766030</td>
                <td>0.0</td>
                <td>8</td>
                <td>36.884894</td>
            </tr>
            <tr>
                <td>0</td>
                <td>2300</td>
                <td>102370</td>
                <td>120953.0</td>
                <td>HomeImp</td>
                <td>Office</td>
                <td>2.0</td>
                <td>0</td>
                <td>0</td>
                <td>90.992533</td>
                <td>0.0</td>
                <td>13</td>
                <td>31.588503</td>
            </tr>
            <tr>
                <td>1</td>
                <td>2400</td>
                <td>34863</td>
                <td>47471.0</td>
                <td>HomeImp</td>
                <td>Mgr</td>
                <td>12.0</td>
                <td>0</td>
                <td>0</td>
                <td>70.491080</td>
                <td>1.0</td>
                <td>21</td>
                <td>38.263601</td>
            </tr>
            <tr>
                <td>0</td>
                <td>2400</td>
                <td>98449</td>
                <td>117195.0</td>
                <td>HomeImp</td>
                <td>Office</td>
                <td>4.0</td>
                <td>0</td>
                <td>0</td>
                <td>93.811775</td>
                <td>0.0</td>
                <td>13</td>
                <td>29.681827</td>
            </tr>
            <tr>
                <td>0</td>
                <td>88900</td>
                <td>57264</td>
                <td>90185.0</td>
                <td>DebtCon</td>
                <td>Other</td>
                <td>16.0</td>
                <td>0</td>
                <td>0</td>
                <td>221.808718</td>
                <td>0.0</td>
                <td>16</td>
                <td>36.112347</td>
            </tr>
            <tr>
                <td>0</td>
                <td>89000</td>
                <td>54576</td>
                <td>92937.0</td>
                <td>DebtCon</td>
                <td>Other</td>
                <td>16.0</td>
                <td>0</td>
                <td>0</td>
                <td>208.692070</td>
                <td>0.0</td>
                <td>15</td>
                <td>35.859971</td>
            </tr>
            <tr>
                <td>0</td>
                <td>89200</td>
                <td>54045</td>
                <td>92924.0</td>
                <td>DebtCon</td>
                <td>Other</td>
                <td>15.0</td>
                <td>0</td>
                <td>0</td>
                <td>212.279697</td>
                <td>0.0</td>
                <td>15</td>
                <td>35.556590</td>
            </tr>
            <tr>
                <td>0</td>
                <td>89800</td>
                <td>50370</td>
                <td>91861.0</td>
                <td>DebtCon</td>
                <td>Other</td>
                <td>14.0</td>
                <td>0</td>
                <td>0</td>
                <td>213.892709</td>
                <td>0.0</td>
                <td>16</td>
                <td>34.340882</td>
            </tr>
            <tr>
                <td>0</td>
                <td>89900</td>
                <td>48811</td>
                <td>88934.0</td>
                <td>DebtCon</td>
                <td>Other</td>
                <td>15.0</td>
                <td>0</td>
                <td>0</td>
                <td>219.601002</td>
                <td>0.0</td>
                <td>16</td>
                <td>34.571519</td>
            </tr>
        </tbody>
    </table>



## 결측치 확인
```  df1.isnull().sum() ```

## 결측치 제거
```df1.dropna(inplace =True)```

## 이상치 확인
```
columns_to_plot = ['BAD', 'LOAN', 'MORTDUE', 'VALUE', 'REASON', 'JOB', 'YOJ', 
                   'DEROG', 'DELINQ', 'CLAGE', 'NINQ', 'CLNO', 'DEBTINC']

df_subset = df1[columns_to_plot]

plt.figure(figsize=(12, 8))
sns.boxplot(data=df_subset)

plt.title('Boxplot of Selected Columns', fontsize=16)
plt.xticks(rotation=90)  # x축 레이블이 잘 보이도록 회전
plt.xlabel('Columns', fontsize=12)
plt.ylabel('Values', fontsize=12)

plt.show()
```

## 대출 상환 여부에 따른 영향인자 확인
```
BAD_L = df2[df2['BAD'] == 0]['LOAN']   # 상환  
good_L = df2[df2['BAD'] == 1]['LOAN']  # 미상환 

# 상환 여부에 따라서 대출액이 차이가 있는가
# 귀무가설 : 상환 여부에 따라서 대출액이 차이가 없다 -> 귀무가설 참 => 상환 여부에 따라서 대출액이 차이가 없다
# 대립가설 : 상환 여부에 따라서 대출액이 차이가 있다 

weight_result= stats.ttest_ind(BAD_L,good_L)
t,p = weight_result.statistic, weight_result.pvalue
print("대출액-sample t-test")
print("t:{}".format(t))
print("p:{}".format(p))

# 가설 검정
alpha = 0.05  # 유의수준 5%

if p < alpha:
    print(" 상환 여부에 따라 대출액에 차이가 있다.")
else:
    print("상환 여부에 따라 대출액에 차이가 없다.")
```

## 인사이트 도출 
![image](https://github.com/user-attachments/assets/5e01f773-3111-4b97-9f0c-5a3d3659e46c)
- 불량거래수가 사무직에 많이 분포되어있으므로 사무직에 근무하는 사람에 대한 신용관리 정보 시스템을 제공필요

