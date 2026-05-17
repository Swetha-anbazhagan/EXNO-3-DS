## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.

STEP 2:Clean the Data Set using Data Cleaning Process.

STEP 3:Apply Feature Encoding for the feature in the data set.

STEP 4:Apply Feature Transformation for the feature in the data set.

STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding:
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.

2. Label Encoding:
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.

3. Binary Encoding:
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.

4. One Hot Encoding:
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:

## Encoding:
```
import pandas as pd
import numpy as np
from scipy import stats
df = pd.read_csv('data.csv')
print(df)

```
<img width="747" height="262" alt="image" src="https://github.com/user-attachments/assets/42d29026-1c01-41ad-87e1-970c6eb1f331" />

### Ordinal Encoding:

```
from sklearn.preprocessing import OrdinalEncoder,LabelEncoder
climate = ['Cold','Warm','Hot','Very Hot']
ele = OrdinalEncoder(categories=[climate])
ele.fit_transform(df[["Ord_1"]])

```
<img width="715" height="261" alt="image" src="https://github.com/user-attachments/assets/6da0157c-e7db-489f-bc7c-80731d3ce0ae" />

```
df['bo2'] = ele.fit_transform(df[["Ord_1"]])
df
```
<img width="663" height="450" alt="image" src="https://github.com/user-attachments/assets/3b97b960-aa0d-44dd-ba6d-c22f86c5c74f" />

### Label Encoding:

```
le = LabelEncoder()
df2 = df.copy()
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2
```
<img width="622" height="442" alt="image" src="https://github.com/user-attachments/assets/49692ee1-d5db-4525-bc1d-9f717a85970d" />

```
df2['Ord_2'] = le.fit_transform(df2['Ord_2'])
df2

```
<img width="631" height="466" alt="image" src="https://github.com/user-attachments/assets/ae38fecd-31ce-4483-b6b7-3140e51cb5fb" />

### OneHot Encoding:

```
from sklearn.preprocessing import OneHotEncoder
ohe = OneHotEncoder()
df3 = df.copy()
enc = pd.DataFrame(ohe.fit_transform(df2[["City"]]))
df2 = pd.concat([enc,df3],axis = 1)
df2
```

<img width="1088" height="453" alt="image" src="https://github.com/user-attachments/assets/2ccbb2b7-03f1-48c2-b358-1d85dd216ab8" />

```

pd.get_dummies(df,columns=['City'])
```

<img width="1056" height="443" alt="image" src="https://github.com/user-attachments/assets/ce223ac9-6c5c-4e21-8944-c5ee9d4e88b4" />


### Binary Encoding:

```
from category_encoders import BinaryEncoder
df = pd.read_csv('data.csv')
df
```

<img width="603" height="432" alt="image" src="https://github.com/user-attachments/assets/91010066-7a50-45d8-8b58-078394a76a62" />

```
be = BinaryEncoder()
nd = be.fit_transform(df['Ord_2'])
df
```

<img width="580" height="446" alt="image" src="https://github.com/user-attachments/assets/a399af85-615e-4f98-bfc7-62800c28d81b" />


### Target Encoding:
```
from category_encoders import TargetEncoder
te = TargetEncoder()
CC = df.copy()
new = te.fit_transform(CC["City"],y=CC["Target"])
CC = pd.concat([CC,new],axis = 1)
CC

```
<img width="712" height="440" alt="image" src="https://github.com/user-attachments/assets/62e17931-62c7-4029-8ab5-95cabacaa7ca" />

```
if 'City' in CC.columns:
    CC = CC.drop('City', axis=1)
new = te.fit_transform(X = df["City"],y=df["Target"])
CC = pd.concat([CC.reset_index(drop=True),new.reset_index(drop=True)],axis = 1)
CC

```

<img width="567" height="446" alt="image" src="https://github.com/user-attachments/assets/0ba26fb8-0fd2-4a73-94fc-230d4423bfd8" />

## Transformation

```

df = pd.read_csv('Data_to_Transform.csv')
df
```
<img width="941" height="477" alt="image" src="https://github.com/user-attachments/assets/aeb47a27-6773-4eca-aa33-c363d3542cd2" />

```
df.skew()

```
<img width="377" height="231" alt="image" src="https://github.com/user-attachments/assets/27088607-8aaa-47b2-863a-3d801ab1c62e" />

