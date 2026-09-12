# مهارة استكشاف وفهم المشاريع لوكلاء الذكاء الاصطناعي 🧭
### `agent-project-discovery-skill`

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v1.1.0-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/tmolavi/agent-project-discovery-skill/pulls)

> **"يجب على وكيل الذكاء الاصطناعي أن يفهم المشروع بعمق قبل أن يُغيّر أي سطر برمجياً."**

هذا المشروع يقدّم مهارة انطلاقة موحدة وشاملة (Startup Skill) لمساعدي ووكلاء البرمجة بالذكاء الاصطناعي (مثل Claude Code، Cursor، Google Antigravity، OpenAI Codex، GitHub Copilot وغيرها). تمنع هذه المهارة الوكلاء من التعديل العشوائي على الكود دون فهم معماري، أو إعادة كتابة أنظمة شغالة، أو طرح أسئلة مزعجة، أو حبسك أمام الشاشة للموافقة على كل أمر تافه!

---

## 🌍 اللغات / Languages
[English](README.md) | [فارسی](README.fa.md) | [Türkçe](README.tr.md) | [Azərbaycanca](README.az.md) | [العربية](README.ar.md)

---

## 🎯 ليش بنينا هذي المهارة؟ (شغل ذاتي طول الليل بدون وجع راس)

الفكرة الأساسية من هذا المشروع إنك **تعطي الوكيل المهمة، وتقفل لابتوبك وتروح تنام مرتاح**، وتصحى الصباح وتلقى الشغل مخلص ومختبر بالكامل؛ مو إن الوكيل يصحّيك كل دقيقة أو يوقف الشغل نص الليل ينتظر تضغط زر موافقة!

الأخطاء الشائعة للوكلاء اللي تخرب الشغل الذاتي الليلي:
1. **فحص الروابط العامة الحية (Live Public URLs):** بدلاً من فحص الكود محلياً، يرسل أوامر `curl` للموقع الفعلي الحي، مما يشغّل فايِروول الساندبوكس ويجمّد الوكيل.
2. **أوامر Git الغريبة والنادرة:** تشغيل أوامر غير شائعة مثل `git count-objects` أو `git fsck` التي لا توجد في القائمة المسموحة فتطلب إذناً يدوياً.
3. **نوافذ التأكيد المزعجة (Permission Popups):** إرسال أوامر ريموت عبر SSH بدون داعٍ وتعطيل المستخدم.
4. **التعديل المتهوّر بدون استكشاف:** الدخول على ملفات عشوائية والتعديل عليها بدون فهم البنية.
5. **الأسئلة البديهية اللي ترفع الضغط:** طرح أسئلة إجاباتها موجودة في الكود نفسه.
6. **مسح وتخريب التعديلات الحالية (Uncommitted Changes):** تجاهل تعديلات المطور غير المحفوظة والكتابة فوقها.

---

## 🛡️ القواعد الذهبية السبع للمهارة

1. **الاستكشاف قبل التنفيذ (Discovery):** فحص بنية المجلدات، ملفات الإرشاد (`README`)، التوثيق المعماري (`docs/`)، ملفات الحزم والاعتماديات (`package.json`, `go.mod`, `Cargo.lock`, `pyproject.toml`)، المتغيرات البيئية وملفات الدوكر والنشر.
2. **الفحص الساكن أولاً (Static Inspection):** قراءة المنافذ والحاويات مباشرة من `docker-compose.yml` و `Dockerfile`، وتجنب فحص الخوادم عن بُعد عبر الشبكة بدون طلب صريح.
3. **احترام حالة Git:** معرفة الفرع الحالي (`branch`)، وفحص `git status`، وحماية كل التعديلات غير المحفوظة الخاصة بالمطور.
4. **بناء نموذج ذهني متكامل (Mental Model):** فهم هدف المشروع، وبنية الطبقات، ومسار البيانات، وخطة الاختبار قبل لمس أي ملف.
5. **حظر الأسئلة الضعيفة:** البحث الذاتي في الكود أولاً. يُمنع سؤال المستخدم إلا في حال كانت المعلومة غير موجودة نهائياً أو كان الإجراء تدميرياً لا رجعة فيه.
6. **بروتوكول الرد الهندسي الموحد:** أول رد للوكيل يكون دائماً مقسّم لأربعة أقسام:
   - `## Understanding` (فهم المشروع والمعمارية)
   - `## Current State` (الحالة الحالية للكود وGit)
   - `## Plan` (خطة التنفيذ خطوة بخطوة وبأقل تعديل ممكن)
   - `## Blocking Questions` (فقط العقبات الحقيقية المستعصية، وإلا يكتب "None")
7. **تقرير الإنجاز الشفاف (Completion Report):** عند انتهاء المهمة، يقدّم الوكيل تقريراً موجزاً يوضح الحالة (`STATUS`)، والملفات المعدلة (`CHANGES`)، ونتائج الفحص والاختبار (`VALIDATION`)، وحالة النشر (`DEPLOYMENT`)، والملاحظات المتبقية (`REMAINING`).

---

## 🚀 طريقة التثبيت والاستخدام

### 1. Google Antigravity
انسخ ملف `SKILL.md` إلى مجلد المهارات لديك:
```bash
mkdir -p ~/.gemini/config/skills/agent-project-discovery-skill
cp SKILL.md ~/.gemini/config/skills/agent-project-discovery-skill/SKILL.md
```

### 2. Claude Code
```bash
mkdir -p .claude/skills
cp SKILL.md .claude/skills/project-discovery.md
```
أو ضع الإرشادات في ملف `CLAUDE.md` داخل مشروعك.

### 3. Cursor
أنشئ الملف `.cursor/rules/discovery.mdc` أو أضف القاعدة في `.cursorrules`:
```markdown
Before making any code edits or asking questions, read and execute the discovery steps in SKILL.md.
Always begin your first response with the 4-part protocol (Understanding, Current State, Plan, Blocking Questions).
```

### 4. GitHub Copilot Workspace
أضف محتوى `templates/AGENTS.md` في المسار `.github/copilot-instructions.md`.

### 5. تشغيل سريع في أي مشروع جديد (خلال 30 ثانية)
نزّل القالب وضعه في المجلد الرئيسي للمشروع:
```bash
curl -sSL https://raw.githubusercontent.com/tmolavi/agent-project-discovery-skill/main/templates/AGENTS.md -o AGENTS.md
```

---

## 📄 الترخيص
هذا المشروع منشور ومتاح تحت رخصة [MIT](LICENSE) المفتوحة، ومجاني بالكامل للاستخدام الشخصي والتجاري والشركات.
