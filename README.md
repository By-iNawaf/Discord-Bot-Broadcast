# Broadcast Bot — بوت البرودكاست

> **Powered By Nawaf**
>
> Developed by [By-inawaf](https://github.com/By-inawaf) — Copyright © 2026 Nawaf (By-inawaf)

لوحة تحكم **ثابتة** (Discord Components V2) لإرسال الرسائل الجماعية والفردية للأعضاء بالأزرار فقط، مع إحصائيات مباشرة ورسالة **Broadcast Control** ثابتة يوقف منها العضو استقبال البرودكاست نهائيًا. بوت **مستقل تمامًا** — ملف واحد، بلا أي ارتباط بأي بوت أو مشروع آخر.

---

## 📦 محتويات الحزمة (نسخة النشر — مشفّرة)
| الملف | وظيفته |
|---|---|
| `index.js` | الملف الرئيسي، **مشفّر بأقصى مستوى حماية** |
| `package.json` | المكتبات وأمر التشغيل |
| `.env.example` | أسماء المتغيرات |
| `README.md` / `LICENSE` | الشرح والترخيص |

> لا توجد أيقونات ولا ملفات صور ولا أي ملفات إضافية. 5 ملفات فقط.

## ✨ المميزات
- **لوحة إدارة** فيها تعليمات البرودكاست والإحصائيات: من أرسل، كم عضوًا وصلته الرسالة، كم فشلت (الخاص مغلق)، وكم عضوًا أوقف البرودكاست.
- **أربعة أزرار**: إرسال لجميع الأعضاء، إرسال لشخص، مساعدة، وتبديل اللغة (عربي ⇄ English).
- **اختيار شكل الرسالة** لكل برودكاست: إمبيد عادي أو إمبيد V2، وبصيغة «عنوان ووصف» أو «وصف فقط»، مع **معاينة** قبل الإرسال.
- **شكل الرسالة النهائي** يُبنى تلقائيًا: منشن العضو، ثم المحتوى، وبجانبه **شعار ثابت**، ثم رابط الموقع، ثم رابط إيقاف البرودكاست.
- **Broadcast Control**: رسالة إمبيد ثابتة فيها زر **Stop Broadcast** (رمادي). من يضغطه لا تصله أي رسالة جماعية نهائيًا. الرسالة **تُعاد تلقائيًا** إن حُذفت، حتى بعد إطفاء البوت وتشغيله، ولا تتكرر.
- **زر «مساعدة» ثابت** على حساب المطوّر في ديسكورد، لا يتغيّر من أي إعداد أو متغير بيئة، لا في النسخة المشفّرة ولا في النسخة العادية.
- **كل شيء محفوظ**: اللوحة، الرسالة الثابتة، من أوقف البرودكاست، الإحصائيات، واللغة. إرسال جماعي ينقطع يُستأنف من حيث توقف دون تكرار الرسائل.
- ردود الأزرار **مخفية** لصاحب الضغطة. محتوى اللوحة **بدون أي إيموجي أو أيقونات**.

## 📋 المتطلبات
- **Node.js 22.13 أو أحدث** (قاعدة البيانات مدمجة في Node، لا مكتبات native).
- **Server Members Intent** مفعّلة من Developer Portal (لازمة لجلب قائمة الأعضاء عند الإرسال لجميعهم).
- قرص دائم لمجلد `data/`.

## 🚀 التثبيت
### 1) إنشاء البوت
1. [Developer Portal](https://discord.com/developers/applications) ← New Application ← Bot ← انسخ التوكن.
2. فعّل **Server Members Intent** (Privileged Gateway Intents).
3. ادعُ البوت بنطاقَي `bot` + `applications.commands` وصلاحيات: **View Channels** و**Send Messages** و**Embed Links**.

### 2) التشغيل على Pterodactyl
1. أنشئ سيرفرًا بـ **Node.js egg** وصورة **Node 22** أو أحدث، وارفع الملفات الخمسة كما هي.
2. في **Startup** اجعل ملف التشغيل `index.js` (الحزم تُثبَّت من `package.json`، أو نفّذ `npm install` من الكونسول).
3. في **Variables** (أو ملف `.env`) أضف على الأقل:
```env
DISCORD_TOKEN=توكن_البوت
OWNER_ID=معرّفك
```
**استضافات أخرى:** `npm install` ثم `npm start`. للتشغيل الدائم: `npm i -g pm2 && pm2 start index.js --name broadcast && pm2 save`.

### 3) أول استخدام
1. `/setup control channel:#الروم` ← تُرسل رسالة **Broadcast Control** الثابتة (لا يعمل الإرسال قبلها لأن رابط الإيقاف جزء من كل رسالة).
2. `/setup panel channel:#الروم` ← تُرسل لوحة الإدارة.
3. اضغط **إرسال لجميع الأعضاء** أو **إرسال لشخص** واتبع الخطوات.

### المتغيرات
| المتغير | الوصف | الافتراضي |
|---|---|---|
| `DISCORD_TOKEN` | توكن البوت (**مطلوب**) | — |
| `OWNER_ID` | معرّف المالك (**مطلوب**) | — |
| `ADMIN_IDS` | معرّفات أشخاص مسموح لهم باللوحة | — |
| `ADMIN_ROLE_IDS` | معرّفات رتب مسموح لها باللوحة | — |
| `PANEL_CHANNEL_ID` / `CONTROL_CHANNEL_ID` | بديل للأمر `/setup` | — |
| `WEBSITE_URL` | رابط الموقع في كل رسالة | `https://bynawaf.xyz/` |
| `LOGO_URL` | رابط صورة الشعار الثابت (إن تُرك فارغًا يُستخدم avatar البوت) | — |
| `STOP_URL` | رابط إيقاف يدوي (افتراضيًا يُبنى من رسالة Broadcast Control) | — |
| `DM_DELAY_MS` | الفاصل بين كل رسالة خاصة بالمللي ثانية | `1500` |
| `DEFAULT_LANG` | `ar` / `en` | `ar` |
| `DB_PATH` | مكان قاعدة البيانات | `./data/broadcast.sqlite` |

> لا يوجد أي متغير لزر «مساعدة» أو رابط الدعم — هذا مقصود؛ الرابط مثبّت داخل الكود ومحمي، ولا يمكن تغييره حتى من صاحب الاستضافة.

## 🧭 طريقة الإرسال
1. اختر **إرسال لجميع الأعضاء** (أو **لشخص** وحدد العضو من القائمة).
2. اختر **نوع الرسالة** (إمبيد عادي / V2) و**الصيغة** (عنوان ووصف / وصف فقط)، ثم **متابعة**.
3. اكتب العنوان والوصف في النافذة، وراجع **المعاينة**، ثم **تأكيد الإرسال**.

مثال على الشكل النهائي للعضو:
```
@العضو
خصم 50% على البوتات والبكجات + كاش باك 10% لمدة يوم          [شعار ثابت]
موقعنا الإلكتروني
لإيقاف البرودكاست، اضغط هنا
```
- المرسَل إليهم: كل الأعضاء عدا **البوتات** ومن **أوقفوا البرودكاست**.
- لا يُرسل برودكاست جديد وآخر قيد الإرسال؛ التقدم يظهر في إحصائيات اللوحة.
- الإرسال لشخص أوقف البرودكاست يُرفض برسالة واضحة.

## ⚠️ ملاحظات مهمة عن Discord
- الرسائل الخاصة الجماعية قد تعرّض البوت للتقييد إن أُسيء استخدامها. أرسل لمن يتوقع رسائل منك فقط، ولا تُنزل `DM_DELAY_MS` كثيرًا. الإرسال لـ 1000 عضو يستغرق تقريبًا 25 دقيقة بالإعداد الافتراضي.
- من أغلق رسائله الخاصة تُحسب له «فشلت (الخاص مغلق)».

## 🛠️ حل المشاكل
| المشكلة | الحل |
|---|---|
| «يجب تحديد قناة Broadcast Control أولًا» | نفّذ `/setup control` |
| البوت لا يرى الأعضاء / يرسل لعدد قليل | فعّل **Server Members Intent** |
| `Used disallowed intents` | فعّل Server Members Intent من Developer Portal ثم أعد التشغيل |
| الأزرار «انتهت صلاحيتها» | ابدأ الإرسال من اللوحة من جديد (المسودة تنتهي بعد 30 دقيقة) |
| `تم اكتشاف تعديل على حقوق المطوّر` أو `رابط الدعم` | عُدّل أحدهما في الملف؛ أعد تحميل النسخة الأصلية — لا يمكن إصلاحها بالتعديل |

## 📜 Copyright & License

Developed by [By-inawaf](https://github.com/By-inawaf)

Copyright © 2026 Nawaf (By-inawaf). All Rights Reserved.

This bot is free to download, run, and share in unmodified form, provided that the original copyright notices and license are preserved.

### Restrictions

* Selling or reselling this bot without written permission is prohibited.
* Removing or altering original copyright notices or the fixed support button is prohibited.
* Claiming ownership or falsely claiming to be the original developer is prohibited.
* Unauthorized circumvention of encryption or technical protections is prohibited to the extent permitted by law.

### License

This bot is governed by the custom license in [`LICENSE`](LICENSE). Third-party components remain subject to their respective licenses.

**FREE TO USE. FREE TO SHARE. NOT FOR SALE.**

**Discord:** [732540761295421480](https://discord.com/users/732540761295421480) · **GitHub:** [By-inawaf](https://github.com/By-inawaf)

---

## English summary
A persistent Components V2 panel for sending mass or individual DMs by buttons only, with live statistics (who sent, how many received, failed, and how many members stopped broadcasts). Pick **Normal Embed or Embed V2** and **Title & Description or Description only**, preview, then confirm. Every DM carries the member mention, a fixed logo, the website link, and a stop link to the persistent **Broadcast Control** message (with a gray **Stop Broadcast** button); members who press it never receive a broadcast again. The Help button is permanently pinned to the developer's Discord profile and cannot be changed by any setting. Everything is saved and interrupted sends resume. This bot is fully standalone — a single file, unrelated to any other bot or project. Requires **Node.js ≥ 22.13** and the **Server Members Intent**.
