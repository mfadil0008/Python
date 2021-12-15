DF-Code:

# Tips and Tricks for Python
List File to CSV

Sometimes we want to input someone's name and id based on the file name into an excel or csv file. When we input the name and id one by one, it takes a lot of time.

### 1. Read list file and save to list_file.txt
`!dir list_file /b` print all file in directoru list_file and `>` for save all output to list_file.txt
```python
!dir list_file /b
!dir list_file /b > list_file.txt
```
output:
```
ID20210001_Name 001_Task Title 001.docx
ID20210002_Name 002_Task Title 002.docx
ID20210003_Name 003_Task Title 003.docx
ID20210004_Name 004_Task Title 004.docx
ID20210005_Name 005_Task Title 005.docx
ID20210006_Name 006_Task Title 006.docx
ID20210007_Name 007_Task Title 007.docx
ID20210008_Name 008_Task Title 008.docx
ID20210009_Name 009_Task Title 009.docx
```
`!dir` for chek file
```python
!dir
```
output:
```
 Volume in drive E is Files
 Volume Serial Number is E019-86CC

 Directory of ~

12/16/2021  01:12 AM    <DIR>          .
12/16/2021  01:12 AM    <DIR>          ..
12/15/2021  11:24 PM    <DIR>          .ipynb_checkpoints
12/16/2021  01:12 AM    <DIR>          list_file
12/16/2021  01:12 AM             6,150 list_file.txt
12/16/2021  01:12 AM            15,700 Untitled.ipynb
               2 File(s)         21,850 bytes
               4 Dir(s)  55,737,835,520 bytes free
```
### 2. Read list file to csv
read `list_file.txt` to csv using library pandas. first  `import library pandas` if error, you can run `!pip install pandas`
```python
import pandas as pd
list_file_csv = pd.read_csv('list_file.txt', sep = '_', header=None)
list_file_csv.columns=['ID','Name','Title']
list_file_csv.head()
```
output:
```
  ID         Name     Title
0 ID20210001 Name 001 Task Title 001.docx
1 ID20210002 Name 002 Task Title 002.docx
2 ID20210003 Name 003 Task Title 003.docx
3 ID20210004 Name 004 Task Title 004.docx
4 ID20210005 Name 005 Title 005.docx
```
### 3. Function clear: clear attribute file (.docx)
columns title: `Task Title 001.docx`. function clear for delete attribute file (.docx)
```python
def clear(text):
    if '.doc' in text:
        return(text[:text.find('.doc')])
    elif '.pdf' in text:
        return(text[:text.find('.pdf')])
    else:
        return(text)
```
Hands-on Data Cleaning using function `applymap`
```python
list_file_csv = list_file_csv.applymap(clear)
list_file_csv.head()
```
output:
```
  ID         Name     Title
0 ID20210001 Name 001 Task Title 001
1 ID20210002 Name 002 Task Title 002
2 ID20210003 Name 003 Task Title 003
3 ID20210004 Name 004 Task Title 004
4 ID20210005 Name 005 Task Title 005
```
### 4. Save data frame to csv
finish save file to csv
```python
list_file_csv.to_csv('list_file.csv',index=None)
```
