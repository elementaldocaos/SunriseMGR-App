# 📖 Manual de Operação do Cockpit — SunriseRMGR v1.2.0

O Cockpit lateral do SunriseRMGR opera em sincronia com o MetaTrader 5, estruturado em 5 módulos operacionais de governança:

---

## 1. ⚡ Live HUD ($T_0$ — Momento da Entrada)
* **Captura Instantânea**: Assim que uma ordem a mercado ou ordem pendente é executada no MT5, o Live HUD captura imediatamente o ticket, lote, preço de abertura, Stop Loss e Take Profit.
* **Tese Operacional**: Campo de texto livre para digitação da premissa analítica que motivou o trade.
* **Gravação Compulsória**: O botão **Gravar Tese** registra os dados no banco de dados SQLite e gera o hash criptográfico SHA-256 do evento.
* **Quick-Tags Institucionais**: Botões rápidos de categorização técnica (*Breakout, Reteste, Reversão POC, Notícia, Scalper Trap*).

---

## 2. 📡 Radar de Posição em Tempo Real
* **Monitoramento Ativo de Posição**:
  * Preço atual do ativo e variação em pontos.
  * Lucro/Prejuízo flutuante (*Floating P&L*) em moeda da conta.
  * Tempo decorrido desde a abertura da ordem.
  * Distância atual em pontos para o Stop Loss e Take Profit.
* **Rastreamento de Excursão (MAE & MFE)**:
  * **MAE (Maximum Adverse Excursion)**: Mede a pior variação negativa enfrentada pela posição (stress test da entrada).
  * **MFE (Maximum Favorable Excursion)**: Mede a melhor variação positiva atingida pelo preço antes do fechamento.

---

## 3. 📊 Confluência Técnica & Atratores
* **Veredito Sintético de Execução**: Apresenta a classificação de risco instantânea (*CONFORMIDADE PLENA, RISCO MODERADO, RISCO DE LIQUIDEZ*).
* **Dinâmica de Atratores**: Confronta o preço da operação contra zonas de consenso de volume e atratores de reversão média.
* **Matriz de Tendência**: Ribbon de médias exponenciais e índice de agressão compradora vs. vendedora no book.

---

## 4. 📋 Pós-Trade Forense ($T_1$ — Encerramento da Operação)
* **Disparo Automático no Fechamento**: Assim que a posição é liquidada no MT5 (por SL, TP ou encerramento manual), a aba $T_1$ é acionada.
* **Confronto Tese vs. Realidade**: Exibe lado a lado o que o trader planejou em $T_0$ versus o comportamento real do preço em $T_1$.
* **Auditoria de Disciplina & Ludomania**: Identificação instantânea de desvios comportamentais:
  * *Revenge Trading*: Abertura de novas posições em menos de 180 segundos após um stop loss.
  * *Stop Loss Tampering*: Afastamento do stop loss durante o drawdown para evitar a saída técnica.
  * *Tilt Sizing / Martingale*: Aumento desproporcional de lote após perda para tentar recuperar capital.
  * *Panic Close*: Encerramento prematuro no início do ruído estocástico antes de atingir as métricas planejadas.

---

## 5. 🛡️ Diário de Bordo & Auditoria Forense
* **Calendário Operacional Interativo**: Grid mensal codificado por cores (dias verdes para lucro líquido, dias vermelhos para prejuízo). Clique em qualquer dia para expandir o extrato forense daquela sessão.
* **Estatísticas Institucionais**:
  * *Sharpe Ratio* e *Payoff Ratio* calculados dinamicamente.
  * *Drawdown Máximo* histórico e *Profit Factor*.
  * Taxa de acerto (*Win Rate*) e média de tempo em posição.
* **Ledger Imutável**: Tabela de blocos criptográficos onde cada operação possui seu hash `SHA-256(prev_hash || trade_id || payload)`, garantindo que registros históricos não foram adulterados ou apagados.
