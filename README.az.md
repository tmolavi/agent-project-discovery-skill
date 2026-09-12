# Süni İntellekt Agentləri Üçün Layihə Kəşfi Bacarığı 🧭
### `agent-project-discovery-skill`

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v1.1.0-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/tmolavi/agent-project-discovery-skill/pulls)

> **"Süni intellekt agenti dəyişiklik etməzdən əvvəl layihəni dərindən anlamalıdır."**

Bu layihə kodlaşdırma agentləri (Claude Code, Cursor, Google Antigravity, OpenAI Codex, GitHub Copilot və s.) üçün universal və istehsala hazır başlanğıc bacarığıdır (startup skill). Agentlərin layihəni başa düşmədən tələsik kod dəyişdirməsinin, mövcud arxitekturanı pozmasının, lazımsız suallar verməsinin və sizi daima ekran qarşısında təsdiq düymələrinə basmağa məcbur etməsinin qarşısını alır.

---

## 🌍 Dillər / Languages
[English](README.md) | [فارسی](README.fa.md) | [Türkçe](README.tr.md) | [Azərbaycanca](README.az.md) | [العربية](README.ar.md)

---

## 🎯 Bu Bacarıq Niyə Yaradıldı? (Gecə Boyu Tam Avtonom İş)

Süni intellektdən istifadənin əsas məqsədi **tapşırığı verib dincəlmək**, səhər işin tam hazır olduğunu görməkdir. Agentin sizi səhərə qədər kompüter qarşısında saxlayıb hər addımda *"Bunu icra edimmi?"*, *"Təsdiq edirsinizmi?"* deyə soruşması süni intellektin təyinatına ziddir!

Bu bacarıq olmadıqda agentlərin etdiyi xətalar:
1. **Kəşf etmədən kod dəyişdirmək:** Layihə strukturunu və asılılıqları yoxlamadan təsadüfi fayllarda dəyişiklik edirlər.
2. **Yersiz və yorucu suallar:** *"Kod haradadır?"*, *"Konfiqurasiya faylı hansıdır?"*, *"Nə edim?"* kimi kod bazasında cavabı olan suallar verirlər.
3. **Davamlı təhlükəsizlik və icazə pəncərələri:** Sadə port və ya konteyner yoxlaması üçün xarici əmrlər çağırıb sizin təsdiqinizi gözləyirlər.
4. **Yadda saxlanılmamış dəyişiklikləri silmək (Uncommitted Changes):** Proqramçının üzərində işlədiyi cari dəyişiklikləri nəzərə almadan üstündən yazırlar.
5. **Mövcud funksiyaları yenidən yazmaq:** Layihədə artıq mövcud olan köməkçi modulları görməzdən gəlib təkrar kod yaradırlar.

---

## 🛡️ Bacarığın 7 Qızıl Qaydası

1. **İcradan Əvvəl Layihə Kəşfi:** Kataloq strukturu, `README`, arxitektura sənədləri (`docs/`), asılılıq faylları (`package.json`, `go.mod`, `Cargo.lock`, `pyproject.toml`), mühit dəyişənləri və CI/CD faylları ətraflı yoxlanılır.
2. **Statik Yoxlamaya Üstünlük:** Portlar və konteynerlər birbaşa `docker-compose.yml` və `Dockerfile` fayllarından oxunur, lüzumsuz şəbəkə sorğuları ilə sistem dayandırılmır.
3. **Git Vəziyyətinin Qorunması:** Cari budaq (`branch`), `git status`, son commit tarixçəsi və proqramçının yadda saxlanılmamış dəyişiklikləri qorunur.
4. **Zehni Modelin Yaradılması (Mental Model):** Kod yazmazdan əvvəl layihənin biznes məqsədi, arxitekturası, məlumat axını və test strategiyası tam dərk edilir.
5. **Yersiz Sualların Qadağan Edilməsi:** Kod bazasında axtarışı mümkün olan heç bir məlumat istifadəçidən soruşulmur. Yalnız həqiqi çatışmazlıqlarda və ya geri dönüşü olmayan əməliyyatlarda sual verilə bilər.
6. **Standart Mühəndislik Cavab Protokolu:** Agent ilk cavabında bu 4 bölməni təqdim edir:
   - `## Understanding` (Layihənin mahiyyəti və kəşf xülasəsi)
   - `## Current State` (Cari git və kod vəziyyəti)
   - `## Plan` (Addım-addım minimal icra planı)
   - `## Blocking Questions` (Yalnız real maneələr, əks halda "None")
7. **Şəffaf Tamamlama Hesabatı (Completion Report):** Tapşırıq bitdikdə status (`STATUS`), dəyişdirilmiş fayllar (`CHANGES`), yoxlama testləri (`VALIDATION`), tətbiq vəziyyəti (`DEPLOYMENT`) və qalan qeydlər (`REMAINING`) dəqiq çatdırılır.

---

## 🚀 Quraşdırma və İnteqrasiya

### 1. Google Antigravity
`SKILL.md` faylını lokal bacarıqlar qovluğuna köçürün:
```bash
mkdir -p ~/.gemini/config/skills/agent-project-discovery-skill
cp SKILL.md ~/.gemini/config/skills/agent-project-discovery-skill/SKILL.md
```

### 2. Claude Code
```bash
mkdir -p .claude/skills
cp SKILL.md .claude/skills/project-discovery.md
```
Və ya layihənizin `CLAUDE.md` faylına daxil edin.

### 3. Cursor
`.cursor/rules/discovery.mdc` yaradın və ya `.cursorrules` faylına əlavə edin:
```markdown
Before making any code edits or asking questions, read and execute the discovery steps in SKILL.md.
Always begin your first response with the 4-part protocol (Understanding, Current State, Plan, Blocking Questions).
```

### 4. GitHub Copilot
`templates/AGENTS.md` məzmununu `.github/copilot-instructions.md` daxilinə yerləşdirin.

### 5. Hər Hansı Layihədə Sürətli Başlanğıc (30 Saniyə)
```bash
curl -sSL https://raw.githubusercontent.com/tmolavi/agent-project-discovery-skill/main/templates/AGENTS.md -o AGENTS.md
```

---

## 📄 Lisenziya
Bu layihə [MIT Lisenziyası](LICENSE) altında yayımlanır. Şəxsi, kommersiya və şirkət layihələrində tamamilə sərbəst istifadə edilə bilər.
