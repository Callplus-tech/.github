# ADR-001 — Governança do GitHub

- **Status:** Aceita
- **Data:** 2026-11-14

## Contexto

A Callplus desenvolve soluções que tratam dados de clientes e conversas de atendimento. A organização no GitHub foi criada em 14/11/2026 e já nasce com o mesmo padrão de governança da Ticket Pra Já, para evitar os problemas encontrados lá: qualquer membro alterando qualquer repositório, sem 2FA, sem proteção de branches e com credenciais gravadas no código.

## Decisão

Adotar o mesmo padrão de governança da Ticket Pra Já e da Ideavelo:

1. Plano GitHub Team, necessário para aplicar regras de proteção em repositórios privados.
2. Permissão base **nenhuma** e acesso por times, conforme a [política de acesso](../governance/access-policy.md).
3. 2FA obrigatório para todos os membros.
4. Proteção das branches por ruleset, conforme o [fluxo de desenvolvimento](../governance/fluxo-de-desenvolvimento.md).
5. Instruções para agentes de IA em `AGENTS.md`.

## Consequências

- Pessoas fora dos times não têm acesso aos repositórios privados; os times são criados antes de convidar as pessoas.
- Mudanças diretas na branch padrão e na `development` não são possíveis.
- Quem acompanha só projetos pode participar como colaborador externo de um repositório público, sem ocupar licença paga.
