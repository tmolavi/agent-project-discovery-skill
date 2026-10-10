# مهارة استكشاف وفهم المشاريع لوكلاء الذكاء الاصطناعي 🧭
### `agent-project-discovery-skill`

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v1.19.0-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/tmolavi/agent-project-discovery-skill/pulls)

> **"يجب على وكيل الذكاء الاصطناعي أن يفهم المشروع بعمق قبل أن يُغيّر أي سطر برمجياً."**

هذا المشروع يقدّم مهارة انطلاقة موحدة وشاملة (Startup Skill) لمساعدي ووكلاء البرمجة بالذكاء الاصطناعي (مثل Claude Code، Cursor، Google Antigravity، OpenAI Codex، GitHub Copilot وغيرها). تمنع هذه المهارة الوكلاء من التعديل العشوائي على الكود دون فهم معماري، أو إعادة كتابة أنظمة شغالة، أو طرح أسئلة مزعجة، أو التوقف عند الحالات غير المتوقعة، أو طلب الإذن لاختبار الكود، فحص المسارات، فحص إصدارات الحزم (`pip show edge-tts`)، ترقية وتحديث الحزم (`pip install -U edge-tts`)، قراءة واستعراض ملفات docker-compose.yml أو التكوين على السيرفر (`cat ... docker-compose.yml`)، استعراض مكونات الواجهة (`cat ... components/MobileMenu.tsx`)، فحص مزودي STT واختبار Groq Whisper، إرسال ملفات عبر SCP عشوائياً أو إعادة تشغيل الحاويات (`docker restart hamzad-ara`)، تشغيل حزم التقييم والقياس المعياري عن بُعد (`test_20_persian_utterances.py`)، فحص مسارات الصحة، سجلات الحاويات، سجل الأوامر، ومجلدات البناء (`/api/health`, `docker logs`, `history`, `ls .next`)، إعادة محاولة اتصال SSH واختبار الجاهزية والصدى (`Allow retrying SSH connection?`, `Allow testing SSH to hamzad_server?`)، الفحص المركب للحاويات وحالة الجيت بالسيرفر (`Allow checking server molavi-pro container and git?`)، استعراض مهارات الخدمات البعيدة (`Allow listing Hermes skills?`)، فحص مجلد .next داخل حاوية السيرفر (`Allow inspecting container .next directory?`)، نسخ الملفات والصفحات عبر SCP عشوائياً (`Allow copying components to server?`, `Allow copying page.tsx and robots.ts to server?`, `Allow copying robots.ts to server?`)، فحص محتويات الحاويات (`docker exec ... ls`)، فحص وسرد فروع الجيت على السيرفر (`git branch -a`)، فحص حاويات السيرفر وحالة الجيت (`docker ps && git status`)، فحص فرع وسجل الجيت (`git branch && git log`)، اختبار توجيه النماذج (central model dispatch)، فحص مكتبة Edge-TTS المحدثة وسرعة تحويل النص إلى كلام (`Allow testing updated Edge-TTS?`, `Allow testing TTS synthesis speed?`)، أو اختبار خط معالجة تحويل الصوت إلى نص STT (`Allow testing STT pipeline?`)، أو حبسك أمام الشاشة للموافقة على كل أمر تافه!

---

## 🌍 اللغات / Languages
[English](README.md) | [فارسی](README.fa.md) | [Türkçe](README.tr.md) | [Azərbaycanca](README.az.md) | [العربية](README.ar.md)

---

## 🌙 بروتوكول النوم الهانئ (Sleep-Well Protocol): أتمتة ليلية ذاتية بالكامل

الفكرة الأساسية من هذا المشروع إنك:
> **"تعطي الوكيل المهمة، وتقفل لابتوبك وتروح تنام مرتاح؛ وتصحى الصباح وتلقى الشغل مخلص ومختبر ونظيف بالكامل، مو واقف نص الليل ينتظر تضغط زر موافقة!"**

---

### ❓ ليش الوكلاء يطلبون تأكيدات ونوافذ موافقة (Approval Modals) طول الوقت؟

