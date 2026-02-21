# 💰 Bot de Controle Financeiro (Telegram → Notion)

Este bot permite que você registre transações financeiras no Notion enviando apenas uma mensagem de texto ou uma foto do comprovante no Telegram. Ele utiliza IA para categorizar os gastos e permite selecionar o cartão de crédito de forma interativa.

## 🚀 Funcionalidades Principais

- **Registro por Texto:** Digite algo como `50 almoço no Brooks` e o bot registra automaticamente.
- **Registro por Foto (OCR):** Envie a foto de um comprovante (Pix, Cartão, Boleto) e a IA extrai valor, local e data.
- **Categorização Automática:** A IA identifica se o gasto é de Alimentação, Transporte, Lazer, etc.
- **Seleção de Cartão Interativa:** Se você digitar "cartão" sem especificar, o bot envia botões para você escolher qual cartão usou.
- **Limpeza Automática:** Todas as mensagens de troca (sua mensagem, a confirmação do bot e perguntas) são apagadas após 1 minuto para manter o chat limpo.

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

### 1. Mensagem de Texto
Envie uma mensagem começando com o valor:
- `50 restaurante` (Registra como Saída/Alimentação/Pix)
- `1500 salário` (Registra como Entrada/Investimento/Pix)
- `30 uber cartão` (O bot perguntará qual cartão você usou)

### 2. Foto de Comprovante
Basta enviar a foto do comprovante. A IA lerá os dados e seguirá o mesmo fluxo de registro.

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
- **v2.0:** Suporte a fotos (OCR), categorias automáticas, descrições detalhadas e seleção interativa de cartões.
