# Access Control Vulnerabilities

## 1️⃣ Access Control

**Access Control** মানে হচ্ছে — কে কোন **resource** বা **functionality** ব্যবহার করতে পারবে তা নিয়ন্ত্রণ করা।

### উদাহরণ
- শুধু **admin user** যেন user delete করতে পারে  
- সাধারণ **user** যেন শুধু নিজের **profile edit** করতে পারে  

যদি এই নিয়ন্ত্রণ ঠিকভাবে না করা হয়, তখন **Access Control Vulnerability** হয়।

---

## 2️⃣ Vertical Access Control

এটা **different privilege level** এর মধ্যে access control।

মানে **low privilege user → high privilege action** করতে পারে কিনা।

### উদাহরণ

Admin panel endpoint:

```
/admin/deleteUser?id=5
```

যদি **normal user** এই URL access করে **user delete** করতে পারে → এটা **Vertical Access Control Vulnerability**।

📌 **সহজ ভাষায়:**  
User → **Admin level action** করতে পারলে = **Vertical Privilege Escalation**

---

## 3️⃣ Horizontal Access Control

এটা **same privilege level users** এর মধ্যে access control।

মানে এক user যেন **অন্য user এর data access** করতে না পারে।

### উদাহরণ

User profile endpoint:

```
/account?id=123
```

যদি তুমি URL change করো:

```
/account?id=124
```

আর অন্য user এর **account দেখতে পাও** → এটা **Horizontal Access Control Vulnerability**।

📌 **সহজ ভাষায়:**  
User A → User B এর **data access** করলে = **Horizontal Privilege Escalation**

---

## 4️⃣ Context-Dependent Access Control

এখানে access **situation বা context** এর উপর depend করে।

মানে action করার জন্য কিছু **condition** থাকতে হবে।

### উদাহরণ

Shopping site এ **order cancel**:

- order cancel করা যাবে **order placed হওয়ার পর 10 মিনিটের মধ্যে**
- order **shipped** হলে cancel করা যাবে না

যদি কেউ **shipped order cancel** করতে পারে → এটা **Context-Dependent Access Control Vulnerability**।

---

## Privilege Escalation

**Privilege Escalation** মানে হলো attacker নিজের **permission বা authority বাড়িয়ে ফেলা**।

➡️ অর্থাৎ একজন **low-level user** এমন কিছু করতে পারে যা **admin level user** এর জন্য রাখা ছিল।

### Example
একজন normal user যদি **URL change করে admin panel access পেয়ে যায়**।

---

## 1️⃣ Vertical Privilege Escalation

**Vertical Privilege Escalation** হলো নিচের level থেকে উপরের level এ যাওয়া।

➡️ **User → Admin**

### Example
ধরো একটা website এ 2 ধরনের account আছে:

- Normal User  
- Admin  

Normal user যদি system এর **bug use করে admin features access করে ফেলে**, তাহলে সেটা **Vertical Privilege Escalation**।

📌 **Example URL**
```
website.com/admin/deleteUser
```

Normal user যদি এই link open করে **user delete করতে পারে** → **Vertical Privilege Escalation**

---

**Use Korbo** : `robot.txt`  or `sitemap.xml` or `.htaccess`(windows)

## 2️⃣ Horizontal Privilege Escalation

**Horizontal Privilege Escalation** মানে হলো **same level user এর data access করা**।

➡️ **User A → User B এর data access**

### Example

ধরো profile URL:
```
website.com/profile?id=101
```

যদি **User A** `id=101` থেকে `id=102` করে **অন্য user এর profile দেখতে পারে**।

তাহলে এটা **Horizontal Privilege Escalation**।

---

## 3️⃣ Horizontal to Vertical Privilege Escalation

এটা একটু **advanced attack**।

প্রথমে attacker **another user এর account access করে (Horizontal)**  
তারপর সেই account যদি **admin হয়**, তাহলে attacker **admin power পেয়ে যায় (Vertical)**।

### Steps

1. **User A → User B account access** (Horizontal)  
2. **User B যদি admin হয় → attacker admin হয়ে যায়** (Vertical)

তাই একে বলে **Horizontal to Vertical Privilege Escalation**।

# TASK 1

![](images/ACV.png)
![](images/ACV1.png)
![](images/ACV2.png)

```Use robots.txt ```

![](images/ACV3.png)<br><br>

![](images/ACV4.png)<br><br>
![](images/ACV5.png)<br><br>
![](images/ACV6.png)<br><br>

```Delete user carlos ``` <br>
`(DONE)`
<br><br><br><br>

# TASK 2
![](images/ACV7.png)<br><br>

`Given: Unpredictable location` <br>
`try normally`
![](images/ACV8.png)<br><br>
![](images/ACV9.png)<br><br>

`-->GO to View Page Source`
![](images/ACV10.png)<br><br><br><br>
![](images/ACV11.png)<br><br>
```Delete user carlos ``` <br>
`(DONE)`

<br><br><br><br>

