---
name: pr-revisor
description: Como revisar o pull request de outra pessoa nos repositórios do Comitê Popular Tech. Use ao revisar, dar parecer, aprovar, pedir mudanças ou comentar um PR, e ao conferir um plano de deploy. Cobre a leitura do bloco "Para quem revisa", baixar e rodar os testes, conferir o diff, o veredito (aprovar, aprovar com ressalvas, pedir mudanças) e o formato dos comentários. Gatilhos - "revisa esse PR", "dá um parecer", "olha esse PR".
---

# pr-revisor

Referência de revisão da org, para pessoa ou LLM, em qualquer repositório. Vale igual para quem entrou hoje e para quem está há mais tempo: o que conta é o que foi conferido e o que está escrito.

## Regras de ouro

1. **O repo alvo prevalece.** Leia o `README`, o `CONTRIBUTING`, o `AGENTS.md`/`CLAUDE.md`, o `SECURITY.md` (se houver) e o template de PR antes de julgar. Convenção que o repo exige (título, idioma) pode justificar pedir mudanças.
2. **Quem é LLM não posta nada antes de a pessoa ler e aprovar o texto**: corpo da revisão, comentários inline, respostas e rascunhos de issue. Grave tudo em arquivos, mostre, espere o ok.
3. **Texto curto, uma vez.** Sem recapitular o PR, sem ressalva genérica.

## Passos

1. **Leia antes do diff.** Comece pelo bloco **"Para quem revisa"** no topo do corpo: é o que a pessoa que revisa precisa ler ou decidir, e a sua revisão responde a ele. Se o bloco não existe, aponte isso na revisão (como "pode melhorar") e deduza o que importa. Depois leia a issue ligada, os comentários e as threads existentes (não repita o que já foi dito) e as regras do repo. Anote o SHA do head e diga na revisão qual commit você conferiu.
2. **Confira o contexto de deploy.** O PR é de fork ou de branch do repo? O CI e o plano rodaram de verdade, ou só "não falhou"? Qual caminho vale (aplica no merge, ou alguém publica à mão) e o que o merge liga ou desliga?
3. **Baixe e rode.** Busque `pull/<n>/head` (por exemplo num worktree temporário) e siga primeiro os passos de **"Como testar"** do corpo; diga na revisão se passaram ou onde falharam. Se o bloco não existe, aponte como "pode melhorar". Depois rode a suíte do repo e reproduza qualquer bug suspeito antes de afirmar. Relate contagem e quais falhas também falham na main. Não apresente o resultado de testes do autor como se fosse seu.
4. **Confira o diff**, sem ordem fixa:
   - o que o PR promete contra o que entrega, e se toca algo fora do que o título diz;
   - correção: dê o cenário (entrada, saída errada);
   - perda de dados, privacidade e segurança, custo e exposição;
   - tamanho: se passa de uns 20 arquivos ou umas 1500 linhas e não está dividido nem justificado, diga; mas não reprove só por isso. Se você não conseguiu ler tudo, diga o que ficou de fora;
   - se a coisa é do app ou compartilhada, e se está no repo certo.
