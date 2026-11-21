# রানা হিসাব — বাইরের অনুমতি ও সেটআপ তালিকা
সর্বশেষ হালনাগাদ: ২১ নভেম্বর ২০২৬

এই নথি রানা হিসাব প্রকল্পের সঙ্গে যুক্ত বাহ্যিক অ্যাকাউন্ট, অনুমতি, কনফিগারেশন ও ব্যবহারকারীর কাছ থেকে প্রয়োজনীয় তথ্য এক জায়গায় রাখার জন্য। ভবিষ্যতে কাজ শুরু করার আগে এই তালিকা দেখুন; একই তথ্য বারবার খোঁজার প্রয়োজন হবে না।

## ১. Firebase / ক্লাউড সিঙ্ক / অনলাইন লগইন
**কেন লাগবে:** একাধিক ডিভাইসে তথ্য সিঙ্ক, অনলাইন ব্যাকআপ, ব্যবহারকারী লগইন ও ভূমিকা/অনুমতি।

**ব্যবহারকারীর কাছ থেকে প্রয়োজন হবে**
- Google অ্যাকাউন্ট দিয়ে Firebase Console-এ প্রবেশের অনুমতি/ব্যবস্থা।
- নতুন Firebase project তৈরির অনুমোদন এবং প্রকল্পের নাম পছন্দ।
- Firebase Authentication-এ কোন লগইন পদ্ধতি চালু হবে তা অনুমোদন (প্রস্তাব: Email/Password; পরে Google sign-in চাইলে আলাদা OAuth সেটআপ)।
- Firestore database তৈরি ও অঞ্চল নির্বাচন অনুমোদন।
- মালিক/প্রশাসকের জন্য নির্ধারিত ইমেইল ঠিকানা।
- প্রাইভেসি নীতি ও ডেটা সংরক্ষণ বিষয়ে সম্মতি।

**প্রকল্প থেকে সংগ্রহ/সেট করতে হবে**
- Firebase project ID এবং Web App configuration: apiKey, authDomain, projectId, appId, messagingSenderId, storageBucket (যদি Storage ব্যবহৃত হয়)।
- Firestore security rules; ব্যবহারকারীভিত্তিক ডেটা আলাদা রাখা এবং admin/user role যাচাই।
- Authentication provider enable করা।
- Offline persistence ও sync conflict handling পরীক্ষা।

**নিরাপত্তা:** Firebase web config সাধারণত অ্যাপের ক্লায়েন্টে থাকে, কিন্তু Service Account private key, Admin SDK key, GitHub secret বা অন্য গোপন credential কখনো APK/HTML-এ বসানো যাবে না। প্রয়োজন হলে GitHub Actions Secrets বা নিরাপদ backend-এ রাখতে হবে।

**অবস্থা:** এখনো Firebase project ID/config, Authentication, Firestore rules বা admin email সরবরাহ/নিশ্চিত হয়নি।

## ২. Google Play Console / Play Store-এ প্রকাশ ও অ্যাপ আপডেট
**কেন লাগবে:** Play Store দিয়ে বৈধভাবে অ্যাপ প্রকাশ এবং Play In-App Updates দিয়ে ব্যবহারকারীকে নতুন সংস্করণে আপডেট করানো। Android অ্যাপ সাধারণত ব্যবহারকারীর সম্মতি ছাড়া নীরবে নিজে APK ইনস্টল করতে পারে না।

**ব্যবহারকারীর কাছ থেকে প্রয়োজন হবে**
- Google Play Console Developer account তৈরি/প্রবেশাধিকার।
- Google-এর পরিচয় ও ডেভেলপার যাচাই সম্পন্ন করা।
- প্রযোজ্য ডেভেলপার নিবন্ধন ফি প্রদান (Google-এর বর্তমান শর্ত অনুযায়ী)।
- অ্যাপ প্রকাশের শর্ত, Data Safety, Content Rating, Privacy Policy ও Store Listing অনুমোদন।
- অ্যাপের নাম, বিবরণ, স্ক্রিনশট, আইকন এবং যোগাযোগের ইমেইল অনুমোদন।
- চূড়ান্ত package/application ID এবং release signing ownership নিশ্চিত করা।

**প্রকল্প থেকে করতে হবে**
- Release signing key নিরাপদে তৈরি/সংরক্ষণ; keystore ও password কেবল নিরাপদ জায়গায় রাখা।
- Play Console-এ Android App Bundle (AAB) আপলোড, internal testing, review এবং production release।
- Play In-App Updates API সংযুক্ত ও পরীক্ষা (Flexible/Immediate flow)।
- প্রতিটি release-এ versionCode/versionName বাড়ানো।