في بيئات البرمجة الذكية الحديثة (مثل Google Antigravity، Claude Code، و Cursor)، يوجد **نظام حماية وساندبوكس (Sandbox)**:
1. **الأوامر الداخلية بالساندبوكس (Standard Sandbox)**: قراءة وتعديل الملفات داخل المشروع، فحص `git status` و `git diff`، البناء المحلي (`npm run build`, `cargo check`) والاختبارات (`pytest`, `vitest`) تشتغل **بشكل صامت وتلقائي 100% بدون أي طلب تأكيد**.
2. **الأسباب اللي تفتح نوافذ التأكيد فجأة وتوقّف الشغل**:
   - **التوقف عند الحالات غير المتوقعة وطرح الأسئلة تباعاً أثناء العمل**: عندما يوقف الوكيل الشغل بدلاً من إكمال المهام الأخرى وتجميع الأسئلة لنهاية العمل.
   - **طلب الإذن لاختبار النقاط النهائية (`Allow testing /api/... ?`)**: لما يوقف الوكيل الشغل عشان يسأل المستخدم هل يسمح باختبار نقطة برمجية أو تشغيل أمر SSH بدلاً من أن يقرر بنفسه.
   - **طلب الإذن لاختبار توجيه النماذج (`Allow testing central model dispatch?`)**: محاولة فحص بوابات النماذج الحية عبر SSH بدلاً من محاكاتها محلياً.
   - **طلب الإذن لاختبار سرعة الصوت، تحويل النص لكلام، أو فحص مكتبة Edge-TTS المحدثة (`Allow testing TTS synthesis speed?`, `Allow testing updated Edge-TTS? ssh ...`)**: محاولة تشغيل قياسات سرعة الصوت، التحقق من Edge-TTS، أو استدعاء `TTSService.synthesize_chunk` على خوادم حية بدلاً من محاكاتها محلياً.
   - **طلب الإذن لاختبار خط أنابيب تحويل الصوت إلى نص STT على السيرفر (`Allow testing STT pipeline?`, `Allow checking STT providers?`, `Allow testing Groq Whisper STT?`):** محاولة الوكيل تشغيل اختبارات رونویسی صوت، أو فحص مفاتيح مزودي STT، أو استدعاء Groq Whisper على خوادم حية بدلاً من محاكاتها واختبارها محلياً.
   - **طلب الإذن لفحص إصدارات الحزم والاعتماديات (`Allow checking edge-tts version? ssh ... "pip show ...")**: محاولة الوكيل تشغيل أوامر `pip show` أو `pip list` عبر SSH لفحص الحزم بدلاً من قراءة ملفات الاعتماديات المحلية.
   - **طلب الإذن لترقية وتحديث الحزم على السيرفر (`Allow upgrading edge-tts? ssh ... "pip install -U ...")**: محاولة خاطئة من الوكيل لتنفيذ أوامر `pip install -U` عبر SSH على السيرفرات أو الحاويات بدلاً من تعديل ملفات المانيفست محلياً.
   - **طلب الإذن لاستعراض ملف docker-compose.yml أو تكوينات النشر على السيرفر (`Allow viewing server docker-compose.yml? ssh ... "cat ... docker-compose.yml"`):** محاولة الوكيل تشغيل أوامر `cat` أو `less` عبر SSH لقراءة ملف `docker-compose.yml` أو تكوينات النشر على الخادم بدلاً من قراءتها مباشرة من ملفات المشروع المحلية.
   - **طلب الإذن لفحص محتويات الحاويات وهيكل المجلدات (`Allow checking container contents? ssh ... "docker exec ... ls -la /app"`):** محاولة الوكيل تشغيل أوامر `docker exec ... ls` عبر SSH لفحص ملفات ومسارات الحاوية بدلاً من مراجعة هيكل ملفات المشروع محلياً وتعليمات `Dockerfile` و `docker-compose.yml`.
   - **طلب الإذن لاستعراض مكونات الواجهة أو الكود المصدري على السيرفر (`Allow checking server MobileMenu.tsx? ssh ... "cat ... components/MobileMenu.tsx"`):** محاولة الوكيل تشغيل أوامر `cat` عبر SSH لقراءة ملفات الواجهة من الخادم بدلاً من مراجعتها من المشروع المحلي.
   - **طلب الإذن للنشر العشوائي عبر SCP أو إعادة تشغيل الحاويات (`Allow deploying updated app files to production?`, `Allow restarting hamzad-ara container?`, `Allow deploying hermes_router and restarting container?`):** محاولة الوكيل إرسال ملفات عبر SCP وإعادة تشغيل الحاويات في منتصف المهمة بدلاً من إنجاز العمل محلياً.
   - **طلب الإذن لتشغيل حزم التقييم والاختبارات المعيارية (`Allow running 20-utterance Persian evaluation suite?`, `Allow running full 20-utterance benchmark?`):** محاولة الوكيل رفع سكربتات الاختبار وتشغيلها داخل حاويات الإنتاج عبر SSH بدلاً من تشغيلها محلياً ببيانات وهمية.
   - **طلب الإذن لفحص نقاط الصحة، سجلات الحاويات، أو تاريخ الأوامر (`Allow checking ARA health endpoint?`, `Allow checking hamzad-ara container logs?`, `Allow checking server command history?`, `Allow checking .next on server host?`):** محاولة تشغيل `curl`, `docker logs`, `history` أو `ls .next` عبر SSH بدلاً من فحصها محلياً.
   - **طلب الإذن لإعادة محاولة اتصال SSH واختبار الجاهزية والصدى (`Allow retrying SSH connection?`, `Allow testing SSH to hamzad_server?`):** محاولة تشغيل `uptime` أو `echo` عبر SSH بدلاً من التراجع للتحقق المحلي عند انقطاع الاتصال.
   - **طلب الإذن للفحص المركب للحاويات وحالة الجيت بالسيرفر (`Allow checking server molavi-pro container and git?`):** محاولة تشغيل سلاسل SSH معقدة بدلاً من الفصل والاستكشاف الساكن.
   - **طلب الإذن لاستعراض مهارات الخدمات ونقاطها الداخلية (`Allow listing Hermes skills?`):** تشغيل `docker exec ... httpx.get` على السيرفر بدلاً من قراءة وثائق وسجلات المهارات محلياً.
   - **طلب الإذن لفحص مجلد .next داخل حاوية السيرفر (`Allow inspecting container .next directory?`):** تشغيل `docker exec ... ls -la /app/.next` بدلاً من التحقق من البناء المحلي (`npm run build`).
   - **طلب الإذن لنسخ الملفات والصفحات عبر SCP عشوائياً (`Allow copying components to server?`, `Allow copying page.tsx and robots.ts to server?`, `Allow copying robots.ts to server?`):** محاولة النسخ اليدوي للملفات عبر SCP بدلاً من الالتزام بسجل الجيت وسكربتات النشر الرسمية.
   - **طلب الإذن لفحص بيئة التشغيل أو إصدار Node على الخادم المضيف (`Allow checking node on server host? ssh ... "node -v || true"`):** محاولة خاطئة من الوكيل لفحص إصدار نود أو البرمجيات على الخادم المضيف عبر SSH بدلاً من فحص ملفات المانيفست المحلية (`package.json`, `.nvmrc`, `Dockerfile`).
   - **طلب الإذن لفحص حاويات السيرفر وحالة الجيت البعيدة (`Allow checking server container and git status?`, `Allow checking server git branch and log?`, `Allow listing git branches on server?`, `Allow checking molavi-pro container on server?`):** محاولة خاطئة من الوكيل للاتصال بالخادم عبر SSH لتشغيل `docker ps`، أو `git status -s`، أو `git branch` و `git log` على السيرفر بدلاً من فحص ملفات المشروع وسجل الجيت محلياً.
   - **طلب الإذن لفحص المسارات والأكواد البعيدة (`Allow checking model router endpoints?`)**: محاولة خاطئة من الوكيل للاتصال بالخادم عبر SSH لقراءة ملفات الكود والمسارات بدلاً من قراءتها محلياً من ملفات المشروع.
   - **طلب الخروج من الساندبوكس (`BypassSandbox: true`)**: لما يحاول الوكيل الوصول المباشر للشبكة أو كامل القرص بدون وجود صلاحية مسجلة مسبقاً.
   - **فحص الروابط الحية على الإنترنت (`curl https://...`)**: إرسال طلبات HTTP لمواقع حية للتأكد من الكود بدلاً من فحصه محلياً.
   - **أوامر الخوادم العشوائية (`ssh`, `scp`, `docker images` على السيرفر)**: محاولة الاتصال بالخادم الحي بدون طلب صريح.
   - **أوامر Git الداخلية العمیقة (`git count-objects`, `git fsck`)**: أوامر غير معتادة تخرق فلاتر الأوامر المسموحة وتطلب إذناً يدوياً.
   - **محاولة تعديل ملفات النظام وإعدادات الـ IDE**: العبث بملفات خارج مجلد المشروع (مثل `config.json`).
   - **سلاسل الأوامر الطويلة بالأنابيب (`cmd1 && cmd2 | grep ... | awk ...`)**: السلاسل المعقدة تكسر ميزة التعرف التلقائي على الأوامر المصرح بها.
   - **أوامر أبل سكربت / المتصفح المتفرقة (`osascript -e '...'`)**: تشغيل سكربتات فردية متتالية لفحص المتصفح تفتح نوافذ تأكيد متكررة.

