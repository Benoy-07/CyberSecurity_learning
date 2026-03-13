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

<br><br><br><br>

## 🔎 Masking কী?

Data Masking হলো একটি technique যেখানে sensitive information আংশিকভাবে hide করা হয়, কিন্তু data-এর structure বা কিছু অংশ visible রাখা হয়। 🔐

এর উদ্দেশ্য হলো data protect করা, কিন্তু একই সাথে user যেন data চিনতে পারে।<br>

Example:<br>

- `Original: 1234 5678 9012 3456`<br>
`Masked: **** **** **** 3456`
- password mask
### Developer কীভাবে Masking ব্যবহার করে

Developerরা sensitive data protect করার জন্য **data masking implement করে**।

তারা সাধারণত:

- Sensitive data এর কিছু অংশ **hide করে**  
- শুধু **শেষের কিছু digit বা character দেখায়**  
- UI বা API response এ **masked value return করে**

### 🕵️ Attacker কী করার চেষ্টা করে

যদি system এ **proper security না থাকে**, attacker কিছু জিনিস চেষ্টা করতে পারে:

 **API response inspect করা**

অনেক সময় UI তে data masked থাকে,  
কিন্তু API response এ **full data পাঠানো হয়**।

Example API response:

`{`
`"cardNumber": "1234567890123456"`
`}`


UI তে দেখা যায়:

`**** **** **** 3456`

# Task 8
![](images/ACV53.png)<br><br>
`After login`
![](images/ACV54.png)<br><br>
`Password UI তে mask করা। কিন্তু inspect করে দেখলাম যে password দেখা যাচ্ছে। তাহলে কোনোভাবে administrator এ যাইতে পারলে ঔটা inspect করে ঔ password টাও পাইতে পারি`
![](images/ACV55.png)<br><br>
`administrator দিলাম`
![](images/ACV56.png)<br><br>
`হয়ে গেছে!!!!`<br>
![](images/ACV57.png)<br><br>
`inspect করে administrator এর password টা পেয়ে গেলাম।`
![](images/ACV58.png)<br><br>
` Administrator এর id password দিয়ে login করলাম`<br>
![](images/ACV59.png)<br><br>
`Go to admin pannel`<br>
![](images/ACV60.png)<br><br>
![](images/ACV61.png)<br><br>
```Delete user carlos ``` <br>
`(DONE)`


<br><br><br><br>
## Insecure Direct Object References (IDOR)

**IDOR** তখন হয় যখন application **direct object ID ব্যবহার করে data access দেয়**, কিন্তু check করে না user এর **permission আছে কিনা**।

### Example
`site.com/account?id=123`

User যদি `123` change করে `124` দেয়:<br>
`site.com/account?id=124`<br>
<br>
➡️ এতে যদি **অন্য user এর account data দেখা যায়**, তাহলে সেটা **IDOR vulnerability**।<br>

👉 কারণ server check করছে না user এই data access করতে পারবে কিনা।

## Direct Reference to Static Files

কখনো **sensitive file direct URL দিয়ে access করা যায়**।

### Example
`site.com/static/users/report.pdf` or `site.com/private/contract.pdf`


➡️ যদি **authentication ছাড়া download করা যায়**, তাহলে এটা **access control vulnerability**।

---

## Vulnerabilities in Multi-Step Process

কিছু action **multiple step এ হয়**, কিন্তু server সব step **properly verify করে না**।

### Example

Online purchase flow:

1. Add to cart  
2. Payment  
3. Confirm order  

যদি attacker **step skip করে সরাসরি confirm request পাঠায়**, তাহলে **payment ছাড়া order complete হতে পারে**।

👉 এটাকে বলে **multi-step process vulnerability**।

---

## Vulnerabilities in Referrer-Based Control

কিছু website **HTTP Referrer header দেখে access control করে**।

### Example
`Referer: site.com/admin`

Server ভাবে request **admin page থেকে এসেছে**।

কিন্তু attacker সহজেই **referrer change করতে পারে**।

👉 Tool ব্যবহার করে **fake referrer পাঠানো যায়**।

তাই এটা **secure method না**।

---

## Vulnerabilities in Location-Based Control

কিছু website **user location বা IP address দেখে access control করে**।

### Example

Admin page শুধু **office IP থেকে open হবে**।

কিন্তু attacker করতে পারে:

- VPN use
- Proxy use
- IP spoofing (কিছু ক্ষেত্রে)

➡️ তখন attacker **restriction bypass করতে পারে**।


<br><br><br><br>

# Task 9

`IDOR এর problem`
![](images/ACV62.png)<br><br>
![](images/ACV63.png)<br><br>
`Live Chat এ গিয়ে একটু Hi Hello করলাম। তারপর view transcript এ  ক্লিক করলে একটা file download হইলো 2.txt নামে।`<br>

![](images/ACV64.png)<br><br>
`২ দেখে ধারনা করলাম এর ID মনে হয় এইটা। Burpsuit গিয়ে দেখলাম এর object ID 2।`<br>
![](images/ACV65.png)<br><br>
`repeater এ পাঠায় দিলাম।`<br>
![](images/ACV66.png)<br><br>
`এবার ID change করে 1 করলাম। করে দেখি পাসওয়ার্ড পেয়ে গেছি।`<br>
![](images/ACV67.png)<br><br>
`Password দিয়ে carlos login করলাম`<br>
![](images/ACV68.png)<br><br>
`(solved)`


