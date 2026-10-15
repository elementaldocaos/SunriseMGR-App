# 🌅 SunriseRMGR — Institutional Trading Governance Cockpit

[![Release: v1.2.0-LTS](https://img.shields.io/badge/Release-v1.2.0--LTS-brightgreen.svg)](https://github.com/elementaldocaos/SunriseMGR-App/releases/tag/v1.2.0)
[![Platform: MetaTrader 5](https://img.shields.io/badge/Platform-MetaTrader%205%20%28x64%29-blue.svg)](https://www.metatrader5.com)
[![Architecture: Native Rust](https://img.shields.io/badge/Architecture-Native%20Rust%20%28Zero--GC%29-orange.svg)](https://www.rust-lang.org)
[![License: Proprietary](https://img.shields.io/badge/License-Proprietary-red.svg)](LICENSE)

**SunriseRMGR** é uma plataforma institucional de governança comportamental, conciliação forense e auditoria de execução para traders de alta performance no **MetaTrader 5 (MT5)**.

Projetado sob a premissa de **anti-euforia e soberania operacional**, o sistema opera como um cockpit analítico em tempo real acoplado magneticamente à janela do MT5 (proporção institucional de tela 75% MT5 / 25% Cockpit), prevenindo o *overtrading*, neutralizando o *revenge trading* e registrando teses operacionais em ledger criptográfico imutável.

---

## 📦 Downloads Oficiais (v1.2.0-LTS)

Acesse a página de [Releases Oficiais](https://github.com/elementaldocaos/SunriseMGR-App/releases/tag/v1.2.0) para baixar os binários pré-compilados para Windows x64:

| Pacote | Tipo | Descrição |
| :--- | :--- | :--- |
| **[`SunriseRMGR-v1.2.0-Windows-x64.zip`](https://github.com/elementaldocaos/SunriseMGR-App/releases/download/v1.2.0/SunriseRMGR-v1.2.0-Windows-x64.zip)** | **Instalador (Recomendado)** | Pacote completo com instalador automático em 1 clique (`Instalar-SunriseRMGR.bat`), ícones de alta resolução e atalhos na Área de Trabalho e Menu Iniciar. |
| **[`SunriseRMGR.exe`](https://github.com/elementaldocaos/SunriseMGR-App/releases/download/v1.2.0/SunriseRMGR.exe)** | **Executável Portátil** | Binário nativo único em Rust x64 (zero-install), pronto para execução imediata sem necessidade de instalação formal. |

---

## ⚡ Novidades & Engenharia da Versão 1.2.0-LTS

A versão **1.2.0-LTS** consolida meses de telemetria contínua e traz melhorias críticas de estabilidade, governança de ciclo de vida e eficiência de rede:

1. **Process Guard Pattern**: Implementação de guarda estrita via detecção de processos Win32 (`is_terminal_running`), eliminando o comportamento do SDK do MetaTrader 5 que reiniciava o terminal (`terminal64.exe`) involuntariamente quando o operador decidia fechá-lo.
2. **Resolução de TIME_WAIT Socket Storm**: Migração da telemetria IPC de conexões efêmeras para pool de conexões persistentes com `Connection: keep-alive`. Elimina 100% da exaustão de portas TCP efêmeras do Windows em operações de alta frequência.
3. **Sincronização Inicial Silenciosa**: Supressão de falsos alarmes $T_0$ na conexão inicial com ordens já abertas na conta antes da inicialização do Cockpit.
4. **WebView2 Power Governor**: Congelamento dinâmico da renderização e loops do DOM via `document.hidden`, derrubando o consumo de CPU e GPU para **0.0%** quando a janela estiver minimizada ou oculta.
5. **Runtime Tokio Single-Thread**: Contenção do orquestrador Rust em `.worker_threads(1)` para IPC loopback local (`127.0.0.1:7482`), reduzindo o footprint de memória para $< 30\text{ MB}$ e latência $< 15\text{ ms}$.
6. **System Tray & Encerramento Atômico**: Ícone persistente na área de notificação do Windows com encerramento em cascata do processo filho (`SENTINEL_CHILD_PID`), impedindo processos zumbis em segundo plano.
7. **Autostart no Registro do Windows**: Migração para inicialização nativa através de chave de registro do usuário (`HKCU\Software\Microsoft\Windows\CurrentVersion\Run`).

---

## 🏛️ Pilares da Arquitetura

```
┌──────────────────────────────────────────────────────────────┐
│                    DESKTOP DO OPERADOR                       │
├──────────────────────────────┬───────────────────────────────┤
│    METATRADER 5 (75%)        │      COCKPIT HUD (25%)        │
│                              │                               │
│  - Gráficos e Order Flow     │  - Live HUD (T0)              │
│  - Execução de Ordens        │  - Radar de Posição & MAE/MFE │
│  - AuditorSentinela.ex5      │  - Confluência Técnica        │
│         │ (HTTP WebRequest)  │  - Pós-Trade & Tese (T1)      │
│         ▼                    │  - Diário & Ledger SHA-256    │
│  127.0.0.1:7482              │                               │
└──────────────────────────────┴───────────────────────────────┘
```

1. **Cockpit Magnético Win32**: Acoplamento automático na lateral direita da tela (proporção 75/25) sem roubo de foco do teclado (`WS_EX_NOACTIVATE`).
2. **Auto-Discovery & Auto-Deploy**: Na primeira execução, o executável varre as instalações ativas do MetaTrader 5 e implanta compulsoriamente o robô `AuditorSentinela.ex5` na pasta de Experts.
3. **Ledger Forense Imutável**: Gravação de cada entrada ($T_0$) com tese declarada pelo trader e confrontação no encerramento ($T_1$) com encadeamento criptográfico SHA-256 em banco SQLite local.
4. **Governança Anti-Tilt**: Monitoramento de violações de disciplina: *Stop Loss Tampering* (afastamento do stop), *Revenge Trading*, *Martingale / Tilt Sizing* e encerramento por pânico.

---

## 🚀 Como Instalar e Executar (Guia Rápido)

### Passo 1: Instalação do Aplicativo
1. Baixe o pacote **`SunriseRMGR-v1.2.0-Windows-x64.zip`** e extraia para qualquer pasta.
2. Dê dois cliques em **`Instalar-SunriseRMGR.bat`** (o script criará a pasta em `%LOCALAPPDATA%\SunriseRMGR` e os atalhos no Desktop).
3. *(Opcional)* Se preferir o modo portátil, basta dar dois cliques diretamente em `SunriseRMGR.exe`.

### Passo 2: Habilitar WebRequest no MetaTrader 5
Para que o MT5 possa enviar telemetria em tempo real para o Cockpit:
1. No MetaTrader 5, pressione `Ctrl + O` (ou acesse **Ferramentas > Opções**).
2. Vá até a aba **Expert Advisors**.
3. Marque a caixa: `[x] Permitir WebRequest para as URLs listadas:`
4. Clique duas vezes no campo de texto e adicione exatamente a URL:
   ```
   http://127.0.0.1:7482
   ```
5. Clique em **OK**.

### Passo 3: Ativar o Auditor Sentinela
1. No MetaTrader 5, abra o Navegador pressionando `Ctrl + N`.
2. Clique com o botão direito em **Expert Advisors** e selecione **Atualizar**.
3. O robô **`AuditorSentinela`** aparecerá na lista.
4. Arraste o robô para qualquer gráfico ativo (ex: EURUSD, XAUUSD, WIN$, WDO$).
5. O Cockpit acoplará imediatamente e a supervisão institucional estará ativa!

Para mais detalhes e configurações avançadas, consulte o [Guia de Instalação](docs/INSTALLATION.md) e o [Manual de Operação](docs/MANUAL.md).

---

## 🛡️ Propriedade Intelectual & Isenção de Responsabilidade

O **SunriseRMGR** é um software analítico e forense de apoio à disciplina e governança operacional. O sistema **NÃO fornece recomendações ou sinais de investimento** e **NÃO realiza gestão discricionária de capital**. As decisões de compra e venda são de responsabilidade exclusiva do operador. O código nativo é compilado e assinado para proteção de modelos matemáticos institucionais.

© 2026 SunriseMGR Core · Todos os direitos reservados.  
*Suporte e Documentação Técnica:* [sepaulresearch.com](https://sepaulresearch.com)
