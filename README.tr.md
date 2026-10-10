# Yapay Zeka Ajanları İçin Proje Keşif Yeteneği 🧭
### `agent-project-discovery-skill`

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v2.0.1-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/tmolavi/agent-project-discovery-skill/pulls)

> **"Bir yapay zeka ajanı, değişiklik yapmadan önce projeyi derinlemesine anlamalıdır."**

Bu proje, kodlama yapan yapay zeka ajanları (Claude Code, Cursor, Google Antigravity, OpenAI Codex, GitHub Copilot vb.) için evrensel, üretime hazır bir başlangıç becerisidir (startup skill). Ajanların projeyi anlamadan aceleyle kod değiştirmesini, çalışan sistemleri baştan yazmasını, gereksiz sorular sormasını, öngörülmeyen durumlarda durup kalmasını, test, rota, paket sürümü (`pip show edge-tts`), paket yükseltme (`pip install -U edge-tts`), sunucuda docker-compose.yml veya konfigürasyon görüntüleme (`cat ... docker-compose.yml`), sunucuda arayüz bileşenlerini ve kaynak kodları görüntüleme (`Allow checking server MobileMenu.tsx? cat ... components/MobileMenu.tsx`), STT sağlayıcıları ve anahtar kontrolü (`Allow checking STT providers?`), Groq Whisper testi (`Allow testing Groq Whisper STT?`), SCP ile dosya dağıtımı ve konteyner yeniden başlatma (`Allow deploying updated app files to production?`, `Allow restarting hamzad-ara container?`), uzak benchmark ve değerlendirme süiti çalıştırma (`Allow running 20-utterance Persian evaluation suite?`), sağlık kontrolü, konteyner logları, komut geçmişi veya sunucu `.next` dizini sorgulama (`Allow checking ARA health endpoint?`, `docker logs`, `history`, `ls .next`), SSH bağlantı tekrarı, uptime ve yankı testi (`Allow retrying SSH connection?`, `Allow testing SSH to hamzad_server?`), birleşik sunucu konteyner ve git kontrolü (`Allow checking server molavi-pro container and git?`), uzak servis yetenekleri listeleme (`Allow listing Hermes skills?`), konteyner içi .next dizini inceleme (`Allow inspecting container .next directory?`), SCP ile parça dosya ve sayfa kopyalama (`Allow copying components to server?`, `Allow copying page.tsx and robots.ts to server?`, `Allow copying robots.ts to server?`), sunucu ana makinesinde node veya çalışma zamanı sürümü kontrolü (`Allow checking node on server host? ssh ... "node -v || true"`), sunucuda docker imajları kontrolü (`Allow checking docker images on server? ssh ... "docker images | grep ..."`), sunucuda çalışan konteynerleri listeleme (`Allow listing containers on hamzad_server? ssh ... "docker ps --format ..."`), derleme arşivini SCP ile sunucuya yükleme (`Allow uploading build assets archive? scp ... /tmp/*.tar.gz ...`), konteynerler arası servis yetenekleri sorgulama (`Allow inspecting Hermes skills from hamzad-ara? ssh ... "docker exec ... http://staging-hermes:8090/api/v1/skills ..."`), varlıkları konteyner içine dağıtıp yeniden başlatma (`Allow deploying assets to container and restarting?`, `Allow deploying assets to hamzad_server?`), tüm Hermes yeteneklerini listeleme ve yazdırma (`Allow listing all Hermes skills?`), Hermes API uç noktalarını, docs veya openapi.json dosyasını sorgulama (`Allow checking Hermes API endpoints?`), konteyner içeriği (`docker exec ... ls`), sunucu git dallarını listeleme (`git branch -a`), sunucu konteyner ve git durumu (`docker ps && git status`, `Allow checking molavi-pro container on server?`), git branch ve commit geçmişi (`git branch && git log`), model dağıtım (central dispatch), güncellenmiş Edge-TTS ve TTS ses sentezi testi (`Allow testing updated Edge-TTS?`, `Allow testing TTS synthesis speed?`) veya STT konuşmayı metne dönüştürme testi (`Allow testing STT pipeline?`) kontrolü için izin istemesini ve sizi sürekli ekran başında onay butonlarına basmak zorunda bırakmasını engeller.

