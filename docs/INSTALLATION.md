# 📦 Guia de Instalação & Configuração — SunriseRMGR v1.2.0

Siga o roteiro abaixo para instalar e conectar o SunriseRMGR ao MetaTrader 5.

---

## 1. Requisitos do Sistema

- **Sistema Operacional**: Windows 10 ou Windows 11 (64-bit).
- **Terminal de Trading**: MetaTrader 5 (versão Build 4000+ recomendada).
- **Runtime Web**: Microsoft Edge WebView2 Runtime (pré-instalado nativamente no Windows 10/11 atualizado).
- **Porta Local**: `127.0.0.1:7482` livre para o servidor de telemetria loopback.

---

## 2. Métodos de Instalação

### Opção A: Instalação Automática (Recomendada)
1. Baixe o arquivo **`SunriseRMGR-v1.2.0-Windows-x64.zip`** da página oficial de [Releases](https://github.com/elementaldocaos/SunriseMGR-App/releases/tag/v1.2.0).
2. Extraia o conteúdo do arquivo ZIP.
3. Dê dois cliques em **`Instalar-SunriseRMGR.bat`**.
4. O instalador copiará os binários para `%LOCALAPPDATA%\SunriseRMGR`, gerará os atalhos de alta resolução na Área de Trabalho e Menu Iniciar, e iniciará o daemon automaticamente.

### Opção B: Execução Portátil (Zero-Install)
1. Baixe o arquivo executável individual **`SunriseRMGR.exe`**.
2. Salve-o em uma pasta de sua preferência (ex: `C:\SunriseRMGR\`).
3. Execute diretamente `SunriseRMGR.exe`. O sistema criará seu banco de dados local SQLite na mesma pasta.

---

## 3. Configuração de Rede no MetaTrader 5

Para que o robô de telemetria consiga enviar cotações e estados de ordens para o Cockpit:

1. Abra o MetaTrader 5.
2. Acesse o menu superior: **Ferramentas > Opções** (ou pressione `Ctrl + O`).
3. Selecione a aba **Expert Advisors**.
4. Marque a caixa:
   - `[x] Permitir WebRequest para as URLs listadas:`
5. Clique duas vezes no campo de texto inferior e insira exatamente a URL:
   ```
   http://127.0.0.1:7482
   ```
6. Clique no botão **OK** para salvar.

---

## 4. Ativação do Robô Sentinela (`AuditorSentinela.ex5`)

1. O **SunriseRMGR** localiza automaticamente todas as pastas de dados do MT5 instaladas na máquina e implanta o arquivo compilado `AuditorSentinela.ex5` na subpasta `MQL5\Experts\`.
2. No MetaTrader 5, abra o painel **Navegador** (`Ctrl + N`).
3. Expanda a pasta **Expert Advisors**, clique com o botão direito e selecione **Atualizar**.
4. Localize o **`AuditorSentinela`** e arraste-o para qualquer gráfico ativo.
5. Na aba *Comum* da janela do robô, certifique-se de que a opção **Permitir Importação de DLL** e **Permitir WebRequest** estejam marcadas.
6. Clique em **OK**. Uma mensagem de conexão bem-sucedida aparecerá na aba *Experts* do terminal.

---

## 5. Resolução de Problemas Frequentes (Troubleshooting)

* **Alerta do Windows SmartScreen:** Como o binário é compilado diretamente do código-fonte em Rust para distribuição independente, o Windows SmartScreen pode exibir um aviso azul na primeira execução. Basta clicar em *"Mais informações"* e em seguida em *"Executar assim mesmo"*.
* **O Cockpit não acopla na tela:** Verifique se o MetaTrader 5 não está minimizado na barra de tarefas. O algoritmo de acoplamento magnético requer que o terminal esteja visível no desktop.
* **Erro de conexão HTTP no EA:** Verifique se a URL `http://127.0.0.1:7482` foi adicionada com precisão (sem espaços ou barras extras) nas opções do WebRequest do MT5.