5. **Testes.** Falham sem a correção? Chamam o código ou só leem texto do arquivo? Cobrem todos os caminhos (cópias do mesmo código, as duas vias de deploy)?
6. **Infra e deploy.** O pré-requisito está em "Antes do merge" e foi feito? O plano foi lido? A main fica vermelha se o merge vier antes ou fora de ordem? Há "Se algo der errado"? Plano de deploy ou runbook: confira cada afirmação contra o código antes de aceitar.
7. **Texto do PR.** Promete algo que só vale com outro PR? A documentação do repo ainda contradiz? Há segredo, e-mail pessoal, caminho de máquina, dado de terceiros ou URL de sessão privada? Há trailer de IA nos commits? O corpo tem barras invertidas sobrando?
8. **Alegação técnica de quem contribui** ("o limite da API é X", "isso já está coberto"): confira na documentação ou no código e marque **confirmado**, **refutado** ou **não dá para saber** (e o acesso que faltou).
9. **Falha de segurança grave**: não comente em público. Siga o `SECURITY.md` do repo; sem ele, mande mensagem direta a alguém do time @comite-popular-tech/infra-sec-nucleo (https://github.com/orgs/comite-popular-tech/teams/infra-sec-nucleo), nunca em issue, PR ou comentário.

## Qualidade do código a fundo

Toda revisão também passa pelo roteiro da [thermo-nuclear-code-quality-review](https://github.com/cursor/plugins/blob/6e3d2ea56d7d446b955eaae6ac4c8eef8bf504cf/cursor-team-kit/skills/thermo-nuclear-code-quality-review/SKILL.md), em inglês: estrutura, arquivo que passa de mil linhas, condicional espalhada, abstração que não se paga, e a reestruturação que apaga complexidade em vez de mudá-la de lugar. Leia pelo link e não copie o texto: o repositório dela não tem licença. Os achados entram como "pode melhorar", salvo regressão estrutural clara; PR mergeável continua sem bloqueio.

## Veredito

- **Aprovar**: pode mergear, nada a mudar. Diga o que você conferiu; aprovação sem corpo não vale.
- **Aprovar com ressalvas**: pode mergear; só há itens "pode melhorar". PR mergeável não é bloqueado.
- **Pedir mudanças**: há pelo menos um problema real que precisa mudar antes do merge.

## Sugestão que amplia o escopo

Nunca é condição de merge. Poste a sugestão na revisão como **"pode melhorar"**. Se já existe uma issue que a cobre, cite a URL. Se não existe, julgue se ela merece uma issue nova; se merece, redija o rascunho (título e corpo curtos) e mostre à pessoa antes de abrir, como em qualquer texto. Com a issue aberta, cite a URL na revisão.

## Formato e tom

Use o [modelo de revisão](modelo-de-revisao.md): veredito primeiro, uma linha por item que precisa mudar, o que foi conferido, depois "pode melhorar".

- **Um só review** com todos os comentários inline, não um review por comentário. Poste tudo de uma vez com `gh api -X POST repos/<org>/<repo>/pulls/<n>/reviews --input revisao.json`, com `body`, `event`, `commit_id` e `comments` num arquivo JSON; nunca texto entre aspas no terminal. Veredito e `event`: Aprovar e Aprovar com ressalvas viram `APPROVE`; Pedir mudanças vira `REQUEST_CHANGES`.
- **Inline só para problema real** ou nit que valha uma linha. Abre com um resumo de uma linha; depois o cenário que quebra, a consequência e a correção, em poucas linhas, com bloco `suggestion` quando a mudança é aplicável. Nit vem marcado "pode melhorar", dizendo que não trava o merge.
- **Links de achado fixados no commit**: `https://github.com/<org>/<repo>/blob/<sha>/<caminho>#L10-L14`, nunca em `main`.
- **Informe** conflitos com outros PRs abertos e arquivos com o mesmo problema que o PR não tocou.
- **Não aprove por cortesia.** Se não achou nada, diga o que conferiu.
- **Relatório de ferramenta** só com resumo legível no corpo; blob codificado não é revisão.
- Sem segredo, e-mail pessoal ou caminho de máquina nos comentários.
- Referências a issues e PRs por URL completa.

## Depois da revisão

- **Resposta às suas threads** (quando a autora ou o autor corrige): curta, com o SHA do commit conferido.
- **Merge.** Mudança de infra ou de deploy precisa da aprovação de alguém que não seja a pessoa autora. PR pequeno e de baixo risco pode ser mergeado por quem o abriu. Quem mergeia cuida do pós-merge ou passa a quem tem acesso, e diz isso no PR; main vermelha é de quem mergeou ou de quem recebeu a passagem.
- **Fechar sem merge** sempre leva um comentário com o motivo (e o PR que o substitui, se houver).
