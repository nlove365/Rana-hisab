রানা হিসাব — আপডেটেড প্রজেক্ট প্যাকেজ

এই ZIP-এ আছে:
- PWA ওয়েব অ্যাপ (index.html, manifest, service worker, icon)
- Android Studio WebView প্রজেক্ট
- GitHub Actions workflow দিয়ে debug APK তৈরির কনফিগারেশন

মূল সুবিধা: আয়-ব্যয় এন্ট্রি, ড্যাশবোর্ড, পণ্য/একক তালিকা, লেনদেন তালিকা, বাংলা স্মার্ট কমান্ড, ব্রাউজার-সমর্থিত ভয়েস ইনপুট, ছবি থেকে OCR (Tesseract.js CDN প্রয়োজন), JSON ব্যাকআপ/রিস্টোর।

PWA ব্যবহার: HTTPS ওয়েব হোস্টিংয়ে Rana-Hisab-PWA ফোল্ডার প্রকাশ করে Android Chrome থেকে Install app নির্বাচন করুন। শুধু ZIP খুলে PWA ইনস্টল হবে না।

Android APK: Android প্রজেক্টটি GitHub-এ push করে Actions workflow চালালে app-debug.apk artifact তৈরি হওয়ার কথা। এই পরিবেশে Android SDK নেই, তাই APK এখানে build/পরীক্ষা করা হয়নি। GitHub repository-তে upload-ও করা হয়নি।

সীমাবদ্ধতা: ডেটা বর্তমানে একই ডিভাইসের browser localStorage-এ থাকে। নিয়মিত JSON backup নিন। Cloud sync, login/roles ও পূর্ণ POS backend এখনো যুক্ত হয়নি। ভয়েস ইনপুট ডিভাইস/ব্রাউজারভেদে ভিন্ন হতে পারে; OCR-এর জন্য প্রথমবার internet লাগে।


কপিরাইট ও মালিকানা:
© 2026 স্বপ্নময় ইনক বিডি। রানা হিসাব সফটওয়্যারটি স্বপ্নময় ইনক বিডি-এর মালিকানাধীন, যা স্বপ্নময় গ্রুপের একটি প্রতিষ্ঠান। সর্বস্বত্ব সংরক্ষিত।
