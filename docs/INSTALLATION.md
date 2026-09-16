# 📦 Guia de Instalação — SunriseRMGR

Siga os passos abaixo para configurar o SunriseRMGR e o MetaTrader 5.

---

## 1. Pré-requisitos
- **Sistema Operacional**: Windows 10 ou Windows 11 (64-bit).
- **Terminal**: MetaTrader 5 (qualquer corretora regulada).
- **Navegador**: Microsoft Edge ou Google Chrome (utilizado para renderizar a janela do Cockpit HUD no painel direito).

---

## 2. Configuração do MetaTrader 5

Para que o MetaTrader 5 envie a telemetria das ordens para o SunriseRMGR local:

1. Abra o MetaTrader 5.
2. No menu superior, vá em **Ferramentas > Opções** (ou pressione Ctrl + O).
3. Selecione a aba **Expert Advisors**.
4. Marque a opção:
   - [x] Permitir WebRequest para as URLs listadas:
5. Clique duas vezes no campo de texto abaixo e adicione a URL exata:
   `
   http://127.0.0.1:7482
   `
6. Clique em **OK**.

---

## 3. Inicialização

1. Execute o arquivo SunriseRMGR.exe.
2. O sistema iniciará o serviço de governança em background e abrirá automaticamente o Cockpit HUD acoplado ao seu MetaTrader 5.
3. Abra um gráfico no MT5 e certifique-se de que o **AuditorSentinela** esteja anexado.
