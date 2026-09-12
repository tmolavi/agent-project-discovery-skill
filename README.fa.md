# مهارت کشف و شناخت پروژه برای ایجنت‌های هوش مصنوعی 🧭
### `agent-project-discovery-skill`

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v1.1.0-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/tmolavi/agent-project-discovery-skill/pulls)

> **«یک ایجنت هوش مصنوعی باید قبل از اعمال تغییرات، پروژه را عمیقاً درک کند.»**

این پروژه یک مهارت استارتاپی جامع، استاندارد و آماده برای دستیاران و ایجنت‌های کدنویسی هوش مصنوعی (نظیر Claude Code، Cursor، Google Antigravity، OpenAI Codex، GitHub Copilot و ...) است. این مهارت مانع از این می‌شود که ایجنت‌ها بدون درک ساختار شروع به تغییر کدها کنند، کدهای سالم را بازنویسی کنند، سوالات بیهوده بپرسند یا با پاپ‌آپ‌های مداوم شما را پای سیستم معطل نگه دارند.

---

## 🌍 زبان‌ها / Languages
[English](README.md) | [فارسی](README.fa.md) | [Türkçe](README.tr.md) | [Azərbaycanca](README.az.md) | [العربية](README.ar.md)

---

## 🎯 چرا این مهارت ساخته شد؟ (حل مشکل کارکرد خودکار و شبانه)

بزرگ‌ترین هدف استفاده از هوش مصنوعی این است که **تسک را به آن بسپارید و بروید استراحت کنید** تا صبح کار انجام شده باشد؛ نه اینکه هوش مصنوعی مدام شما را پای سیستم نگه دارد!

رفتارهای اشتباه رایج ایجنت‌ها بدون این مهارت:
1. **دستکاری شتاب‌زده بدون دیسکاوری:** بدون خواندن فایل‌های پروژه، شروع به تغییر کدهای رندوم می‌کند.
2. **پرسیدن سوالات کلافه‌کننده:** مدام سوال می‌پرسد: «کد کجاست؟»، «پیکربندی چیه؟»، «فایل‌ها رو بده».
3. **پاپ‌آپ‌های بی‌پایان تایید دسترسی (Confirmation Prompts):** برای هر بررسی ساده شبکه یا داکر، دستورات خارج از سندباکس می‌فرستد و سیستم را منتظر تأیید دستی شما قفل می‌کند.
4. **تخریب کارهای انجام‌نشده (Uncommitted Changes):** تغییرات در حال انجام شما را نادیده گرفته یا بازنویسی می‌کند.
5. **تکرار چرخ و بازنویسی کد:** به جای استفاده از توابع و پکیج‌های موجود، کد جدید از اول می‌نویسد!

---

## 🛡️ ۷ قانون طلایی این مهارت

1. **کشف و شناخت پروژه قبل از هر اقدامی (Discovery):** بررسی ساختار دایرکتوری‌ها، فایل‌های راهنما (`README`)، معماری (`docs/`)، نیازمندی‌ها (`package.json`, `go.mod`, `Cargo.lock`, `pyproject.toml`)، متغیرهای محیطی و فایل‌های داکر و استقرار.
2. **بررسی استاتیک به جای اتصالات ریموت بیهوده:** خواندن پورت‌ها و کانتینرها از روی `docker-compose.yml` و `Dockerfile`، بدون اجرای دستورات شبکه یا درخواست‌های دسترسی غیرضروری.
3. **درک وضعیت گیت (Git Understanding):** بررسی شاخه فعلی (`branch`)، وضعیت درخت کاری (`git status`) و حفظ تمام کدهای کامیت‌نشده‌ی کاربر.
4. **ساخت مدل ذهنی (Mental Model):** درک هدف بیزینس، معماری لایه‌ها، جریان داده‌ها و استراتژی تست قبل از تغییر حتی یک فایل.
5. **سیاست ممنوعیت سوالات ناتوان‌کننده:** جستجوی خودکار در کد و مستندات؛ سوال فقط زمانی پرسیده می‌شود که اطلاعات اصلاً وجود نداشته باشد یا تغییر تخریبی باشد.
6. **پروتکل پاسخگویی استاندارد مهندسی:** ارائه تحلیل در قالب ۴ بخش در اولین پاسخ:
   - `## Understanding` (درک پروژه)
   - `## Current State` (وضعیت فعلی کد و گیت)
   - `## Plan` (برنامه اجرایی مرحله‌به‌مرحله)
   - `## Blocking Questions` (فقط موانع واقعی، در غیر این صورت هیچ)
7. **گزارش شفاف پایان کار (Completion Report):** ارائه گزارش نهایی شامل وضعیت موفقیت (`STATUS`)، فایل‌های تغییریافته (`CHANGES`)، اعتبارسنجی و تست‌ها (`VALIDATION`)، وضعیت استقرار (`DEPLOYMENT`) و موارد باقی‌مانده (`REMAINING`).

---

## 🚀 نحوه نصب و استفاده در ایجنت‌های مختلف

### ۱. گوگل آنتی‌گرویتی (Google Antigravity)
فایل `SKILL.md` را در مسیر اسکیل‌های محلی خود قرار دهید:
```bash
mkdir -p ~/.gemini/config/skills/agent-project-discovery-skill
cp SKILL.md ~/.gemini/config/skills/agent-project-discovery-skill/SKILL.md
```

### ۲. کلود کد (Claude Code)
```bash
mkdir -p .claude/skills
cp SKILL.md .claude/skills/project-discovery.md
```
یا محتوای `templates/AGENTS.md` را در فایل `CLAUDE.md` پروژه خود اضافه کنید.

### ۳. کرسر (Cursor)
فایل `.cursor/rules/discovery.mdc` را بسازید یا دستورالعمل زیر را در `.cursorrules` قرار دهید:
```markdown
Before making any code edits or asking questions, read and execute the discovery steps in SKILL.md.
Always begin your first response with the 4-part protocol (Understanding, Current State, Plan, Blocking Questions).
```

### ۴. گیت‌هاب کوپایلوت (GitHub Copilot Workspace)
متن فایل `templates/AGENTS.md` را در مسیر `.github/copilot-instructions.md` قرار دهید.

### ۵. راه‌اندازی سریع در هر پروژه دلخواه (۳۰ ثانیه)
کافی است تمپلیت آماده را دانلود و در ریشه پروژه‌تان بگذارید:
```bash
curl -sSL https://raw.githubusercontent.com/tmolavi/agent-project-discovery-skill/main/templates/AGENTS.md -o AGENTS.md
```

---

## 📄 لایسنس
این پروژه تحت لایسنس آزاد و متن‌باز [MIT](LICENSE) منتشر شده است و استفاده از آن در پروژه‌های شخصی، تجاری و سازمانی کاملاً رایگان است.
