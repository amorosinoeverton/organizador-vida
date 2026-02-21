# 📹 Telegram → Notion Media Tracker (AI Enhanced)

Este é um workflow avançado para **n8n** que transforma seu Telegram em uma central de inteligência pessoal. Ele captura links de redes sociais, organiza no Notion com metadados ricos e ainda serve como um assistente de chat com memória.

## 🚀 Funcionalidades

- **Captura Automática:** Detecta links do Instagram e YouTube enviados para o seu bot.
- **Enriquecimento com IA:** 
  - Gera títulos curtos e contextuais usando o **ChatGPT (GPT-4o mini)**.
  - Extrai informações de legendas e metadados de vídeo.
- **Organização Premium no Notion:**
  - Adiciona Capas (Thumbnails) e Ícones automáticos.
  - Insere o vídeo (embed) dentro da página para visualização direta.
  - Define o status como `🔴 Não Assistido`.
- **Assistente de Chat Integrado:**
  - Responde perguntas e executa comandos diretamente no Telegram.
  - Possui **Memória de Conversa** (Window Buffer), lembrando do contexto anterior.
- **Autogestão de Canal:**
  - Deleta mensagens de links processados para manter o canal limpo.
  - Notifica erros críticos em um canal de monitoramento.

## 📋 Pré-requisitos

1. **n8n:** Versão estável com suporte a nós de LangChain.
2. **Telegram:** Um bot criado via [@BotFather](https://t.me/botfather).
3. **Notion:** Uma integração com permissão de leitura/escrita e um Banco de Dados configurado.
4. **OpenAI:** API Key com créditos para o modelo `gpt-4o-mini`.

## 🛠️ Configuração Passo a Passo

### 1. Preparando o Notion
Crie um Banco de Dados no Notion com as seguintes propriedades:
- **Titulo** (Nome/Title)
- **URL** (URL)
- **Status** (Seleção: `🔴 Não Assistido`, `🟡 Assistindo`, `🟢 Concluído`)
- **Plataforma** (Seleção: `Instagram`, `YouTube`)
- **Data de Captura** (Data)
- **Miniatura** (Arquivos e Mídia)

*Dica: Compartilhe o Banco de Dados com sua Integração do Notion.*

### 2. Configurando as Credenciais no n8n
No seu painel do n8n, crie as seguintes credenciais:
- **Telegram API:** Use o Token do seu bot.
- **Notion API:** Use o Token da sua integração.
- **OpenAI API:** Use a sua API Key (modelo recomendado: `gpt-4o-mini`).

### 3. Importação do Workflow
1. Copie o conteúdo do arquivo `workflow.json` (neste repositório).
2. No n8n, clique em **Import from JSON** e cole o código.
3. No nó **NotionSave**, selecione o seu Banco de Dados no campo `Database ID`.
4. Certifique-se de que os nós de IA estão conectados às credenciais corretas.

## 🧠 Como usar

1. **Para Salvar Conteúdo:** Simplesmente mande um link do Instagram ou YouTube para o seu bot. Ele fará o resto e apagará a mensagem em seguida.
2. **Para Conversar:** Mande qualquer texto ou pergunta. O assistente usará o contexto da conversa para te responder.

---
Desenvolvido por **Everton Santana** com auxílio da IA.
