🌍 [English](README.md) | [Türkçe](README.tr.md) | [Español](README.es.md)

# 🥧 Pi Coding Agent — Guía General de Usuario

> **El asistente de codificación minimalista basado en terminal que se adapta a tu flujo de trabajo.**

<div align="center">

![Versión](https://img.shields.io/badge/version-0.80.3-blue)
![Licencia](https://img.shields.io/badge/license-MIT-green)
![GitHub Stars](https://img.shields.io/github/stars/earendil-works/pi?style=social)

</div>

---

## 📚 Tabla de Contenidos

- [¿Qué es Pi?](#qué-es-pi)
- [Instalación](#instalación)
- [Inicio Rápido](#inicio-rápido)
- [Modo Interactivo (TUI)](#modo-interactivo-tui)
- [Proveedores y Modelos](#proveedores-y-modelos)
- [Sesiones](#sesiones)
- [Personalización](#personalización)
- [Ajustes](#ajustes)
- [Referencia de CLI](#referencia-de-cli)
- [Consejos y Trucos](#consejos-y-trucos)
- [Recursos](#recursos)
- [Tarjeta de Referencia Rápida](#tarjeta-de-referencia-rápida)

---

## ¿Qué es Pi?

**Pi** es un arnés de agente de codificación mínimo basado en terminal creado con Node.js y TypeScript. Conecta modelos de lenguaje (LLM) a sus archivos locales y shell mediante cuatro herramientas: **read** (leer), **write** (escribir), **edit** (editar) y **bash** (terminal).

---

## Instalación

### Vía npm (Recomendado)
```bash
npm install -g --ignore-scripts @earendil-works/pi-coding-agent
```

### Vía script de instalación (curl)
```bash
curl -fsSL https://pi.dev/install.sh | sh
```

### 🪟 Windows (WinGet)
```powershell
winget install EarendilWorks.pi
```

---

## Inicio Rápido

### 1. Configurar la clave API
```bash
export ANTHROPIC_API_KEY=sk-ant-... # Linux/macOS
$env:ANTHROPIC_API_KEY="sk-ant-..." # Windows PowerShell
```

### 2. Iniciar Pi
```bash
pi
```

---

## Tarjeta de Referencia Rápida

```
┌──────────────────────────────────────────────────────────┐
│                 🥧 Referencia Rápida de Pi               │
├──────────────────────────────────────────────────────────┤
│                                                          │
│  INICIO                    GESTIONAR                     │
│  pi              .......  Iniciar TUI     /new           │
│  pi "prompt"     .......  Con prompt      /resume        │
│  pi -p "..."     .......  Una respuesta   /tree          │
│  pi -c           .......  Continuar       /quit          │
│  pi -r           .......  Seleccionar                    │
│                                                          │
│  EDITOR                    PERSONALIZAR                  │
│  @archivo        .......  Ref. archivo    /reload        │
│  !comando        .......  Ejecutar bash   Extensiones    │
│  Shift+Enter     .......  Nueva línea     Habilidades    │
│  Ctrl+V          .......  Pegar imagen    Plantillas     │
│  Escape          .......  Cancelar        Temas          │
│                                                          │
│  MODELO                    SESIÓN                        │
│  Ctrl+L          .......  Sel. modelo     /session       │
│  Ctrl+P          .......  Ciclar modelos  /compact       │
│  Shift+Tab       .......  Nivel de pensar /export        │
│  /model          .......  Cambiar modelo                 │
│                                                          │
│  COLA DE MENSAJES           HERRAMIENTAS                 │
│  Enter (stream)  .......  Dirigir          read          │
│  Alt+Enter       .......  Seguimiento      write         │
│  Alt+Up          .......  Recuperar        edit          │
│                                            bash          │
│                                            grep          │
│                                            find          │
│                                            ls            │
└──────────────────────────────────────────────────────────┘
```
