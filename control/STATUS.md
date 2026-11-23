# Status

## A conferir

- Os planos históricos têm etapas sem marca de conclusão, mas já existem implementações correspondentes; conferir quais etapas ainda se aplicam antes de tratá-las como backlog atual — fonte: [planos](plans/) e [implementação da instalação](../src/init.js).
- A checklist de desenvolvimento descreve espelhos obrigatórios do core e de skills em templates, mas o instalador usa fontes canônicas e copia skills diretamente; conferir a atualização dessas instruções — fonte: `.claude/skills/opensquad-dev/SKILL.md`, seções “How opensquad Distribution Works” e “Check A/B/H”, [src/init.js](../src/init.js) e [plano de eliminação de duplicação](plans/superpowers/2026-03-27-eliminate-template-duplication.md).
- As instruções herdadas descrevem `/opensquad dashboard` e geração de um site por squad; confirmar a vigência desse fluxo diante da aplicação Vite compartilhada — fonte: [README](../README.md), linhas 81 e 233, [README de instalação](../src/readme/README.md) e [dashboard](../dashboard/src/App.tsx).

## Tarefas abertas

| id | título | estado | depende de | indispensável | evidência |
|---|---|---|---|---|---|
| T-001 | Validar com Claude o plano de adaptação multiplataforma antes da implementação (specs/cross-platform.md, Portabilidade) | TODO | | | |
| T-002 | Criar src/runtime.js para operações de arquivos, JSON, run_id, versões e paths com node:path (specs/cross-platform.md, Portabilidade) | TODO | T-001 | | |
| T-003 | Substituir Bash no runner: gates, pastas de execução, cópia de estado, migração de memória e versões (specs/cross-platform.md, Runner) | TODO | T-001 | | |
| T-004 | Revisar paths nos exemplos, .mcp.json e templates de IDE para Windows, Linux e macOS (specs/cross-platform.md, Portabilidade e Templates) | TODO | | | |
| T-005 | Traduzir instruções para português brasileiro e documentar GPT, VS Code e Codex, preservando identificadores técnicos em inglês (specs/cross-platform.md, Templates e documentação instrutiva) | TODO | | | |
| T-006 | Adicionar testes de operações de arquivo e paths Windows/POSIX (specs/cross-platform.md, Portabilidade) | TODO | T-001 | | |

## Verificações pendentes

- Executar no Windows npm ci, npm test, npm run lint e, em dashboard/, npm ci, npm run build e npm audit --omit=dev — fonte: [requisitos de validação](../specs/cross-platform.md#validação).
- Executar npm audit --omit=dev em dashboard/ no Linux; a tentativa de 2026-11-21 não consultou o registro npm por falha de DNS (EAI_AGAIN), sem resultado de vulnerabilidades — fonte: [requisitos de validação](../specs/cross-platform.md#validação).
- Executar uma squad simples no Linux e no Windows, conferir leitura de state.json no dashboard e equivalência lógica dos outputs — fonte: [requisitos de validação](../specs/cross-platform.md#validação).
- Confirmar funcionamento do Playwright MCP com paths relativos em todos os sistemas previstos — fonte: [requisitos de portabilidade](../specs/cross-platform.md#portabilidade-entre-sistemas-operacionais).

## Débitos técnicos

- O runner exige Bash para gates de entrada/saída, criação de pastas, versões e cópia do estado; a adaptação multiplataforma está registrada em T-002/T-003 — fonte: [runner](../_opensquad/core/runner.pipeline.md), seção “Initialization” (item “Initialize run folder”), item “Pre-Step Input Validation” em “For each pipeline step” e seção “Post-Step Output Validation”, e [requisitos](../specs/cross-platform.md).
- Com dashboard/dist presente após npm run build, a instalação copia o build para o destino e falha o teste “init does not copy dashboard node_modules or dist to user project” (tests/init.test.js:513; asserção em :523); DASHBOARD_EXCLUDES não inclui dist — fonte: [src/init.js](../src/init.js), constante DASHBOARD_EXCLUDES, e [teste](../tests/init.test.js).
- A skill image-ai-generator manda executar skills/image-generator/scripts/generate.py, caminho anterior à renomeação da pasta; o script existe em skills/image-ai-generator/scripts/generate.py — fonte: [SKILL.md](../skills/image-ai-generator/SKILL.md), linhas 58, 69 e 81.

## Decisões em aberto

- Definir se a documentação específica de GPT, VS Code e Codex deve ficar em AGENTS.md, CODEX.md ou outro arquivo, considerando o AGENTS.md já existente — fonte: [requisitos de documentação](../specs/cross-platform.md#templates-e-documentação-instrutiva).