---

## 🌍 Diller / Languages
[English](README.md) | [فارسی](README.fa.md) | [Türkçe](README.tr.md) | [Azərbaycanca](README.az.md) | [العربية](README.ar.md)

---

## 🌙 "Rahat Uyu" Protokolü (Sleep-Well Protocol): Kesintisiz Gece Otonomisi

Bu projenin en temel tasarım hedefi şudur:
> **"Görevi yapay zekaya verin, dizüstü bilgisayarınızın kapağını kapatın ve rahatça uyuyun. Sabah kalktığınızda onay pencerelerine takılıp donmamış, temizce test edilmiş ve tamamlanmış bir iş teslim alın."**

---

### ❓ Ajanlar Neden Sürekli Onay Penceresi (Approval Modal) Açar?

Modern yapay zeka kodlama araçlarında (Google Antigravity, Claude Code, Cursor) yerleşik bir **Güvenli Kum Havuzu (Sandbox)** mimarisi bulunur:
1. **Kum Havuzu İçi Standart Komutlar (Standard Sandbox)**: Çalışma alanı içindeki dosya okuma/yazma işlemleri, yerel git durumları (`git status`, `git diff`), yerel derleme (`npm run build`, `cargo check`) ve yerel testler (`pytest`, `vitest`) **tamamen sessiz, otomatik ve kullanıcıdan onay istemeden** çalışır.
2. **Onay Penceresi Tetikleyen Durumlar**:
   - **Öngörülmeyen Durumlarda Durup Tek Tek Soru Sorma**: Ajanın diğer işleri bitirip soruları sona saklamak yerine çalışma ortasında sürekli duraklaması.
   - **Rutin Test Onayı İsteme (`Allow testing /api/... ?`)**: Ajanın bağımsız karar vermek yerine test çalıştırmak veya SSH betiği çalıştırmak için kullanıcıyı durdurup onay beklemesi.
   - **Model Yönlendirme ve Dağıtım Onayı İsteme (`Allow testing central model dispatch?`)**: Ajanın model ağ geçidini yerel ortamda mock'lamak yerine canlı sunucuda test etmek için onay sorması.
   - **Ses ve TTS Sentez Hızı veya Güncellenmiş Edge-TTS Testi Onayı İsteme (`Allow testing TTS synthesis speed?`, `Allow testing updated Edge-TTS? ssh ...`)**: Ajanın konuşma sentezi, güncellenmiş Edge-TTS veya ses işleme hızını yerel ortamda mock'lamak yerine uzak sunucuda canlı test etmek için onay sorması.
   - **STT ve Konuşmayı Metne Dönüştürme Testi Onayı İsteme (`Allow testing STT pipeline?`, `Allow checking STT providers?`, `Allow testing Groq Whisper STT?`):** Ajanın ses transkripsiyonu, sağlayıcı anahtarları veya Groq Whisper servislerini yerel ortamda mock'lamak yerine uzak sunucuda canlı test etmek için onay sorması.
   - **Paket ve Bağımlılık Sürümü Kontrolü İçin İzin İsteme (`Allow checking edge-tts version? ssh ... "pip show ...")**: Ajanın yerel bağımlılık bildirimlerini okumak yerine uzak ortama SSH ile `pip show` veya `pip list` komutları göndermesi.
   - **Paket Yükseltme ve Değiştirme İçin İzin İsteme (`Allow upgrading edge-tts? ssh ... "pip install -U ...")**: Ajanın yerel manifest dosyalarını güncellemek yerine uzak sunucuya SSH atıp `pip install -U` komutu çalıştırmaya çalışması.
   - **Sunucu docker-compose.yml ve Dağıtım Konfigürasyonunu Görüntüleme İçin İzin İsteme (`Allow viewing server docker-compose.yml? ssh ... "cat ... docker-compose.yml"`):** Ajanın yerel çalışma alanındaki `docker-compose.yml` ve konfigürasyon dosyalarını okumak yerine uzak sunucuya SSH atıp `cat` komutu çalıştırmaya çalışması.
   - **Konteyner İçeriği ve Dizin Kontrolü İçin İzin İsteme (`Allow checking container contents? ssh ... "docker exec ... ls -la /app"`):** Ajanın yerel çalışma alanı ve `Dockerfile` direktiflerini incelemek yerine uzak sunucuya SSH atıp `docker exec ... ls` çalıştırmaya çalışması.
   - **Sunucu Arayüz Bileşeni veya Kaynak Kodu Görüntüleme İçin İzin İsteme (`Allow checking server MobileMenu.tsx? ssh ... "cat ... components/MobileMenu.tsx"`):** Ajanın yerel çalışma alanındaki bileşenleri okumak yerine uzak sunucuya SSH atıp `cat` komutu çalıştırmaya çalışması.
   - **SCP ile Dosya Dağıtımı ve Konteyner Yeniden Başlatma Onayı İsteme (`Allow deploying updated app files to production?`, `Allow restarting hamzad-ara container?`):** Ajanın değişiklikleri yerel olarak doğrulamak yerine SSH/SCP ile uzak ortama dosya atıp konteyner yeniden başlatmaya çalışması.
   - **Uzak Değerlendirme ve Benchmark Çalıştırma Onayı İsteme (`Allow running 20-utterance Persian evaluation suite?`):** Ajanın testleri yerel ortamda yürütmek yerine canlı sunucuya SCP ile aktarıp konteyner içinde çalıştırmaya çalışması.
   - **Sağlık Kontrolü, Konteyner Logları veya Geçmiş Kontrolü İçin İzin İsteme (`Allow checking ARA health endpoint?`, `docker logs`, `history`, `ls .next`):** Ajanın yerel çıktıları incelemek yerine uzak sunucuda `curl`, `docker logs` veya `history` çalıştırmaya çalışması.
   - **SSH Bağlantı Tekrarı, Uptime ve Yankı Testi İçin İzin İsteme (`Allow retrying SSH connection?`, `Allow testing SSH to hamzad_server?`):** Zaman aşımı durumunda yerel çalışma alanına dönmek yerine uzak sunucuya `uptime` veya `echo` göndermeye çalışması.
   - **Birleşik Konteyner ve Git Durumu Kontrolü İçin İzin İsteme (`Allow checking server molavi-pro container and git?`):** Uzak sunucuya zincirlenmiş SSH komutları göndermeye çalışması.
   - **Uzak Servis Yetenekleri Listeleme İçin İzin İsteme (`Allow listing Hermes skills?`):** Uzak sunucuda `docker exec ... httpx.get` çalıştırmak yerine yerel kayıt dosyalarını okumaması.
   - **Konteyner İçi .next Dizini İnceleme İçin İzin İsteme (`Allow inspecting container .next directory?`):** Yerel derleme çıktısını doğrulamak yerine konteyner içine `ls -la /app/.next` göndermesi.
   - **SCP ile Parça Dosya ve Sayfa Kopyalama İçin İzin İsteme (`Allow copying components to server?`, `Allow copying page.tsx and robots.ts to server?`, `Allow copying robots.ts to server?`):** Git commit ve resmi dağıtım betiği kullanmak yerine rastgele SCP ile dosya kopyalaması.
   - **Sunucu Konteyner ve Git Durumu Kontrolü İçin İzin İsteme (`Allow checking server container and git status?`, `Allow checking server git branch and log?`, `Allow listing git branches on server?`, `Allow checking molavi-pro container on server?`):** Ajanın yerel dosyaları ve yerel git durumunu kontrol etmek yerine uzak sunucuya SSH atıp `docker ps`, `git status -s`, `git branch` ve `git log` çalıştırmaya çalışması.
   - **Rota ve Kod Kontrolü İçin İzin İsteme (`Allow checking model router endpoints?`)**: Ajanın yerel dosyaları okumak yerine uzak sunucuya SSH atıp rota dosyalarını parse etmeye çalışması.
   - **Kum Havuzunu Aşma Talebi (`BypassSandbox: true`)**: Ajanın ham ağ erişimi veya disk geneline erişim talep etmesi ve buna uygun izin kuralının tanımlı olmaması.
   - **Canlı Genel URL'leri Sorgulamak (`curl https://...`)**: Kod doğrulaması için canlı internet sitelerine HTTP istekleri atılması.
   - **Gereksiz Uzak Sunucu Sorguları (`ssh`, `scp`, uzak `docker images`)**: Konfigürasyon dosyalarını okumak yerine canlı sunuculara veya GitHub'a SSH ile bağlanmaya çalışılması.
   - **Derin Git Sıhhat Komutları (`git count-objects`, `git fsck`)**: Standart dışı dahili komutlar izin filtrelerini aşar ve onay gerektirir.
   - **Proje Dışı Ayar Dosyalarını Değiştirme**: Sistemin genel ayarlarını veya IDE konfigürasyonunu (`config.json`) kurcalamaya çalışmak.
   - **Boru Hattı ile Zincirlenmiş Kabuk Komutları (`cmd1 && cmd2 | grep ... | awk ...`)**: Karmaşık zincirler IDE'nin ön ek eşleştirme mekanizmasını bozar.
   - **Parçalı Tarayıcı / AppleScript Kodları (`osascript -e '...'`)**: Tarayıcı sekmelerini veya masaüstünü sorgularken parça parça onlarca satır çalıştırmak.