**অবস্থা:** Play Console account, developer verification, payment, privacy policy URL ও Play release setup এখনো নিশ্চিত/সরবরাহ হয়নি। GitHub Actions-এর debug APK build Play Store release-এর বিকল্প নয়।

## ৩. Android নেটিভ নোটিফিকেশন / অ্যাপ বন্ধ থাকলেও রিমাইন্ডার
**কেন লাগবে:** অ্যাপ বন্ধ বা ব্যাকগ্রাউন্ডে থাকলেও নির্ধারিত সময়ে নির্ভরযোগ্য সতর্কবার্তা।

**ব্যবহারকারীর অনুমতি/পদক্ষেপ**
- ফোনে Android 13 বা পরবর্তী সংস্করণে notification permission চাইলে অনুমতি দেওয়া।
- প্রয়োজনীয় battery/background restriction পরীক্ষার সময় অনুমোদন/সেটিংস ঠিক রাখা।

**প্রকল্প থেকে করতে হবে**
- Android notification channel ও POST_NOTIFICATIONS permission যোগ।
- নির্ধারিত কাজের জন্য AlarmManager/WorkManager উপযুক্তভাবে সংযুক্ত; সঠিক সময়ের জন্য Android-এর exact alarm নীতিমালা যাচাই।
- reboot-এর পর reminder পুনরায় schedule এবং notification tap করলে সংশ্লিষ্ট কাজ খোলা।
- Android 13+ এবং বিভিন্ন ফোনে পরীক্ষা।

**ঐচ্ছিক:** Firebase Cloud Messaging (FCM) দিয়ে সার্ভার-প্রেরিত push notification চাইলে Firebase project ও FCM configuration লাগবে; শুধু ফোনে স্থানীয় reminder-এর জন্য FCM বাধ্যতামূলক নয়।

**অবস্থা:** বর্তমানে অ্যাপ খোলা থাকলে foreground reminder আছে; অ্যাপ বন্ধ থাকলে নির্ভরযোগ্য native reminder এখনো সম্পন্ন নয়।

## ৪. ক্যামেরা / বারকোড / OCR
**কেন লাগবে:** ক্যামেরা দিয়ে বারকোড স্ক্যান এবং ছবি থেকে পণ্যের/রসিদের লেখা পড়া।

**ব্যবহারকারীর অনুমতি**
- ফোনে Camera permission।
- ছবি/ফাইল বাছাইয়ের সময় Android Photo Picker/ফাইল অ্যাক্সেস অনুমতি, যেখানে প্রযোজ্য।

**প্রকল্প থেকে করতে হবে**
- Android Manifest ও runtime camera permission।
- বারকোডের জন্য on-device ML Kit Barcode Scanning বা সমমানের লাইব্রেরি।
- OCR-এর জন্য on-device ML Kit Text Recognition বা সমমানের ইঞ্জিন; বাংলা ভাষা সমর্থন ও মডেল ডাউনলোড/অফলাইন আচরণ যাচাই।
- ক্যামেরা preview, focus, scan result ও low-light পরীক্ষা।

**বাহ্যিক অ্যাকাউন্ট:** on-device ML Kit ব্যবহার করলে সাধারণত আলাদা API key/account প্রয়োজন হয় না। Cloud OCR বেছে নিলে provider account, API key, billing ও privacy approval লাগবে—এখনো কোনো provider নির্বাচন করা হয়নি।

**অবস্থা:** ক্যামেরা/OCR/বারকোডের বাস্তব ফোন পরীক্ষা বাকি; সব ডিভাইসে কাজ করে বলে নিশ্চিত নয়।

## ৫. AI Help Center-কে সত্যিকারের অনলাইন AI করা (ঐচ্ছিক)
**কেন লাগবে:** বর্তমানে Help Center অফলাইন নির্দেশনা; AI সার্ভারের সঙ্গে যুক্ত নয়।

**ব্যবহারকারীর অনুমতি/সিদ্ধান্ত**
- কোন AI provider ব্যবহার হবে এবং সম্ভাব্য মাসিক খরচের সীমা অনুমোদন।
- কোন তথ্য AI-তে পাঠানো যাবে/যাবে না সে বিষয়ে privacy consent।