### Function Transformation:

```
np.log(df["Highly Positive Skew"])

```

<img width="365" height="553" alt="image" src="https://github.com/user-attachments/assets/f01238fe-7e45-40d5-aee1-1930e7f1c316" />

```
np.reciprocal(df["Moderate Positive Skew"])

```

<img width="392" height="562" alt="image" src="https://github.com/user-attachments/assets/60f65e32-c94e-4105-9ef9-8ca7553518df" />

```
np.sqrt(df["Highly Positive Skew"])

```

<img width="352" height="567" alt="image" src="https://github.com/user-attachments/assets/d1f851bc-7604-4403-86b5-d9e4f64b6145" />

```
np.square(df["Highly Positive Skew"])
```

<img width="422" height="562" alt="image" src="https://github.com/user-attachments/assets/5e07b9e5-ad5c-4078-a853-fc2f3d33a5fd" />


### Power Transformation

```
df["Highly Positive Skew_boxcox"], parameters = stats.boxcox(df["Highly Positive Skew"])
df
```
<img width="1232" height="507" alt="image" src="https://github.com/user-attachments/assets/d984511f-c63f-403a-9755-f1450c30ee5e" />

```
df["Moderate Negative Skew_yeojohnson"], parameters = stats.yeojohnson(df["Moderate Negative Skew"])
df
```
<img width="1570" height="510" alt="image" src="https://github.com/user-attachments/assets/9c5ed6bc-279e-4923-afa1-29de1c0e74c2" />

```
from sklearn.preprocessing import QuantileTransformer
qt = QuantileTransformer(output_distribution = 'normal')
df["Moderate Negative Skew_1"] = qt.fit_transform(df[["Moderate Negative Skew"]])
df

```

<img width="1677" height="568" alt="image" src="https://github.com/user-attachments/assets/1117aa21-e720-4aba-bac3-7fce6149062e" />

```

import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
import scipy.stats as stats
sm.qqplot(df["Moderate Negative Skew"],line = '45')
plt.show()

```

<img width="712" height="531" alt="image" src="https://github.com/user-attachments/assets/867de01c-f788-476d-9f93-5842018c607c" />

```

sm.qqplot(df["Moderate Negative Skew_1"],line = '45')
plt.show()

```

<img width="707" height="541" alt="image" src="https://github.com/user-attachments/assets/194aa3e4-1325-4e25-9e04-250bfb82b328" />


```
df["Highly Negative Skew_1"] = qt.fit_transform(df[["Highly Negative Skew"]])
sm.qqplot(df["Highly Negative Skew"],line = '45')
plt.show()
```

<img width="706" height="537" alt="image" src="https://github.com/user-attachments/assets/4a834de6-a932-4769-9dc8-b0c509282ca3" />

```
sm.qqplot(np.reciprocal(df["Moderate Negative Skew_1"]),line = '45')
plt.show()

```
<img width="712" height="508" alt="image" src="https://github.com/user-attachments/assets/de3784a3-e043-46f2-aea1-57862c682815" />

```
sm.qqplot(df["Highly Negative Skew_1"],line = '45')
plt.show()

```
<img width="702" height="535" alt="image" src="https://github.com/user-attachments/assets/2f01537e-edf7-421b-828d-d652b5cb0a30" />

```
sm.qqplot(np.abs(df["Highly Negative Skew_1"]),line = '45')
plt.show()

```
<img width="705" height="537" alt="image" src="https://github.com/user-attachments/assets/03e776be-9a86-42e7-b141-f5f73a662fe5" />

```
sm.qqplot(np.log(df["Highly Negative Skew_1"]),line = '45')
plt.show()

```
<img width="710" height="546" alt="image" src="https://github.com/user-attachments/assets/d3063a0a-2b88-488c-b756-6dda74ebc4ce" />

```
sm.qqplot(np.sqrt(df["Moderate Negative Skew_1"]),line='45')
plt.show()

```

<img width="702" height="535" alt="image" src="https://github.com/user-attachments/assets/5ecf22eb-2ddb-4941-adc9-72286092bd0c" />

```
pd.concat([CC,new],axis = 1)

```

<img width="677" height="442" alt="image" src="https://github.com/user-attachments/assets/9677b947-23dc-42f1-a149-dee1de4240da" />

# RESULT:
       # INCLUDE YOUR RESULT HERE

       
