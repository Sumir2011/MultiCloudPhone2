# Multi Cloud Phone – Starter (২টি ডিভাইস)

এটি Android অ্যাপের **starter project**, সম্পূর্ণ cloud Android service নয়। এতে দুটি ডিভাইসের dashboard, API connection setting এবং Start/Stop/Restart action-এর প্রাথমিক UI আছে। সত্যিকারের ভার্চুয়াল Android চালাতে আলাদা Linux cloud server, KVM/সমর্থিত virtualization এবং backend লাগবে।

## শুধু Android মোবাইল দিয়ে APK build

1. GitHub-এ account খুলুন এবং নতুন public/private repository তৈরি করুন।
2. এই ZIP-এর ফাইলগুলো repository-তে upload করুন (GitHub mobile app বা Chrome-এর Desktop site)।
3. `.github/workflows/build-apk.yml` ফাইলটি-সহ commit করুন।
4. GitHub repository → Actions → **Build Android APK** → Run workflow.
5. Build শেষ হলে workflow run খুলুন → Artifacts → `MultiCloudPhone-debug-apk` ডাউনলোড করুন।
6. ZIP extract করে `app-debug.apk` Android ফোনে install করুন। Unknown apps install permission দিতে হতে পারে।

## API server
অ্যাপের Settings-এ আপনার backend-এর HTTPS base URL দিন, যেমন `https://your-domain.example`। এটি উদাহরণ; বাস্তব server URL নিজে deploy না করা পর্যন্ত কাজ করবে না।

Backend API:
- `GET /api/devices`
- `POST /api/devices/{id}/start`
- `POST /api/devices/{id}/stop`
- `POST /api/devices/{id}/restart`

প্রত্যাশিত device JSON:
```json
[
  {"id":"phone-1","name":"Cloud Phone 1","status":"stopped"},
  {"id":"phone-2","name":"Cloud Phone 2","status":"stopped"}
]
```

## গুরুত্বপূর্ণ সীমাবদ্ধতা
- এই starter-এ cloud Android image, streaming, authentication, persistent virtual device storage বা APK installation server-side implementation নেই।
- শুধু dashboard APK তৈরি হবে। Backend ও virtualization আলাদাভাবে তৈরি/deploy/test করতে হবে।
- বিনামূল্যের সার্ভার একসঙ্গে দুটি Android VM চালাতে পারবে—এমন নিশ্চয়তা নেই। KVM/CPU/RAM/স্টোরেজ ও provider policy যাচাই করুন।
- কোনো cloud quota বা provider restriction bypass করবেন না।
