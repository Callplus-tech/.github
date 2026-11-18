# Infraestrutura no Coolify

Inventário da infraestrutura dos produtos Callplus no Coolify. Decisão registrada na [ADR-005](../decisions/ADR-005-infraestrutura-coolify.md).

> **Situação em 18/11/2026:** Postgres e Keycloak **em execução e saudáveis** nos dois ambientes. Backup **pendente**. Nenhum produto conectado ainda.

## Servidor

| Item | Valor |
|---|---|
| Provedor | Hostinger (VPS com Ubuntu e Coolify), conta separada da Ideavelo |
| Recursos | 16 GB de RAM, 200 GB de disco |
| IP público | `187.53.121.97` |
| Painel | https://coolify.callplus.com.br (Coolify 4.7.5, time **Root Team**) |
| Servidor no Coolify | `localhost` (`zcjbxldunfkvdo44gmrw7rd1`) |
| DNS | `*.callplus.com.br` aponta para o IP da VPS (registro curinga); subdomínio novo não precisa de registro |

## Projeto `Infrastructure`

UUID `dkbypdpjsoyfgywq3sm4mltz`. Recursos compartilhados pelos produtos, com produção isolada do resto.

| Ambiente | UUID | Uso |
|---|---|---|
| `production` | `2izxy2ehorukagsmqeluvc2v` | Produção |
| `non-production` | `p1hz47bk8b8qcrsfcxjbieoq` | Development e staging |

### Recursos

| Recurso | Ambiente | Tipo | UUID | Endereço | Situação |
|---|---|---|---|---|---|
| `shared-postgres` | production | PostgreSQL `postgres:17-alpine`, limite 4 GB | `fjquya0aarhzaoimtioz7tg1` | interno: `fjquya0aarhzaoimtioz7tg1:5432` | em execução |
| `shared-postgres-dev` | non-production | PostgreSQL `postgres:17-alpine`, limite 2 GB | `wjdmyxek0g3lpfc0o9t4sfz9` | interno: `wjdmyxek0g3lpfc0o9t4sfz9:5432` | em execução |
| `keycloak` | production | Serviço (Compose) `quay.io/keycloak/keycloak:26.4` | `dcdhgyofskvfyzzzcho3dx6x` | https://id.callplus.com.br | em execução, `/realms/master` respondendo 200 |
| `keycloak-dev` | non-production | Serviço (Compose) `quay.io/keycloak/keycloak:26.4` | `kui7g83pkpgcfyqyetnzqugq` | https://id-dev.callplus.com.br | em execução, `/realms/master` respondendo 200 |

Os bancos **não são públicos**. Aplicações e serviços acessam pela rede Docker do Coolify, pelo UUID do banco como host.

### Padrão dos bancos

- Usuário administrador `platform_admin`, banco inicial `platform`. Só a infraestrutura usa esse usuário.
- Cada produto ganha **um banco e um usuário próprios** em cada ambiente. No `shared-postgres-dev`, development e staging têm bancos separados (por exemplo `crm_dev` e `crm_staging`).

### Como o Keycloak cria o próprio banco

O Compose de cada Keycloak tem dois contêineres:

1. `keycloak-db-init` (`postgres:17-alpine`): espera o Postgres, cria ou atualiza o usuário `keycloak` com a senha gerada pelo Coolify e cria o banco `keycloak`. Roda a cada subida e é idempotente.
2. `keycloak`: sobe só depois do init terminar com sucesso. Modo `start`, HTTP atrás do proxy do Coolify (`KC_PROXY_HEADERS=xforwarded`), health check em `/health/ready` na porta 9000.

## Onde ficam as credenciais

Os valores **não** são registrados aqui. Todos ficam no Coolify.

| Credencial | Onde |
|---|---|
| Senha do `platform_admin` de cada Postgres | Página do banco → **Configuration → Credentials → Password** |
| Senha do admin do Postgres usada pelo init do Keycloak | Variável `SHARED_PG_ADMIN_PASSWORD` do serviço (literal), copiada da senha acima |
| Senha do usuário `keycloak` no Postgres | Variável `SERVICE_PASSWORD_KCDB` do serviço, gerada pelo Coolify |
| Admin do Keycloak (realm `master`) | Variáveis `SERVICE_USER_KCADMIN` e `SERVICE_PASSWORD_KCADMIN` do serviço, geradas pelo Coolify |

Se a senha de um Postgres for trocada, atualize também o `SHARED_PG_ADMIN_PASSWORD` do Keycloak do mesmo ambiente.

## Acesso dos agentes

- O Coolify expõe o MCP em `https://coolify.callplus.com.br/mcp`, com a API ligada em **Settings → Advanced → API and MCP**.
- O conector **Coolify Callplus** do Claude usa o token de API `claude-callplus`, com as permissões **read, write e deploy** e sem `read:sensitive` (não lê valores de variáveis), `delete` ou `root`. Vence em **16/02/2027**; renove antes em **Keys & Tokens → API Tokens** e atualize o cabeçalho `authorization` do conector.
- A lista **Allowed IPs** da API está vazia (aberta a qualquer origem), protegida só pelo token.

## Pendências

- [ ] Backup diário dos dois Postgres para um armazenamento fora da VPS (S3 ou compatível). Hoje **não há backup**.
- [ ] Realm `callplus` e clients do `api.callplus` e do `app.callplus` nos dois Keycloak.
- [ ] Bancos e usuários de cada produto e ambiente.
- [ ] GitHub App da Callplus-tech no Coolify e criação das aplicações `api.callplus` e `app.callplus`.
- [ ] Notificações do Coolify (nenhum canal configurado).
- [ ] Remover o projeto de teste `My first project` (app `nginx-teste` em `teste.callplus.com.br`), se não for mais usado.
