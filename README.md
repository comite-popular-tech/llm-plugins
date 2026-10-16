# llm-plugins

Skills em português do Brasil para quem trabalha nos repositórios do [Comitê Popular Tech](https://github.com/comite-popular-tech), pessoa ou LLM, de qualquer iniciativa. O repositório é um marketplace de plugins do Claude Code, e as mesmas skills funcionam no Codex e no OpenCode, porque todas seguem o padrão [Agent Skills](https://agentskills.io): uma pasta com um `SKILL.md`.

## Skills

| Skill | Para quê |
|---|---|
| [`pr-abridor`](plugins/pr/skills/pr-abridor/SKILL.md) | Abrir um pull request: issue antes do código, tamanho, testes, corpo com "Para quem revisa", "Como testar", "Antes do merge" e "Se algo der errado" |
| [`pr-revisor`](plugins/pr/skills/pr-revisor/SKILL.md) | Revisar o pull request de outra pessoa: o que ler, o que rodar, veredito e formato dos comentários |

As skills não substituem as regras de cada repositório. Elas mandam ler o `README`, o `CONTRIBUTING`, o `AGENTS.md`/`CLAUDE.md` e o template de PR do repo alvo, e esses prevalecem.

## Instalar

### Claude Code

```bash
claude plugin marketplace add comite-popular-tech/llm-plugins
claude plugin install pr@comite-popular-tech
```

Dentro de uma sessão, os mesmos comandos são `/plugin marketplace add ...` e `/plugin install ...`. As skills entram como `/pr:pr-abridor` e `/pr:pr-revisor`, e o Claude também as usa sozinho quando o pedido combina com a descrição ("abre um PR", "revisa esse PR"). Para atualizar: `claude plugin marketplace update comite-popular-tech` e depois `claude plugin update pr@comite-popular-tech`, ou ligue a atualização automática em `/plugin` → Marketplaces.

### Codex

O Codex lê skills de `.agents/skills/` (no repositório, de onde você abre o Codex até a raiz) e de `~/.agents/skills/` (pessoal). Clone este repositório e copie ou aponte as pastas:

```bash
git clone https://github.com/comite-popular-tech/llm-plugins.git
mkdir -p ~/.agents/skills
ln -s "$PWD/llm-plugins/plugins/pr/skills/pr-abridor" ~/.agents/skills/pr-abridor
ln -s "$PWD/llm-plugins/plugins/pr/skills/pr-revisor" ~/.agents/skills/pr-revisor
```

O Codex segue links simbólicos. Reinicie o Codex se as skills não aparecerem; chame com `$pr-abridor` ou `$pr-revisor`. Para atualizar, rode `git pull` no clone.

### OpenCode

O OpenCode procura em `.opencode/skills/`, `.agents/skills/` e `.claude/skills/` (no projeto) e em `~/.config/opencode/skills/`, `~/.agents/skills/` e `~/.claude/skills/` (pessoal). Se já fez os links do Codex, o OpenCode já os enxerga; senão, copie as pastas das skills para um desses lugares, por exemplo:

```bash
mkdir -p ~/.config/opencode/skills
cp -r llm-plugins/plugins/pr/skills/pr-abridor llm-plugins/plugins/pr/skills/pr-revisor ~/.config/opencode/skills/
```

O agente carrega a skill pela ferramenta `skill` quando a tarefa combina com a descrição. Para atualizar, copie de novo.

### Outras ferramentas

Qualquer ferramenta que leia o padrão Agent Skills serve: aponte para as pastas `plugins/pr/skills/<skill>/`. Se a ferramenta só lê `AGENTS.md`, peça no `AGENTS.md` do seu projeto para ler o `SKILL.md` da skill antes de abrir ou revisar um PR.

## Estrutura

```text
.claude-plugin/marketplace.json         catálogo do marketplace
plugins/pr/.claude-plugin/plugin.json   manifesto do plugin
plugins/pr/skills/pr-abridor/           SKILL.md + modelo-de-corpo.md
plugins/pr/skills/pr-revisor/           SKILL.md + modelo-de-revisao.md
```

Cada skill tem um só `SKILL.md`, usado pelas três ferramentas. O frontmatter usa só os campos do padrão (`name` e `description`), para não quebrar fora do Claude Code.

## Como contribuir

1. Abra uma issue com a mudança que você quer, ou comente numa existente. Regra nova ou polêmica começa ali, antes do texto.
2. Faça a mudança num branch (ou fork, se não tiver escrita) e abra o PR seguindo o [`pr-abridor`](plugins/pr/skills/pr-abridor/SKILL.md).
3. A revisão segue o [`pr-revisor`](plugins/pr/skills/pr-revisor/SKILL.md). Mudança neste repositório vale para todo mundo da org, então peça a revisão de alguém que não seja você. A aprovação que conta é de quem está no `.github/CODEOWNERS`, porque plugin pode trazer hook e MCP que rodam na máquina de quem instala.
4. Antes de pedir revisão: `claude plugin validate .`

Critérios para o texto de uma skill:

- português do Brasil, curto, em ordem de importância; `SKILL.md` com menos de 200 linhas, e modelos longos em arquivo ao lado;
- vale para qualquer pessoa da org: sem hierarquia, sem nome de pessoa como autoridade;
- nada interno: conta, zona, host, token, caminho de máquina, quadro ou ID de ninguém;
- o que é detalhe de um repositório fica no repositório (`CONTRIBUTING`, `AGENTS.md`); a skill só manda ler.

## Segurança

Falha de segurança: mande mensagem direta a alguém do time @comite-popular-tech/infra-sec-nucleo (https://github.com/orgs/comite-popular-tech/teams/infra-sec-nucleo), nunca em issue, PR ou comentário.
