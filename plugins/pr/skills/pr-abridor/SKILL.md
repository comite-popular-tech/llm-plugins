---
name: pr-abridor
description: Como abrir um pull request nos repositórios do Comitê Popular Tech. Use ao preparar uma mudança para PR, escrever o título e o corpo, escolher branch ou fork, responder uma revisão ou fechar um PR. Cobre issue antes do código, tamanho, testes, bloco "Para quem revisa", "Antes do merge" e "Se algo der errado". Gatilhos - "abre um PR", "escreve a descrição do PR", "responde a revisão".
---

# pr-abridor

Como abrir um pull request em qualquer repositório da org. Vale igual para quem entrou hoje e para quem está há mais tempo, e para pessoa ou LLM.

## Regras de ouro

1. **O repo alvo prevalece.** Antes de qualquer coisa, leia o `README`, o `CONTRIBUTING`, o `AGENTS.md`/`CLAUDE.md`, o `SECURITY.md` (se houver) e o template de PR do repo. Onde divergirem desta skill, vale o repo.
2. **Quem é LLM não faz push, não abre PR e não comenta antes de a pessoa ler e aprovar o rascunho** (corpo, respostas, issue). Escreva os textos em arquivos, mostre, espere o ok.
3. **Texto curto.** Diga cada coisa uma vez. Detalhe vai em tabela ou link.

## 1. Antes de codar

- **Issue.** Veja se a issue está pronta (critérios, sem bloqueio) e se alguém já pegou; se pegou, fale antes. Avise que você pegou. PR sem issue é aceitável, mas o corpo diz de onde veio o pedido.
- **Proposta ou decisão** começa na issue (pode ser "decidir X"), com a proposta curta. A discussão de desenho acontece ali, antes do código.
- **Sem plano nem especificação no repo.** Especificação ou plano gerado por IA não é commitado. As decisões vão no corpo do PR (por quê, o que ficou de fora e por quê). O repo guarda só documentação durável, que descreve o sistema como ele é hoje. Se o `CONTRIBUTING` do repo disser outra coisa, siga o repo.
- **Falha de segurança** não vai em issue nem em PR públicos. Siga o `SECURITY.md` do repo; sem ele, mande mensagem direta a alguém do time @comite-popular-tech/infra-sec-nucleo (https://github.com/orgs/comite-popular-tech/teams/infra-sec-nucleo), nunca em issue, PR ou comentário.

## 2. Ao fazer a mudança

- **Uma coisa por PR.** Como guia, até uns 20 arquivos e umas 1500 linhas. Passou disso, divida ou empilhe e diga a ordem; se não dá (arquivo gerado, dependência copiada), diga no corpo o que é e que não muda o comportamento. Mudança que dispara deploy aparece no título e no corpo, nunca escondida em PR de documentação.
- **Testes.** Rode a suíte do repo e relate o comando e a contagem. Falha que já existia na main é relatada como tal. Correção de bug traz teste que falha sem a correção: reverta a correção e veja o teste falhar.
- **Documentação.** Atualize no mesmo PR o que a mudança contradiz. O efeito para quem usa vai para a documentação do repo, porque o corpo do PR some do dia a dia.
- **Código.** Comentário só com o porquê. Português do Brasil em código, comentários, textos e commits (termos técnicos em inglês são ok), inclusive nos arquivos de instrução para agentes, salvo regra do repo.
- **Infra, workflow e deploy.** Rode as checagens do repo (por exemplo `fmt` e `validate` do Terraform, `actionlint` para workflow). Não aplique da sua máquina. Actions fixadas por SHA e permissões mínimas. Permissão ou segredo novo é pré-requisito: vai em "Antes do merge".
- **Nada pessoal.** Sem segredo, e-mail pessoal, caminho da sua máquina, dado de produção ou de terceiros em código, corpo, print ou vídeo. Mídia com dados fictícios. De segredo, diga só o nome, o escopo e onde mora; nunca o valor.
- **Rastros de IA.** Sem URL de sessão privada e sem trailer de IA (`Co-Authored-By`, `Claude-Session` e parecidos) nos commits. O rodapé "Generated with" no corpo é escolha de cada pessoa.
- **Releia o seu próprio diff** antes de pedir revisão: sobras, caminhos, depuração.

## 3. Ao abrir

- **Branch no próprio repo** se você tem escrita: assim o CI e o plano rodam. **Fork** só sem escrita; nesse caso o topo do corpo diz que não houve CI nem plano completos e que alguém com acesso precisa rodar.
- **Nome do ramo e título no padrão do repo.** Olhe os últimos PRs mergeados e copie o padrão (área, imperativo, o que for). Sem `feat:`/`fix:` se o repo não usa.
- **Atualize com a main** e diga quais PRs abertos conflitam ou dependem deste.
- **Corpo.** Use o template do repo, se houver; senão o [modelo de corpo](modelo-de-corpo.md). Nos dois casos o corpo **abre com "Para quem revisa"**: duas linhas ou uma lista curta com exatamente o que a pessoa que revisa precisa ler ou decidir ("decidir X", "conferir o arquivo Y", "nada a decidir: só conferir o plano"). Logo depois vem **"Como testar"**: um roteiro rápido para quem revisa seguir, de 2 a 5 passos numerados, cada um com o comando ou o clique exato e o resultado esperado ("1. `npm test` → 42 passam. 2. Abra /agenda e filtre por cidade → só eventos da cidade."). Depois vem "Antes do merge" (se houver) e o restante do corpo, que pode ser tão detalhado quanto for preciso; os dois primeiros blocos são curtos e inconfundíveis. O relato completo dos seus testes (comando, contagem, falhas antigas, o que não conferiu) fica em outra seção, "Resultado dos testes", ou na seção de testes do template do repo.
- **Referências** a issues e PRs como URL completa, mantendo a palavra de fechamento: `Fecha https://github.com/<org>/<repo>/issues/<n>`.
- **Escreva o corpo num arquivo** e use `gh pr create --body-file corpo.md` (e `gh pr edit --body-file`). Não passe o texto com aspas no terminal: as barras invertidas sobram na página. Confira o corpo renderizado.
- **"Antes do merge"** logo depois de "Como testar", quando houver pré-requisito (token, segredo, permissão, ordem): o que falta, quem tem acesso, o que quebra se o merge vier antes. Só nomes, nunca valores.
- **"Se algo der errado"** (como voltar atrás) é obrigatório em PR de infra ou deploy e opcional nos demais.
- **O que o merge faz** e quem publica: se o merge aplica sozinho ou se alguém publica à mão. Diga se a funcionalidade chega ligada ou desligada.
- Peça a revisão com a URL do PR e uma linha de contexto.

## 4. Depois de abrir

- **Responda cada thread** de revisão, curto e com o SHA da correção ("Corrigido em `abc1234`.") ou com o motivo de não proceder.
- **O que ficou de fora** vira issue própria, com o link no PR. Não deixe promessa solta.
- **Aprovação e merge.** Mudança de infra ou de deploy precisa da aprovação de alguém que não seja a pessoa autora. PR pequeno e de baixo risco pode ser mergeado por quem o abriu.
- **Depois do merge**, confira o apply ou o deploy. Se a main ficar vermelha, quem mergeou corrige ou passa a quem tem acesso, e diz isso no PR.
- **Fechar sem merge** sempre leva um comentário com o motivo (e o PR que o substitui, se houver).
