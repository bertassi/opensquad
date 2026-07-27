# TODO

## Portabilidade entre sistemas operacionais

- Validar o plano de adaptação cross-platform com Claude antes da implementação.
- Remover dependência obrigatória de Bash no fluxo core.
- Substituir comandos como `test -s`, `mkdir -p`, `grep`, `ls`, `sort`, `tail` e `cp` por operações Node.js.
- Criar uma camada utilitária cross-platform em `src/runtime.js`.
- Centralizar nessa camada:
  - validação de arquivo existente e não vazio;
  - criação recursiva de diretórios;
  - cópia de arquivos;
  - leitura e escrita de JSON;
  - geração de `run_id`;
  - detecção de versões de output;
  - normalização de paths.
- Garantir que paths sejam tratados com APIs de `node:path`, sem assumir `/` ou `\`.
- Evitar paths absolutos específicos de Linux ou Windows nos exemplos e templates.
- Revisar `.mcp.json` e templates de IDE para confirmar compatibilidade com Windows, Linux e macOS.
- Verificar se o Playwright MCP funciona com paths relativos em todos os sistemas.
- Adicionar testes automatizados para cenários com paths estilo Windows e POSIX.
- Validar o projeto em Linux e Windows antes de cada PR relevante.

## Runner

- Atualizar `_opensquad/core/runner.pipeline.md` para não exigir Bash como contrato de execução.
- Trocar gates baseados em Bash por validações baseadas em operações de arquivo cross-platform.
- Remover instruções que mandam executar comandos shell para validação de input/output.
- Atualizar lógica de criação de pasta de execução para usar operação abstrata.
- Atualizar lógica de cópia de `state.json` para operação abstrata.
- Atualizar lógica de migração de memória para não depender de `grep`.
- Atualizar lógica de detecção de versões para não depender de `ls`, `grep`, `sort` e `tail`.

## Templates e documentação instrutiva

- Traduzir para português os documentos instrutivos usados pelos agentes e pelo runtime.
- Criar documentação específica sobre uso com GPT, VS Code e Codex, equivalente ao papel do `CLAUDE.md`.
- Avaliar se essa documentação deve ser `AGENTS.md`, `CODEX.md` ou outro nome mais adequado ao padrão do Codex.
- Priorizar:
  - `AGENTS.md`;
  - `CLAUDE.md`;
  - `_opensquad/core/runner.pipeline.md`;
  - `_opensquad/core/architect.agent.yaml`;
  - `_opensquad/core/prompts/*.md`;
  - `templates/ide-templates/**`;
  - `skills/**/SKILL.md`, quando forem instruções exibidas ou seguidas por agentes.
- Manter nomes de arquivos, chaves YAML, comandos e APIs em inglês quando forem identificadores técnicos.
- Padronizar o idioma de saída como português brasileiro.
- Revisar exemplos para evitar comandos dependentes de shell específico.

## Validação

- Rodar no Linux:
  - `npm test`;
  - `npm run lint`;
  - `cd dashboard && npm run build`;
  - `cd dashboard && npm audit --omit=dev`.
- Rodar no Windows:
  - `npm ci`;
  - `npm test`;
  - `npm run lint`;
  - `cd dashboard && npm ci`;
  - `cd dashboard && npm run build`;
  - `cd dashboard && npm audit --omit=dev`.
- Executar uma squad simples no Linux e no Windows.
- Confirmar que o dashboard lê `state.json` corretamente nos dois sistemas.
- Confirmar que outputs são criados no mesmo formato lógico em ambos os sistemas.

## Critério de pronto

- O projeto roda em Windows, Linux e macOS sem exigir Bash, Git Bash ou WSL.
- O runner não contém comandos shell como requisito funcional.
- Os documentos instrutivos principais estão em português brasileiro.
- Testes automatizados cobrem operações de arquivo multiplataforma.
- Dashboard e CLI passam nas validações locais.
