# ADR-004 — Fluxo de desenvolvimento orientado por issue e executado por agente de IA

- **Status:** Aceita
- **Data:** 2026-11-14
- **Decisor:** Rafael (PO)

## Contexto

A Callplus começa a desenvolver seus produtos em 14/11/2026 e adota desde o início o fluxo já validado na Ticket Pra Já: agentes de IA (Claude Code e Cursor) escrevem a maior parte do código, com o desenvolvedor no papel de revisor, e cada tarefa é rastreável da issue à produção.

## Decisão

1. **Um board único** (projeto 1 da organização) para todos os repositórios, com os status Backlog → Pronto → Em andamento → Em revisão → Homologação → Aprovado → Concluído, mais Bloqueado. Aprovado é marcado pelo PO depois do teste em homologação, e o PR de release mostra em vermelho o que ainda não foi aprovado.
2. **Toda mudança nasce de uma issue** criada por formulário com critérios de aceite obrigatórios.
3. **Branches**: `development` = homologação; branch padrão = produção; trabalho em `tipo/NUMERO-descricao`.
4. **Conventional Commits** em títulos de PR e commits, com descrição em português (ADR-003).
5. **Status do board é automático** a partir de eventos do GitHub, via workflow reutilizável e GitHub App.
6. **Padrão verificado por máquina**: workflow `padrao-pr.yml` como check obrigatório nos repositórios de produto.
7. **Agente orientado por regra versionada** (`AGENTS.md`, lido pelo Cursor diretamente e pelo Claude Code via `CLAUDE.md`): só trabalha a partir de issue e só commita após aprovação do desenvolvedor.
8. **Pendências com o PO por label**: `needs-owner` move o card para Bloqueado e avisa o Rafael; só ele remove o label, e a remoção devolve a tarefa ao responsável. Impedimentos técnicos usam `blocked`. Mesmo padrão adotado na Ticket Pra Já e na Ideavelo.
9. **Merges em dois níveis**: em `development`, o próprio desenvolvedor mescla o seu PR com a validação verde, sem revisão de outra pessoa, adequado ao tamanho da equipe; em produção (`main`/`master`, inclusive hotfix), o PR é obrigatório, sem exigência de aprovação, e só o PO mescla. Garantido pelos rulesets da organização `protege-development` e `producao-somente-po`; os limites estão no documento do fluxo. O repositório `.github` segue a mesma regra de produção.
10. **Todos os repositórios já nascem no fluxo.** Diferente da Ticket Pra Já, não há repositório legado para migrar.

## Consequências

- Rastreabilidade completa: issue → branch → PR → homologação → produção.
- O desenvolvedor não arrasta cards nem escreve boilerplate; foca em descrever e revisar.
- Exige um GitHub App com acesso a Projects e o ambiente de homologação ligado à `development` em cada repositório.

## Alternativas consideradas

- **Jira/Linear**: mais um sistema e custo por usuário; o GitHub Projects já está incluído no plano Team e integra nativamente com PRs.
- **Workflows nativos do Projects apenas**: não diferenciam merge em `development` de merge em produção.
