# ADR-005 — Infraestrutura no Coolify

- **Status:** Aceita
- **Data:** 2026-11-18

## Contexto

Os novos produtos da Callplus (`api.callplus` em .NET 10 e `app.callplus` em Next.js) precisam de banco de dados e de autenticação. A Callplus contratou uma VPS na Hostinger, com Ubuntu e Coolify (16 GB de RAM, 200 GB de disco). Na Ideavelo, o padrão é PostgreSQL e Keycloak compartilhados no projeto `Infrastructure` do Coolify, com um banco e um usuário por produto, e produção numa VPS separada.

## Decisão

- **Uma VPS para tudo:** development, staging e produção ficam no mesmo Coolify (`coolify.callplus.com.br`).
- **Produção isolada por instância:** o projeto `Infrastructure` tem dois ambientes, cada um com o próprio PostgreSQL e o próprio Keycloak:
  - `production`: `shared-postgres` e `keycloak` (`id.callplus.com.br`);
  - `non-production`: `shared-postgres-dev` e `keycloak-dev` (`id-dev.callplus.com.br`), usados por development e staging.
- **Mesmo padrão da Ideavelo:** PostgreSQL 17, Keycloak 26.4 com banco no Postgres compartilhado, um banco e um usuário por produto e ambiente.
- Credenciais ficam só no Coolify; o repositório registra apenas onde cada uma está.

O inventário e a operação estão em [Infraestrutura no Coolify](../infraestrutura/coolify.md).

## Consequências

- Uma falha da VPS derruba todos os ambientes ao mesmo tempo. Backup fora da VPS é obrigatório antes de dados reais.
- Testes em development ou staging não afetam o banco nem os usuários de produção, mas competem pela mesma CPU e memória. Os limites de memória dos bancos (4 GB em produção, 2 GB fora) reservam espaço para produção.
- Separar produção numa VPS própria no futuro exige migrar `shared-postgres` e `keycloak`, sem mudar o restante do padrão.
