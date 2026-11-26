# SHAHIN APP — Abrar Trading Corporation

এটি নতুন করে তৈরি করা মোবাইল-ফার্স্ট ওয়েব অ্যাপের **Preview/Starter Release**। পুরোনো অ্যাপের ডেটা বা হিসাব এতে আনা হয়নি।

## কীভাবে চালু করবেন

1. ZIP Extract করুন। `index.html`, `app.js`, `style.css`, `api/`, `sql/` যেন Repository-র Root-এ থাকে।
2. GitHub-এ সব ফাইল Root-এ Upload করে Commit করুন।
3. Vercel-এ ওই Repository Import/Connect করুন। Framework Preset: Other; Build Command ফাঁকা বা `npm run build`; Output Directory ফাঁকা/Root; Install Command `npm install`।
4. Deploy শেষে Vercel-এর Visit দিয়ে খুলুন।

## Preview-তে বর্তমানে যা কাজ করে

- বাংলা responsive dashboard এবং bottom navigation
- Product, Shop, Stock (Central/Vehicle/General) local entry
- DSR Sales, Cash Deposit, Damage entry
- ৭-লাইন DSR statement: Gross, Damage, Net, Cash, Today Due, Previous Due, Total Due
- Print/PDF এবং CSV Export
- Company Challan manual entry
- AI Scanner API endpoint (Gemini key থাকলে), review ও confirm UI
- AI Support API endpoint (Gemini key থাকলে)
- Role switch UI (শুধু Preview demonstration)
- Local browser storage persistence

## AI চালু করতে

Vercel → Project → Settings → Environment Variables-এ `GEMINI_API_KEY` যোগ করুন, তারপর Redeploy করুন। API key কখনো `app.js` বা public HTML-এ রাখবেন না।

## গুরুত্বপূর্ণ সীমাবদ্ধতা — Production-এর আগে আবশ্যক

- এই Release-এর operational data browser-এর Local Storage-এ থাকে; অন্য ডিভাইসে Sync হয় না।
- Role selector কেবল UI Preview; এটি নিরাপদ Authentication/Authorization নয়। বাস্তব ব্যবহারকারীর জন্য Supabase Auth, business membership ও কঠোর role-based RLS integration করতে হবে।
- AI Support কেবল browser থেকে পাঠানো summary context দেখে; এটি সরাসরি নিরাপদ Database query করে না। তাই এটিকে হিসাবের authoritative source হিসেবে ব্যবহার করবেন না।
- Scanner API AI-তে ছবি পাঠায়; Confirm করার আগে review দরকার। Duplicate challan check এবং transactional stock posting production-এ যোগ করতে হবে।
- Sales/returns/damage/stock transfer-এর সম্পূর্ণ atomic business workflow, nested packaging conversion, ticket persistence, notification, multi-device conflict handling ও production-grade audit workflow এখনো সম্পূর্ণ নয়।
- SQL হলো নতুন Supabase project-এর schema foundation; এটি production-ready role matrix-এর বিকল্প নয়। SQL-এ দেওয়া RLS membership-ভিত্তিক প্রাথমিক নীতি; DSR/Manager-এর সূক্ষ্ম row-level সীমা deploy করার আগে যোগ ও পরীক্ষা করতে হবে।

**এই ZIP-কে Production-ready হিসাব সফটওয়্যার ধরে বাস্তব টাকা/স্টক পরিচালনা করবেন না, যতক্ষণ না উপরের Backend/Auth/Stock workflow সম্পূর্ণ ও পরীক্ষা করা হয়।**

## নতুন Supabase project

শুধুমাত্র নতুন Supabase project-এ `sql/001_schema.sql` চালান। পুরোনো Project-এ চালাবেন না। Supabase `service_role` key কখনো Frontend বা GitHub-এ দেবেন না।