---

### 🛠️ Bu Beceri Sorunları Nasıl Çözer?

1. **Öngörülmeyen Durumlarda Kesintisiz İlerleme ve Soruları Sona Saklama ("Devam Et ve Hepsini Sonda Topluca Sor")**: Beklenmeyen bir hata veya belirsizlikle karşılaşıldığında ajan asla işi ortada durdurmaz; güvenli varsayılan kararı uygular, diğer tüm işleri tamamlar ve tüm soruları görevin sonunda tek bir raporda topluca iletir.
2. **Bağımsız Test ve Doğrulama Kararı**: Ajan "Uç noktayı test edeyim mi?", "Allow retrying SSH connection?", "Allow checking server molavi-pro container and git?", "Allow listing Hermes skills?", "Allow inspecting container .next directory?" veya "Allow copying components to server?" diye sormaz. Değişiklikleri yerel mock'lar, birim testleri ve yerel döngü (`127.0.0.1`) ile kendisi doğrulamaya karar verir ve raporlar.
3. **Yalnızca Yerel ve Belirleyici Doğrulama**: Kodlar canlı genel sitelere veya uzak sunuculara istek atılarak değil; yerel testler ve derleme çıktıları üzerinden doğrulanır.
4. **Model ve Dağıtım Mocking**: Akıl yürütme router'ları ve model dağıtım katmanları uzak sunucuya bağlanmadan yerel mock'lar ile test edilir.
5. **Yerel TTS, Ses Sentezi ve Güncellenmiş Edge-TTS Mocking**: Ses sentez servisleri (`TTSService`), güncellenmiş Edge-TTS kütüphanesi ve ses akışı gecikmeleri uzak sunucuda canlı test edilmek yerine yerel asenkron mock'lar (`AsyncMock`) ile doğrulanır.
6. **Yerel Bağımlılık ve Paket Analizi (Manifest Discovery)**: Paket sürümleri ve bağımlılıklar uzak sunucuya SSH ile `pip show`, `pip list` veya `pip freeze` çalıştırılarak değil, yerel manifest dosyalarından (`requirements.txt`, `pyproject.toml`, `poetry.lock`, `package.json`, `Dockerfile`) okunur.
7. **Yerel Paket Yükseltme ve Manifest Yönetimi**: Paket yükseltmeleri veya hata düzeltmeleri canlı sunucuya SSH ile `pip install -U` çalıştırılarak değil, doğrudan yerel manifest dosyalarında (`requirements.txt`, `pyproject.toml`) güncellenir ve yerel testlerle doğrulanır.
8. **Yerel Konteyner ve Git Durumu Analizi**: Konteyner mimarisi ve portlar yerel manifest dosyalarından (`docker-compose.yml`, `Dockerfile`), git branch, tüm dallar (`git branch -a`), commit geçmişi ve değişiklik durumu ise doğrudan yerel çalışma alanından (`git status -s`, `git branch --show-current`, `git log -n 5`) okunur; uzak sunucuya SSH atılmaz.
9. **Yerel Konteyner Dosya Sistemi ve Dizin Analizi**: Konteyner dosya sistemi hiyerarşisi ve uygulama yolları (`/app`, `/workspace`), uzak sunucuda `docker exec ... ls` komutları çalıştırılmadan doğrudan yerel çalışma alanı dosyaları, `Dockerfile` (WORKDIR, COPY direktifleri) ve `docker-compose.yml` hacim (volume) eşlemeleri üzerinden incelenir.
10. **Yerel Dağıtım ve docker-compose Manifest Analizi**: `docker-compose.yml`, servis tanımları, `Dockerfile` ve ortam konfigürasyonları uzak sunucuya SSH ile `cat` veya `less` gönderilmeden doğrudan yerel çalışma alanından incelenir.
11. **Yerel STT ve Konuşmayı Metne Dönüştürme Mocking**: Konuşmayı metne dönüştürme servisleri (`STTService`), `transcribe_audio_bytes` fonksiyonu, sağlayıcı anahtarları ve Groq Whisper uzak sunucuda test edilmek yerine yerel asenkron mock'lar (`AsyncMock`) ve sentetik ses baytları ile doğrulanır.
12. **Yerel Arayüz Bileşeni ve Kaynak Kod Analizi**: Arayüz bileşenleri (`components/MobileMenu.tsx`, `.tsx`, `.jsx`, `.vue`) ve kaynak kodlar uzak sunucuya SSH ile `cat` veya `less` gönderilmeden doğrudan yerel çalışma alanından incelenir.
13. **Yerel Dağıtım Yönetimi ve SCP Engeli**: Dosyalar yerel çalışma alanında hazırlanır ve paketlenir; görev ortasında uzak sunuculara rastgele `scp` veya `docker restart` komutları gönderilmez.
14. **Yerel Değerlendirme ve Benchmark Süiti Çalıştırma**: Çoklu cümle değerlendirme betikleri (`test_20_persian_utterances.py`) uzak üretim sunucularına yüklenmeden yerel mock verileriyle çalıştırılır.
15. **Yerel Teşhis ve Hata Ayıklama**: Sağlık rotaları (`/api/health`), konteyner logları, komut geçmişi ve derleme çıktıları (`.next`) uzak sunucuya bağlanılmadan yerel kod ve loglardan incelenir.
16. **Otomatik SSH Yedek Planı ve Uptime Testi Engeli:** SSH zaman aşımı veya bağlantı kopmasında ajan kullanıcıyı yeniden deneme veya uptime sorguları ile durdurmaz; derhal yerel doğrulamaya ve mock'lara geçer, erişim sorununu görev sonundaki rapora ekler.
17. **Birleşik Komutların Ayrıştırılması:** Konteyner mimarisi manifestlerden statik olarak, git branch ve commit durumu ise doğrudan yerel olarak incelenir; zincirlenmiş SSH komutları çalıştırılmaz.
18. **Yerel Mikroservis Yetenekleri Keşfi:** Servis yetenekleri (örneğin Hermes) uzak API çağrıları (`docker exec ... httpx.get`) yerine doğrudan yerel kayıt manifestlerinden (`hermes-skill-discovery-registry-v1.json`) okunur.
19. **Konteyner İçi .next Yerine Yerel Derleme Doğrulaması:** Derleme çıktıları ve `.next/` dizini konteyner içine bağlanılmadan, doğrudan yerel derleme (`npm run build`) ile doğrulanır.
20. **Git Tabanlı Sürüm ve SCP ile Manuel Kopyalamanın Kaldırılması:** Tüm kod değişiklikleri git commit olarak kaydedilir ve sunucu dağıtımları ad-hoc SCP yerine yalnızca resmi dağıtım betiği (`deploy.sh`) ile yapılır.
21. **Yerel Çalışma Zamanı ve Ortam Keşfi:** Node.js veya Python çalışma zamanı gereksinimleri doğrudan yerel `package.json` (`engines`), `.nvmrc` ve `Dockerfile` dosyalarından okunur; uzak sunucu ana makinesine `node -v` komutları gönderilmez.
22. **Yerel Docker İmajı ve Etiket Keşfi:** Docker imaj etiketleri ve temel imajlar doğrudan yerel `docker-compose.yml` ve `Dockerfile` dosyalarından incelenir; uzak sunucuya `docker images` veya grep komutları gönderilmez.
23. **Yerel Konteyner Topolojisi Keşfi:** Servis adları, konteyner adları ve port eşlemeleri doğrudan yerel `docker-compose.yml` ve `Dockerfile` dosyalarından incelenir; uzak sunucuya `docker ps --format ...` komutları gönderilmez.
24. **Yerel Derleme Doğrulaması ve SCP Arşiv Yükleme Engeli:** Derleme çıktıları yerel olarak doğrulanır ve sunucu dağıtımları rastgele SCP arşiv yüklemeleri yerine resmi dağıtım betiği (`deploy.sh`) üzerinden yürütülür.
25. **Konteynerler Arası Servis Keşfi ve Yerel Mocking:** Mikroservis yetenekleri ve dahili uç noktalar yerel kayıt manifestlerinden (`hermes-skill-discovery-registry-v1.json`, `docker-compose.yml`) okunur ve yerel olarak mock'lanır.
26. **Atomik Dağıtım ve Konteyner Sıcak Yama Engeli:** Konteyner güncellemeleri parçalı SSH komutları veya geçici dağıtım betikleri (`/tmp/deploy_molavi.sh`) yerine resmi dağıtım betiği (`deploy.sh`) üzerinden atomik olarak yürütülür.
27. **Statik Yetenek Kataloğu Keşfi:** Mikroservis yetenek listeleri doğrudan yerel kayıt dosyalarından (`hermes-skill-discovery-registry-v1.json`) okunur; uzak sunucuda yetenek tarama betikleri çalıştırılmaz.
28. **Statik API Rotası ve Şema Keşfi:** API uç noktaları ve şemaları doğrudan yerel kaynak kodlarından incelenir; sunucudaki `/docs` veya `/openapi.json` adreslerine SSH sorguları gönderilmez.
29. **Statik Başlık ve Meta Veri Doğrulaması:** Başlıklar ve HTML etiketleri canlı URL sorguları (`curl`) yerine doğrudan kaynak dosyalardan (`layout.tsx`, `index.html`) incelenir.
30. **Yerel WebSocket ve Uyandırma Kelimesi Testi:** WebSocket protokolleri, oturum akışları ve uyandırma kelimesi olayları (`wake_detected`) canlı konteynerler yerine doğrudan yerel mock istemcileri ile test edilir.
31. **Mikroservis Uç Noktalarını Yerel Keşfetme ve Mock Etme:** Mikroservis rotaları ve sağlık uç noktaları doğrudan yerel koddan incelenir ve uzak SSH tarama döngüleri yerine yerel mock istemcileri ile test edilir.
32. **Git Tabanlı Sürümleme ve Çoklu SCP/SSH Cat Engeli:** Değişiklikler git commit olarak kaydedilir ve dağıtımlar parçalı çok dosyalı SCP veya SSH cat yönlendirmeleri yerine resmi dağıtım betiği (`deploy.sh`) üzerinden yapılır.
33. **Tek Dosyalı Otomasyon (Single-Runner Batching)**: Kullanıcı tarayıcı oturumlarını (Chrome, Safari, cPanel, bulut panelleri, Colab) veya uzak veritabanlarını incelemeyi istediğinde, ajan parçalı komutlar çalıştırmak yerine tek bir yardımcı betik (Python veya AppleScript) yazar, bunu tek seferde çalıştırır ve yapılandırılmış JSON çıktısını işler.
34. **Statik Dağıtım Analizi**: Konteynerler ve portlar canlı sunucuya bağlanmadan, `docker-compose.yml` ve `Dockerfile` dosyalarından okunur.
35. **Proje İzolasyonu**: Çalışma alanı dışındaki hiçbir dosya değiştirilmez.