---

### 🛠️ كيف تعالج هذه المهارة كل هذي المشاكل؟

1. **الاستمرار في الحالات غير المتوقعة وتجميع الأسئلة في النهاية ("استمر واطرح كل شيء دفعة واحدة في الأخير")**: عند مواجهة أي غموض أو خطأ غير متوقع، لا يتوقف الوكيل أبداً في منتصف العمل؛ بل يتخذ القرار الآمن التلقائي، وينجز كل المهام الأخرى المتاحة، ويجمع كل الأسئلة لطرحها في تقرير واحد منسق بنهاية العمل.
2. **القرار الذاتي في الاختبار والتحقق**: لا يسأل الوكيل "هل أختبر النقطة النهائية؟"، "Allow retrying SSH connection?"، "Allow checking server molavi-pro container and git?"، "Allow listing Hermes skills?"، "Allow inspecting container .next directory?" أو "Allow copying components to server؟"؛ بل يتخذ القرار ذاتياً باختبار الكود عبر المحاكاة المحلية (Mocks)، واختبارات الوحدة، والسيرفر المحلي (`127.0.0.1`) ويقدم النتيجة في التقرير النهائي.
3. **التحقق المحلي والحتمي فقط**: منع فحص الروابط الحية أو الخوادم البعيدة بدون طلب صريح؛ ويتم التحقق من الأكواد عبر البناء المحلي (`npm run build`) والاختبارات المحلية.
4. **محاكاة النماذج والتوجيه المركزي**: اختبار موجهات الاستدلال وبوابات النماذج عبر النقل المحاكى محلياً بدون الاتصال بالسيرفرات.
5. **محاكاة الصوت، خدمات تحويل النص إلى كلام (TTS)، ومكتبة Edge-TTS المحدثة**: اختبار خدمات الصوت (`TTSService`)، مكتبة Edge-TTS المحدثة، وتدفق المقاطع الصوتية محلياً باستخدام محاكيات غير متزامنة (`AsyncMock`) وبيانات صوتية وهمية بدلاً من تشغيل قياسات على الخوادم البعيدة.
6. **الفحص الساكن للحزم والاعتماديات محلياً (Manifest Discovery)**: قراءة إصدارات الحزم والمكتبات مباشرة من ملفات المشروع المحلية (`requirements.txt`, `pyproject.toml`, `poetry.lock`, `package.json`, `Dockerfile`) بدلاً من تنفيذ أوامر `pip show` أو `pip list` عبر SSH على الخوادم البعيدة.
7. **الترقية المحلية للحزم وإدارة المانيفست**: ترقية الحزم أو إصلاح المشاكل البرمجية يتم مباشرة عبر تحديث ملفات المانيفست المحلية (`requirements.txt`, `pyproject.toml`) واختبارها محلياً، بدلاً من إرسال أوامر `pip install -U` عبر SSH إلى الخوادم البعيدة.
8. **الفحص المحلي للحاويات وحالة الجيت**: قراءة إعدادات الحاويات والمنافذ من ملفات المشروع المحلية (`docker-compose.yml`, `Dockerfile`)، وفحص حالة الجيت والفرع وكامل الفروع (`git branch -a`) وسجل الالتزامات محلياً (`git status -s`, `git branch --show-current`, `git log -n 5`) بدون أوامر SSH إلى الخوادم.
9. **الفحص المحلي لنظام ملفات الحاويات وهيكل المجلدات**: فحص هيكل مسارات التطبيق (`/app`، `/workspace`) وملفات الحاويات مباشرة من ملفات المشروع المحلية، وتعليمات `Dockerfile` (أوامر WORKDIR و COPY) وربط الأحجام (volumes) في `docker-compose.yml` بدون تنفيذ أوامر استكشاف مثل `docker exec ... ls` عبر SSH.
10. **الفحص المحلي لمانيفست النشر و docker-compose**: مراجعة ملف `docker-compose.yml` وتعريفات الخدمات و `Dockerfile` وتكوينات البيئة مباشرة من مجلد العمل المحلي بدون إرسال أوامر `cat` أو `less` عبر SSH إلى الخوادم البعيدة.
11. **محاكاة خدمات تحويل الصوت إلى نص (STT)، ومزودي الخدمة، وGroq Whisper**: اختبار خدمات استخراج النصوص من الصوت (`STTService`)، ودالة `transcribe_audio_bytes`، وتكوينات مزودي الخدمة ومفتاح Groq Whisper محلياً باستخدام محاكيات غير متزامنة (`AsyncMock`) وبيانات وهمية بدلاً من تشغيل اختبارات رونویسی على الخوادم البعيدة.
12. **الفحص المحلي لمكونات الواجهة والكود المصدري**: فحص مكونات الواجهة الأمامية (`components/MobileMenu.tsx`، ملفات `.tsx`، `.jsx`، `.vue`) والأكواد المصدرية مباشرة من ملفات المشروع المحلية دون تنفيذ أوامر `cat` عبر SSH على السيرفر.
13. **الإدارة المحلية للنشر وحظر أوامر SCP العشوائية**: تحضير التغييرات وحزمها واختبارها محلياً في المشروع، وتجنب رفع الملفات عبر SCP أو إعادة تشغيل الحاويات في منتصف المهمة.
14. **التشغيل المحلي لأجنحة التقييم والقياس المعياري**: تشغيل حزم التقييم واختبارات الجمل المتعددة (`test_20_persian_utterances.py`) محلياً باستخدام بيانات ومحاكيات وهمية بدلاً من رفعها وتشغيلها على حاويات الإنتاج البعيدة.
15. **التشخيص المحلي لمسارات الصحة، وسجلات الحاويات، وملفات البناء**: فحص مسارات الصحة (`/api/health`)، وسجلات الأخطاء، وسجل الأوامر، ومجلدات البناء (`.next`) محلياً من الكود والمخرجات دون إرسال أوامر SSH مثل `curl` أو `docker logs` أو `history`.
16. **الخطة البديلة التلقائية لاتصال SSH وحظر اختبارات Uptime:** في حال انقطاع اتصال SSH أو انتهاء المهلة، لا يوقف الوكيل المستخدم بطلبات إعادة المحاولة أو اختبارات uptime و echo؛ بل يتحول فوراً للتحقق المحلي والمحاكاة ويسجل تعذر الاتصال في التقرير النهائي.
17. **الفصل التلقائي للأوامر المركبة واستكشافها محلياً:** يتم استكشاف معمارية الحاويات ساكناً من ملفات المانيفست، وتُفحص فروع الجيت وسجل الالتزامات محلياً دون إطلاق أوامر SSH مركبة.
18. **الاستكشاف المحلي لمهارات الخدمات المصغرة:** تُستكشف مهارات وخدمات النظام (مثل هرمس) مباشرة من ملفات التسجيل المحلية (`hermes-skill-discovery-registry-v1.json`) بدلاً من تنفيذ استدعاءات API بعيدة عبر `docker exec`.
19. **التحقق من البناء المحلي بدلاً من تفتيش مجلد .next البعيد:** يتم التأكد من سلامة ملفات ومخرجات مجلد `.next/` عبر أمر البناء المحلي (`npm run build`) دون إرسال أوامر تفتيش إلى داخل الحاويات البعيدة.
20. **النشر الرسمي عبر Git وإلغاء النسخ اليدوي بـ SCP:** تُسجل جميع التعديلات كالتزامات في الجيت، ويقتصر النشر إلى السيرفر على سكربتات الإصدار الرسمية (`deploy.sh`) بدلاً من النسخ العشوائي عبر SCP.
21. **الاستكشاف المحلي لبيئات التشغيل والمكتبات:** تُفحص متطلبات بيئة Node.js أو بايثون مباشرة من ملفات المانيفست المحلية (`package.json` حقل engines، ملف `.nvmrc`، `Dockerfile`) دون إرسال أوامر SSH مثل `node -v` إلى الخادم المضيف.
22. **سكربت التشغيل الموحد لأتمتة المتصفح والنظام (Single-Runner Batching)**: إذا طلب المستخدم فحص تبويبات المتصفح النشطة (مثل cPanel، سحابة، كولاب) أو فحص قاعدة بيانات، يقوم الوكيل بكتابة سكربت بايثون أو أبل سكربت كامل ومستقل، ويشغله **مرة واحدة فقط** ويقرأ النتيجة المهيكلة (JSON) بدون تكرار النوافذ المزعجة.
23. **الفحص الساكن للنشر**: قراءة الحاويات والمنافذ من `docker-compose.yml` و `Dockerfile` بدلاً من إرسال أوامر SSH متكررة.
24. **عزل المشروع بالكامل**: عدم المساس بأي ملفات عامة خارج مجلد العمل.

