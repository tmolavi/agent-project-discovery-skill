# Süni İntellekt Agentləri Üçün Layihə Kəşfi Bacarığı 🧭
### `agent-project-discovery-skill`

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v2.2.2-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/tmolavi/agent-project-discovery-skill/pulls)

> **"Süni intellekt agenti dəyişiklik etməzdən əvvəl layihəni dərindən anlamalıdır."**

Bu layihə kodlaşdırma agentləri (Claude Code, Cursor, Google Antigravity, OpenAI Codex, GitHub Copilot və s.) üçün universal və istehsala hazır başlanğıc bacarığıdır (startup skill). Agentlərin layihəni başa düşmədən tələsik kod dəyişdirməsinin, mövcud arxitekturanı pozmasının, lazımsız suallar verməsinin, gözlənilməz hallarda dayanıb qalmasının, test, marşrut, paket versiyası (`pip show edge-tts`), paket yüksəltmə (`pip install -U edge-tts`), serverdə docker-compose.yml və ya konfiqurasiya fayllarını oxumaq (`cat ... docker-compose.yml`), interfeys komponentləri (`cat ... components/MobileMenu.tsx`), STT provayder açarları və Groq Whisper, ad-hoc SCP fayl köçürmələri və konteyner yenidən başlatmaları (`docker restart hamzad-ara`), uzaq benchmark və qiymətləndirmə süitləri (`test_20_persian_utterances.py`), sağlamlıq marşrutları, konteyner loqları, əmr tarixçəsi və quraşdırma faylları (`/api/health`, `docker logs`, `history`, `ls .next`), SSH bağlantı təkrarı, uptime və əks-səda yoxlanışı (`Allow retrying SSH connection?`, `Allow testing SSH to hamzad_server?`), birləşdirilmiş server konteyner və git yoxlanışı (`Allow checking server molavi-pro container and git?`), uzaq xidmət bacarıqları siyahısı (`Allow listing Hermes skills?`), konteyner daxili .next qovluğu araşdırması (`Allow inspecting container .next directory?`), SCP ilə parça fayl və səhifə köçürmələri (`Allow copying components to server?`, `Allow copying page.tsx and robots.ts to server?`, `Allow copying robots.ts to server?`), server ana maşınında node və ya işləmə mühiti versiyası yoxlanışı (`Allow checking node on server host? ssh ... "node -v || true"`), serverdə docker imiclərinin yoxlanışı (`Allow checking docker images on server? ssh ... "docker images | grep ..."`), serverdə aktiv konteynerlərin siyahılanması (`Allow listing containers on hamzad_server? ssh ... "docker ps --format ..."`), qurma arxivinin SCP ilə serverə yüklənməsi (`Allow uploading build assets archive? scp ... /tmp/*.tar.gz ...`), konteynerlərarası servis bacarıqlarının sorğulanması (`Allow inspecting Hermes skills from hamzad-ara? ssh ... "docker exec ... http://staging-hermes:8090/api/v1/skills ..."`), resursların konteynerə paylanması və yenidən başladılması (`Allow deploying assets to container and restarting?`, `Allow verifying live production authentication suite?`, `Allow verifying live production login endpoint?`, `Allow testing production login with default passcode?`, `Allow testing SSH connectivity to hamzad_server?`, `Allow testing SSH connection with IPQoS=none?`, `Allow running live test?`, `Allow deploying updated code to production?`, `Allow deploying updated ARA files to production server?`, `Allow deploying updated files?`, `Allow executing deployment script? bash /tmp/deploy_molavi.sh`, `Allow deploying assets to hamzad_server?`), bütün Hermes bacarıqlarının siyahılanması (`Allow listing all Hermes skills?`), Hermes API marşrutlarının, docs və ya openapi.json faylının sorğulanması (`Allow checking Hermes API endpoints?`), konteyner tərkibi (`docker exec ... ls`), server git budaqlarını sıralama (`git branch -a`), server konteyner və git vəziyyəti (`docker ps && git status`), git budaq və commit tarixçəsi (`git branch && git log`), model paylama (central dispatch), yenilənmiş Edge-TTS və TTS nitq sintezi yoxlanışı (`Allow testing updated Edge-TTS?`, `Allow testing TTS synthesis speed?`) və ya STT nitqin mətnə çevrilməsi yoxlanışı (`Allow testing STT pipeline?`) üçün icazə istəməsinin və sizi daima ekran qarşısında təsdiq düymələrinə basmağa məcbur etməsinin qarşısını alır.

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
   - **Səs, TTS Sintez Sürəti və ya Yenilənmiş Edge-TTS Yoxlanışı Üçün İcazə İstəmək (`Allow testing TTS synthesis speed?`, `Allow testing updated Edge-TTS? ssh ...`)**: Agentin nitq sintezini, yenilənmiş Edge-TTS kitabxanasını və ya səs emal sürətini lokal mühitdə mock etmək əvəzinə canlı serverdə test etmək üçün icazə istəməsi.
   - **STT və Nitqin Mətnə Çevrilməsi Testi Üçün İcazə İstəmək (`Allow testing STT pipeline?`, `Allow checking STT providers?`, `Allow testing Groq Whisper STT?`):** Agentin audio transkripsiyası, provayder açarları və ya Groq Whisper xidmətlərini lokal mühitdə mock etmək əvəzinə canlı serverdə test etmək üçün icazə istəməsi.
   - **Paket və Asılılıq Versiyası Yoxlanışı Üçün İcazə İstəmək (`Allow checking edge-tts version? ssh ... "pip show ...")**: Agentin lokal asılılıq bəyannamələrini oxumaq əvəzinə uzaq mühitə SSH ilə `pip show` və ya `pip list` əmrləri göndərməsi.
   - **Paket Yüksəltmə və Dəyişdirmə Üçün İcazə İstəmək (`Allow upgrading edge-tts? ssh ... "pip install -U ...")**: Agentin lokal manifest fayllarını yeniləmək əvəzinə uzaq serverə SSH ilə `pip install -U` əmri icra etməyə cəhd etməsi.
   - **Server docker-compose.yml və Dağıtım Konfiqurasiyası Faylını Oxumaq Üçün İcazə İstəmək (`Allow viewing server docker-compose.yml? ssh ... "cat ... docker-compose.yml"`):** Agentin lokal iş mühitindəki `docker-compose.yml` və konfiqurasiya fayllarını birbaşa oxumaq əvəzinə uzaq serverə SSH ilə `cat` əmri icra etməyə cəhd etməsi.
   - **Konteyner Tərkibi və Qovluq Yoxlanışı Üçün İcazə İstəmək (`Allow checking container contents? ssh ... "docker exec ... ls -la /app"`):** Agentin lokal iş mühiti və `Dockerfile` direktivlərini araşdırmaq əvəzinə uzaq serverə SSH ilə `docker exec ... ls` icra etməyə cəhd etməsi.
   - **Server İnterfeys Komponenti və ya Mənbə Kodunu Oxumaq Üçün İcazə İstəmək (`Allow checking server MobileMenu.tsx? ssh ... "cat ... components/MobileMenu.tsx"`):** Agentin lokal iş sahəsindəki komponentləri araşdırmaq əvəzinə uzaq serverə SSH ilə `cat` əmri göndərməsi.
   - **SCP ilə Dağıtım və Konteyner Yeniden Başlatma Üçün İcazə İstəmək (`Allow deploying updated app files to production?`, `Allow restarting hamzad-ara container?`, `Allow deploying hermes_router and restarting container?`):** Dəyişiklikləri lokal olaraq yoxlamaq əvəzinə uzaq serverə tələsik `scp` və konteyner restart göndərmək.
   - **Uzaq Qiymətləndirmə və Benchmark Süiti İcrası Üçün İcazə İstəmək (`Allow running 20-utterance Persian evaluation suite?`, `Allow running full 20-utterance benchmark?`):** Testləri lokal mühitdə mock-larla icra etmək əvəzinə canlı serverdə konteyner daxilində icra etməyə cəhd etmək.
   - **Sağlamlıq Marşrutu, Konteyner Loqları, Əmr Tarixçəsi və ya Quraşdırma Qovluğu Üçün İcazə İstəmək (`Allow checking ARA health endpoint?`, `Allow checking container logs?`, `Allow checking hamzad-ara container logs?`, `Allow checking server command history?`, `Allow checking .next on server host?`):** Uzaq serverə `curl`, `docker logs`, `history` və ya `ls .next` göndərmək.
   - **SSH Bağlantı Təkrarı, Uptime və Əks-səda Yoxlanışı Üçün İcazə İstəmək (`Allow retrying SSH connection?`, `Allow testing SSH to hamzad_server?`):** Vaxtaşımı zamanı lokal iş sahəsinə keçmək əvəzinə uzaq serverə `uptime` və ya `echo` göndərməyə cəhd etmək.
   - **Birləşdirilmiş Konteyner və Git Vəziyyəti Yoxlanışı Üçün İcazə İstəmək (`Allow checking server molavi-pro container and git?`):** Uzaq serverə zəncirlənmiş SSH əmrləri göndərməyə cəhd etmək.
   - **Uzaq Xidmət Bacarıqları Siyahısı Üçün İcazə İstəmək (`Allow listing Hermes skills?`):** Uzaq serverdə `docker exec ... httpx.get` icra etmək əvəzinə lokal reyestr sənədlərini oxumamaq.
   - **Konteyner Daxili .next Qovluğu Araşdırması Üçün İcazə İstəmək (`Allow inspecting container .next directory?`):** Lokal build yoxlamaq əvəzinə konteyner daxilinə `ls -la /app/.next` göndərmək.
   - **SCP ilə Parça Fayl və Səhifə Köçürmələri Üçün İcazə İstəmək (`Allow copying components to server?`, `Allow copying page.tsx and robots.ts to server?`, `Allow copying robots.ts to server?`):** Git commit və rəsmi buraxılış skripti istifadə etmək əvəzinə nizamsız SCP istifadə etmək.
   - **Server Konteyner və Git Vəziyyəti Yoxlanışı Üçün İcazə İstəmək (`Allow checking server container and git status?`, `Allow checking server git branch and log?`, `Allow listing git branches on server?`, `Allow checking molavi-pro container on server?`):** Agentin lokal faylları və lokal git vəziyyətini yoxlamaq əvəzinə uzaq serverə SSH ilə qoşulub `docker ps`, `git status -s`, `git branch` və `git log` icra etməyə cəhd etməsi.
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
2. **Müstəqil Test və Doğrulama Qərarı**: Agent "Test edimmi?", "Allow retrying SSH connection?", "Allow checking server molavi-pro container and git?", "Allow listing Hermes skills?", "Allow inspecting container .next directory?" və ya "Allow copying components to server?" deyə soruşmur. Dəyişiklikləri lokal maketlər, vahid testləri və lokal loopback (`127.0.0.1`) ilə müstəqil yoxlamağı qərara alır və hesabat verir.
3. **Yalnız Lokal və Dəqiq Doğrulama**: Kodlar canlı saytlara və ya uzaq serverlərə sorğu göndərməklə deyil, lokal testlər və daxili build ilə yoxlanılır.
4. **Model və Paylama Mocking**: Mühakimə router-ləri və model şlüzləri uzaq serverə qoşulmadan lokal maketlərlə yoxlanılır.
5. **Lokal TTS, Səs Sintezi və Yenilənmiş Edge-TTS Mocking**: Səs sintezi xidmətləri (`TTSService`), yenilənmiş Edge-TTS kitabxanası və audio axını gecikmələri uzaq serverdə canlı test edilmək əvəzinə lokal asinxron mock-lar (`AsyncMock`) ilə yoxlanılır.
6. **Lokal Asılılıq və Paket Təhlili (Manifest Discovery)**: Paket versiyaları və asılılıqlar uzaq serverə SSH ilə `pip show`, `pip list` və ya `pip freeze` icra etməklə deyil, lokal manifest fayllarından (`requirements.txt`, `pyproject.toml`, `poetry.lock`, `package.json`, `Dockerfile`) oxunur.
7. **Lokal Paket Yüksəltmə və Manifest İdarəetməsi**: Paket versiyalarının yüksəldilməsi canlı serverə SSH ilə `pip install -U` icra edilərək deyil, birbaşa lokal manifest fayllarında (`requirements.txt`, `pyproject.toml`) yenilənir və lokal testlərlə yoxlanılır.
8. **Lokal Konteyner və Git Vəziyyəti Təhlili**: Konteyner konfiqurasiyaları və portlar lokal manifest fayllarından (`docker-compose.yml`, `Dockerfile`), git budaq, bütün budaqlar (`git branch -a`), commit tarixçəsi və dəyişiklik vəziyyəti isə birbaşa lokal iş qovluğundan (`git status -s`, `git branch --show-current`, `git log -n 5`) oxunur; uzaq serverə SSH sorğusu göndərilmir.
9. **Lokal Konteyner Fayl Sistemi və Qovluq Təhlili**: Konteyner fayl sistemi iyerarxiyası və tətbiq yolları (`/app`, `/workspace`), uzaq serverdə `docker exec ... ls` əmrləri icra edilmədən birbaşa lokal iş sahəsi faylları, `Dockerfile` (WORKDIR, COPY direktivləri) və `docker-compose.yml` həcm (volume) təyinatları vasitəsilə araşdırılır.
10. **Lokal Dağıtım və docker-compose Manifest Təhlili**: `docker-compose.yml`, servis tərifləri, `Dockerfile` və mühit konfiqurasiyaları uzaq serverə SSH ilə `cat` və ya `less` göndərilmədən birbaşa lokal iş sahəsindən araşdırılır.
11. **Lokal STT, Provayderlər və Groq Whisper Mocking**: Nitqin mətnə çevrilməsi xidmətləri (`STTService`), `transcribe_audio_bytes` funksiyası, provayder açarları və Groq Whisper uzaq serverdə canlı test edilmək əvəzinə lokal asinxron mock-lar (`AsyncMock`) və süni audio baytları ilə yoxlanılır.
12. **Lokal Komponent və Mənbə Kodu Təhlili**: İnterfeys komponentləri (`components/MobileMenu.tsx`, `.tsx`, `.jsx`, `.vue`) və mənbə kodları uzaq serverə SSH ilə `cat` göndərilmədən birbaşa lokal iş sahəsindən araşdırılır.
13. **Lokal Dağıtım İdarəetməsi və SCP Qadağası**: Dəyişikliklər lokal mühitdə hazırlanır və paketlənir; tapşırıq ortasında uzaq serverə plansız `scp` göndərilmir və konteynerlər yenidən başladılmır.
14. **Lokal Qiymətləndirmə və Benchmark Süiti İcrası**: Çoxsaylı cümlə qiymətləndirmə və benchmark skriptləri (`test_20_persian_utterances.py`) uzaq serverə yüklənmədən lokal mock məlumatları ilə yoxlanılır.
15. **Lokal Diaqnostika, Sağlamlıq, Loqlar və Quraşdırma Faylları**: Sağlamlıq marşrutları (`/api/health`), konteyner loqları, əmr tarixçəsi və quraşdırma çıxışları (`.next`) uzaq serverə bağlanmadan lokal kod və loqlardan araşdırılır.
16. **Avtomatik SSH Ehtiyat Planı və Uptime Sorğusu Qadağası:** SSH vaxtaşımı və ya əlaqə kəsilməsində agent istifadəçini yenidən cəhd və ya uptime sorğuları ilə dayandırmır; dərhal lokal yoxlamaya və maketlərə keçir, çatışmazlığı tapşırıq sonundakı hesabatda qeyd edir.
17. **Birləşdirilmiş Əmrlərin Ayrılması:** Konteyner arxitekturası manifestlərdən statik olaraq, git budaq və commit vəziyyəti isə birbaşa lokal olaraq araşdırılır; zəncirlənmiş SSH əmrləri icra edilmir.
18. **Lokal Mikroservis Bacarıqları Kəşfi:** Servis bacarıqları (məsələn, Hermes) uzaq API çağırışları (`docker exec ... httpx.get`) əvəzinə birbaşa lokal reyestr manifestlərindən (`hermes-skill-discovery-registry-v1.json`) oxunur.
19. **Konteyner Daxili .next Əvəzinə Lokal Build Doğrulaması:** Build çıxışları və `.next/` qovluğu konteyner daxilinə bağlanmadan birbaşa lokal build (`npm run build`) vasitəsilə yoxlanılır.
20. **Git Əsaslı Buraxılış və SCP ilə Əllə Köçürmənin Ləğvi:** Bütün kod dəyişiklikləri git commit kimi qeyd edilir və server dağıtımları plansız SCP əvəzinə yalnız rəsmi buraxılış skripti (`deploy.sh`) ilə aparılır.
21. **Lokal İşləmə Mühiti və Konfiqurasiya Kəşfi:** Node.js və ya Python mühit tələbləri birbaşa lokal `package.json` (`engines`), `.nvmrc` və `Dockerfile` fayllarından oxunur; uzaq server ana maşınına `node -v` əmrləri göndərilmir.
22. **Lokal Docker İmicləri və Teqlər Kəşfi:** Docker imic tərifləri və baza imicləri birbaşa lokal `docker-compose.yml` və `Dockerfile` fayllarından araşdırılır; uzaq serverə `docker images` əmrləri göndərilmir.
23. **Lokal Konteyner Topologiyası Kəşfi:** Xidmət və konteyner adları, port təyinatları birbaşa lokal `docker-compose.yml` və `Dockerfile` fayllarından araşdırılır; uzaq serverə `docker ps --format ...` göndərilmir.
24. **Lokal Qurma Doğrulaması və SCP Arxiv Qadağası:** Qurma nəticələri birbaşa lokal olaraq yoxlanılır və serverə paylanma plansız SCP arxivləri əvəzinə rəsmi buraxılış skripti (`deploy.sh`) ilə aparılır.
25. **Konteynerlərarası Servis Kəşfi və Lokal Mocking:** Mikroservis bacarıqları və daxili marşrutlar birbaşa lokal reyestr sənədlərindən (`hermes-skill-discovery-registry-v1.json`, `docker-compose.yml`) oxunur və lokal olaraq mock edilir.
26. **Atomik Paylanma və Konteyner Qaynar Yama Qadağası:** Konteyner yeniləmələri plansız parçalı SSH əmrləri və ya müvəqqəti dağıtım skriptləri (`/tmp/deploy_molavi.sh`) əvəzinə rəsmi buraxılış skripti (`deploy.sh`) ilə aparılır.
27. **Statik Bacarıq Kataloqu Kəşfi:** Mikroservis bacarıqları birbaşa lokal reyestr sənədlərindən (`hermes-skill-discovery-registry-v1.json`) oxunur; uzaq serverdə skript icra edilmir.
28. **Statik API Marşrutları və Sxem Kəşfi:** API marşrutları və sxemləri birbaşa lokal mənbə kodlarından araşdırılır; serverdəki `/docs` və ya `/openapi.json` ünvanlarına SSH sorğuları göndərilmir.
29. **Statik Başlıq və Meta Məlumat Yoxlanışı:** Səhifə başlıqları və HTML teqləri ictimai URL sorğuları (`curl`) əvəzinə birbaşa lokal mənbə fayllarından (`layout.tsx`, `index.html`) araşdırılır.
30. **Lokal WebSocket və Oyanma Sözü Testi:** WebSocket axınları və oyanma sözü hadisələri (`wake_detected`) canlı konteyner əvəzinə birbaşa lokal test vasitələri ilə yoxlanılır.
31. **Mikroservis Marşrutlarının Lokal Kəşfi və Mock Edilməsi:** Mikroservis yolları və sağlamlıq marşrutları birbaşa lokal koddan araşdırılır və uzaq SSH zondlama dövrələri əvəzinə lokal mock müştəriləri ilə test edilir.
32. **Git Əsaslı Buraxılış və Çoxfayllı SCP / SSH Cat Qadağası:** Dəyişikliklər git commit kimi saxlanılır və paylanma parçalı SCP və ya `ssh cat >` əvəzinə rəsmi buraxılış skripti (`deploy.sh`) ilə aparılır.
33. **Tək Fayllı Skript Metodu (Single-Runner Batching)**: İstifadəçi brauzer seanslarını (Chrome, Safari, cPanel, bulud konsolları, Colab) və ya uzaq verilənlər bazasını yoxlamağı tapşırdıqda, agent dağınıq sətirlər işlətmir; layihədə vahid köməkçi skript (Python və ya AppleScript) hazırlayır, onu bir dəfə icra edir və strukturlaşmış JSON nəticəsini oxuyur.
34. **Statik Dağıtım Təhlili**: Portlar və konteynerlər canlı serverə bağlanmadan `docker-compose.yml` və `Dockerfile` fayllarından oxunur.
35. **Layihə İzolasiyası**: Qovluqdan kənar heç bir qlobal fayla toxunulmur.

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