---

### 🛡️ Geliştirici Kılavuzu: Tam Erişim İzni (Full Access Setup)

Ajanınızın hiçbir onay penceresi açmadan tam otonom çalışmasını isterseniz:

#### 1. Google Antigravity
Kullanıcı ayarlarınızdaki `~/.gemini/config/config.json` dosyasına ön ek izinlerini ekleyin:
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
Proje veya kullanıcı konfigürasyonunuza otomatik onaylanan komutları ekleyin:
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
`.cursorrules` veya `.cursor/rules/discovery.mdc` içerisine `templates/AGENTS.md` kurallarını dahil edin.

---

## 🛡️ Becerinin 7 Temel İlkesi

1. **Uygulamadan Önce Proje Keşfi:** Dizin yapısı, `README`, mimari belgeleri (`docs/`), paket kilit dosyaları (`package.json`, `pnpm-lock.yaml`, `Cargo.lock`, `pyproject.toml`, `go.mod`), ortam değişkenleri (`.env.example`) ve CI/CD akışları eksiksiz taranır.
2. **Statik İnceleme Önceliği:** Portlar, servisler ve konteynerler doğrudan `docker-compose.yml`, `Dockerfile` ve reverse-proxy yapılandırmalarından okunur. Gereksiz ağ sorgularıyla sistem durdurulmaz.
3. **Git Durumunun Korunması:** Aktif dal (`branch`), `git status`, son commit geçmişi ve geliştiricinin henüz commit yapmadığı değişiklikler korunur.
4. **Zihinsel Model Oluşturma (Mental Model):** Kod yazmadan önce projenin işlevi, mimarisi, veri akışı ve test stratejisi eksiksiz modellenir.
5. **Gereksiz Soru Yasağı:** Kod tabanında aranabilecek hiçbir şey kullanıcıya sorulmaz. Sadece gerçek eksikliklerde veya geri dönüşü olmayan yıkıcı işlemlerde soru sorulur.
6. **Standart Mühendislik Yanıt Protokolü:** Ajan ilk yanıtında şu şablonu kullanır:
   - `## Understanding` (Proje özeti ve mimari keşif)
   - `## Current State` (Mevcut git durumu ve ilgili modüller)
   - `## Plan` (Adım adım minimal uygulama planı)
   - `## Blocking Questions` (Varsa yalnızca gerçek engeller, yoksa "None")