<br><br><br><br>

### URL-based access control bypass

Problem ta ki---<br>
ওয়েবসাইটে একটা admin panel আছে: /admin<br>

কিন্তু normal user browser দিয়ে গেলে access পাবে না, কারণ front-end system (proxy / load balancer / WAF) external request block করে দেয়।<br>

মানে তুমি যদি যাও: `https://target.com/admin` <br>
তাহলে response হবে: `403 Forbidden` <br>

কিন্তু problem হচ্ছে:<br>

➡️ Back-end framework X-Original-URL header support করে।<br>

এটা attacker use করে restriction bypass করতে পারে।<br>

X-Original-URL হলো একটা special HTTP header। এটা back-end কে বলে: `Actually request ta kon URL er jonno chilo`

- Example

`GET /admin HTTP/1.1`<br>
`Host: vulnerable-website.com`<br>

Front-end দেখবে: /admin। তাই block করবে।<br>

### Request modify করো, Header add করো:--<br>

`GET / HTTP/1.1` <br>
`Host: vulnerable-website.com`<br>
`X-Original-URL: /admin`<br>

Front-end দেখবে: `Path = /` <br>
তাই block করবে না।<br>

কিন্তু back-end দেখবে:<br>

`X-Original-URL: /admin`

তখন সে মনে করবে: <br>

user /admin access korte chacche এবং admin panel return করে দিবে।
<br><br><br><br>

# Task 10

![](images/ACV69.png)<br><br>
![](images/ACV70.png)<br><br>
`Admin pannel এ যাওয়ার চেষ্টা করলাম access denied দেখাইলো`<br><br>
![](images/ACV71.png)<br><br>
`Burpsuit এ যাই`<br>
![](images/ACV72.png)<br><br>
`Normally একবার দেখলাম।  কাজ হইলো না। Front end থেকে admin পেলে block করে দিচ্ছে। X-Original-Url: /admin দেই আর GET এ শুধু /।  `
`এখন Front end "/" পেয়ে block করবে না। আর X-Original-Url backend  `
`এ কাজ করবে এবং end point change করে দিবে। কাজ শেষ!!!`<br>
![](images/ACV73.png)<br><br>
`এবার carlos user delete করতে হবে। তো request line parameters দিয়ে দিলাম। যেহেতু এটি normal হোমপেজ request block করবে না। main কাজ করবে তো X-Original-Url। ``backend কে বলবে /admin/delete তে যাও। `
`Bypass done`<br>
![](images/ACV74.png)<br><br>
`(Solved)`

<br><br><br><br>

# Task 11
`administrator login করে carlos কে admin access দিলাম`<br>
`এখন কাজ হলো wiener কে admin access দিতে হবে`<br>
`এর জন্য wiener এর session ID বসিয়ে try করে দেখলাম হইলো না`<br>
`block করা`<br>
`Post er bodole get request দিলে হয়ে গেলো`<br>
![](images/ACV91.png)<br><br>
![](images/ACV92.png)<br><br>
![](images/ACV93.png)<br><br>
![](images/ACV94.png)<br><br>
![](images/ACV95.png)<br><br>


<br><br><br><br>

# Task 12
`Multi step process user  এর role change করার জন্য। এখানে দুইটা স্টেপ।  একটায় upgrade user করে। অন্য ধাপে confirmation হয় ঔটার।`<br>
![](images/ACV75.png)<br><br>
![](images/ACV76.png)<br><br>
`Admin login. Give carlos admin access`<br>
![](images/ACV77.png)<br><br>
![](images/ACV78.png)<br><br>
`Burpsuit এ দেখলাম দুইটা reponse`<br>
![](images/ACV79.png)<br><br>
![](images/ACV80.png)<br><br>
`Repeater e gelam. আমাদের কাজ হলো wiener কে admin এর access দেওয়া। তো এখানে আমরা যদি carlos এর session ID টা replace করে wiener করে দিতে পারি তাহলে কাজ হতে পারে।`<br>
![](images/ACV81.png)<br><br>
`wiener login করলাম`
![](images/ACV82.png)<br><br>
`Burpsuit থেকে wiener এর session ID copy করলাম।`<br>
![](images/ACV83.png)<br><br><br>
`session ID বসিয়ে দেখলাম হয়ে গেছে`<br>
![](images/ACV84.png)<br><br>
`(Done)`


<br><br><br><br>

# Task 13
`Referer based problem...এখানে server referer চেক করে`<br>
![](images/ACV85.png)<br><br><br>
`আগেরটার মতোই admin এ লাগইন করে carlos কে admin দিলাম`<br>
`এখন আমার wiener কে admin বানাতে হবে`<br>
![](images/ACV86.png)<br><br>
![](images/ACV87.png)<br><br>
![](images/ACV88.png)<br><br>
`wiener এর session id নিয়ে চেঞ্জ করে দিলেই কাজ শেষ..`<br>
![](images/ACV89.png)<br><br>
`(SOLVED)`<br>
`
`এই problem ta easily solve হয়ে গেছে যদিও। কিন্তু এখানে referer check করে। যদি /admin হয় তাহলে server access দেয়। কিন্তু যেই হ্যাকার cookies change করতে পারে, সে ``এইটা চেঞ্জ করতে পারবে না!!!`
`এমন ডেভেলপার হওয়ার চেয়ে না হওয়া ভালো।`<br>
![](images/ACV90.png)<br><br>





