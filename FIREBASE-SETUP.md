# 🔥 Firebase Setup Guide — دليل إعداد Firebase

## خطوات الإعداد (5 دقائق)

### 1. إنشاء مشروع Firebase
1. افتح https://console.firebase.google.com
2. اضغط **Create a project** أو **إنشاء مشروع**
3. سمّه **learntrack** واضغط Continue
4. أوقف Google Analytics (مو ضروري) واضغط **Create project**

### 2. تفعيل تسجيل الدخول بـ Google
1. من القائمة الجانبية اختر **Authentication**
2. اضغط **Get started**
3. اضغط على **Google** من قائمة Sign-in providers
4. فعّله (Enable) واختر إيميلك كـ Project support email
5. اضغط **Save**

### 3. إنشاء قاعدة بيانات Firestore
1. من القائمة الجانبية اختر **Firestore Database**
2. اضغط **Create database**
3. اختر **Start in test mode** (نسوي الحماية لاحقاً)
4. اختر أقرب موقع (مثلاً europe-west1) واضغط **Enable**

### 4. نسخ مفاتيح الربط
1. اضغط على ⚙️ Settings بجانب Project Overview
2. اضغط **Project settings**
3. انزل لقسم **Your apps** واضغط **</>** (Web)
4. سمّه **learntrack** واضغط **Register app**
5. بيظهر لك كود فيه `firebaseConfig` — انسخ القيم الستة
6. افتح ملف `index.html` وبدّل القيم في أول الملف

### 5. تأمين قاعدة البيانات
بعد ما يشتغل كل شي، روح Firestore → Rules وبدّل القواعد بهذي:
```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId} {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```
هذي تضمن إن كل شخص يشوف بياناته بس.

### 6. إضافة الدومين المسموح
1. في Authentication → Settings → Authorized domains
2. أضف دومين Vercel مالك (مثلاً learntrack-xyz.vercel.app)

---
Done! 🎉
