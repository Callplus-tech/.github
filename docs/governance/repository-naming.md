# Padrão de nomenclatura de repositórios — v1.0

**Status:** aprovado em 14/11/2026 ([ADR-002](../decisions/ADR-002-repository-naming.md)).

## Regra

`{tipo}.callplus`, em minúsculas. O tipo vem primeiro; quando houver mais de um repositório do mesmo tipo, acrescente o nome antes do produto: `{tipo}.{nome}.callplus`.

| Tipo | Uso | Exemplo |
| --- | --- | --- |
| `api` | APIs e serviços de backend | `api.callplus` |
| `app` | Aplicação web principal | `app.callplus` |
| `web` | Outros sites e painéis | `web.admin.callplus` |
| `integration` | Integrações com canais e sistemas de terceiros | `integration.whatsapp.callplus` |
| `worker` | Processamento assíncrono, filas e automações | `worker.callplus` |
| `infra` | Infraestrutura e automação operacional | `infra.callplus` |
| `lib` | Bibliotecas compartilhadas | `lib.callplus` |
| `e2e` | Testes de ponta a ponta | `e2e.callplus` |

Exceção: `.github` (repositório institucional).

## Metadados obrigatórios

Todo repositório deve ter:

- **Descrição** de uma linha.
- **Topics**: o tipo (`api`, `app`...), a tecnologia principal (`dotnet`, `nextjs`...) e o estado (`producao`, `legado` ou `em-desenvolvimento`).
- **README** com propósito, como executar localmente e onde é implantado (sem endereços internos ou segredos).
- **Time responsável** com acesso definido conforme a [política de acesso](access-policy.md).
