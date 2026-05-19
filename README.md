Aqui está o conteúdo completo para você copiar e colar:

```markdown
# ⚡ Sistema ChargeGrid AI

> Orquestrando a mobilidade elétrica comercial com Dados, IoT e Inteligência Artificial.

**EV Challenge 2026 — FIAP x GoodWe**
Turma Presencial — 1° Ano

---

## 👥 Integrantes

| Nome | RM |
|---|---|
| Enrico Marinho de Aquino | 569338 |
| Heitor Maximus Mucha | 571407 |
| Fernando Lobato Rodrigues | 569377 |
| Andrei Henrique Santos | 569440 |
| Josué Franco Braga | 569174 |
| Manoel Da Silva Ferreira | 572045 |

---

## 🔍 Problema Abordado

A GoodWe possui uma solução de carregamento de veículos elétricos consolidada para o ambiente residencial (linha HCA G2). No entanto, a transição para o ambiente **comercial** expõe uma lacuna crítica: os eletropostos atuais não possuem mecanismos integrados para **orquestrar potência entre múltiplos carregadores simultâneos**, **registrar e faturar sessões de recarga** e **comunicar informações operacionais em tempo real** para operadores e usuários.

Sem essa camada de inteligência, o modelo comercial de recarga é inviável — seja em estacionamentos, shoppings ou frotas corporativas.

---

## 💡 Proposta do Sistema

O **Sistema ChargeGrid AI** é uma plataforma web/mobile que transforma os carregadores GoodWe HCA G2 em uma infraestrutura comercial completa. O coração do sistema é um **agente de IA conversacional** que atende qualquer usuário da interface, responde perguntas e, quando necessário, executa ferramentas integradas ao app para entregar respostas baseadas em dados reais.

### Como funciona

O agente recebe a pergunta do usuário junto com o contexto da sessão atual e decide autonomamente entre duas ações:

**Responder via RAG** — para perguntas gerais sobre o serviço, o app e os equipamentos GoodWe, o agente busca na base documental e gera uma resposta contextualizada.

**Executar uma ferramenta** — para perguntas que exigem dados em tempo real, o agente chama uma das três funções disponíveis no sistema:

- `calcular_preco()` — calcula o valor a pagar pela sessão com base no kWh consumido e na tarifa vigente.
- `calcular_demanda()` — retorna o status dos carregadores ativos e como a potência disponível está sendo distribuída.
- `calcular_estimativa()` — estima o tempo restante para completar a carga com base na potência disponível e na capacidade da bateria.

---

## 🎯 Escopo e Persona

**Contexto:** ChargeGrid Intelligence — setor comercial e varejo (turma presencial).

**Persona:** Qualquer usuário da interface — linguagem simples e objetiva, sem distinção de perfil na Sprint 1.

**O que o agente responde:**

Via RAG:
- Dúvidas sobre o funcionamento do serviço e do app
- Problemas técnicos e erros nos carregadores
- Perguntas sobre a GoodWe e seus produtos

Via ferramentas:
- Quanto custa a sessão atual
- Status e distribuição de potência dos carregadores
- Tempo estimado para completar a carga

**Fora do escopo (Sprint 1):**
- Análise de dados históricos e insights financeiros
- Controle de acesso por perfil de usuário

---

## 🔄 Fluxograma de Funcionamento

O fluxograma completo está disponível em `/docs/fluxograma.png`.

**Resumo do fluxo:**

Usuário
    ↓
App ChargeGrid AI
    ↓
Contexto injetado (dados dinâmicos + base documental)
    ↓
Agente — GPT-4o + LangChain
    ↓
Responde direto ou usa ferramenta?
    ├── Via RAG → busca na base documental
    └── Via ferramenta → calcular_preco() / calcular_demanda() / calcular_estimativa()
    ↓
Resposta no app
    ↓
Log de sessão → BD dinâmico



---

## 🛠️ Tecnologias Selecionadas e Justificativa Técnica

| Tecnologia | Função | Justificativa |
|---|---|---|
| **GPT-4o (OpenAI API)** | LLM e agente principal | Melhor suporte nativo a function calling — o modelo decide sozinho quando e qual ferramenta chamar. Ecossistema mais maduro para esse padrão de arquitetura. |
| **LangChain** | Orquestração do agente | Gerencia o agente, o histórico de conversa, o pipeline RAG e a execução das ferramentas em um único framework consolidado. |
| **ChromaDB** | Banco vetorial (RAG) | Leve, roda localmente e ideal para o escopo acadêmico. Armazena os embeddings da base documental para recuperação semântica. |
| **sentence-transformers** | Embeddings (RAG) | Modelo open-source `all-MiniLM-L6-v2` para vetorizar documentos e queries sem custo de API adicional. |
| **Python + FastAPI** | Backend | API REST que recebe mensagens do app, monta o contexto, aciona o agente e retorna a resposta. Integração nativa com LangChain. |
| **React** | Frontend | Interface web responsiva para operador e cliente, consumindo a API do backend. |
| **PostgreSQL** | Banco de dados dinâmico | Armazena sessões de recarga, status dos carregadores, tarifas e potência disponível — atualizado em tempo real via OCPP/MODBUS. |
| **OCPP / MODBUS** | Protocolo IoT | Padrões abertos exigidos pela ANEEL (RN 1.000/2021) para comunicação com os carregadores GoodWe HCA G2. |

---

## 🤖 Contexto Injetado no Agente

A cada conversa, o agente recebe dois tipos de contexto:

**Dados dinâmicos (tempo real — via PostgreSQL):**
- Sessão ativa do usuário: kWh consumido, potência atual, tempo decorrido
- Status geral dos carregadores: quantos ativos, potência total disponível
- Tarifa vigente

**Base documental (RAG — via ChromaDB):**
- Documentação do app ChargeGrid AI: funcionalidades, como usar, fluxos
- Documentação da GoodWe: empresa, produtos, linha HCA G2
- FAQs e guias de solução de problemas técnicos

---

## 🧪 Modelo de Teste

O modelo de teste com 5 perguntas e respostas esperadas está disponível em `/docs/modelo-de-teste.md`.

---

## 📋 System Prompt Base

O system prompt utilizado para condicionar o agente ao contexto GoodWe está disponível em `/docs/system-prompt.md`.

---

## 📁 Estrutura do Repositório

sistema-chargegrid-ai/
├── README.md
├── docs/
│   ├── fluxograma.html
│   ├── modelo-de-teste.html
│   └── system-prompt.md
└── src/
    └── (desenvolvimento Sprint 2+)




