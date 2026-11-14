# Callplus | Engineering Hub

Repositório institucional de **padrões de engenharia e colaboração** da organização [Callplus](https://github.com/Callplus-tech).

> Este repositório é público. Não publique credenciais, diagramas internos, endpoints privados, dados de clientes ou configurações sensíveis.

## Organização

| Documento | Finalidade |
| --- | --- |
| [Perfil institucional](profile/README.md) | Apresentação pública da organização |
| [Padrões de engenharia](docs/ENGINEERING.md) | Arquitetura, tecnologias e práticas recomendadas |
| [Governança](docs/governance/) | Nomes de repositórios, catálogo, política de acesso e fluxo de desenvolvimento |
| [Decisões (ADRs)](docs/decisions/) | Registro das decisões de arquitetura e governança |
| [Instruções para agentes de IA](AGENTS.md) | Regras para agentes que leem ou alteram os repositórios |
| [Contribuição](CONTRIBUTING.md) | Fluxo de mudanças, revisão e qualidade |
| [Segurança](SECURITY.md) | Comunicação responsável de vulnerabilidades |
| [Template de pull request](.github/PULL_REQUEST_TEMPLATE.md) | Checklist de revisão para mudanças |

## Plataforma e tecnologias

O ecossistema Callplus contempla aplicações web, APIs, integrações com canais de comunicação e automações de atendimento, CRM e Customer Success.

**Tecnologias utilizadas em partes da plataforma:** C#/.NET, ASP.NET Core, React, Next.js e TypeScript. Há integrações com canais de atendimento (WhatsApp, e-mail, telefonia e outros) e serviços de inteligência artificial.

As tecnologias e versões **variam conforme o repositório**. A fonte de verdade para build, dependências, execução e deploy é sempre a documentação e a configuração de cada projeto. Este documento não determina migração de versões nem publica detalhes de infraestrutura.

## Princípios de engenharia

- **Segurança por padrão:** menor privilégio, gestão de segredos e validação de entradas.
- **Mudanças rastreáveis:** issues, pull requests e histórico de decisões.
- **Qualidade verificável:** testes e verificações proporcionais ao risco.
- **Compatibilidade:** contratos de API e mudanças de banco avaliados antes do deploy.
- **Observabilidade:** logs estruturados, correlação e métricas sem exposição de dados sensíveis.
- **Operação responsável:** deploy controlado e plano de reversão quando aplicável.

Consulte os [padrões de engenharia](docs/ENGINEERING.md) para orientações detalhadas.

## Uso e colaboração

Os repositórios de produto podem ser privados. A publicação deste repositório **não concede acesso** a código, documentação interna ou ambientes da plataforma.

Antes de contribuir, leia [CONTRIBUTING.md](CONTRIBUTING.md). Para reportar uma vulnerabilidade, siga [SECURITY.md](SECURITY.md) e não abra issues públicas com detalhes exploráveis.

## Contato

- Site: https://callplus.com.br
- E-mail: contato@callplus.com.br

© Callplus. Todos os direitos reservados.
