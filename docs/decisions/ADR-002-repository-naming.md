# ADR-002 — Nomenclatura de repositórios

- **Status:** Aceita
- **Data:** 2026-11-14

## Decisão

Usar `{tipo}.callplus`, em minúsculas, conforme o [padrão de nomes](../governance/repository-naming.md). Os primeiros repositórios são `api.callplus` e `app.callplus`.

## Renomeações

Renomear um repositório pode quebrar integrações de deploy e scripts que usam a URL. Por isso, cada renomeação:

1. Acontece em janela combinada, um repositório por vez.
2. Confere antes quais integrações usam o repositório.
3. Atualiza as integrações e confirma o deploy logo depois.

O GitHub redireciona a URL antiga, mas esse redirecionamento não deve ser usado como solução permanente.
