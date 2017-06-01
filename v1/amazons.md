
# Konimbo API Docs
## מוצרים
### תוכן עניינים
0. [חזור לדף הראשי](https://github.com/heimanmorad/konimbo-api-docs)
1. [הקדמה](#user-content-הקדמה)
2. [EndPoints](#user-content-endpoints)
3. [פירוט השדות](#user-content-פירוט-השדות)
4. [מוצר](#user-content-מוצר)
5. [מוצרים](#user-content-מוצרים)
6. [יצירת מוצר](#user-content-יצירת-מוצר)
7. [עריכת מוצר](#user-content-עריכת-מוצר)
8. [מחיקת מוצר](#user-content-מחיקת-מוצר)

### הקדמה
בעזרת נקודת קצה זו ניתן לקרוא קבצים מ - Amazon s3
### EndPoints
* [POST /{apiVersion}/items](#user-content-יצירת-מוצר)

### פירוט השדות
#### שדות פשוטים:
שם השדה | סכמה | ניתן לעדכון | הסבר | דוגמא
:--|:---|---:|---:|---:
id                     | Integer         | לא | מספר המוצר במערכת קונימבו | `1203546`
title                  | String          | כן | כותרת המוצר | `טלפון סלולארי`
store_category_title   | String          | כן | הקטגוריה שאליה המוצר שייך | `טלפונים`
price                  | Numeric         | כן | מחיר המוצר | `55.50`, `999`
origin_price           | Numeric         | כן | מחיר מקורי (לפני מבצע) | `1499`, `1999.99`
code                   | String          | כן | מק"ט המוצר | `SKU#123`, `49841687468`
second_code            | String          | כן | מקט משני (לשימוש פנימי) | `6418351816`
desc                   | String          | כן | תיאור קצר על המוצר | `טלפון מתקדם מיצרן בינלאומי, מספר אחד בתחום הטלפונים`
visible                | Boolean         | כן | האם המוצר מופיע בחנות או מוסתר | `true`, `false`
model_title            | String          | כן | שם הספק | `MyProvider`
created_at             | Time (ISO-8601) | לא | זמן יצירת המוצר | `2016-01-01T09:00:00Z`
updated_at             | Time (ISO-8601) | לא | זמן העדכון האחרון של המוצר | `2017-01-01T09:00:00Z`
related_items          | Array           | כן | רשימת הids של המוצרים הנלווים | `[1253456, 654879]`



### אמזון
#### תיאור
בעזרת השירות הזה, ניתן להחזיר מידע של קובץ בתצורת XML או JSON

ניתן לבקש מהשרת רק את השדות שתרצו

#### EndPoint
```
POST /{apiVersion}/item/{id/code/second_code}?token={yourToken}
Host: api.konimbo.co.il
```

#### Parameters
##### בקשת שדות מסויימים
כדי שהשרת יידע איזה שדות להחזיר יש לציין בפרמטר attributes את השדות המבוקשים מופרדים בפסיקים.

[לרשימת השדות](#user-content-פירוט-השדות)

לדוגמא: `attributes=id,price,code`

במידה ולא נשלח פרמטר זה, יוחזרו כל השדות המורשים למשתמש זה.

#### Responses
* 200 - The requested item
* 401 - Unauthorized
* 404 - No results found
* 500 - Internal error

#### דוגמאות
הקריאה הבאה תחזיר את כל השדות המורשים למוצר עם הid 1234567
```
GET /v1/items/1234567?token=e012a2944be024a85062c2bbd27b9f61284bf2439fd87992069b84b6a4ef93ca HTTP/1.1
Host: api.konimbo.co.il
```

הקריאה הבאה תחזיר את השדות title,store_category_title של המוצר עם הid1234567
```
GET /v1/items/1234567?token=e012a2944be024a85062c2bbd27b9f61284bf2439fd87992069b84b6a4ef93ca&attributes=title,store_category_title HTTP/1.1
Host: api.konimbo.co.il
```

**ניתן לחפש לפי מק"ט או לפי מקט משני, כדי לעשות זאת יש ליצור קשר עם התמיכה**

