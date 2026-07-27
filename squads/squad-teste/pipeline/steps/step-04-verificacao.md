---
id: verificacao
agent: orquestrador
execution: inline
model_tier: fast
inputFile: squads/squad-teste/output/{run_id}/article-final.md
outputFile: squads/squad-teste/output/{run_id}/quality-check.md
---

Leia o artigo final e faça uma verificação objetiva.

Responda:

- o artigo fala sobre o Deserto do Atacama?
- tem estrutura de artigo?
- o tom está natural?
- há sinais de texto robótico?
- o texto está aprovado para este teste local?

Salve a verificação em `squads/squad-teste/output/{run_id}/quality-check.md`.
