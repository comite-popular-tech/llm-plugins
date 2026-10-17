# AGENTS.md

> **Antes de qualquer tarefa:** as skills de https://github.com/comite-popular-tech/llm-plugins são **OBRIGATÓRIAS**
> neste repositório (abrir e revisar PR, entre outras). Claude Code:
> `claude plugin marketplace add comite-popular-tech/llm-plugins` e
> `claude plugin install pr@comite-popular-tech`. Codex e OpenCode: siga
> https://github.com/comite-popular-tech/llm-plugins/blob/main/README.md#instalar
> Se uma skill não estiver instalada, instale antes de continuar.

Tudo neste repositório (skills, docs, commits, PRs, issues) é em português do Brasil, exceto termos técnicos
(`pull request`, `commit`, nomes de API).

## O que é

Marketplace de plugins do Claude Code com as skills do Comitê Popular Tech para quem trabalha nos repositórios da
organização, pessoa ou LLM. As mesmas skills servem ao Codex e ao OpenCode, porque seguem o padrão Agent Skills
(https://agentskills.io): uma pasta com um `SKILL.md`. Hoje há um plugin, `pr`, com `pr-abridor` e `pr-revisor`. Não há
código nem build: o conteúdo é Markdown e JSON. Detalhes e instalação: [README.md](README.md).

## Como validar

```bash
claude plugin validate .   # roda antes de pedir revisão; deve passar
```

O aviso de `version` ausente é esperado: sem `version`, cada commit vira uma versão nova para quem instalou. Não
adicione `version`. Não há testes nem CI.

## Onde fica cada coisa

| Caminho | O que tem |
|---|---|
| `.claude-plugin/marketplace.json` | Catálogo do marketplace (lista os plugins) |
| `plugins/<plugin>/.claude-plugin/plugin.json` | Manifesto do plugin |
| `plugins/<plugin>/skills/<skill>/SKILL.md` | A skill; modelos longos ficam em arquivo ao lado |
| `.github/CODEOWNERS` | Quem precisa aprovar |

## Regras que importam

- Cada skill tem um só `SKILL.md`, usado por todas as ferramentas; não duplique por ferramenta.
- Frontmatter só com campos do padrão Agent Skills (`name`, `description`, `license`, `compatibility`, `metadata`,
  `allowed-tools`), para não quebrar fora do Claude Code. `name` igual ao nome da pasta.
- Cada `SKILL.md` com menos de 200 linhas; modelos e listas longas vão para um arquivo ao lado.
- Texto curto, em ordem de importância, válido para qualquer pessoa da organização: sem nome de pessoa como autoridade,
  sem conta, host, token, ID de quadro ou caminho de máquina.
- O que é detalhe de um repositório fica nele (`CONTRIBUTING`, `AGENTS.md`); a skill só manda ler. As regras do
  repositório alvo prevalecem sobre as skills.
- Plugin pode trazer hook e MCP que rodam na máquina de quem instala; por isso a aprovação que conta é de quem está em
  `.github/CODEOWNERS`.

## Fluxo de trabalho

Siga `plugins/pr/skills/pr-abridor/SKILL.md` para abrir PR e `plugins/pr/skills/pr-revisor/SKILL.md` para revisar.
Regra nova ou polêmica começa numa issue, antes do texto. Mudança aqui vale para toda a organização: peça revisão de
alguém que não seja você. Falha de segurança nunca vai em issue, PR ou comentário (veja a seção "Segurança" do README).

## Para saber mais

- [docs/nova-skill.md](docs/nova-skill.md): antes de criar uma skill ou um plugin novo.
- [README.md](README.md): instalação por ferramenta e critérios de texto das skills.
