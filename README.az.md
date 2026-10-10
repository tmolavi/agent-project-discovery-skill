# Süni İntellekt Agentləri Üçün Layihə Kəşfi Bacarığı 🧭
### `agent-project-discovery-skill`

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v1.8.0-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/tmolavi/agent-project-discovery-skill/pulls)

> **"Süni intellekt agenti dəyişiklik etməzdən əvvəl layihəni dərindən anlamalıdır."**

Bu layihə kodlaşdırma agentləri (Claude Code, Cursor, Google Antigravity, OpenAI Codex, GitHub Copilot və s.) üçün universal və istehsala hazır başlanğıc bacarığıdır (startup skill). Agentlərin layihəni başa düşmədən tələsik kod dəyişdirməsinin, mövcud arxitekturanı pozmasının, lazımsız suallar verməsinin, gözlənilməz hallarda dayanıb qalmasının, test, marşrut, paket versiyası (`pip show edge-tts`), model paylama (central dispatch) və ya TTS nitq sintezi yoxlanışı üçün icazə istəməsinin və sizi daima ekran qarşısında təsdiq düymələrinə basmağa məcbur etməsinin qarşısını alır.

---

## 🌍 Dillər / Languages
[English](README.md) | [فارسی](README.fa.md) | [Türkçe](README.tr.md) | [Azərbaycanca](README.az.md) | [العربية](README.ar.md)

---

## 🌙 "Rahat Yuxu" Protokolu (Sleep-Well Protocol): Fasiləsiz Gecə Avtonomiyası

Bu layihənin əsas məqsədi budur:
> **"Tapşırığı süni intellektə verin, noutbuku bağlayın və rahat yatın. Səhər durduqda təsdiq pəncərələrinə ilişib donmamış, tam test edilmiş və səliqəli kod təhvil alın."**

---

### ❓ Agentlər Niyə Davamlı Təsdiq Pəncərəsi (Approval Modal) Açır?