---

### 🛡️ دليل المطور: تفعيل الصلاحيات الكاملة (Full Access Setup)

إذا كنت تبغى تعطي الأداة صلاحيات كاملة وتشتغل بدون أي نافذة تأكيد:

#### 1. Google Antigravity
أضف الأوامر المسموحة في ملف إعداداتك `~/.gemini/config/config.json` تحت `globalPermissionGrants.allow`:
```json
{
  "globalPermissionGrants": {
    "allow": [
      "command(git)",
      "command(pnpm)",
      "command(npm)",
      "command(python3)",
      "command(node)",
      "command(ssh)",
      "command(docker)",
      "command(curl)",
      "command(osascript)",
      "unsandboxed(python3)",
      "unsandboxed(bash)",
      "unsandboxed(osascript)",
      "unsandboxed(ssh)",
      "unsandboxed(docker)",
      "unsandboxed(curl)"
    ]
  }
}
```

#### 2. Claude Code
حدّد الأوامر التلقائية في الإعدادات:
```json
{
  "allowedCommands": [
    "git *",
    "pnpm *",
    "npm *",
    "python3 *",
    "pytest *",
    "node *"
  ]
}
```

#### 3. Cursor
أضف `templates/AGENTS.md` في جذر مشروعك أو في `.cursorrules`.

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
أو أضف محتوى `templates/AGENTS.md` إلى ملف `CLAUDE.md`.

### 3. Cursor
أنشئ ملف `.cursor/rules/discovery.mdc` أو أضف هذا التوجيه إلى `.cursorrules`:
```markdown
Before making any code edits or asking questions, read and execute the discovery steps in SKILL.md.
Always begin your first response with the 4-part protocol (Understanding, Current State, Plan, Blocking Questions).
```

### 4. GitHub Copilot
أضف محتوى `templates/AGENTS.md` إلى `.github/copilot-instructions.md`.

### 5. بداية سريعة في أي مشروع (30 ثانية)
```bash
curl -sSL https://raw.githubusercontent.com/tmolavi/agent-project-discovery-skill/main/templates/AGENTS.md -o AGENTS.md
```

---

## 📄 الترخيص
هذا المشروع منشور تحت رخصة البرمجيات الحرة مفتوحة المصدر [MIT](LICENSE)، وهو متاح للاستخدام الشخصي والتجاري والمؤسسي مجاناً بالكامل.
