# 🧠 Spec-Driven Agents — Boas Práticas

> Desenvolvimento orientado a especificações com agentes de IA: do "vibe coding" à engenharia com intenção.

---

## Sumário

- [O problema com o Vibe Coding](#o-problema-com-o-vibe-coding)
- [O que é Spec-Driven Development?](#o-que-é-spec-driven-development)
- [Os três níveis de SDD](#os-três-níveis-de-sdd)
- [Por que arquitetos estão adotando SDD?](#por-que-arquitetos-estão-adotando-sdd)
- [Os artefatos centrais](#os-artefatos-centrais)
- [Estrutura de arquivos deste repositório](#estrutura-de-arquivos-deste-repositório)
- [Guia de uso dos arquivos de contexto (.github/)](#guia-de-uso-dos-arquivos-de-contexto-github)
- [Workflow orientado a contexto — Casos de uso](#workflow-orientado-a-contexto--casos-de-uso)
- [Ferramentas do ecossistema SDD](#ferramentas-do-ecossistema-sdd)
- [Cuidados e limitações](#cuidados-e-limitações)
- [Referências](#referências)

---

## O problema com o Vibe Coding

O *vibe coding* — descrever o que você quer em linguagem natural e deixar a IA gerar o código — é mágico para protótipos rápidos. Mas em sistemas reais, ele cria problemas sérios:

**Inconsistência arquitetural**: a IA foca na tarefa imediata e não entende a arquitetura geral. Cada conversa existe em uma bolha. Peça uma feature hoje e outra amanhã, e você pode obter código que conflita com o que foi gerado ontem.

**Desalinhamento de equipe**: sem um entendimento compartilhado, cada desenvolvedor e agente de IA toma decisões isoladas, sem uma fonte de verdade comum.

**Dívida técnica invisível**: a natureza espontânea do vibe coding resulta em má documentação e implementações que se afastam gradualmente do plano original, sem registro de "o que mudou" ou "por quê".

**Perda de contexto entre sessões**: agentes de IA não têm memória entre conversas. Perguntas feitas hoje podem gerar respostas diferentes amanhã, para o mesmo problema.

A raiz do problema não é a capacidade dos modelos — é a abordagem. Estamos tratando agentes de IA como mecanismos de busca quando deveríamos tratá-los como parceiros de programação literais, que precisam de instruções inequívocas.

---

## O que é Spec-Driven Development?

Spec-Driven Development (SDD) não é uma ideia nova. Arquitetos de software usam especificações para guiar o desenvolvimento há décadas: desenvolvimento API-first, especificações OpenAPI, documentos de requisitos formais. O que mudou é o contexto.

Com agentes de IA se tornando nossos principais parceiros de implementação, especificações passam a cumprir um papel diferente e mais crítico: **são o mecanismo pelo qual mantemos supervisão humana em um processo de desenvolvimento cada vez mais autônomo.**

Em vez de codificar primeiro e escrever documentação depois, no SDD você começa com uma especificação. Essa spec é um contrato de como seu código deve se comportar e se torna a fonte de verdade que suas ferramentas e agentes de IA usam para gerar, testar e validar código.

> "No novo mundo, *manter software significa evoluir especificações*. [...] A língua franca do desenvolvimento move para um nível mais alto, e o código é a abordagem de última milha." — GitHub Spec Kit

> "Uma abordagem de desenvolvimento onde specs — não código — são o artefato primário. Specs descrevem intenção em linguagem estruturada e testável, e agentes geram código para corresponder a elas." — Tessl

---

## Os três níveis de SDD

Conforme análise de Birgitta Böckeler (Thoughtworks/Martin Fowler Blog), existem três níveis de maturidade na adoção de SDD:

| Nível | Descrição | Quando usar |
|-------|-----------|-------------|
| **Spec-first** | Uma spec bem elaborada é escrita primeiro e usada no fluxo de trabalho com IA para a tarefa em questão. Após a tarefa, pode ser descartada. | Ponto de partida recomendado para qualquer equipe |
| **Spec-anchored** | A spec é mantida mesmo após a tarefa ser concluída, continuando a ser usada para evolução e manutenção da funcionalidade. | Projetos em produção com manutenção contínua |
| **Spec-as-source** | A spec é o arquivo-fonte principal. O humano nunca edita o código diretamente; apenas a spec é editada, e agentes geram o código a partir dela. | Exploratório / futuro próximo |

A maioria das ferramentas atuais opera no nível **spec-first**, com algumas aspirando ao **spec-anchored**. O nível spec-as-source ainda é experimental.

---

## Por que arquitetos estão adotando SDD?

Três razões fundamentais impulsionam a adoção:

**Controle sem microgerenciamento**: você não precisa supervisionar cada linha de código, mas garante que o agente opere dentro dos limites arquiteturais que você definiu. A spec é o guardrail.

**Escalabilidade para times e sistemas complexos**: o vibe coding funciona bem para desenvolvedores solo em projetos pequenos. Em sistemas complexos com múltiplos agentes de IA e desenvolvedores, sem especificações compartilhadas você obtém caos. Specs se tornam a fonte de verdade que mantém todos — humanos e agentes — alinhados.

**Persistência e memória organizacional**: conversas com IA são efêmeras. Especificações fornecem memória — não apenas para a IA, mas para todo o processo de desenvolvimento. Erros com migrações de banco? Adicione diretrizes ao `design.md`. IA gerando estilo de código inconsistente? Atualize seus padrões de projeto.

---

## Os artefatos centrais

O SDD moderno tipicamente gira em torno de três tipos de artefatos, que precisam ser precisos o suficiente para máquinas enquanto permanecem legíveis para os arquitetos que os mantêm:

```
📄 requirements.md  →  O QUÊ e POR QUÊ
                        Lógica de negócios, restrições, critérios de aceitação,
                        jornadas de usuário e definição de sucesso.

📄 design.md        →  COMO (arquitetura técnica)
                        Componentes, fluxo de dados, padrões de integração,
                        modelos de dados, stack tecnológico.

📄 tasks.md         →  SEQUÊNCIA DE EXECUÇÃO
                        Trabalho decomposto em partes discretas e verificáveis,
                        cada uma implementável e testável de forma isolada.
```

Além desses, ferramentas modernas introduzem o conceito de **Memory Bank** (ou "constitution") — arquivos de contexto persistente que se aplicam a *todas* as sessões de desenvolvimento, não apenas a uma tarefa específica:

```
📄 copilot-instructions.md  →  Instruções globais para o agente no repositório
📄 AGENTS.md / CLAUDE.md    →  Contexto e diretrizes para agentes específicos
📄 constitution.md          →  Princípios não-negociáveis do projeto
```

---

## Estrutura de arquivos deste repositório

```
spec-driven-agents/
├── .github/
│   ├── copilot-instructions.md   ← Instruções globais para GitHub Copilot
│   └── instructions/             ← Instruções específicas por contexto
│       ├── requirements.instructions.md
│       ├── design.instructions.md
│       └── tasks.instructions.md
├── brain/                        ← Artefatos de especificação do projeto
│   ├── requirements.md
│   ├── design.md
│   └── tasks.md
├── README.md
└── LICENSE
```

---

## Guia de uso dos arquivos de contexto (.github/)

Esta é a seção mais importante para quem trabalha com agentes de IA. Os arquivos na pasta `.github/` são o mecanismo central de **passagem de contexto** — eles garantem que o agente saiba onde está, o que foi decidido e como deve se comportar.

### Como funciona a hierarquia de contexto

```
┌─────────────────────────────────────────────────────────┐
│  NÍVEL 1 — Contexto Global (Memory Bank)                │
│  .github/copilot-instructions.md                        │
│  Aplicado em TODAS as sessões e requisições             │
├─────────────────────────────────────────────────────────┤
│  NÍVEL 2 — Contexto por Fase                            │
│  .github/instructions/*.instructions.md                 │
│  Aplicado a tarefas específicas via `applyTo`           │
├─────────────────────────────────────────────────────────┤
│  NÍVEL 3 — Artefatos de Especificação                   │
│  brain/requirements.md, design.md, tasks.md             │
│  Referenciados explicitamente no prompt da tarefa       │
└─────────────────────────────────────────────────────────┘
```

### `copilot-instructions.md` — O contexto global

Este arquivo é lido pelo GitHub Copilot em **toda** requisição feita ao agente no repositório. Use-o para:

- Descrever o propósito do projeto e decisões arquiteturais fundamentais
- Definir convenções de código obrigatórias (padrões de nomeação, estrutura de pastas)
- Especificar dependências e stack tecnológico
- Documentar comandos essenciais de build, test e execução
- Informar restrições de segurança ou compliance que devem sempre ser respeitadas

**Exemplo de conteúdo:**

```markdown
## Propósito do projeto
API REST para gestão de pedidos em e-commerce B2B.
Stack: Node.js 20, TypeScript, Express, PostgreSQL, Prisma ORM.

## Convenções obrigatórias
- Toda função assíncrona deve ter tratamento de erro com try/catch
- Use injeção de dependência via construtores, nunca imports diretos de serviços
- Testes unitários obrigatórios para toda lógica de negócio em /src/services/

## Comandos essenciais
- `npm run dev` — inicia servidor em desenvolvimento
- `npm run test` — executa suite de testes
- `npm run migrate` — aplica migrações de banco de dados
```

### `requirements.instructions.md` — Instruções para fase de requisitos

Use o frontmatter `applyTo` para que essas instruções sejam carregadas automaticamente quando o agente trabalhar com arquivos de requisitos:

```markdown
---
applyTo: "**/requirements.md"
---

## Ao trabalhar com requisitos

- Sempre estruture user stories no formato "Como [persona], quero [ação], para [benefício]"
- Cada requisito deve ter critérios de aceitação no formato DADO/QUANDO/ENTÃO
- Requisitos não-funcionais (performance, segurança) devem ser explicitamente numerados
- Nunca inclua decisões de implementação em requisitos funcionais
```

### `design.instructions.md` — Instruções para fase de design

```markdown
---
applyTo: "**/design.md"
---

## Ao trabalhar com design técnico

- Sempre inclua diagrama de componentes em formato Mermaid
- Documente trade-offs de decisões arquiteturais relevantes
- Referências a padrões externos devem incluir links para documentação oficial
- Identifique explicitamente pontos de integração com sistemas externos
```

### `tasks.instructions.md` — Instruções para decomposição de tarefas

```markdown
---
applyTo: "**/tasks.md"
---

## Ao decompor tarefas

- Cada tarefa deve ser implementável e testável de forma isolada
- Estime complexidade relativa (P, M, G, XG) para cada tarefa
- Tarefas devem referenciar os requisitos que implementam (ex: REQ-001)
- Inclua critérios de "done" claros e verificáveis para cada tarefa
```

### Passando contexto explicitamente no prompt

Mesmo com os arquivos de instrução configurados, **sempre referencie os artefatos relevantes explicitamente** ao iniciar uma sessão com o agente:

```
# Início de sessão recomendado

"Leia os seguintes arquivos de contexto antes de qualquer ação:
- .github/copilot-instructions.md (contexto global do projeto)
- brain/requirements.md (o que estamos construindo e por quê)
- brain/design.md (como está arquitetado)

Com base nesses artefatos, [sua instrução aqui]."
```

---

## Workflow orientado a contexto — Casos de uso

### Caso de uso 1: Novo projeto (Greenfield)

Quando você está iniciando um projeto do zero, a tentação é começar a codificar imediatamente. O SDD inverte essa ordem.

```
FASE 1 — ESPECIFICAR (o quê e por quê)
┌──────────────────────────────────────────────────────────┐
│ Prompt inicial ao agente:                                │
│                                                          │
│ "Vou construir [descrição do produto]. O público-alvo    │
│ é [personas]. O problema principal que resolve é         │
│ [problema]. Gere um requirements.md estruturado com      │
│ user stories e critérios de aceitação. Foque em          │
│ jornadas de usuário, não em tecnologia."                │
└──────────────────────────────────────────────────────────┘
         ↓ Revise e refine o requirements.md
         ↓ Responda às perguntas de clarificação do agente

FASE 2 — PLANEJAR (arquitetura técnica)
┌──────────────────────────────────────────────────────────┐
│ "Com base no requirements.md gerado, crie um design.md   │
│ com a arquitetura técnica. Nossa stack preferida é       │
│ [stack]. Temos estas restrições: [restrições].           │
│ Inclua diagrama de componentes, modelo de dados          │
│ e estratégia de testes."                                │
└──────────────────────────────────────────────────────────┘
         ↓ Revise e refine o design.md
         ↓ Valide que atende aos requisitos

FASE 3 — DECOMPOR (tarefas concretas)
┌──────────────────────────────────────────────────────────┐
│ "Com base no requirements.md e design.md, gere um        │
│ tasks.md com tarefas concretas e implementáveis.         │
│ Cada tarefa deve ser pequena o suficiente para           │
│ implementar e testar de forma isolada."                  │
└──────────────────────────────────────────────────────────┘
         ↓ Revise a lista de tarefas

FASE 4 — IMPLEMENTAR (tarefa por tarefa)
┌──────────────────────────────────────────────────────────┐
│ "Implemente a tarefa TASK-001 do tasks.md.               │
│ Consulte o design.md para decisões arquiteturais         │
│ e o requirements.md para critérios de aceitação."        │
└──────────────────────────────────────────────────────────┘
         ↓ Revise o código gerado
         ↓ Repita para cada tarefa
```

**Checkpoint obrigatório após cada fase**: não avance sem validar que o artefato gerado está correto, completo e alinhado com sua intenção real.

---

### Caso de uso 2: Nova feature em sistema existente (N → N+1)

Este é o cenário onde o SDD é mais poderoso — e mais crítico. Adicionar features a codebases complexas é arriscado sem contexto adequado.

```
PASSO 1 — Carregue o contexto existente
┌──────────────────────────────────────────────────────────┐
│ Antes de qualquer coisa, garanta que o agente            │
│ conhece o estado atual do sistema:                       │
│                                                          │
│ "Leia copilot-instructions.md, requirements.md e        │
│ design.md. Após ler, descreva em 3 frases o que          │
│ o sistema faz atualmente e as principais decisões        │
│ arquiteturais tomadas."                                  │
└──────────────────────────────────────────────────────────┘
         ↓ Valide que o agente compreendeu o contexto

PASSO 2 — Especifique apenas a nova feature
┌──────────────────────────────────────────────────────────┐
│ "Considerando a arquitetura existente descrita no        │
│ design.md, preciso adicionar [feature]. Gere uma        │
│ spec apenas para esta feature, indicando:               │
│ - Como ela se integra com componentes existentes        │
│ - Que partes do design.md precisam ser atualizadas      │
│ - Novos requisitos que surgem desta adição"             │
└──────────────────────────────────────────────────────────┘

PASSO 3 — Atualize os artefatos
┌──────────────────────────────────────────────────────────┐
│ Após validar a spec da feature:                          │
│                                                          │
│ 1. Atualize requirements.md com os novos requisitos     │
│ 2. Atualize design.md com as mudanças arquiteturais     │
│ 3. Adicione as novas tarefas ao tasks.md                │
└──────────────────────────────────────────────────────────┘

PASSO 4 — Implemente com contexto completo
┌──────────────────────────────────────────────────────────┐
│ "Implemente TASK-015 do tasks.md. O código novo deve    │
│ ser consistente com os padrões definidos em             │
│ copilot-instructions.md e respeitar as interfaces       │
│ descritas em design.md."                                │
└──────────────────────────────────────────────────────────┘
```

---

### Caso de uso 3: Debugging e refatoração com contexto

Quando algo quebra ou precisa ser refatorado, o contexto é ainda mais valioso para evitar que o agente "conserte" o problema de forma que quebre outra coisa.

```
ANTES DE PEDIR O FIX:
┌──────────────────────────────────────────────────────────┐
│ "Leia design.md seção 'Componente de Autenticação'.      │
│ O seguinte erro está ocorrendo: [erro].                  │
│                                                          │
│ Antes de sugerir uma correção:                           │
│ 1. Identifique a causa raiz considerando a arquitetura  │
│ 2. Liste componentes que podem ser afetados pelo fix    │
│ 3. Proponha uma solução que respeite o design existente │
└──────────────────────────────────────────────────────────┘
```

---

### Caso de uso 4: Onboarding de novo membro (humano ou agente)

Uma das maiores vantagens do SDD é que os artefatos servem como onboarding documentado.

```
PARA NOVO DESENVOLVEDOR HUMANO:
"Leia nesta ordem: copilot-instructions.md → requirements.md
→ design.md → tasks.md. Após ler, você terá o contexto
completo do que foi construído, por quê, e o que falta."

PARA NOVA SESSÃO DE AGENTE:
"Este é o contexto do projeto [nome]. Leia os arquivos
a seguir na ordem indicada:
1. .github/copilot-instructions.md — visão geral e convenções
2. brain/requirements.md — o que estamos construindo
3. brain/design.md — como está arquitetado
4. brain/tasks.md — status atual das tarefas

Confirme sua compreensão antes de prosseguir."
```

---

### Caso de uso 5: Revisão de consistência entre artefatos

Antes de iniciar implementação, use o agente para validar que seus artefatos são consistentes entre si.

```
REVISÃO DE CONSISTÊNCIA:
┌──────────────────────────────────────────────────────────┐
│ "Analise os três artefatos (requirements.md, design.md,  │
│ tasks.md) e identifique:                                │
│                                                          │
│ 1. Requisitos sem tarefas correspondentes               │
│ 2. Componentes no design sem requisitos associados      │
│ 3. Tarefas que conflitam com decisões do design         │
│ 4. Lacunas ou ambiguidades que podem gerar problemas    │
│    durante a implementação                              │
└──────────────────────────────────────────────────────────┘
```

---

## Ferramentas do ecossistema SDD

O ecossistema de ferramentas que trata especificações como cidadãos de primeira classe está crescendo rapidamente:

| Ferramenta | Tipo | Workflow | Compatível com |
|------------|------|----------|----------------|
| **[Kiro](https://kiro.dev/)** (Amazon) | IDE (VS Code-based) | Requirements → Design → Tasks | Integrado ao Kiro IDE |
| **[Spec Kit](https://github.com/github/spec-kit)** (GitHub) | CLI + templates | Constitution → Specify → Plan → Tasks → Implement | Copilot, Claude Code, Gemini CLI, Cursor, e outros |
| **[Claude Code](https://docs.anthropic.com/en/docs/claude-code/overview)** (Anthropic) | CLI | Lê `CLAUDE.md` para contexto | Terminal-based |
| **[Tessl](https://docs.tessl.io/)** (privado beta) | CLI + MCP server | Spec-anchored / spec-as-source | Cursor, VS Code, e outros |
| **[cc-sdd](https://github.com/gotalab/cc-sdd)** (comunidade) | CLI | Requirements → Design → Tasks (estilo Kiro) | Claude Code, Copilot, Gemini, Cursor, e outros |

### Iniciando com o Spec Kit (recomendado para times)

```bash
# Instale e inicialize o projeto para GitHub Copilot
uvx --from git+https://github.com/github/spec-kit.git specify init <NOME_DO_PROJETO> --ai copilot

# Ou para Claude Code
uvx --from git+https://github.com/github/spec-kit.git specify init <NOME_DO_PROJETO> --ai claude
```

Após a inicialização, você terá acesso aos comandos slash no seu agente:
- `/speckit.specify` — gera a especificação funcional
- `/speckit.plan` — cria o plano técnico
- `/speckit.tasks` — decompõe em tarefas implementáveis
- `/speckit.implement` — orienta a implementação
- `/speckit.constitution` — estabelece princípios não-negociáveis do projeto

---

## Cuidados e limitações

Baseado em análise crítica da prática real (Birgitta Böckeler, Thoughtworks):

**O SDD não é uma bala de prata.** Tenha em mente:

- **Tamanho importa**: workflows elaborados com muitos artefatos podem ser excessivos para bugs pequenos ou tarefas triviais. Calibre a profundidade da spec ao tamanho do problema.

- **O agente pode ignorar instruções**: contextos maiores não garantem que o agente seguirá todas as instruções. Sempre revise o que foi gerado — especialmente em sistemas existentes, onde o agente pode tratar descrições de código já existente como especificações para gerar código novo, criando duplicatas.

- **Falsa sensação de controle**: muitos arquivos e checklists não eliminam alucinações. O papel do desenvolvedor é verificar cada fase, não apenas aprovar.

- **Separação funcional vs. técnico é difícil**: manter requisitos puramente funcionais (sem decisões de implementação) requer disciplina consistente da equipe.

- **Verbosidade tem custo**: revisar muitos arquivos Markdown pode ser mais lento do que codificar diretamente para problemas simples. Reserve o SDD para problemas de complexidade adequada.

- **Aprenda com o passado**: SDD tem paralelos com Model-Driven Development (MDD) dos anos 2000. O MDD nunca decolou para aplicações de negócio por criar overhead excessivo. LLMs removem parte desse overhead, mas introduzem não-determinismo. Use os aprendizados históricos para não repetir os mesmos erros.

---

## Referências

- [Spec Kit](https://github.com/github/spec-kit) - Build high-quality software faster. GitHub repository
- [From "Vibe Coding" to Spec-Driven Development](https://hammansamuel.medium.com/from-vibe-coding-to-spec-driven-development-c9aec008a81c) — Hamman Samuel, PhD
- [Spec-driven development with AI: Get started with a new open source toolkit](https://github.blog/ai-and-ml/generative-ai/spec-driven-development-with-ai-get-started-with-a-new-open-source-toolkit/) — GitHub Blog
- [Understanding Spec-Driven-Development: Kiro, spec-kit, and Tessl](https://martinfowler.com/articles/exploring-gen-ai/sdd-3-tools.html) — Birgitta Böckeler (martinfowler.com)
- [Spec-driven development: Using Markdown as a programming language](https://github.blog/ai-and-ml/generative-ai/spec-driven-development-using-markdown-as-a-programming-language-when-building-with-ai/) — GitHub Blog
- [github/spec-kit](https://github.com/github/spec-kit) — Toolkit open source para SDD
- [eduardoveloso/spec-driven-agents](https://github.com/eduardoveloso/spec-driven-agents) — Template base deste repositório
- [Adding repository custom instructions for GitHub Copilot](https://docs.github.com/copilot/customizing-copilot/adding-custom-instructions-for-github-copilot) — GitHub Docs

---

> **Princípio central**: especificações não são documentação — são o mecanismo pelo qual humanos mantêm intenção e controle em um processo de desenvolvimento cada vez mais autônomo. O agente gera; você verifica e corrige o rumo.

