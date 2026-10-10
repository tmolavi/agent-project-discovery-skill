# Yapay Zeka Ajanları İçin Proje Keşif Yeteneği 🧭
### `agent-project-discovery-skill`

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v1.3.0-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/tmolavi/agent-project-discovery-skill/pulls)

> **"Bir yapay zeka ajanı, değişiklik yapmadan önce projeyi derinlemesine anlamalıdır."**

Bu پروژه, kodlama yapan yapay zeka ajanları (Claude Code, Cursor, Google Antigravity, OpenAI Codex, GitHub Copilot vb.) için evrensel, üretime hazır bir başlangıç becerisidir (startup skill). Ajanların projeyi anlamadan aceleyle kod değiştirmesini, çalışan sistemleri baştan yazmasını, gereksiz sorular sormasını, test için izin istemesini ve sizi sürekli ekran başında onay butonlarına basmak zorunda bırakmasını engeller.

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
   - **Rutin Test Onayı İsteme (`Allow testing /api/... ?`)**: Ajanın bağımsız karar vermek yerine test çalıştırmak veya SSH betiği çalıştırmak için kullanıcıyı durdurup onay beklemesi.
   - **Kum Havuzunu Aşma Talebi (`BypassSandbox: true`)**: Ajanın ham ağ erişimi veya disk geneline erişim talep etmesi ve buna uygun izin kuralının tanımlı olmaması.
   - **Canlı Genel URL'leri Sorgulamak (`curl https://...`)**: Kod doğrulaması için canlı internet sitelerine HTTP istekleri atılması.
   - **Gereksiz Uzak Sunucu Sorguları (`ssh`, `scp`, uzak `docker images`)**: Konfigürasyon dosyalarını okumak yerine canlı sunuculara veya GitHub'a SSH ile bağlanmaya çalışılması.
   - **Derin Git Sıhhat Komutları (`git count-objects`, `git fsck`)**: Standart dışı dahili komutlar izin filtrelerini aşar ve onay gerektirir.
   - **Proje Dışı Ayar Dosyalarını Değiştirme**: Sistemin genel ayarlarını veya IDE konfigürasyonunu (`config.json`) kurcalamaya çalışmak.
   - **Boru Hattı ile Zincirlenmiş Kabuk Komutları (`cmd1 && cmd2 | grep ... | awk ...`)**: Karmaşık zincirler IDE'nin ön ek eşleştirme mekanizmasını bozar.
   - **Parçalı Tarayıcı / AppleScript Kodları (`osascript -e '...'`)**: Tarayıcı sekmelerini veya masaüstünü sorgularken parça parça onlarca satır çalıştırmak.

---

### 🛠️ Bu Beceri Sorunları Nasıl Çözer?

1. **Bağımsız Test ve Doğrulama Kararı**: Ajan "Uç noktayı test edeyim mi?" diye sormaz. Değişiklikleri yerel mock'lar, birim testleri ve yerel döngü (`127.0.0.1`) ile kendisi doğrulamaya karar verir ve raporlar.
2. **Yalnızca Yerel ve Belirleyici Doğrulama**: Kodlar canlı genel sitelere veya uzak sunuculara istek atılarak değil; yerel testler ve derleme çıktıları üzerinden doğrulanır.
3. **Tek Dosyalı Otomasyon (Single-Runner Batching)**: Kullanıcı tarayıcı oturumlarını (Chrome, Safari, cPanel, bulut panelleri, Colab) veya uzak veritabanlarını incelemeyi istediğinde, ajan parçalı komutlar çalıştırmak yerine tek bir yardımcı betik (Python veya AppleScript) yazar, bunu tek seferde çalıştırır ve yapılandırılmış JSON çıktısını işler.
4. **Statik Dağıtım Analizi**: Konteynerler ve portlar canlı sunucuya bağlanmadan, `docker-compose.yml` ve `Dockerfile` dosyalarından okunur.
5. **Proje İzolasyonu**: Çalışma alanı dışındaki hiçbir dosya değiştirilmez.

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
