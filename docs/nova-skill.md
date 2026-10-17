# Criar uma skill ou um plugin

Os critérios de texto de uma skill estão no [README](../README.md#como-contribuir). Aqui, a parte mecânica.

## Skill nova num plugin existente

1. Crie `plugins/<plugin>/skills/<skill>/SKILL.md`. O nome da pasta é o `name` do frontmatter.
2. O frontmatter leva só `name` e `description`; a `description` diz quando usar e traz os gatilhos.
3. Mantenha o `SKILL.md` com menos de 200 linhas. Modelo ou lista longa vai para um arquivo ao lado, como
   `modelo-de-corpo.md` na `pr-abridor`.
4. Acrescente a skill à tabela de skills e à seção "Estrutura" do README.
5. Rode `claude plugin validate .`.

## Plugin novo

1. Crie `plugins/<plugin>/.claude-plugin/plugin.json` (copie o de `plugins/pr/` e ajuste `name`, `description` e
   `keywords`). Não adicione `version`.
2. Registre o plugin em `plugins` no `.claude-plugin/marketplace.json`, com `name`, `source` (`./plugins/<plugin>`) e
   `description`.
3. Atualize o README (skills, instalação com `claude plugin install <plugin>@comite-popular-tech`, estrutura).
4. Rode `claude plugin validate .`.

## Revisão

A aprovação que conta é de quem está em `.github/CODEOWNERS`.
