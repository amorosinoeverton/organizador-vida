# 🧠 Organizador de Vida (Mega Bot: Finanças + Ideias + Vídeos)

Este bot é o seu comando central no Telegram. Ele organiza suas finanças, captura links de vídeos e agora permite capturar ideias rápidas para sua Inbox do Notion.

## 🚀 Funcionalidades Principais

- **Registro Financeiro (Texto/Foto):** Digite o valor ou mande foto do comprovante para registrar gastos e ganhos.
- **Captura de Ideias (!):** Use o prefixo `!` para salvar pensamentos e ideias rápidas na sua Inbox.
- **Categorização por IA:** A IA identifica categorias financeiras e extrai detalhes de comprovantes.
- **Seleção de Cartão Interativa:** Botões interativos para escolher o cartão de crédito.
- **Limpeza Automática:** Mantém o chat limpo apagando mensagens antigas após 1 minuto.

---

## 🛠️ Requisitos no Notion

Sua base de dados no Notion (chamada **(PES) Transação**) deve conter as seguintes propriedades:

| Propriedade | Tipo | Descrição |
| :--- | :--- | :--- |
| **Nome** | Title | Descrição do gasto (Ex: Almoço no Brooks) |
| **Valor** | Number | Valor da transação |
| **Tipo** | Select | Opções: `Entrada`, `Saída` |
| **Data** | Date | Data da transação |
| **Categoria** | Select | Categorias (Ex: 🍽️ Alimentação, 🚌 Transporte, 🎉 Lazer) |
| **Método** | Select | Métodos (Ex: 💜 Nubank, ⚫ C6 Bank, 📱 Pix, 💵 Dinheiro) |
| **Realizado** | Checkbox | Marcado automaticamente como `true` |

---

## 🤖 Como usar

### 1. Mensagem de Texto (Finanças)
Envie uma mensagem começando com o valor:
- `50 restaurante` (Gasto em Alimentação)
- `1500 salário` (Entrada/Receita)

### 2. Captura de Ideias (Inbox)
Envie qualquer texto começando com `!`:
- `! fazer sorvete de flocos com banana`
- `! estudar automação de processos`
O bot removerá o `!` e salvará a frase diretamente na sua base de dados de **Inbox (Ver Depois)**.

### 3. Foto de Comprovante
Basta enviar a foto do comprovante. A IA lerá os dados e seguirá o mesmo fluxo de registro financeiro.

---

## ⚙️ Estrutura do Workflow (n8n)

O workflow `💰 Finanças Pessoais (Telegram → Notion)` é composto por:

1.  **TelegramTrigger:** Escuta mensagens e cliques em botões.
2.  **Roteamento:** Identifica se é uma foto, um texto financeiro ou uma resposta de botão.
3.  **Motores de IA:**
    *   **OpenAiFinance:** Processa textos e extrai categorias/detalhes.
    *   **OpenAIVision (GPT-4o-mini):** Lê imagens de comprovantes com baixíssimo custo.
4.  **Lógica Interestelar:**
    *   Se o cartão for ambíguo, o bot salva os dados temporariamente e envia um teclado inline.
    *   Ao clicar no botão, o bot retoma os dados e finaliza o salvamento.
5.  **NotionFinanceSave:** Conecta-se à API do Notion para gravar os dados.
6.  **Sistema de Limpeza:** Um temporizador de 1 minuto apaga o rastro das mensagens no Telegram.

---

## 📝 Notas de Versão
- **v1.0:** Integração base Notion.
- **v1.5:** IA para extração de dados e melhorias de segurança.
- **v2.0:** Suporte a fotos (OCR), categorias automáticas e seleção interativa de cartões.
- **v2.5:** Integração de **Captura de Ideias** via comando `!` salvando na Inbox (Media Tracker).