# Task 3
![](images/ACV12.png)<br><br>
![](images/ACV13.png)<br><br>
![](images/ACV14.png)<br><br>
![](images/ACV15.png)<br><br>
![](images/ACV16.png)<br><br>
<br>
`Go to Repeater`<br>
<br>
![](images/ACV17.png)<br><br>
![](images/ACV18.png)<br><br>
<br>

`test ok`<br>
`Now,`<br>
`First copy the cookie line.` <br>
`Go to Proxy --> Match and replace--> Add`<br>
`Set Admin = true `
`paste cookie line on Original request secition`

<br>

![](images/ACV19.png)<br><br>
![](images/ACV20.png)<br><br>
![](images/ACV21.png)<br><br>
```Delete user carlos ``` <br>
`(DONE)`

<br><br><br><br>

# Task 4
![](images/ACV22.png)<br><br>
```Only accessable with roleid:2 ``` <br>
![](images/ACV23.png)<br><br>
![](images/ACV24.png)<br><br>
![](images/ACV25.png)<br><br>
![](images/ACV26.png)<br><br>
```This users roleid is 1``` <br>
![](images/ACV27.png)<br><br>
```Replace the roleid by 2 in json  ``` <br>
![](images/ACV28.png)<br><br>
`refresh the browser`
![](images/ACV29.png)<br><br>
![](images/ACV30.png)<br><br>
```Delete user carlos ``` <br>
`(DONE)`

<br><br><br><br>

# Task 5
![](images/ACV31.png)<br><br>
`AFTER login`
![](images/ACV32.png)<br><br>
![](images/ACV33.png)<br><br>
`here we see wiener API key`<br>
`Now change the parameter`
![](images/ACV34.png)<br><br>
`Got it`
![](images/ACV35.png)<br><br>
![](images/ACV36.png)<br><br>
```Submit carlos API ``` <br>
`(DONE)`

<br><br><br><br>

## 🔑 GUID / UUID

**UUID (Universally Unique Identifier)** এবং  
**GUID (Globally Unique Identifier)** হলো **128-bit unique ID**। এখানে মোট 32টি hexadecimal character থাকে এবং সাধারণত 5টি অংশে ভাগ করা থাকে।

এগুলো **database বা system-এ user, file, transaction, object uniquely identify** করতে ব্যবহার করা হয়।

**GUID** মূলত **Microsoft এর ব্যবহার করা UUID implementation**।

### Example
`550e8400-e29b-41d4-a716-446655440000`

**👨‍💻 Developerরা কেন ব্যবহার করে**
- ID অনেক **random ও বড়**
- তাই **attacker guess করতে পারবে না**
- ফলে **data secure থাকবে**
### Example URL
`site.com/api/user/550e8400-e29b-41d4-a716-446655440000`<br>

কিন্তু গুরুত্বপূর্ণ বিষয় হলো:

⚠️ **UUID** নিজে কোনো security mechanism না। শুধু **UUID** ব্যবহার করলে access control নিশ্চিত হয় না।

## 🕵️ Attacker কীভাবে Attack করতে পারে

যদি **server proper access control check না করে**, তাহলে attacker:

1️⃣ অন্য **UUID ব্যবহার করে request পাঠাতে পারে**  
2️⃣ **API response থেকে অন্য UUID collect করতে পারে**  
3️⃣ **Burp Suite বা অন্য tool দিয়ে request modify করতে পারে**


<br><br><br><br>

# Task 6
(horizontal privilege escalation)
![](images/ACV37.png)<br><br>
![](images/ACV38.png)<br><br>
![](images/ACV39.png)<br><br>
`After login`
![](images/acv40.png)<br><br>
`Here use GUID. So ager problem er moto id = carlos kore dile API key pabo na.`<br>
![](images/ACV41.png)<br><br>
`Dorking kora lagbe. Home e giye khuje ber korlam je beta carlos kicu post kore rakhse. Kochi kore carlos name er upor click kore dilam. Peye gelam carlos er GUID. ekhon oita niye My account e giye id=GUID ta dilei API key peye jabo. `
![](images/ACV42.png)<br><br>
`copy the GUID`
![](images/ACV43.png)<br><br>
![](images/ACV44.png)<br><br>
![](images/ACV45.png)<br><br>
```Submit carlos API ``` <br>
`(DONE)`

<br><br><br><br>

# Task 7
![](images/ACV46.png)<br><br>
![](images/ACV52.png)<br><br>
`Task 5 er moto id = carlos diye try kore dekhlam hoilo na. Ekta jhamela pakano hoise. Developer code er moddhe ektu karshaji korse...jodi kew onno id use kore try korte chay tahole abar take Login Page e redirect kore daw. Kintu ei kaj ta Burpsuit diye kora jay`
- `burpsuit e giye check dilam. Repeater e pathay dilam`
![](images/ACV47.png)<br><br>
`id = carlos korlam`
![](images/ACV48.png)<br><br>
`Api key peye gechi!!!`
![](images/ACV49.png)<br><br>
 `html code theke khuje nilam API key ta`
![](images/ACV50.png)<br><br>
![](images/ACV51.png)<br><br>
```Submit carlos API ``` <br>
`(DONE)`

