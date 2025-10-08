# Spec Driven Agents
Template para desenvolvimento orientado a especificações com modo de agente no VS Code

## Contexto
https://hammansamuel.medium.com/from-vibe-coding-to-spec-driven-development-c9aec008a81c

## Resumo
O artigo discute a evolução do desenvolvimento de software na era da Inteligência Artificial Generativa (GenAI) e da IA Agente, focando na transição do "Vibe Coding" para o Desenvolvimento Orientado por Especificação (Spec-Driven Development - SDD).

Do "Vibe Coding" ao Desenvolvimento Orientado por Especificação
### 1. O Fenômeno "Vibe Coding" e Seus Limites

O "Vibe Coding" (Codificação por Vibe) refere-se ao uso de linguagem natural e conversas informais com a IA para gerar código. Embora seja rápido e acessível para protótipos, ele é criticado em círculos de desenvolvimento sério por levar à falta de disciplina de engenharia. Os principais problemas são:

Inconsistência Arquitetural: A IA foca na tarefa imediata e não entende a arquitetura geral, gerando código que pode entrar em conflito com decisões anteriores.

Desalinhamento de Equipe: Sem um entendimento compartilhado, cada desenvolvedor e agente de IA toma decisões isoladas.

Dívida Técnica: A natureza espontânea da abordagem resulta em má documentação e código que se afasta do plano original.

### 2. A Ascensão do Spec-Driven Development (SDD)

O SDD não é novo, mas ganha um papel mais crucial com a IA. Ele passa a ser o "contrato vivo" e a abordagem de "humano no meio" para guiar agentes de IA autônomos. As especificações modernas são divididas em três tipos de artefatos, que são lidos e interpretados por agentes de IA:

Requisitos: Capturam o "o quê" e o "porquê" (lógica de negócios e restrições).

Design (Arquitetura): Define a arquitetura técnica, limites de componentes e fluxo de dados.

Implementação: Quebra o trabalho em tarefas discretas e gerenciáveis, servindo como um roteiro.

### 3. Por Que Arquitetos Estão Adotando o SDD

A abordagem SDD fornece a estrutura necessária para que a IA seja utilizada de forma escalável e sustentável:

Controle: Permite que os arquitetos estabeleçam limites e garantam que a IA opere dentro da coerência arquitetural definida.

Escalabilidade: Mantém o alinhamento entre múltiplos agentes de IA e desenvolvedores humanos em sistemas complexos.

Persistência: As especificações atuam como uma memória para o processo de desenvolvimento, fornecendo uma fonte única de verdade (Source of Truth).

### Conclusão:

A mudança do "Vibe Coding" para o SDD representa uma elevação no nível de abstração para os arquitetos, que passam a focar no design e nas restrições do sistema ("o quê" e "porquê"), enquanto deixam a IA lidar com os detalhes de implementação ("como"). Essa abordagem sistemática e baseada em configuração é vista como a chave para aproveitar o potencial da IA na construção de software de alta qualidade e sustentável a longo prazo.