**প্রকল্প থেকে করতে হবে**
- নিরাপদ backend/proxy তৈরি; API key কখনো APK বা client-side JavaScript-এ রাখা যাবে না।
- rate limit, user authentication, logging minimization ও খরচ নিয়ন্ত্রণ।
- বাংলা প্রশ্নোত্তর ও ভুল উত্তরের সতর্কতা পরীক্ষা।

**অবস্থা:** কোনো AI provider, account, API key বা backend এখনো দেওয়া/নির্বাচন করা হয়নি। ব্যবহারকারীর স্পষ্ট অনুমোদন ছাড়া paid API চালু করা হবে না।

## ৬. সরকারি ছুটির লাইভ তথ্য (ঐচ্ছিক)
**কেন লাগবে:** সরকারি ছুটির তারিখ স্বয়ংক্রিয়ভাবে হালনাগাদ করা।

**প্রয়োজন:** নির্ভরযোগ্য সরকারি তথ্যসূত্র/API নির্বাচন; API থাকলে access terms/key ও ব্যবহারের অনুমতি। API না থাকলে নির্ভরযোগ্য সরকারি প্রজ্ঞাপন দেখে ম্যানুয়াল ডেটা আপডেট।

**অবস্থা:** বর্তমান ছুটির তালিকা live government feed নয়; ভবিষ্যৎ বছরের তথ্য যাচাই ও আপডেট প্রয়োজন।

## ৭. বাস্তব ফোনে ব্যবহারকারী-পরীক্ষা
এটি কোনো বাইরের developer account নয়, তবে ব্যবহারকারীর সহযোগিতা লাগবে:
- Android ফোনের মডেল ও Android version জানানো।
- পরীক্ষার APK ইনস্টল করে POS বিক্রি/বাতিল, stock, backup/export, restore/import, offline/online sync ও notification পরীক্ষা।
- প্রয়োজন হলে screenshot/error text পাঠানো।
- বাস্তব ব্যবসার সংবেদনশীল তথ্য না দিয়ে sample data দিয়ে পরীক্ষা।

## ৮. ইতিমধ্যে থাকা / এখনই পুনরায় চাইতে হবে না
- GitHub repository: https://github.com/nlove365/Rana-hisab
- Repository: `nlove365/Rana-hisab`, branch: `main`
- GitHub Actions দিয়ে debug APK build workflow আছে।
- সাম্প্রতিক Build 78 সফল হয়েছিল; Build 82-তে task/reminder code ও build checks যোগ করার পর নতুন build চালু হয়েছিল। Build status আলাদাভাবে যাচাই করতে হবে।
- GitHub repo access/workflow permission আগে থেকেই ব্যবহৃত হচ্ছে; কোনো নতুন GitHub permission চাইতে হবে কি না তা প্রয়োজন হলে নির্দিষ্ট error দেখে ঠিক করা হবে।

## ৯. পরে ব্যবহারকারীর কাছ থেকে একবারে যেসব বিষয় নিশ্চিত করতে হবে
1. Firebase project তৈরি ও cloud sync চালুর অনুমতি; Firebase project-এর নাম।
2. Admin account হিসেবে ব্যবহার করার ইমেইল।
3. Login method: Email/Password যথেষ্ট কি না।
4. Google Play Console account আছে কি না; না থাকলে ব্যবহারকারী নিজে account/verification/fee সম্পন্ন করবেন কি না।
5. Play Store-এ অ্যাপ প্রকাশের জন্য privacy policy/contact email ও store listing অনুমোদন।
6. AI Help Center-এ paid API চান কি না এবং খরচের সীমা।
7. Cloud OCR দরকার কি না, নাকি প্রথমে offline/on-device OCR যথেষ্ট।
8. Live holiday API-এর বদলে যাচাইকৃত ম্যানুয়াল সরকারি ছুটির তালিকা গ্রহণযোগ্য কি না।

**গুরুত্বপূর্ণ:** কোনো password, private key, recovery code বা payment card তথ্য চ্যাটে পাঠাবেন না। প্রয়োজন হলে নিরাপদ Google/GitHub console-এ নিজে প্রবেশ করে অনুমতি দিন বা secret manager ব্যবহার করুন। অনুমতি/অ্যাকাউন্ট না পাওয়া পর্যন্ত সংশ্লিষ্ট ফিচারকে “বাকি” হিসেবেই চিহ্নিত রাখতে হবে; সম্পন্ন বলে দাবি করা যাবে না।
