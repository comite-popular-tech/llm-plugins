# Instruções para quem altera este repositório

- Este repositório guarda skills em `plugins/<plugin>/skills/<skill>/SKILL.md`. Cada skill tem um só `SKILL.md`, usado por todas as ferramentas; não duplique.
- Frontmatter só com os campos do padrão Agent Skills (`name`, `description`, `license`, `compatibility`, `metadata`, `allowed-tools`). `name` igual ao nome da pasta.
- Tudo em português do Brasil, curto. Sem nomes de pessoas como autoridade, sem contas, hosts, tokens ou caminhos de máquina.
- Cada `SKILL.md` fica com menos de 200 linhas; modelos e listas longas vão para um arquivo ao lado.
- Para abrir um PR aqui, siga `plugins/pr/skills/pr-abridor/SKILL.md`; para revisar, `plugins/pr/skills/pr-revisor/SKILL.md`.
- Antes de pedir revisão: `claude plugin validate .`
- O aviso de `version` ausente é esperado: sem `version`, cada commit vira uma versão nova para quem instalou. Não adicione `version`.
