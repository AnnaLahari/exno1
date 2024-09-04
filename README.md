# Exno:1
Data Cleaning Process

# AIM:
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation:
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm:
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output:
```
import pandas as pd
df=pd.read_csv("/content/SAMPLEIDS.csv")
df
```
![image](https://github.com/user-attachments/assets/891df9ef-3f6f-475f-9092-f78bcc3f768b)

```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/f3c29954-7533-4ae6-8eb7-be470b8f0807)

```
df.isnull().any()
```
![Screenshot 2024-09-04 181834](https://github.com/user-attachments/assets/82a124dd-9681-483c-9dce-84c3e6e5011b)
```
df.dropna()
```

![image](https://github.com/user-attachments/assets/1147f0e9-dede-4039-8d31-c6f8dc981394)

```
df.fillna(0)
```

![image](https://github.com/user-attachments/assets/f0e15529-30b0-4ab4-933f-89f93f7ee154)

```
df.fillna(method = 'ffill')
```

![image](https://github.com/user-attachments/assets/1c03480c-2a30-4a86-89cf-2dd9f7f58f96)

```
df.fillna(method = 'bfill')
```
![image](https://github.com/user-attachments/assets/a8df7402-9a5d-4c06-9a12-1d4d01adc315)

```
df_dropped = df.dropna()
df_dropped
```

![image](https://github.com/user-attachments/assets/6e793791-6582-403e-8e0d-7aaacb5aabd4)

```
df.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```

![image](https://github.com/user-attachments/assets/8eae12c1-e4c6-48c2-b5e5-e6019f3b79df)


## IQR(Inter Quartile Range)

```
import pandas as pd
ir = pd.read_csv('/content/iris.csv')
ir
```

![image](https://github.com/user-attachments/assets/78161f01-7c48-47f6-8070-07e5f483d7cc)

```
ir.describe()
```
![image](https://github.com/user-attachments/assets/5e86e363-fb4b-4723-8d3c-2eb77a1a753a)

```
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/user-attachments/assets/1cc948cc-0da9-4388-b1bd-dd34a208d246)
```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq = c3-c1
print(c3)
```
![image](https://github.com/user-attachments/assets/c1321252-a661-46dd-a73b-0ac0d3f47bea)
```
rid = ir[((ir.sepal_width < (c1 - 1.5 * iq)) | (ir.sepal_width > (c3 + 1.5 * iq)))]
rid['sepal_width']
```

![image](https://github.com/user-attachments/assets/21fd2fe7-9f06-41c6-9f43-9e30c570ff4a)
```
delid =ir[~((ir.sepal_width < (c1 - 1.5 * iq)) | (ir.sepal_width > (c3 + 1.5 * iq)))]
delid
```
![image](https://github.com/user-attachments/assets/0be6ea84-c630-4b53-af0f-2a936e265f70)

```
sns.boxplot(x='sepal_width', data=delid)
```
![Screenshot 2024-09-04 205505](https://github.com/user-attachments/assets/dcb63b9e-9e84-4326-91dc-5116ee2d2c7e)

```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset = pd.read_csv('/content/heights.csv')
dataset
```
![image](https://github.com/user-attachments/assets/34882a14-c093-499b-a257-337f29ec1337)
```
df = pd.read_csv('/content/heights.csv')
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3 - q1
iqr
```
![image](https://github.com/user-attachments/assets/d941b7c5-e27f-42b1-ab36-f027ea777827)
```
low = q1 - 1.5 * iqr
low
```
![image](https://github.com/user-attachments/assets/81121ed0-200f-4258-a9d7-0269cd15de09)
```
high = q3 + 1.5 * iqr
high
```
![image](https://github.com/user-attachments/assets/82c1f85c-677a-41b4-b62c-4aebe163b6c2)
```
df1 = df[(df['height'] >= low) & (df['height'] <= high)]
df1
```
![image](https://github.com/user-attachments/assets/c91b74af-0ac9-467a-bd0a-99c99b63a667)

```
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/user-attachments/assets/cfe8c0bb-5313-468d-94e1-17223f7acdf6)
```
df1 = df[(z < 3)]
df1
```
![image](https://github.com/user-attachments/assets/daa1818f-8826-4330-9b35-7edc3d3297c7)

## Result:
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
