# Yapay Zeka Ajanları İçin Proje Keşif Yeteneği 🧭
### `agent-project-discovery-skill`

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Release](https://img.shields.io/badge/release-v1.1.0-emerald.svg)](https://github.com/tmolavi/agent-project-discovery-skill/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/tmolavi/agent-project-discovery-skill/pulls)

> **"Bir yapay zeka ajanı, değişiklik yapmadan önce projeyi derinlemesine anlamalıdır."**

Bu proje, kodlama yapan yapay zeka ajanları (Claude Code, Cursor, Google Antigravity, OpenAI Codex, GitHub Copilot vb.) için evrensel, üretime hazır bir başlangıç becerisidir (startup skill). Ajanların projeyi anlamadan aceleyle kod değiştirmesini, çalışan sistemleri baştan yazmasını, gereksiz sorular sormasını ve sizi sürekli ekran başında onay butonlarına basmak zorunda bırakmasını engeller.

---

## 🌍 Diller / Languages
[English](README.md) | [فارسی](README.fa.md) | [Türkçe](README.tr.md) | [Azərbaycanca](README.az.md) | [العربية](README.ar.md)

---

## 🎯 Bu Beceri Neden Geliştirildi? (Gece Boyu Otonom Çalışma)

Yapay zeka asistanı kullanmanın asıl amacı **görevi verip uyumak**, sabah kalktığınızda işin tamamlanmış olduğunu görmektir. Sizi sabaha kadar ekran başında tutup sürekli *"Şunu çalıştırayım mı?"*, *"Onaylıyor musunuz?"* diye sorması yapay zekanın mantığına aykırıdır!

Bu beceri olmadan ajanların yaptığı kritik hatalar:
1. **Keşif Yapmadan Kod Değiştirme:** Proje yapısını, paketleri veya mimariyi incelemeden rastgele dosyalarda değişiklik yapmaya başlarlar.
2. **Gereksiz ve Bunalten Sorular:** *"Kod nerede?"*, *"Yapılandırma dosyası hangisi?"*, *"Ne yapmalıyım?"* gibi kod tabanında zaten cevabı olan sorular sorarlar.
3. **Sürekli Güvenlik ve Onay Pencereleri (Prompts):** Basit bir port veya konteyner kontrolü için gereksiz yere dış komutlar tetikleyip onayınızı beklerler.
4. **Kaydedilmemiş Değişiklikleri Ezme (Uncommitted Changes):** Geliştiricinin o anda üzerinde çalıştığı kodları fark etmeden siler veya üzerine yazarlar.
5. **Var Olan Kütüphaneleri Yeniden Yazma:** Projede zaten bulunan yardımcı fonksiyonları görmezden gelip sıfırdan gereksiz kodlar üretirler.

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
Veya projenizdeki `CLAUDE.md` dosyasına ekleyin.

### 3. Cursor
`.cursor/rules/discovery.mdc` oluşturun veya `.cursorrules` dosyasına ekleyin:
```markdown
Before making any code edits or asking questions, read and execute the discovery steps in SKILL.md.
Always begin your first response with the 4-part protocol (Understanding, Current State, Plan, Blocking Questions).
```

### 4. GitHub Copilot
`templates/AGENTS.md` içeriğini `.github/copilot-instructions.md` içerisine yerleştirin.

### 5. Herhangi Bir Projede Hızlı Başlangıç (30 Saniye)
```bash
curl -sSL https://raw.githubusercontent.com/tmolavi/agent-project-discovery-skill/main/templates/AGENTS.md -o AGENTS.md
```

---

## 📄 Lisans
Bu proje [MIT Lisansı](LICENSE) ile dağıtılmaktadır. Kişisel, kurumsal ve ticari projelerde özgürce kullanılabilir.
