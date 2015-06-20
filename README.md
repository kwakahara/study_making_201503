﻿# 2015年3月度課題 #

Lv.1, Lv.2 共通  
■  

- ユーザーテーブル(USERS)は入会日(JOINED_DATE)と退会日(LEFT_DATE)を持っている  

- 退会していないユーザーの場合、退会日にはNULLが入る
 
## (1-1) ユーザー数の増減を確認するために、日付単位で入会したユーザーの人数と退会したユーザーの人数を一覧化したい。  どうすれば取得できるか？ ##

ユーザーテーブル(USERS)
---
| UID(主キー) | JOINED_DATE | LEFT_DATE  |
|-------------|-------------|------------|
| １          | 2015-03-01  | 2015-03-10 |
| 2           | 2015-03-01  | 2015-03-05 |
| 3           | 2015-03-03  | NULL       |
| 4           | 2015-03-03  | 2015-03-10 |
| 5           | 2015-03-10  | NULL       |

期待する出力結果
---
| DATE       | JOINED_COUNT | LEFT_COUNT |
|------------|--------------|------------|
| 2015-03-01 | 2            | 0          |
| 2015-03-03 | 2            | 0          |
| 2015-03-05 | 0            | 1          |
| 2015-03-10 | 1            | 2          |

スキーマ作成用のSQL
---
>CREATE TABLE USERS (  
UID INTEGER PRIMARY KEY,  
JOINED_DATE DATE NOT NULL,  
LEFT_DATE DATE NULL  
);

---  
>INSERT INTO USERS VALUES (1, '2015-03-01', '2015-03-10');  
INSERT INTO USERS VALUES (2, '2015-03-01', '2015-03-05');  
INSERT INTO USERS VALUES (3, '2015-03-03', NULL);  
INSERT INTO USERS VALUES (4, '2015-03-03', '2015-03-10');  
INSERT INTO USERS VALUES (5, '2015-03-10', NULL);  
---  

## (1-2)その日時点での会員数も取得してください。 ##

期待する出力結果
---
| DATE       | JOINED_COUNT | LEFT_COUNT | USER_COUNT |
|------------|--------------|------------|------------|
| 2015-03-01 | 2            | 0          | 2          |
| 2015-03-03 | 2            | 0          | 4          |
| 2015-03-05 | 0            | 1          | 3          |
| 2015-03-10 | 1            | 2          | 2          |

___