Müasir süni intellekt mühitlərində (Google Antigravity, Claude Code, Cursor) daxili **Qum Qutusu (Sandbox) Təhlükəsizlik Sistemi** mövcuddur:
1. **Qum Qutusu Daxilində Standart Əmrlər (Standard Sandbox)**: Layihə qovluğu daxilində faylların oxunması/yazılması, lokal git statusu (`git status`, `git diff`), lokal yığma (`npm run build`, `cargo check`) və testlər (`pytest`, `vitest`) **tam avtomatik, səssiz və heç bir təsdiq istəmədən** işləyir.
2. **Təsdiq Pəncərəsi Tələb Edən Səbəblər**:
   - **Gözlənilməz Hallarda Dayanıb Tək-Tək Sual Vermək**: Agentin digər işləri bitirib sualları sona saxlamaq əvəzinə işin ortasında davamlı donması.
   - **Rutin Test Təsdiqi Tələbi (`Allow testing /api/... ?`)**: Agentin müstəqil qərar vermək əvəzinə test icrası və ya SSH skripti üçün istifadəçidən icazə istəməsi.
   - **Mərkəzi Model Paylanması Onayı İstəmək (`Allow testing central model dispatch?`)**: Agentin model şlüzünü lokal mühitdə mock etmək əvəzinə canlı serverdə test etmək üçün icazə istəməsi.
   - **Səs və TTS Sintez Sürəti Yoxlanışı Üçün İcazə İstəmək (`Allow testing TTS synthesis speed? ssh ...`)**: Agentin nitq sintezini və ya səs emal sürətini lokal mühitdə mock etmək əvəzinə canlı serverdə test etmək üçün icazə istəməsi.
   - **Paket və Asılılıq Versiyası Yoxlanışı Üçün İcazə İstəmək (`Allow checking edge-tts version? ssh ... "pip show ...")**: Agentin lokal asılılıq bəyannamələrini oxumaq əvəzinə uzaq mühitə SSH ilə `pip show` və ya `pip list` əmrləri göndərməsi.
   - **Marşrut və Kod Yoxlanışı Üçün İcazə İstəmək (`Allow checking model router endpoints?`)**: Agentin lokal faylları oxumaq əvəzinə uzaq serverə SSH ilə qoşulub kod fayllarını oxumağa cəhd etməsi.
   - **Qum Qutusundan Çıxış Tələbi (`BypassSandbox: true`)**: Agentin xam şəbəkəyə və ya diskə çıxış istəməsi və uyğun prefiks icazəsinin olmaması.
   - **Canlı İctimai Saytları Yoxlamaq (`curl https://...`)**: Kodun işləməsini yoxlamaq üçün canlı veb-saytlara HTTP sorğuları atmaq.
   - **Lüzumsuz Uzaq Server Əmrləri (`ssh`, `scp`, `docker images`)**: Konfiqurasiya fayllarını oxumaq əvəzinə canlı serverə və ya GitHub-a SSH ilə bağlanmağa cəhd etmək.
   - **Daxili Dərin Git Əmrləri (`git count-objects`, `git fsck`)**: Standartdan kənar sistem əmrləri icazə filtrlərini aşaraq təsdiq tələb edir.
   - **Layihədən Kənar Ayar Fayllarına Toxunmaq**: Sistemin qlobal konfiqurasiyasını (`config.json`) dəyişməyə cəhd etmək.
   - **Borularla Zəncirlənmiş Əmrlər (`cmd1 && cmd2 | grep ... | awk ...`)**: Mürəkkəb zəncirlər avtomatik təsdiq mexanizmini sıradan çıxarır.
   - **Hissə-Hissə İcra Edilən AppleScript/OS Əmrləri (`osascript -e '...'`)**: Brauzer və ya sistem yoxlanışı zamanı ard-arda onlarca tək-sətirli əmr icra etmək.

---

### 🛠️ Bu Bacarıq Problemləri Necə Həll Edir?

1. **Gözlənilməz Hallarda Fasiləsiz İrəliləmə və Sualları Sona Saxlama ("Davam Et və Hamısını Sonda Birdəfəlik Soruş")**: Gözlənilməz xəta və ya qeyri-müəyyənliklə qarşılaşdıqda agent heç vaxt işi ortada dayandırmır; təhlükəsiz standart qərarı seçir, digər bütün işləri tamamlayır və bütün sualları tapşırığın sonunda vahid hesabatda birdəfəlik təqdim edir.
2. **Müstəqil Test və Doğrulama Qərarı**: Agent "Test edimmi?" deyə soruşmur. Dəyişiklikləri lokal maketlər, vahid testləri və lokal loopback (`127.0.0.1`) ilə müstəqil yoxlamağı qərara alır və hesabat verir.
3. **Yalnız Lokal və Dəqiq Doğrulama**: Kodlar canlı saytlara və ya uzaq serverlərə sorğu göndərməklə deyil, lokal testlər və daxili build ilə yoxlanılır.
4. **Model və Paylama Mocking**: Mühakimə router-ləri və model şlüzləri uzaq serverə qoşulmadan lokal maketlərlə yoxlanılır.
5. **Lokal TTS və Səs Sintezi Mocking**: Səs sintezi xidmətləri (`TTSService`) və audio axını gecikmələri uzaq serverdə canlı test edilmək əvəzinə lokal asinxron mock-lar (`AsyncMock`) ilə yoxlanılır.
6. **Lokal Asılılıq və Paket Təhlili (Manifest Discovery)**: Paket versiyaları və asılılıqlar uzaq serverə SSH ilə `pip show`, `pip list` və ya `pip freeze` icra etməklə deyil, lokal manifest fayllarından (`requirements.txt`, `pyproject.toml`, `poetry.lock`, `package.json`, `Dockerfile`) oxunur.
7. **Tək Fayllı Skript Metodu (Single-Runner Batching)**: İstifadəçi brauzer seanslarını (Chrome, Safari, cPanel, bulud konsolları, Colab) və ya uzaq verilənlər bazasını yoxlamağı tapşırdıqda, agent dağınıq sətirlər işlətmir; layihədə vahid köməkçi skript (Python və ya AppleScript) hazırlayır, onu bir dəfə icra edir və strukturlaşmış JSON nəticəsini oxuyur.
8. **Statik Dağıtım Təhlili**: Portlar və konteynerlər canlı serverə bağlanmadan `docker-compose.yml` və `Dockerfile` fayllarından oxunur.
9. **Layihə İzolasiyası**: Qovluqdan kənar heç bir qlobal fayla toxunulmur.

---

### 🛡️ Tərtibatçı Bələdçisi: Tam Giriş İcazəsi (Full Access Setup)

Agentinizin heç bir təsdiq pəncərəsi açmadan tam avtonom işləməsini təmin etmək üçün:

#### 1. Google Antigravity
İstifadəçi qovluğundakı `~/.gemini/config/config.json` faylına prefiks icazələrini daxil edin:
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
Konfiqurasiya faylında avtomatik təsdiqlənən əmrləri qeyd edin:
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
`.cursorrules` və ya `.cursor/rules/discovery.mdc` daxilinə `templates/AGENTS.md` qaydalarını əlavə edin.

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
Və ya layihənizin `CLAUDE.md` faylına `templates/AGENTS.md` məzmununu əlavə edin.

### 3. Cursor
`.cursor/rules/discovery.mdc` faylını yaradın və ya `.cursorrules` daxilinə əlavə edin:
```markdown
Before making any code edits or asking questions, read and execute the discovery steps in SKILL.md.
Always begin your first response with the 4-part protocol (Understanding, Current State, Plan, Blocking Questions).
```

### 4. GitHub Copilot
`templates/AGENTS.md` məzmununu `.github/copilot-instructions.md` daxilinə əlavə edin.

### 5. İstənilən Layihədə Sürətli Başlanğıc (30 Saniyə)
```bash
curl -sSL https://raw.githubusercontent.com/tmolavi/agent-project-discovery-skill/main/templates/AGENTS.md -o AGENTS.md
```

---

## 📄 Lisenziya
Bu layihə açıq mənbəli [MIT](LICENSE) lisenziyası ilə yayımlanır. Şəxsi və kommersiya məqsədli istifadə üçün tamamilə pulsuzdur.
