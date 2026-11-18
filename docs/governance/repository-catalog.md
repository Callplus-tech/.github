# Catálogo de repositórios — v1.0

Inventário de 2026-11-14, atualizado em 2026-11-18.

| Repositório | Tipo | Tecnologia | Estado | Observação |
| --- | --- | --- | --- | --- |
| `api.callplus` | API | C# / .NET 10 | Em desenvolvimento | Mesmas configurações da `api.v2.ticketpraja` |
| `app.callplus` | App web | Next.js / TypeScript | Em desenvolvimento | Mesmas configurações do `marketplace.ticketpraja`, conduzido pelo Claude |
| `app.acl.meli1p.crm.callplus` | App desktop + API | C# / .NET Framework 4.x (Windows Forms, ASP.NET Web API) | Produção | CRM/tabulador da operação ACL Mercado Livre 1P. Cópia, com histórico, do `HMB-Tecnologia/CALLPLUS_ACL_MP_ML1P` (14/11/2026). Build em Windows (`build-dotnet-framework.yml`) |
| `web.callplus` | Site | HTML / CSS | Em desenvolvimento | Site institucional em `callplus.com.br`, página estática no mesmo formato do `Ideavelo/website` (criado em 18/11/2026) |
| `infra.callplus` | Infraestrutura | Markdown | Ativo | Inventário e decisões de infraestrutura da plataforma, tema do Keycloak e kit de identidade visual (privado, criado em 18/11/2026) |
| `.github` | Institucional | Markdown | Ativo | Padrões, modelos e automações da organização |

## Regras

- Repositório novo só é criado seguindo o [padrão de nomes](repository-naming.md) e é adicionado a este catálogo no mesmo PR.
- Repositório sem uso há mais de 12 meses deve ser **arquivado**, não apagado, após confirmação do PO.
- Este catálogo não registra endereços, servidores ou credenciais.
