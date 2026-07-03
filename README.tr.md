🌍 [English](README.md) | [Türkçe](README.tr.md) | [Español](README.es.md)

# 🥧 Pi Coding Agent — Genel Kullanım Kılavuzu

> **İş akışınıza ayak uyduran minimal, terminal tabanlı yapay zeka kodlama yardımcısı.**

<div align="center">

![Sürüm](https://img.shields.io/badge/version-0.80.3-blue)
![Lisans](https://img.shields.io/badge/license-MIT-green)
![GitHub Stars](https://img.shields.io/github/stars/earendil-works/pi?style=social)

</div>

---

## 📚 İçindekiler

- [Pi Nedir?](#pi-nedir)
- [Kurulum](#kurulum)
- [Hızlı Başlangıç](#hızlı-başlangıç)
- [Etkileşimli Mod (TUI)](#etkileşimli-mod-tui)
- [Sağlayıcılar ve Modeller](#sağlayıcılar-ve-modeller)
- [Oturumlar](#oturumlar)
- [Özelleştirme](#özelleştirme)
- [Ayarlar](#ayarlar)
- [CLI Referansı](#cli-referansı)
- [İpuçları ve Hileler](#ipuçları-ve-hileler)
- [Kaynaklar](#kaynaklar)
- [Hızlı Başvuru Kartı](#hızlı-başvuru-kartı)

---

## Pi Nedir?

**Pi**, Node.js ve TypeScript ile oluşturulmuş minimal, terminal tabanlı bir yapay zeka kodlama aracıdır. Büyük Dil Modellerini (LLM) yerel dosyalarınıza ve kabuğunuza bağlar: **read** (oku), **write** (yaz), **edit** (düzenle) ve **bash** (terminal).

---

## Kurulum

### npm ile (Önerilen)
```bash
npm install -g --ignore-scripts @earendil-works/pi-coding-agent
```

### Kurulum Betiği (curl) ile
```bash
curl -fsSL https://pi.dev/install.sh | sh
```

### 🪟 Windows (WinGet)
```powershell
winget install EarendilWorks.pi
```

---

## Hızlı Başlangıç

### 1. API Anahtarını Tanımlama
```bash
export ANTHROPIC_API_KEY=sk-ant-... # Linux/macOS
$env:ANTHROPIC_API_KEY="sk-ant-..." # Windows PowerShell
```

### 2. Pi'yi Başlatma
```bash
pi
```

---

## Hızlı Başvuru Kartı

```
┌──────────────────────────────────────────────────────────┐
│                     🥧 Pi Hızlı Başvuru                  │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  BAŞLAT                    YÖNET                         │
│  pi              .......  TUI Başlat      /new           │
│  pi "prompt"     .......  Prompt ile      /resume        │
│  pi -p "..."     .......  Tek seferlik    /tree          │
│  pi -c           .......  Devam et        /quit          │
│  pi -r           .......  Listeden seç                   │
│                                                          │
│  EDİTÖR                    ÖZELLEŞTİR                    │
│  @dosya          .......  Dosya ekle      /reload        │
│  !komut          .......  Bash çalıştır   Eklentiler     │
│  Shift+Enter     .......  Yeni satır      Yetenekler     │
│  Ctrl+V          .......  Görsel yapıştır Şablonlar      │
│  Escape          .......  İptal et        Temalar        │
│                                                          │
│  MODEL                     OTURUM                        │
│  Ctrl+L          .......  Model Seç       /session       │
│  Ctrl+P          .......  Model Değiştir  /compact       │
│  Shift+Tab       .......  Düşünme Seviye  /export        │
│  /model          .......  Modeli Güncelle                │
│                                                          │
│  MESAJ KUYRUĞU              ARAÇLAR                      │
│  Enter (stream)  .......  Yönlendir        read          │
│  Alt+Enter       .......  Takip et         write         │
│  Alt+Up          .......  Geri al          edit          │
│                                            bash          │
│                                            grep          │
│                                            find          │
│                                            ls            │
└──────────────────────────────────────────────────────────┘
```