7. **Şeffaf Tamamlama Raporu (Completion Report):** Görev bittiğinde durum (`STATUS`), değişen dosyalar (`CHANGES`), doğrulama testleri (`VALIDATION`), canlıya alma durumu (`DEPLOYMENT`) ve kalan notlar (`REMAINING`) net olarak bildirilir.

---

## 🚀 Kurulum ve Entegrasyon

### 1. Google Antigravity
`SKILL.md` dosyasını yerel beceri klasörünüze kopyalayın:
```bash
mkdir -p ~/.gemini/config/skills/agent-project-discovery-skill
cp SKILL.md ~/.gemini/config/skills/agent-project-discovery-skill/SKILL.md
```

### 2. Claude Code
```bash
mkdir -p .claude/skills
cp SKILL.md .claude/skills/project-discovery.md
```
Veya projenizin `CLAUDE.md` dosyasına `templates/AGENTS.md` içeriğini ekleyin.

### 3. Cursor
`.cursor/rules/discovery.mdc` dosyasını oluşturun veya `.cursorrules` içerisine ekleyin:
```markdown
Before making any code edits or asking questions, read and execute the discovery steps in SKILL.md.
Always begin your first response with the 4-part protocol (Understanding, Current State, Plan, Blocking Questions).
```

### 4. GitHub Copilot
`templates/AGENTS.md` içeriğini `.github/copilot-instructions.md` içerisine ekleyin.

### 5. Herhangi Bir Projede Hızlı Başlangıç (30 Saniye)
```bash
curl -sSL https://raw.githubusercontent.com/tmolavi/agent-project-discovery-skill/main/templates/AGENTS.md -o AGENTS.md
```

---

## 📄 Lisans
Bu proje açık kaynaklı [MIT](LICENSE) lisansı ile sunulmaktadır. Bireysel ve kurumsal kullanım için tamamen ücretsizdir.
