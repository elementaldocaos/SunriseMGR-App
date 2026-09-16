# 🌅 SunriseRMGR — Institutional Trading Governance Cockpit

[![License: Proprietary](https://img.shields.io/badge/License-Proprietary-red.svg)](LICENSE)
[![Platform: MetaTrader 5](https://img.shields.io/badge/MetaTrader-5-blue.svg)](https://www.metatrader5.com)
[![Architecture: Native Rust](https://img.shields.io/badge/Architecture-Native%20Rust%20%28x64%29-orange.svg)](https://www.rust-lang.org)

**SunriseRMGR** é uma plataforma institucional de governança de risco, conciliação forense e auditoria de execução para traders de alta performance no **MetaTrader 5 (MT5)**.

Projetado sob a premissa de **anti-euforia e soberania operacional**, o sistema atua como um cockpit analítico em tempo real (acoplado lado a lado ao MT5) para prevenir o *overtrading*, eliminar o *revenge trading* e registrar teses operacionais em ledger criptográfico imutável.

---

## ⚡ Pilares da Arquitetura

1. **Cockpit Magnético Win32**: Acoplamento automático lado a lado com a janela do MetaTrader 5 (proporção de tela institucional).
2. **Agente Sentinela de Telemetria (AuditorSentinela.ex5)**: Monitoramento contínuo de ordens ativas, cálculo de MAE/MFE e sincronização bidirecional via loopback local seguro (127.0.0.1:7482).
3. **Ledger Forense Imutável**: Gravação de cada entrada ($) com tese em texto livre do trader e confrontação pós-trade ($) com encadeamento de integridade SHA-256.
4. **Governança Comportamental Anti-Tilt**: Detecção de desvios de disciplina, infrações de stop loss (*stop tampering*), alavancagem desproporcional (*martingale*) e encerramento por pânico.

---

## 🚀 Como Instalar e Executar

Para instruções passo a passo de instalação, consulte o [Guia de Instalação](docs/INSTALLATION.md).

Para o manual completo de operação das abas da interface, consulte o [Manual do Usuário](docs/MANUAL.md).

---

## 🛡️ Propriedade Intelectual & Isenção de Responsabilidade

O SunriseRMGR é uma ferramenta analítica de disciplina e governança forense. O software **NÃO fornece sinais automatizados de compra ou venda** e **NÃO realiza gestão discricionária de capital**. Os modelos matemáticos internos são compilados nativamente em código fechado para proteção institucional.

© 2026 SunriseMGR Core. Todos os direitos reservados.
